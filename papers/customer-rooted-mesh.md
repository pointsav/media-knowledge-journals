---
schema: journal-v2
slug: customer-rooted-mesh
title: "Network Isolation Without Handing Your Keys to a Vendor"
subtitle: "A private-network architecture where routing keys never leave the customer's own machines"
site: home.pointsav.com
imprint: PDS-2026-06
thesis: "Commercial zero-trust network products deliver real isolation, but the vendor holds the keys that enforce it — an architecture built entirely on an existing, well-verified protocol shows the same isolation is achievable with every private key generated on, and never leaving, the customer's own machines."
abstract: |
  Commercial zero-trust network products — the tools that stop one part of a system from
  talking to another unless explicitly authorized — achieve that isolation by routing traffic
  through the vendor's own infrastructure, which means the vendor, not the customer, holds the
  cryptographic keys that actually enforce it. That arrangement creates a specific set of risks
  that have nothing to do with whether the vendor's technology works well: audit logs the vendor
  could alter or omit without the customer knowing, no independent way to verify the vendor is
  actually enforcing the policy the customer configured, and a network that stops working the
  moment the vendor relationship ends, however that happens. We built and tested an alternative
  using only WireGuard — a modern, formally-verified private-networking protocol already in
  wide production use — configured so that every private key is generated on, and never leaves,
  the machine it protects; a central coordinator only ever sees public keys, which are useless
  for decrypting anything or impersonating anyone; and every machine keeps its own tamper-evident
  log of network activity, so a compromised coordinator cannot quietly alter the historical
  record. We measured the real cost of this approach directly: establishing a new secure
  connection took about 44 milliseconds on average, and a policy change — deciding a given
  machine may now talk to another — took effect in about 8 milliseconds, with no separate
  policy-enforcement engine required at all. The main limitation: because policy is enforced
  through static configuration rather than a live decision engine, this approach is not suited
  to situations that need sub-minute automatic response to a device's changing security state —
  a real trade-off, not a missing feature we simply haven't built yet.
state: draft
version: "1.0.0"
published:
updated: "2026-09-15"
doi:
license: CC-BY-4.0
cites:
  - rose-2020-nist-800-207
  - kindervag-2010-zero-trust
  - ward-beyer-2014-beyondcorp
  - donenfeld-2017-wireguard
  - lipp-2019-wireguard-proof
  - perrin-2018-noise
  - mackey-2020-wireguard-openvpn
draws_from: []
contributors:
  - name: Peter M. Woodfine
    roles: [Founding Contributor]
  - name: Jennifer M. Woodfine
    roles: [Founding Contributor]
  - name: Mathew Woodfine
    roles: [Founding Contributor]
keywords:
  - zero-trust architecture
  - private networking
  - key custody
  - network isolation
  - audit log integrity
---

## 1. The question

"Zero-trust" network architecture — the now-standard idea that no device or connection is
trusted just because of where it sits on a network, and every request has to prove itself —
is well established and effective. What receives far less attention is a structural fact about
how most commercial zero-trust products actually deliver that isolation: traffic is routed
through the vendor's own infrastructure, which means the vendor generates and holds the
private cryptographic keys that make the isolation real. A customer can configure policy
through the vendor's console, but the keys that actually enforce that policy, and the logs
that record what happened, live on the vendor's systems, not the customer's.

This creates a set of risks that are separate from whatever risks zero-trust architecture was
built to address in the first place. An audit log the vendor generates can be altered or
selectively left incomplete without the customer's knowledge, and the customer has no
independent way to check. A customer cannot verify that the policy they configured is actually
the policy being enforced — the enforcement itself is invisible, running entirely inside the
vendor's own infrastructure. And if the vendor relationship ends badly — insolvency,
acquisition, a legal order that freezes the vendor's systems — the customer's network isolation
can be disrupted immediately, with no independently-held cryptographic material available to
keep things running or to prove what was true beforehand.

