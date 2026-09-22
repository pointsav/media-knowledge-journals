---
schema: journal-v2
slug: ai-as-the-optional-third-ring
title: "Keeping AI Out of the Write Path"
subtitle: "Why a wall is a different kind of assurance from a rule"
site: home.pointsav.com
imprint: PDS-010
thesis: "A system where AI has no path to write to a record is a stronger assurance than a policy promising that it will not."
abstract: |
  Our thesis is that the assurance a business needs about AI and its records is structural,
  not procedural: not a promise that artificial intelligence will never write to the
  authoritative record, but a design in which no path exists by which it could. The platform
  is built in three concentric layers. The inner layer takes in raw material and writes it to
  an unalterable record. The middle layer reads that record and produces structured knowledge
  by repeatable computation — the same input always producing the same output — and structured
  data never passes through a language model at all. The outer layer,
  where inference lives, may read from the middle layer and return proposals; it has no write
  path, and every accepted proposal enters the record through the middle layer with a person
  at the checkpoint. A deployment can leave the outer layer out
  entirely, because the two inner layers carry no dependency on it. Four limits are stated
  where they arise rather than collected at the end: the single gateway all inference passes
  through does not yet remove personal or location details from a prompt before an external
  call; calls to an outside model are not switched on, being wired only against a test
  stand-in; the deliberately AI-disabled operating mode is not built as a distinct mode; and
  the deepest enforcement layer this design points toward is a direction, not a running
  system.
state: draft
version: "0.1.0"
published:
updated: "2026-09-21"
cite_as:
license: CC-BY-4.0
cites:
  - sel4-klein-2009-sosp
  - olmo3-allenai
  - rfc-9162
draws_from:
  - three-ring-architecture
  - doorman-protocol
  - sovereign-ai-routing
  - substrate-without-inference-base-case
  - tier-zero-customer-side-sovereign-specialist
  - four-tier-slm-substrate
  - worm-ledger-architecture
  - source-of-truth-inversion
  - diode-standard
  - customer-hostability
  - capability-geometry
prepared_by: "Woodfine Management Corp."
keywords:
  - AI architecture
  - deterministic processing
  - audit ledger
  - human approval
  - regulated deployment
---

> This paper is provided for engineering, operational, and research purposes and does not
> constitute investment advice or a solicitation to invest in any Woodfine direct-hold
> solution. Statements marked "planned," "intended," "targeted," "may," or "expected" are
> forward-looking and subject to change. Full disclosures appear at the end of this paper.

Working Paper PDS-010 · v0.1.0 · CC BY 4.0

Our thesis is that the right assurance about artificial intelligence and a business's records
is a structural one, not a procedural one. A policy stating that AI will never write directly
to your records can be broken — by a mistake, by a configuration changed in a hurry, by a
compromised system, by an employee who meant well. A design in which AI has no path to write
to your records cannot be broken that way. It can only be removed and rebuilt, which is a
visible act somebody has to perform deliberately, rather than an invisible one that happens
while nobody is looking.

The shape that follows from this is three concentric layers with strictly one-way
dependencies. The inner layer takes in raw material — documents, messages, files — and writes
it to a record that cannot be altered afterwards. The middle layer reads that record and turns
it into structured knowledge using ordinary, repeatable computation: the same input always
produces the same output, and structured data is never routed through a language model at all.
The outer layer is where inference lives. It may read from the middle layer and return
proposals — a draft, a suggested classification, a summary — and it has no write path to
anything. Every proposal that is accepted enters the record through the middle layer, with a
person at the checkpoint.

The two inner layers carry no dependency on the outer one, so a deployment can leave the outer
layer out altogether and still be a complete system. Four things are not finished, and this
paper puts each beside the claim it qualifies rather than gathering them into a confession at
the end: the single gateway every inference request passes through does not yet remove personal
or location details from a prompt before an external call; calls to an outside model are not
switched on at all today; the deliberately AI-disabled operating mode is not built as a
distinct mode; and the deepest enforcement layer this design points toward is a direction
rather than a running system. This paper is written for a reader with no background in
computing, and its purpose is to make the difference between a rule and a wall legible enough
that a skeptical person can check it rather than take it on faith.

## 1. The thesis

State the two possibilities as plainly as possible.

In the first, a system is configured so that AI does not write to the authoritative record.
The capability exists — the software could do it — and a setting, a policy, or a code path
prevents it. The assurance is that the setting is correct, that everyone who can change it
will not, and that no defect elsewhere causes the prevention to be skipped.

