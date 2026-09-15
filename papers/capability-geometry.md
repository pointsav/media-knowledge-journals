---
schema: journal-v2
slug: capability-geometry
title: "Making Infrastructure Ownership Transfer a Single Verifiable Event"
subtitle: "A substrate architecture combining a verified microkernel, a public transparency log, and a customer-held signing key"
site: home.pointsav.com
imprint: PDS-2026-05
thesis: "Combining a formally-verified microkernel, a public tamper-evident log, and a customer-held signing key makes handing over an entire running system to a new owner a single, math-checkable event, rather than a weeks-long identity-migration project."
abstract: |
  Handing an infrastructure deployment from one operator to another today usually means a
  vendor-mediated migration — new accounts, new credentials, a window where trust in the old
  operator and the new one overlaps, and no independently verifiable record of exactly when
  control actually changed hands. This paper describes an architecture that makes that handover
  a single, cryptographically-verifiable event instead. It combines three separately mature,
  independently trusted technologies — a formally-verified operating-system kernel whose
  security guarantees are proven mathematically rather than asserted by a vendor, a public,
  tamper-evident log of every access-control decision the system makes, and a signing key held
  by the customer rather than the vendor — so that the customer's own key, not the vendor's
  infrastructure, is what actually controls the system. Ownership transfer becomes a single
  entry in the public log, co-signed by the outgoing and incoming owner, after which the old
  key is cryptographically refused by the system going forward. We built a working
  implementation of the core mechanism and measured it directly: the everyday check the system
  performs before honoring a request costs about 11 nanoseconds when answered from cache, versus
  4 milliseconds for the full cryptographic verification underneath it — a difference of roughly
  350,000 times, which is what makes checking every request against the log fast enough to be
  practical rather than a theoretical nicety. The main limitation: this is a working substrate,
  not yet a finished production system — the higher-level software that would actually run on
  top of it is still a prototype, and the benchmark numbers come from ordinary server hardware
  standing in for the specialized hardware the finished system is meant to run on.
state: draft
version: "1.0.0"
published:
updated: "2026-09-15"
doi:
license: CC-BY-4.0
cites:
  - rfc-9162
  - rfc-6962
  - sel4-klein-2009-sosp
  - sewell-2011-sel4-integrity-itp
  - murray-2013-sel4-ifp-oakland
  - capsicum-watson-2010
  - macaroons-birgisson-2014
draws_from: []
contributors:
  - name: Peter M. Woodfine
    roles: [Founding Contributor]
  - name: Jennifer M. Woodfine
    roles: [Founding Contributor]
  - name: Mathew Woodfine
    roles: [Founding Contributor]
keywords:
  - capability systems
  - transparency logs
  - verified microkernel
  - ownership transfer
  - infrastructure independence
---

## 1. The question

Moving a piece of infrastructure from one operator to another — because a vendor relationship
ends, a business is sold, or an operator simply wants the option of leaving — is usually slow,
expensive, and only partially verifiable. Access credentials for identity systems and
authentication vendors typically take on the order of a week to migrate per ten applications,
by the vendors' own published guidance. Cloud attestation systems that prove a workload is
running correctly — including the most rigorous ones publicly documented — prove it to the
vendor operating the hardware, not to the customer, and are not built to be handed to a new
operator at all. Formal security certifications are typically issued against a specific
vendor's product; moving to new ownership can invalidate the certificate entirely, even though
nothing about the underlying software changed.

The pattern across all of these is the same: trust is rooted in something the vendor holds —
their keys, their attestation infrastructure, their certificate — rather than in something the
customer holds directly. That means genuine ownership transfer is never really a single event;
it is a migration project, with a window during which both the old and new arrangement are
partially in effect, and no independently checkable record of the exact moment authority
actually moved.

The question this paper asks is whether ownership transfer can instead be made a single,
verifiable event: one entry in a public record, checkable by anyone, after which the previous
operator's authority is cryptographically refused rather than merely revoked by policy. We
answer this by combining three technologies that already exist and are independently
trustworthy, rather than inventing a new one: a operating-system kernel whose core security
properties have been proven correct with machine-checked mathematics rather than asserted by
whoever sells it; a public, tamper-evident log — the same kind of technology that underlies
web certificate transparency today — recording every significant access-control decision the
system makes; and a signing key that belongs to the customer, not the vendor, such that the
system will only act on instructions authenticated by that key.

## 2. What we found

**The combination works, and we built a real, tested implementation of its core mechanism, not
just a design.** The working code — three components, roughly 150 automated tests between
them, plus a set of timed performance benchmarks — implements the actual decision logic a
system like this needs: whether to honor a given access request, whether an access right that
is about to expire can be legitimately extended, and how to execute an ownership handover as a
single, dual-signed event in the public log rather than as a multi-step migration.