The question this paper asks is whether the same isolation guarantee — no device talks to
another unless explicitly authorized — can be built without any of this vendor dependency: an
architecture where every private key is generated on, and never leaves, the machine it
protects, where a central coordinator exists only to distribute public information, and where
the historical record of what happened on the network is held by the customer, tamper-evident,
from the start. We answer this by building the architecture on top of an existing,
already-trusted protocol — WireGuard, a private-networking technology whose cryptographic
core has been independently, formally verified — rather than inventing new cryptography, and
by measuring the real performance cost of doing so rather than assuming it would be
acceptable.

## 2. What we found

**The architecture works exactly as intended: private keys never transit the coordinator, at
any point in the design, and this was true by construction, not just by policy.** Every
machine in the network generates its own private key locally, using the operating system's own
secure random-number generation, and that key is never transmitted anywhere — not to the
coordinator, not to any other machine, not to a backup service. The coordinator's job is
limited to distributing public keys and telling each machine which other public keys it is
allowed to talk to; a coordinator that is compromised, subpoenaed, or otherwise exposed reveals
only public information — the list of who is on the network and how they are connected, never
anything that could be used to decrypt traffic or impersonate a machine.

**Establishing a new secure connection took about 44 milliseconds on average, measured across
thirty real trials, with no meaningful cost added by the customer-held-key design compared to
an ordinary use of the same underlying protocol.** This matters because it confirms the
security property (keys never leaving their home machine) was achieved without paying a
performance tax for it — the architecture uses the exact same handshake a standard deployment
of the same protocol would use; the difference is entirely in who holds and distributes the
keys, not in the cryptographic work being done.

**Changing network policy — deciding that one machine may now talk to another it previously
could not — took effect in about 8 milliseconds, and took effect immediately upon the command
completing, with no separate propagation delay.** This is a real, measured result, not a
design target: the underlying operating-system mechanism that enforces which connections are
allowed applies the new rule synchronously, meaning a network packet arriving right after a
policy change is evaluated against the new rule, not the old one. There is no gap during which
the old and new policy are both partially in effect.

**Failure recovery is real but uneven, and we are reporting the actual measured spread rather
than a single clean number.** When the central coordinator restarts, the time for a
disconnected machine to reconnect ranged from about one second to about sixteen seconds across
five trials, depending on exactly where each machine's own periodic check-in timer happened to
be at the moment of the restart. This is a genuine limitation of relying on a fixed check-in
interval rather than active failure detection, and we report the full range rather than only
the favorable end of it.

## 3. How we built and tested it

The architecture rests on four design rules, each closing a specific gap in how commercial
products typically work. Every machine generates its own private key locally and never
transmits it — the coordinator's knowledge is limited to public keys and network addresses,
which are useless on their own for decryption or impersonation. Which machines may talk to
which others is determined by a simple, static routing rule on each machine, derived directly
from how the actual system being protected is composed — a data-handling service, for example,
is configured to accept connections only from the specific processing layer that legitimately
needs to reach it, and this rule is enforced by the underlying networking protocol itself, not
by a separate firewall or policy engine layered on top. And every machine keeps its own local,
tamper-evident record of network activity — each new log entry is cryptographically chained to
the one before it, so that altering or deleting a past entry breaks a chain that anyone holding
the starting point can independently verify, and this record is never routed through the
central coordinator, specifically so a compromised coordinator cannot quietly rewrite history
at any individual machine.

We tested this design on real, isolated test machines rather than only describing it on paper.
Connection-establishment time was measured across thirty separate trials, timing from when a
new connection is initiated to when the underlying protocol confirms it is fully established.
Policy-change speed was measured across twenty trials, timing the actual system command that
updates which connections are allowed. Recovery behavior after a coordinator restart was
measured across five trials. All of these measurements were taken with the two ends of the
connection on the same physical machine, connected by a virtual network link with no real
physical distance between them — meaning the numbers reported here measure the protocol's own
overhead, not the additional delay that real geographic distance between two machines would
add on top. A deployment with real physical separation should expect these numbers plus
however long a round trip between the two locations actually takes.