In the second, the component that performs inference is not connected to the record in the
write direction at all. It can be asked questions. It can return text. What it cannot do is
cause a record to change, because there is no line from it to the record along which a change
could travel. The assurance is that the line does not exist, which is checkable by inspecting
the software rather than by trusting an operator.

We hold that only the second is worth much to a business whose records matter, and that the
first is what most platforms actually offer while describing it in language that sounds like
the second. The distinction is not about anybody's honesty. It is about what kind of thing is
being relied on: a rule, which is only as good as its enforcement, or a wall, which is as good
as its construction.

The composition is the claim. None of the three layers is novel. Separating the intake of raw
material from its interpretation is ordinary good practice. Insisting that a processing step be
repeatable — that running it twice on the same input gives the same answer both times — is how
any auditable calculation has always been built. Requiring a person to approve a change before
it takes effect is as old as double signature on a cheque. What we hold is that assembling the
three so that inference is structurally outside the write path, rather than administratively
restrained within it, converts a promise into something a stranger can verify.

## 2. The problem, in the reader's terms

A company has a policy that the filing room is restricted to three named staff. The policy is
genuine. It is written down, everyone knows it, and breaches are disciplined. It is also a
rule, which means its effectiveness depends on people: a temporary worker who is let in
because they seemed to need something, a door left propped on a warm day, a manager who
overrides it for a good reason and sets a precedent for a bad one.

Now suppose instead that the filing room has a lock, and the three named staff hold the only
keys. The policy has not changed. What has changed is that a fourth person's not entering is
no longer a matter of anyone's compliance. They cannot enter. If they do enter, something
physical happened — a key was copied, a lock was forced — and that something leaves traces and
required effort.

Every serious institution understands this distinction and acts on it constantly. A bank does
not rely on a policy that tellers will not take money from the vault; it relies on a vault. A
pharmacy does not rely on a rule that controlled drugs stay in the cabinet; it relies on a
cabinet with a lock and a register. The pattern is so familiar that its absence from software
goes unnoticed: in most business systems, the equivalent of the drug cabinet is a setting.

We think this is the single most useful question a non-technical owner can put to a software
supplier about AI, and it is answerable without any technical vocabulary: *is what you are
describing a rule or a wall?* If AI is prevented from changing records by a configuration, a
policy, or a promise, it is a rule. If it is prevented because no connection exists, it is a
wall. Both are worth having. They are not the same kind of thing, and the difference matters
most precisely when something has gone wrong, which is when rules are least reliable.

There is a second, quieter reason to prefer the wall, and it concerns what an examiner can do
afterwards. With a rule, establishing that AI did not alter a record means examining logs
produced by the same system that would have done the altering. With a wall, it means examining
the shape of the system: if the outer layer has no write path, then no log needs to be trusted
to establish that it did not write. The first is an investigation. The second is an
architectural fact.

## 3. What "deterministic" means, and why records belong there

### Two different kinds of computer program

There is a distinction here that almost nobody outside software has had reason to learn, and
the whole argument depends on it, so it is worth building up slowly.

Most computer programs are **deterministic**. Given the same input, they produce the same
output, every time, forever. A payroll calculation is deterministic: the same hours, the same
rate, and the same tax table produce the same net pay in January and in July, on this machine
and on that one. If you want to know why a program produced a particular answer, you can run it
again on the same input and watch it produce the same answer. If you disagree with the answer,
you can trace the steps, because the steps are fixed.

A **language model** — the kind of program people mean when they say AI — is not like this. It
works by having been trained on an enormous quantity of text and, given a prompt, producing
text that is statistically plausible as a continuation. That is a genuinely useful thing to be
able to do: it will draft a letter, summarise a long document, suggest a category for an
uncategorised item, or answer a question in ordinary language. It is also a different kind of
thing from a calculation. Ask it the same question twice and it may answer differently. Ask it
something it has no basis for and it will usually produce a confident answer anyway, because
producing plausible text is what it does and declining is not its natural behaviour.

We are not making an argument against language models. We use them and we intend to use them
more. The local one we run is a fully open model published by a research institute, which
matters to us because a model whose weights and training data are public can be examined,
retained, and run indefinitely without anyone's permission [olmo3-allenai]. The argument is
narrower: a program of that second kind should not be the thing that decides what a business's
authoritative record says, because the essential property of a record is that it is fixed and
traceable, and the essential property of a language model is that it is neither.

### Where the two kinds go