**The performance number that makes the whole approach practical, not just theoretically
sound, is a roughly 350,000-times difference between two ways of answering the same
question.** Checking whether a request should be allowed can be answered two ways: by
consulting a fast, local cache of the system's current, already-verified state (measured at
about 11 nanoseconds), or by performing the full cryptographic signature check that
establishes that state is actually genuine in the first place (measured at about 4
milliseconds). Because the system's authoritative state changes only occasionally — when
something is actually granted, revoked, or extended — almost every request can be answered
from the fast cache, with the expensive cryptographic check running only when the underlying
state genuinely changes. Without this gap between "cheap to check" and "expensive to
establish," checking every single request cryptographically would be far too slow to be
usable in practice; with it, verifying every request against a public, tamper-evident record
becomes fast enough to simply always do.

**Ownership transfer works as a single, publicly verifiable event, and we tested this directly
rather than only describing it.** The handover mechanism requires both the outgoing and
incoming operator's signatures on a single record in the public log; after that record is
published, the system verifiably refuses to act on the outgoing operator's signature alone,
and this refusal was confirmed to actually happen in our test implementation, not merely
asserted as a design intention. A third party with access to the public log can identify the
exact point at which authority changed hands and confirm both parties agreed to it, without
needing to trust either party's own account of what happened.

**The system is designed to run on two different kinds of hardware without changing its
behavior, and this matters for how practical the approach actually is.** The formally-verified
kernel offers the strongest guarantees but currently reaches a narrower range of hardware; a
second, commodity-hardware-compatible mode extends the same ownership and verification model
to a much broader range of machines a customer might already own, using a verified-boot
mechanism that has been in real production use for two decades, rather than something newly
invented for this purpose. The two modes are built to produce identical results for the same
inputs — the customer chooses hardware reach or maximum formal assurance, not a materially
different ownership or verification model.

## 3. How we built and tested it

The mechanism has three moving parts, each doing a specific job.

**A record of who is allowed to do what, and when that record was last checked.** Every
significant access right in the system carries, alongside its normal permissions, a reference
to exactly which version of the public log was current when that right was granted or last
extended. This means an auditor with access to the public log alone — no cooperation from
either the vendor or the customer required — can determine when any given right actually came
into existence.

**A public, tamper-evident log, built on the same technology already used for web certificate
transparency.** Every grant, extension, and revocation is recorded as an entry in an
append-only log structured so that altering any past entry would be detectable by anyone who
re-checks the log's internal structure. This is not a new invention — it is the same
underlying technique, standardized for over a decade, that already lets anyone independently
audit which security certificates have been issued for which websites; we are applying it to a
different kind of record.

**A signing ceremony that makes ownership transfer atomic.** The log format we use supports
more than one valid signature on the same entry, which lets a handover be recorded as one
event carrying both the outgoing and incoming operator's signatures together, rather than as
two separate actions with a gap between them. We tested the specific property this is meant to
guarantee directly: that after this joint-signature record is published, the system accepts
further instructions only from the new operator's key, and a test that tries to act using the
old key afterward is refused, not merely warned against.

We benchmarked the core operations — checking a cached decision, performing the full
cryptographic check, verifying that a claimed record actually exists in the log — using
standard, repeatable microbenchmarking methodology on ordinary cloud server hardware, run
multiple times to check for consistency. We want to be direct that this hardware is a stand-in
for the specialized hardware the finished system is intended to run on eventually, and that the
cryptographic-verification cost specifically is expected to be meaningfully higher on that
target hardware — a limitation discussed directly in §5, not glossed over.

## 4. What it changes

For an organization evaluating infrastructure they do not want to be permanently locked into a
single vendor for, the practical change this architecture makes is what "leaving" actually
requires. Under a vendor-rooted trust model, leaving means a migration project: new
credentials, a transition window, and no independent way to verify exactly when the old
arrangement actually ended. Under this architecture, leaving — or more precisely, transferring
ownership to any new operator, including bringing operations fully in-house — is a single,
jointly-signed event in a log anyone can check, after which the old operator's authority is not
just revoked by policy but cryptographically refused by the system itself.

This changes the shape of a real, practical risk: vendor dependency risk that compounds
silently over time. An organization that has built years of operational dependence on a single
vendor's infrastructure, under a vendor-rooted trust model, faces a real switching cost that
grows the longer the relationship continues — precisely the dynamic described in our companion
paper on software licensing economics. An architecture where the customer's own key, not the
vendor's cooperation, is what actually controls the system removes that specific risk
structurally, regardless of how the commercial relationship with any given vendor evolves.

It also changes what an audit or a regulator can verify independently. Because every
significant access-control decision and every ownership transfer is recorded in a public,
tamper-evident log, an outside party does not need to take either the vendor's or the
customer's word for what happened and when — they can check the log directly, which is a
meaningfully different evidentiary position than being told a migration completed correctly.

## 5. Where this could be wrong

**The higher-level software that would actually run on top of this substrate is still a
prototype, not a finished, production-deployed system.** The core mechanism described in this
paper — the verification logic, the log structure, the handover ceremony — is built and tested.
The complete operating environment a real customer would actually use day to day is not yet at
that stage, and claims about when it will be are forward-looking, not current fact.

