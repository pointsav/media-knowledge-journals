---
schema: journal-v2
slug: multi-archive-dev-coordination
title: "Coordinating Many Concurrent AI Development Sessions Without a Human Bottleneck"
subtitle: "An archive-scoped session and mailbox architecture, evaluated on a real 21-archive deployment"
site: home.pointsav.com
imprint: PDS-2026-04
thesis: "Isolating and coordinating many concurrent AI development sessions can be done structurally — archive-scoped sessions, a lock protocol, and an asynchronous mailbox — rather than by routing every decision through a human or a single coordinator process."
abstract: |
  Running many concurrent AI development sessions against many separate codebases creates a
  coordination problem that most tooling does not address: how does one session avoid
  corrupting another's uncommitted work, and how do sessions that must exchange information do
  so without either sharing memory directly or waiting on a human to relay every message? This
  paper describes an architecture built to answer both questions — an archive-scoped session
  model in which each session is bound at startup to exactly one version-controlled directory,
  a crash-consistent lock protocol that distinguishes a genuinely concurrent session from a
  merely crashed one, and a structured, file-based mailbox protocol that lets sessions exchange
  information without ever sharing a working directory. We evaluate this architecture against a
  real, production 21-archive deployment, not a synthetic benchmark. Before a set of targeted
  fixes, only 4 of 21 archives (19%) could publish their own work without a human coordinator's
  involvement; after correcting a real mismatch between the declared publication policy and the
  code that was supposed to enforce it, 10 of 21 (48%) could. A naive text-matching count of
  pending coordination messages overstated the real backlog by roughly two times — 157 apparent
  messages against 77 real ones — once messages were counted correctly. The main limitation:
  this is a single production system studied by the people who operate it, with no control
  group, and generalizing the specific numbers to other environments or larger scale has not
  been tested.
state: draft
version: "1.0.0"
published:
updated: "2026-09-15"
doi:
license: CC-BY-4.0
cites:
  - dennis-vanhorn-1966-capability-based-protection
  - cervero-kockelman-1997-travel-demand-3ds
draws_from: []
contributors:
  - name: Peter M. Woodfine
    roles: [Founding Contributor]
  - name: Jennifer M. Woodfine
    roles: [Founding Contributor]
  - name: Mathew Woodfine
    roles: [Founding Contributor]
keywords:
  - multi-agent coordination
  - AI-assisted software development
  - session isolation
  - asynchronous mailbox protocol
  - branch isolation
---

## 1. The question

Running one AI development session against one codebase is a solved problem. Running many
concurrent sessions, each against its own separate codebase, on the same host, raises a
question most single-session tooling never has to answer: how do you stop one session's
half-finished work from contaminating another's, and how do sessions that genuinely need to
exchange information do so without either sharing a working directory directly or requiring a
human to relay every message by hand?

Human development teams solve a version of this problem with tools built for synchronous or
near-synchronous availability — pull request queues, chat channels, shared CI pipelines. Those
tools assume a person is generally around to notice a message and act on it soon after it
arrives. AI agent sessions are not like that: they run episodically, in bursts bounded by a
context window, often started and stopped by an operator at times that have nothing to do with
when another session might be waiting for a reply. A coordination substrate built for people
who are usually online does not transfer cleanly to sessions that are usually not.

The question this paper asks is narrow and practical: can isolation and coordination between
many concurrent development sessions be enforced structurally — by the shape of the
architecture itself — rather than by policy that depends on every session behaving correctly,
or by routing every decision through a single human or coordinator process that becomes a
bottleneck as the number of sessions grows? And if such an architecture is built, does it
actually reduce the bottlenecks it is meant to reduce, measured against a real deployment
rather than a synthetic test?

We answer both halves of this question directly. The architecture has three pieces: sessions
are bound to exactly one version-controlled archive at startup, with no ability to read or
write another archive's state by accident; a lock protocol gives each archive a single active
session at a time, while still being able to tell a genuinely concurrent second session apart
from a session that simply crashed and left a stale lock behind; and a structured,
asynchronous mailbox lets sessions exchange information without ever touching each other's
working directories directly. We evaluate this architecture against a real, production
21-archive deployment that adopted it, and report what actually changed, not what was
predicted to change.

## 2. What we found

**The self-service publication rate roughly doubled once a real, previously-invisible
enforcement gap was fixed.** Before any change, 4 of 21 archives (19%) were declared eligible,
in the deployment's own configuration, to publish their finished work directly without a human
coordinator's involvement. In practice, none of them actually could: the code responsible for
enforcing publication permissions ran a hard, unconditional block before it ever checked what
the configuration file actually declared, which meant the eligibility declaration was
completely inoperative regardless of what it said. Once the enforcement code was corrected to
actually check the declared eligibility first, six more archives were confirmed to already
meet the bar and were promoted — bringing the real, working self-service rate to 10 of 21
(48%), with no change at all to the underlying eligibility policy itself. The entire
improvement came from making the enforcement mechanism match a specification that had already
existed but was never actually being read.