The middle layer of this design is deterministic, entirely. It parses documents, builds the
structured knowledge, maintains the index that makes things findable, and writes the structured
records. Because it is deterministic, it is replayable: an examiner who questions a
classification can re-run the same step against the unaltered inner-layer record and get the
same answer. Nothing in the authoritative record varies between runs, because nothing that
varies between runs was allowed to produce it.

Structured data — the numbers, dates, identifiers, and categorised fields a business actually
relies on — is never routed through a language model at all. That is not a preference expressed
in a policy document; it is a binding design decision that the middle layer's own construction
reflects. The companion rule governs writing: nothing in the outer layer writes to the
structured knowledge stores or to the record beneath them, by any path.

### What the inner layer does with what it receives

The inner layer's job is narrow. Each of its services accepts raw material from one outside
source — a filesystem, a mailbox, an uploaded document, an identity directory — and writes it to
a record without transforming or classifying it. Nothing is interpreted at this stage; things
are only stored. The inner layer also runs separately for each tenant — one process with its
own storage root per tenant, rather than one shared store holding everybody's raw material
together. The container that storage belongs to is a Totebox Archive: a self-contained,
portable, and encrypted repository for data and applications, designed for long-term storage
and secure access. What such a container is, and why it is built to be handed over rather than
exported from, is the subject of a separate paper on this site.

The record it writes to is append-only. Nothing is ever altered in place. Each entry carries a
fingerprint computed from the entry before it, so altering any past entry would visibly break
every entry that follows — the same construction used by the public systems that police the
security certificates the whole web depends on, and specified in a published internet standard
[rfc-9162]. Completed portions are marked read-only on disk, and the programming interface
exposes no operation that removes or modifies an entry, so the capability is absent rather than
merely discouraged.

One honest limit belongs here. An unalterable record says nothing about whether what was
written into it was correct. If a wrong figure is entered, the record faithfully preserves the
wrong figure forever, alongside any correction that follows. Correctness is the job of the
human review step before a record is committed; the storage layer's job is only to make sure
that what was committed cannot be quietly changed afterwards. Confusing the two is the most
common way a claim about tamper-evident records gets overstated, including by us if we are not
careful.

### And what "optional" means in practice

Because the dependencies run one way only — the middle layer reads the inner, the outer reads
the middle, and nothing reads backwards — the two inner layers contain no reference to the
outer one anywhere. A deployment that excludes the AI layer is not a deployment with AI turned
off. It is a deployment in which the AI software is not present: fewer programs running, less
surface exposed, and no external network requirement to justify to whoever asks. For a business
under a rule that prohibits sending data to outside services, this is the difference between
demonstrating a configuration and demonstrating an absence.

## 4. Where inference actually sits

### One door, not ten

If every program in a system can call an outside AI service, then every program is its own
opening in the wall. Ten programs with ten openings means ten places where credentials are
kept, ten places where calls might go unlogged, and ten separate things to inspect when
somebody asks what left the building.

This design has one opening. A single component is the only place an inference request can
pass through, and it is the only place that holds credentials for any outside model. No other
part of the system holds such a credential or makes an outbound call to an external model. This
is not a convention that programs are asked to follow; it is where the credentials are, which
means a program that tried to go around the door would have nothing to present when it
arrived.

At that one door, every request is recorded. The entry notes the time, a request identifier,
which tenant it belonged to, which compute tier answered it, which model, how long it took, an
estimated cost, and whether it completed or failed; each entry carries a fingerprint computed
when it is written. The record is append-only — nothing in it is modified or deleted after the
fact. The consequence for an owner is that "what did this system send to an AI, and when" is a
question with a complete answer held on the owner's own equipment rather than the supplier's.

The entry also carries a field marking whether the outbound content was cleaned before it
left. The field exists; the cleaning it refers to does not, and the next section says so
plainly rather than letting the field's presence imply otherwise.

### Three places the computing can happen

Inference is not one thing, and where it runs is the decision that matters most for anyone with
records they cannot let out of the building. Three placements are available, chosen deliberately
per deployment rather than assumed:

**On the owner's own hardware.** A modest open model runs locally, on the machine in the
building. No request leaves the premises. There is no per-request cost, because there is no
outside party to bill it. The reference unit for this is a small appliance in the three hundred
to fifteen hundred dollar range depending on the size of the business, with an intended monthly
operating cost of zero — no subscription, no cloud fee, no per-seat charge. It handles the
routine work: short answers, mechanical edits, lookups against the business's own records.