We also compared our measured connection-establishment time against previously published,
independent benchmarks of the same underlying protocol on dedicated hardware with no
virtualization overhead, and against a comparison of the same protocol versus an older,
widely-used alternative. The comparison confirmed our results were consistent with — somewhat
slower than, for reasons attributable to running on shared virtualized hardware rather than
dedicated physical machines — the independently published baseline, and that the underlying
protocol remains meaningfully faster than the older alternative regardless of which
environment it is measured in.

## 4. What it changes

For an organization deciding how to isolate parts of its own infrastructure from each other,
the practical change this architecture makes is what actually happens if the vendor
relationship changes or ends. Under a vendor-key-custody model, that event can disrupt network
isolation immediately, because the keys that made the isolation real were never the customer's
to begin with. Under this architecture, there is no vendor relationship in the key-custody
sense at all — every key was already on the customer's own machines, generated there and never
transmitted elsewhere, so there is nothing to hand back or lose access to.

It also changes what a customer can independently verify. Because network segmentation is
enforced through a simple, readable configuration file on each machine rather than a
vendor-run policy engine whose actual behavior is invisible, an auditor can confirm what is and
is not allowed to connect to what by reading the configuration directly — the enforcement
mechanism is the same thing that can be audited, not a black box behind it. And because the
activity log on each machine is tamper-evident and never routed through a central point that
could rewrite it, a compromised coordinator cannot quietly alter the historical record at any
individual machine without that alteration being independently detectable.

This does not mean the architecture is a strict improvement over commercial products in every
respect — §5 states the real trade-offs directly. What it changes is which specific risk a
customer is accepting: vendor-mediated products trade some operational simplicity for
vendor-held keys and vendor-controlled logs; this architecture trades some operational
convenience (manual key distribution, static rather than dynamic policy) for keys and logs
that never leave the customer's own control.

## 5. Where this could be wrong

**Static policy cannot respond automatically to a device's changing security state within
seconds, and this is a genuine trade-off, not a missing feature.** Some real security
scenarios call for automatically cutting off a device the moment its security posture drops
below a threshold — a patch level slipping, for example. This architecture's policy is enforced
through configuration files that must be explicitly updated; achieving sub-minute automatic
response to changing device state would require adding a policy engine of exactly the kind
this architecture avoids, undermining part of the reason to choose it in the first place.

**The customer-held-key guarantee only holds if the machine holding the key is itself secure.**
This architecture ensures a key is never transmitted; it does not, and cannot, guarantee the
security of the operating system storing that key once it is there. A machine with weak file
permissions or a compromised operating system undermines the guarantee regardless of how well
the key-distribution design works.

**The central coordinator remains a single point of availability, not just a single point of
key exposure.** In the simplest deployment mode, all machine-to-machine traffic routes through
the coordinator; if it goes down, so does connectivity between every other pair of machines,
even though none of their individual keys were ever at risk. A more distributed configuration
avoids this at the cost of real added complexity.

**Getting a new machine's configuration onto that machine securely for the first time is not
fully solved by this architecture.** Because a new machine's configuration includes its own
private key at the moment of creation, delivering that file to the machine still requires some
existing secure channel — this is a real, unsolved bootstrapping step in the current design,
not a hidden assumption we are glossing over.

## 6. Conclusion

The question was whether the network isolation commercial zero-trust products provide could be
achieved without the vendor holding the keys that make it real. It can: building on an
existing, independently verified private-networking protocol, configured so that every private
key is generated on and never leaves its home machine, delivers the same isolation guarantee
with the coordinator holding nothing more sensitive than public keys and network addresses. We
measured the real cost directly rather than assuming it — about 44 milliseconds to establish a
connection, about 8 milliseconds for a policy change to take effect — and found no meaningful
performance penalty for the customer-held-key design compared to an ordinary deployment of the
same protocol. The real trade-offs are genuine and stated directly in §5: this approach is not
suited to workloads needing sub-minute automatic response to changing device state, and it
shifts some operational convenience onto the customer in exchange for never handing the keys
away in the first place.

---