**A naive way of counting pending coordination messages overstated the real backlog by about
two times.** A simple text search for the string marking a message as still pending returned
157 hits across the deployment's mailboxes. Counting properly — treating each mailbox message
as a structured block and counting blocks, not string occurrences — found 77 genuinely pending
messages. The gap came from the same marker text appearing inside the body of some messages
(as ordinary prose, not as the structural marker it resembled) and, occasionally, from a
message block carrying a duplicated header line from two sessions writing to the same file at
close to the same time. Neither of these is a rare or unusual failure mode in a plain-text,
append-based coordination system; both are exactly the kind of error a text-matching count
will silently produce and a structured, block-aware count will not.

**A second, unrelated but real gap was found and fixed in the same pass: a second human
operator's ability to commit work at all was blocked by a missing credential directory.** The
system's identity-resolution logic expected signing keys to exist at a specific per-operator
location; for the second operator, that location had simply never been provisioned, which
silently failed every commit attempt from that operator's own session. This was not a subtle
architectural finding — it was a straightforward provisioning gap — but it is worth reporting
directly, because it illustrates a real failure class in multi-operator coordination systems
that neither the archive-isolation model nor the mailbox protocol addresses on their own:
correct architecture for coordinating sessions does not by itself guarantee that every
authorized human operating those sessions has actually been set up correctly to use it.

**A third finding, this time about the deployment's git history rather than its runtime
behavior, deserves the same directness.** At audit time, the majority of the deployment's
archives — the paper's own record states this at two different points, once as 21 archives in
scope and once, in a specific discussion of session-state contamination, as 24 of 25 — had
session-state files present in their canonical version-control history from before branch
isolation was adopted. We are stating this numeric inconsistency plainly rather than silently
resolving it in one direction, because we do not have a way to independently confirm which
figure reflects the deployment's true state at the moment being described; it may simply
reflect the archive count changing between when different parts of the underlying audit were
performed, which would be unremarkable in a system that was actively being provisioned during
the same period. What is not in dispute is the direction of the finding: session-state
contamination of canonical history was a real, pre-existing condition from before branch
isolation existed, and no new contamination has been found since branch isolation was adopted
— retroactive cleanup of the pre-existing contamination is a separate, planned piece of work,
not yet done.

## 3. How the architecture works

**Archive-scoped sessions.** Each session is bound, at startup, to exactly one version-
controlled directory — an archive — containing that archive's own code, data, and session-
state files. The session reads a machine-readable manifest from the archive root describing
the archive's identity and its relationships to other archives in the deployment, and holds no
file path or reference that points outside its own archive boundary except through the
mailbox described below. This is an architectural constraint, not a policy one: a session
simply has nothing in hand that would let it reach into another archive's state, correctly or
by mistake.

**The lock protocol.** Immediately after reading its manifest, a session writes a lock file
recording its own process identifier and the identifier of the current system boot. This lets
any later session starting in the same archive tell apart three distinct situations: a lock
whose process is still alive, meaning a real concurrent session is active and the new session
should stop and warn rather than proceed; a lock whose process is gone but whose boot
identifier matches the current one, meaning the previous session likely crashed and the lock
can be treated as stale after confirmation; and a lock whose boot identifier does not match the
current one at all, meaning the machine itself has rebooted since that lock was written, in
which case it can safely be cleared automatically. This distinction — crashed versus
concurrent versus simply pre-reboot — is what lets the lock protocol be strict about
concurrency without becoming unusable after an ordinary restart.

**The mailbox protocol.** Sessions that need to exchange information do not share memory, a
file descriptor, or a direct connection to one another. Each archive maintains its own inbox
and outbox file; a message is written to the sender's outbox and later delivered into the
recipient's inbox by a separate relay step, rather than being written directly into another
archive's files. Every message carries a small structured header — sender, recipient, subject,
timestamp, and a delivery status that moves from pending to delivered to actioned as the
message works its way through the system. A message addressed to a destination that does not
exist, or that the sender is not permitted to address, is rejected at the point of writing,
rather than silently misdelivered later. This gives the deployment a single, auditable point
through which every piece of inter-archive communication passes, without requiring any two
sessions to ever touch each other's working directory directly.

**Branch isolation.** Each archive works on its own dedicated version-control branch rather
than directly on the shared canonical branch, specifically so that ordinary session-state
housekeeping — mailbox entries, working notes, in-progress memory files — can accumulate
freely without contaminating the canonical history that other archives and outside
collaborators actually see. A publication step filters out session-state paths before
anything is merged into the canonical branch, so the separation is enforced at the point of
publication, not left to individual session discipline.

## 4. What it changes

For a team or workspace running many concurrent AI development sessions, the practical change
this architecture makes is where coordination bottlenecks actually live. Under a model where a
single coordinator mediates every publication decision and manually relays every message, the
coordinator's own availability becomes the ceiling on how fast the whole system can move,
regardless of how many sessions are actually ready to act. Under this architecture, a session
that has demonstrated it meets a declared bar can publish its own work directly, and messages
move through an automated, auditable relay rather than a manual one — which is exactly the
shift the real deployment's before-and-after numbers in §2 show happening in practice, not
just in principle.