**On a larger machine, briefly.** For work the local model cannot do well — long documents,
translation, heavier reasoning — a larger model runs on a graphics machine that is started when
needed and shut down when idle, on a default idle window of half an hour. That machine may be
rented capacity or one the owner has bought, at the owner's choice; either way the owner
controls when it starts and stops, and the request still passes through the same single door
and is recorded in the same place.

**At an outside service.** For a narrow set of precise tasks, a request may be sent to an
external model provider. This is the placement that concerns anyone with confidential records,
and it is the placement where this design's obligations of honesty are heaviest — Section 5 is
where they are met.

Most deployments are intended to operate without the third placement at all. It is off by
default and it is off today, for reasons the next section gives.

### The person at the checkpoint

Whatever the outer layer produces is a proposal. Text the operator reads. A draft the operator
approves or discards. A suggested classification the operator accepts or overrides. Every
accepted proposal reaches the authoritative record by being written through the middle layer's
own write path, with a person deciding that it should be.

This is where a reader should press hardest, and we would rather press first. A human checkpoint
is only worth what the human's attention is worth. A person approving the fortieth
AI-drafted item in an afternoon is not performing the same act as a person approving the first,
and a design that counts on sustained scrutiny without doing anything to sustain it is relying
on a rule again, wearing the costume of a wall. Our structural claim is exact and narrower than
it might be read as: no change reaches the record without a deliberate human act. It is not a
claim that the human act was well-considered. The gap between those two is real, we do not
have a solution to it, and it is the first item in the invitation below.

## 5. Where the wall is unfinished

Four things in this design are not what a reader of the sections above might reasonably assume,
and they belong here, in the paper's own voice, rather than in a footnote.

**Personal and location details are not removed from a prompt before an external call.** The
single door does not scrub personally identifying information or location data from what it
sends onward. The only sanitising code that exists on the platform today removes secrets — keys,
tokens, passwords — and it runs solely on the path that writes training examples into the
learning corpus, never on the path toward an external model. This is a compliance-relevant gap
rather than a cosmetic one, and the specific consequence for a regulated business is worth
stating without softening: were external calls switched on today, a prompt containing client
names, ledger entries, or property and owner records would reach the outside model with those
details intact. Any confident claim that this platform protects such content on that path would
be false until a real scrubbing mechanism is built and independently checked.

**External calls are not switched on.** There are no live calls to any outside model provider in
the current release. The software that would make them exists and is wired against a test
stand-in rather than a real endpoint, and the list of task types permitted to make such a call
is fixed when the software is built and cannot be extended while it runs. Switching them on is a
deliberate, separate decision, not a build in progress. The gap above is therefore not currently
exposing anything — but it is the reason the switch stays off, and stating one without the other
would mislead in either direction.

**The deliberately AI-free operating mode is not built as a mode.** The design requires that
everything load-bearing keeps working when no inference is available anywhere, and that
requirement is met: the record store, the knowledge queries, the keyword search, the audit
queries, and the health checks all work with no inference tier at all. What does not exist is a
distinct, labelled mode for it — an operator's view that says plainly "AI is disabled here" and
turns AI-dependent commands into graceful no-operations rather than errors. The capability
survives without inference; the presentation of that fact to an operator does not yet exist.
This is the thinnest of the four gaps and the one most likely to be closed first, and it is
still the difference between a property and a property a customer can see.

**No spending limit governs where a request is sent.** Costs are tracked and prices are
configured, but nothing currently connects a tenant's accumulated spend to a routing decision.
An owner who wants a hard ceiling on what AI can cost them in a month does not have one in
software today.

Two further limits belong in this section because they bear on the strength of everything above.

The first concerns a design rule we hold but do not yet enforce. The platform's stated topology
has command and data moving in one direction only, from an authoritative side to a subordinate
side, with no return path capable of carrying instructions. Several real mechanisms follow that
rule in their own domains — the strongest of them governs how source code reaches production and
actively refuses the reverse case. But no component enforces the rule by name, checks conformance
to it, or refuses traffic for violating it. A reader assessing this platform's isolation should
treat the one-way property as an architectural intention supported by the current shape of the
code, not as a checked invariant. We think naming this plainly is more useful than the
alternative, since the whole argument of this paper is that the distinction between a rule and a
wall is the thing worth knowing — and here, on this specific point, what we have is a rule.