**The benchmark numbers come from general-purpose server hardware, not the specialized
hardware this system is ultimately meant to run on**, and the gap matters specifically for the
expensive cryptographic-verification step: on the target hardware class, that check is expected
to run meaningfully slower than measured here, which narrows — without eliminating — the
practical advantage of the fast-cache design described in §2.

**The formally-verified kernel's guarantees do not currently extend to running multiple
processing cores at once**, a harder problem that remains open research in the underlying
kernel project; the architecture described here is built for single-core or a more limited
multi-core configuration until that work completes elsewhere.

**Verified silicon does not exist at commodity prices**, and this paper does not claim it does.
The guarantees described here apply to the software and its cryptographic verification, not to
the physical chip or its firmware, which remain outside what any practical system can currently
verify end to end.

## 6. Conclusion

The question was whether transferring ownership of a running infrastructure deployment could
be made a single, independently verifiable event, rather than a slow, partially-trusted
migration. Combining a formally-verified kernel, a public tamper-evident log, and a
customer-held signing key makes this achievable, and we built and tested the core mechanism
rather than only describing it: a real implementation, real tests, and a measured roughly
350,000-times gap between the fast, cached everyday check and the expensive cryptographic
verification underneath it — the gap that makes checking every request against a public
record fast enough to actually do. What remains is finishing the production software that runs
on top of this substrate and confirming the performance characteristics on the hardware the
finished system is meant to target, both of which are real, stated next steps rather than
completed work.

---

## 7. Claims and falsification

**H1 (transferability).** A customer holding only their own signing key and a short reference
value can fully reconstitute a deployment's access state, history, and identity on new
hardware, without the original vendor's involvement.

**H2 (behavioral equivalence).** The same software, run on either of the two supported
hardware modes, produces identical access-control decisions given identical inputs.

| Test | What it checks | Status |
|---|---|---|
| Cache-vs-full-verification benchmark | The ~350,000x speed gap that makes per-request log checking practical | Measured directly, reported in §2-3 |
| Handover refusal test | The old operator's key is refused after a handover record is published | Tested and confirmed in the working implementation |
| Full recovery drill | H1: reconstituting a deployment from just a key and a reference value, with no vendor involvement | Designed; not yet run as a full end-to-end drill |
| Cross-hardware equivalence test | H2: identical decisions from both hardware modes on the same inputs | Designed; not yet executed |

H1 is falsified if any step of reconstitution requires the original vendor's infrastructure,
or if an independent audit of the reconstituted system requires vendor cooperation to verify.
H2 is falsified if the two hardware modes produce different decisions for the same input.

### Appendix A — Measured performance (representative results)

| Operation | Measured cost |
|---|---|
| Cached access-decision check | ~11 nanoseconds |
| Full cryptographic verification | ~4 milliseconds |
| Two-signature handover verification | ~7.7 milliseconds |
| Log-inclusion check (small log) | ~5 microseconds |
| Log-inclusion check (1,000+ entries) | ~18 microseconds |

Measurements taken on general-purpose cloud server hardware (Intel Xeon class), using
standard, repeatable microbenchmarking methodology, multiple runs. Expected to differ
materially on the specialized hardware the finished system targets — see §5.

### Appendix B — What is, and is not, verified

The mathematical proofs underlying the kernel cover its access-control logic, not the physical
chip, its microcode, or its firmware. Formal verification currently covers single-core
operation; multi-core verification is ongoing work in the underlying kernel project, not this
paper's own contribution.

## References

Capsicum: Watson, R. N. M., et al. 2010. Capsicum: Practical capability-based security for
UNIX. *USENIX Security Symposium.*

Klein, G., et al. 2009. seL4: Formal verification of an OS kernel. *ACM SOSP.*

Macaroons: Birgisson, A., et al. 2014. Macaroons: Cookies with contextual caveats for
decentralized authorization in the cloud. *NDSS.*

Murray, T., et al. 2013. seL4: From general purpose to a proof of information flow
enforcement. *IEEE Symposium on Security and Privacy.*

RFC 6962. 2013. *Certificate Transparency.* Internet Engineering Task Force.

RFC 9162. 2022. *Certificate Transparency Version 2.0.* Internet Engineering Task Force.

Sewell, T., et al. 2011. seL4 enforces integrity. *International Conference on Interactive
Theorem Proving.*

---

## Contributors

Peter M. Woodfine, Jennifer M. Woodfine, and Mathew Woodfine are credited as founding
contributors to PointSav Digital Systems's systems-architecture research programme.

## How this paper was produced

This paper was prepared with AI assistance under human editorial direction; all analytical
claims and conclusions are the responsibility of the named institutional author.

## Disclosures

The architecture and implementation described are this workspace's own engineering work. This
paper contains forward-looking statements about production deployment timelines and target
hardware performance; such statements reflect current intentions and are subject to change
without notice.

## Data and reproducibility

The implementation described is Rust source code with an automated test suite and a
benchmarking harness; the formal verification artifacts underlying the kernel are part of that
kernel project's own public record, not produced by this paper. Benchmark methodology and
representative results are given in Appendix A.