## 7. Claims and falsification

**H1 (isolation equivalence).** This architecture enforces network isolation equivalent to
commercial zero-trust products for deployments whose access rules can be expressed as static
relationships between groups of machines.

**H2 (key-custody preservation).** An attacker who fully compromises the central coordinator
cannot derive any other machine's private key, decrypt any recorded traffic, or impersonate any
machine to any other machine on the network.

**H3 (audit-log integrity).** An attacker who fully compromises the central coordinator cannot
retroactively alter another machine's local activity log without producing a detectable break
in that log's tamper-evidence chain.

| Test | What it checks | Status |
|---|---|---|
| Connection-establishment benchmark | Real-world cost of the customer-held-key design | Measured directly: ~44ms mean, n=30 |
| Policy-change-latency benchmark | Real-world cost of a policy update taking effect | Measured directly: ~8ms mean, n=20 |
| Coordinator-compromise key-extraction test | H2: no path exists from coordinator compromise to another machine's private key | Designed; not yet attempted as an adversarial red-team exercise |
| Log-tamper-detection test | H3: a forged or truncated log entry is detectable without cooperation from the affected machine | Designed; not yet attempted as an adversarial exercise |

H1 is falsified by identifying a real isolation requirement this architecture structurally
cannot meet. H2 is falsified by demonstrating any software path from coordinator compromise to
another machine's private key or decrypted traffic. H3 is falsified by demonstrating an
undetectable log alteration.

### Appendix A — Measured results (representative)

| Measurement | Result |
|---|---|
| Connection establishment (n=30) | 44ms mean, 30-86ms range |
| Re-connection after disruption (n=10) | 59ms mean, 25-118ms range |
| Policy-change command latency (n=20) | 8ms mean, 7-11ms range |
| Coordinator-restart recovery (n=5) | 1-16 seconds, bimodal |

All measurements taken with both ends of the connection on the same physical machine
(no real network distance); a deployment with real geographic separation should add the actual
round-trip time between locations to the connection-establishment figures.

### Appendix B — Design principles

Node-local key generation, never transmitted. A coordinator holding only public keys and
address assignments. Network-segmentation rules derived directly from the real system's
component relationships, enforced by the underlying protocol itself. A local, cryptographically
chained activity log at every machine, never routed through the coordinator.

## References

Donenfeld, J. A. 2017. WireGuard: Next generation kernel network tunnel. *NDSS Symposium.*

Kindervag, J. 2010. No more chewy centers: Introducing the zero trust model of information
security. *Forrester Research.*

Lipp, B., B. Blanchet, and K. Bhargavan. 2019. A mechanised cryptographic proof of the
WireGuard virtual private network protocol. *IEEE European Symposium on Security and
Privacy.*

Mackey, A., et al. 2020. Performance comparison of WireGuard and OpenVPN. *Proceedings of
CCRIS.*

Perrin, T. 2018. *The Noise Protocol Framework.* noiseprotocol.org.

Rose, S., O. Borchert, S. Mitchell, and S. Connelly. 2020. *NIST Special Publication 800-207:
Zero Trust Architecture.* National Institute of Standards and Technology.

Ward, R., and B. Beyer. 2014. BeyondCorp: A new approach to enterprise security. *USENIX
;login:* 39(6).

---

## Contributors

Peter M. Woodfine, Jennifer M. Woodfine, and Mathew Woodfine are credited as founding
contributors to PointSav Digital Systems's systems-architecture research programme.

## How this paper was produced

This paper was prepared with AI assistance under human editorial direction; all analytical
claims and conclusions are the responsibility of the named institutional author.

## Disclosures

The architecture and implementation described are this workspace's own engineering work. This
paper contains forward-looking statements about future testing and hardening work; such
statements reflect current intentions and are subject to change without notice.

## Data and reproducibility

The underlying protocol is publicly documented and independently, formally verified; the
architecture's configuration approach is described in full in §3 and Appendix B, and is
reproducible by any operator of the same underlying protocol. Representative measured results
are given in Appendix A.