The second concerns the floor everything stands on. Every boundary described in this paper is
enforced by well-tested application software running on ordinary operating systems. The
strongest version of this design would have the boundaries enforced by the small core program
that decides what every other program on a machine may touch, and specifically by one
mathematically proven to enforce exactly those boundaries and nothing else
[sel4-klein-2009-sosp]. That is the direction the software is written toward, and a companion
paper on this site sets out that arrangement — Capability Geometry — in full. No platform service
runs on seL4 today; the services that carry live traffic are ordinary programs on ordinary
operating systems.

One smaller matter, for completeness, because it is the kind of detail that gets omitted from
papers like this one. The tag identifying which tenant a request belongs to is enforced strictly
on the knowledge-graph paths, which refuse a request whose tag is missing or malformed. On the
main inference path, a malformed tag is refused but an absent one falls back to a default with a
warning logged — a narrower guarantee on that path than on the others.

## 6. What this changes for the owner

The first change is the shape of the question an owner has to ask. Instead of "do I trust this
supplier's policy about AI," the question becomes "can this system's AI write to my records at
all, by design." That question has an answer somebody can check by inspecting how the software
is put together, and it has the same answer regardless of who is operating it, how tired they
are, or what the commercial relationship looks like next year.

The second change is what an examiner can establish. Because the middle layer is deterministic
and replayable, a disputed classification can be re-derived from the unaltered inner record and
shown to produce the same answer. Because the outer layer has no write path, establishing that
AI did not alter a record does not require trusting any log. And because every inference request
is recorded at a single door on the owner's own equipment, "what did this system send to an AI"
is answerable from records the owner holds.

The third change is what a deployment can be. An owner who cannot send data outside their
premises is not choosing a restricted version of the product. They are choosing a deployment in
which the software that would send data outside is not installed, and everything load-bearing
works anyway.

The trade-offs belong in the same paragraph. Keeping structured data out of the AI layer means
giving up the conveniences that come from letting a language model operate directly on
records — which is a real cost, and it is what many buyers are actually shopping for. A human
checkpoint on every change is slower than no checkpoint, and its value depends on attention we
cannot guarantee. Running inference on the owner's own hardware means the owner's hardware sets
the ceiling on what the AI can do, and a small appliance's ceiling is genuinely low. And on the
specific matter a regulated buyer cares most about — content leaving for an outside model — what
protects them today is that the switch is off, not that a scrubbing mechanism exists.

## 7. An open invitation

The position in this paper is one we hold with confidence. Several of the problems it leaves
open belong to specialists, and we would rather work them with those specialists than pretend
they are closed.

To researchers in AI safety and human-factors security: the checkpoint problem in Section 4 is
the one we are least able to solve alone. A design where nothing changes without a human act is
structurally sound and behaviourally uncertain, because approval fatigue is real and well
documented in every other domain where it has been studied. What would actually preserve
scrutiny at the fortieth item — rate limits, sampling, forced diffs, adversarial second opinions,
something else entirely — is an empirical question we would rather have answered by field study
than by our own intuition.

To systems-security researchers: our claim is about the absence of a write path, which is a
claim about the current shape of the code. An absent capability is a property any future change
can silently remove, whereas a mechanism that refuses an unauthorised write is a property that
survives. What a positive mechanism at that boundary would look like — something that refuses,
rather than merely does not attempt — and whether it can be built without reintroducing a
trusted intermediary of the kind this whole architecture avoids, is real unsolved design work.

To privacy engineers and data-protection practitioners: the gap in Section 5 is the one with a
deadline attached, because it must close before external calls can be switched on for any
regulated use. We are specifically unsure how much of it is solvable at all. Removing names and
addresses from a prompt is tractable; removing enough that a prompt about a particular building,
lease, or transaction is no longer re-identifiable, while leaving it useful enough to be worth
sending, may not be. We would rather be told that early than discover it after building the
wrong mechanism.

To auditors and assurance professionals: replayable, deterministic processing over an
append-only record is, we think, unusually good evidence by the standards of what software
normally offers an examiner. It is also not a recognised form of evidence in any assurance
standard. What documentation, procedure, and independent attestation would be needed before a
replay against a customer-held record could substitute for a management representation is a
question for that profession rather than for us.

And to anyone who buys software for a regulated business: the question in Section 2 — rule or
wall — is one we would like to see asked of us as hard as of anyone else. If the question turns
out to have a version we cannot answer well, we would rather learn that from a buyer's
scepticism than from an incident.

## 8. Conclusion