The self-service finding in §2 carries a lesson that generalizes beyond this specific
deployment: a capability declared in a configuration file is not the same thing as a capability
that is actually enforced, and the two can silently diverge for a long time before anyone
notices, because the failure mode — everything still routes through the coordinator, which
still works, just more slowly than it should — does not announce itself as a bug. Any system
that separates "what is declared as allowed" from "what the enforcement code actually checks"
should expect this exact class of drift, and should look for it directly rather than assuming
a configuration file's contents are actually being honored.

The message-count finding carries a similarly general lesson for any plain-text, append-based
coordination system: a naive text search over message content will overstate a queue's real
depth whenever the marker text can also appear as ordinary prose inside a message body, and the
fix is a structural, block-aware count, not a smarter search string. A team using text search
to decide where to allocate coordination attention should treat that number with real
suspicion until it has been checked against a proper parse.

## 5. Where this could be wrong

**This is one system, studied by the people who operate it.** The researchers and the
operators of the system under study are the same people, which means what was measured and
what was fixed were not decided by an independent party, and there was no pre-registration of
what would be checked before the audit began. We report this directly rather than presenting
the case study as more independent than it is.

**There was no control group.** The system was modified in place; the "before" state is
reconstructed from inspecting the code and configuration as they existed, not from an
instrumented baseline recorded in real time. The direction of the findings — self-service rate
increased, message count was overstated, a credential gap existed — is not in doubt, but exact
magnitudes of the "before" state rest on reconstruction rather than live measurement.

**Scale is modest, and we do not know how these patterns hold beyond it.** Twenty-one archives
on a single host is a real deployment, but a small one. Whether the same architecture and the
same class of finding — a declared-but-unenforced capability, an inflated naive count —
recurs at ten times this scale, or across multiple hosts, has not been tested here.

**One internal inconsistency in the underlying record was not resolved, and we are saying so
rather than picking a number.** As noted in §2, the source material for this paper states the
archive count differently in two places (21 in its primary scope, 24 of 25 in one specific
discussion). We could not independently confirm which is correct and have left it stated as an
open discrepancy rather than silently choosing one.

## 6. Conclusion

The question was whether isolating and coordinating many concurrent AI development sessions
could be done structurally, and whether doing so actually reduces the bottlenecks a
single-coordinator model creates as the number of sessions grows. On a real, 21-archive
production deployment, it did: correcting a real mismatch between a declared publication
policy and the code meant to enforce it more than doubled the self-service publication rate
with no change to the policy itself, and switching from a naive text count to a structured
message count corrected a roughly two-times overstatement of the real coordination backlog.
Neither result required replacing the underlying architecture — both came from making the
enforcement of an already-correct design actually match its specification. That is the paper's
real, modest, and checkable finding: the bottleneck was not the architecture, it was a gap
between what the architecture declared and what its own enforcement code was doing.

---

## 7. Claims and what would count against them

**Claim.** Archive-scoped session isolation, a boot-aware lock protocol, and a structured
asynchronous mailbox reduce coordination bottlenecks in a multi-session AI development
environment when their enforcement is verified to actually match their specification.

**This claim would be wrong if:** a deployment adopting this same architecture, with its
enforcement code correctly matching its declared policy from the outset, showed no reduction
in coordinator-mediated bottlenecks relative to a single-coordinator baseline — which would
suggest the improvement measured here came specifically from fixing a bug, not from anything
general about the architecture. We consider this a live possibility worth testing directly in
a future, cleaner deployment, not a concern we can rule out from this case study alone.

**What this claim does not say.** It does not claim these specific percentages (19%, 48%,
157, 77) generalize to other environments or to significantly larger scale. It does not claim
the lock protocol or mailbox design is the only workable approach to this coordination
problem, only that this one, evaluated against a real deployment, produced the measured
result reported in §2.

## References

Dennis, J. B., and E. C. Van Horn. 1966. Programming semantics for multiprogrammed
computations. *Communications of the ACM* 9(3): 143–155.

---

## Contributors

Peter M. Woodfine, Jennifer M. Woodfine, and Mathew Woodfine are credited as founding
contributors to PointSav Digital Systems's systems-architecture research programme.

## How this paper was produced

This paper was prepared with AI assistance under human editorial direction; all analytical
claims and conclusions are the responsibility of the named institutional author. The empirical
measurements reported in §2 are from the production system under study, logged during the
audit described in §3–§4.

## Disclosures

The researchers reporting this case study also operate the system under study; this is
disclosed directly in §5 as a real limitation on the independence of the findings, not merely
a formality. This paper contains forward-looking statements about planned future work (retroactive
history cleanup, testing at larger scale); such statements reflect current intentions and are
subject to change without notice.

## Data and reproducibility

The configuration and measurement approach described in this paper are specific to the
production system studied. The method — comparing a declared capability against its actual
enforcement, and a naive text count against a structured block-level count — is described in
full in §3–§4 and is reproducible against any comparably-structured coordination system.