The assurance worth having about AI and a business's records is structural. AI should be able to
read finished records and propose changes to them, and it should have no path by which a change
could be written, so that the guarantee rests on the construction of the system rather than on
anybody's compliance with a rule. That is the design: raw material into an unalterable record,
structured knowledge produced by repeatable computation with no language model anywhere near the
structured data, inference in an outer layer that reads and proposes and cannot write, and a
person at the checkpoint for every change that lands. Two of those layers run today and carry no
dependency on the third, so a deployment may leave the third out and still be complete. What
does not run is the removal of personal detail before an outside call, the outside call itself,
the labelled AI-free mode, a spending ceiling, and the verified machine core beneath all of it.
The industry's answer to "will your AI touch my records" has been a promise for as long as the
question has been asked. We hold that a promise is the wrong kind of answer, and we intend to
build the other kind.

## References

Klein, G., et al. 2009. seL4: Formal verification of an OS kernel. *ACM Symposium on Operating
Systems Principles.* [https://doi.org/10.1145/1629575.1629596](https://doi.org/10.1145/1629575.1629596)

Allen Institute for AI. *OLMo 3 — open language models with open weights and open training
data.* [https://allenai.org/olmo](https://allenai.org/olmo)

Laurie, B., Messeri, E., and Stradling, R. 2021. *RFC 9162 — Certificate Transparency Version
2.0.* Internet Engineering Task Force. [https://www.rfc-editor.org/rfc/rfc9162.html](https://www.rfc-editor.org/rfc/rfc9162.html)

## Contributors

Prepared by Woodfine Management Corp.

## How this paper was produced

This paper is grounded in the operating and development work the preparing staff do themselves, and in what they have learned from the people they work with routinely: the graphic designers, web developers, and software developers and engineers who build the platform alongside them, and the architects and structural, building-services, and civil engineers they develop buildings with. No outside professional reviewed or approved this paper, and nothing in it is professional advice. It was drafted and edited with AI assistance under editorial direction, and the analysis and conclusions are Woodfine's own.

## Disclosures

Woodfine Capital Projects Inc. ("Woodfine") is the author of record. PointSav Digital Systems,
which builds the platform described, is currently a trade name of Woodfine, planned to become a
wholly-owned Woodfine subsidiary upon incorporation; PointSav does not itself offer, sell, or
solicit any security. The architecture described is our own; the components discussed are
software we wrote or intend to write, and the hardware and deployment arrangement described in
Section 4 is our own commercial model, so this paper argues for an approach we have a commercial
interest in. This work was funded internally; no external research funding was received. The
discussion of regulated deployment in Sections 3 and 6 describes a design and its limits in
general terms; it is not advice on any organisation's obligations under any data-protection,
records, or sectoral regime, and nothing here should be read as asserting that any particular
regulatory requirement is satisfied. This paper's content is provided for engineering,
operational, and research purposes and does not constitute investment advice or a solicitation to
invest in any Woodfine direct-hold solution. Some statements above describe planned or intended
future work; language such as "planned," "intended," "targeted," "may," and "expected" marks
this forward-looking content, which is subject to change and does not constitute a commitment
regarding future performance.

## Data and reproducibility

The specific version numbers, model identifiers, ledger field names, and cost figures behind
this paper's claims are recorded in the platform's own engineering documentation rather than
restated here in full; this paper reports the shape of what exists rather than an inventory of
the implementation. The append-only record store described in Section 3 is an early-stage,
independently tested open-source component with its tests passing as of this paper's
preparation, and its programming interface exposes no operation that removes or modifies a
stored entry — something any reader with access to the source can confirm directly. The
external-model client described in Sections 4 and 5 was read directly for this paper: it
contains no live calls in the current release, is wired against a test stand-in rather than a
real provider, and carries its list of permitted task types as a value fixed when the software
is compiled, so the list cannot be widened while the software runs. The local model named in
Section 3 is published by an external research institute with open weights and open training
data, which is why it can be run and retained indefinitely without anyone's continuing
permission. The hardware cost range in Section 4 is an estimate for the reference appliance
class at the two smallest business sizes, not a quoted price, and the stated zero monthly
operating cost describes the absence of any subscription or per-seat charge from us rather than
the absence of electricity and maintenance. The code is open source, published in full including
its tests, under licences that in one case require anyone running a modified version as a network
service to publish their changes as well. No independent party has audited this software,
verified these boundaries, or reviewed these claims; in particular, the claim that no write path
exists from the inference layer to the authoritative record has been checked by us and not by
anyone else.

Totebox Archive™, Capability Geometry™, PointSav Digital Systems™, and Woodfine Capital
Projects™ are trademarks of Woodfine Capital Projects Inc.
