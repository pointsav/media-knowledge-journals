---
schema: journal-v2
slug: version-trail-for-buildings
title: "A Version Trail for a Building's Equipment"
subtitle: "Treating equipment history as a record accountable to a person, not a stream of readings"
site: home.pointsav.com
imprint: PDS-011
thesis: "A building's equipment becomes accountable when its history is kept as a signed, ordered record inside the building's own archive rather than as raw telemetry."
abstract: |
  Our thesis is that a building's equipment becomes accountable the moment its history is
  kept the way a well-run business keeps its books — ordered, unalterable, timestamped, and
  attributable to a named responsible person — rather than as a stream of sensor readings
  passing through whichever vendor supplied the equipment. The record belongs in the
  building's own archive. A PropertyArchive is a Totebox OS archive for a physical property,
  anchored to a Land Title parcel identifier or legal address, holding permits, lifecycle
  records, building drawings, sensor data, the lease register, and the maintenance history. A
  building of 2000 vintage with a heating and cooling system installed in 2020 has two vendors
  and two eras of technology that often cannot see each other at all, and no cooperation
  between them produces one answer to "who changed this, when, and on whose authority."
  Bringing every device under one record-keeping discipline inside that archive produces the
  answer, as a one-time integration cost for the building rather than a recurring charge per
  device or per seat. This paper concerns operational and equipment history; where a
  building's design record should be hosted is argued separately. The main limits: the record
  store and the double-entry construction
  ledger that demonstrate the discipline are real and running, while the companion files and
  sensor-ingestion path that would carry equipment history into a PropertyArchive are a
  specified layout rather than shipped components. No PropertyArchive is in service today.
state: draft
version: "0.1.0"
published:
updated: "2026-09-21"
cite_as:
license: CC-BY-4.0
cites:
  - ifc-4-3
  - iso-19650
  - rfc-9162
  - c2sp-signed-note
  - sigstore-rekor-v2
  - eidas-qualified-preservation
draws_from:
  - asset-anchored-bim-vault
  - totebox-archive
  - worm-ledger-architecture
  - source-of-truth-inversion
  - tool-construction
  - flat-file-bim-leapfrog
  - economic-model
  - tier-zero-customer-side-sovereign-specialist
  - customer-hostability
  - three-ring-architecture
prepared_by: "Woodfine Management Corp."
keywords:
  - building operations
  - maintenance history
  - append-only records
  - open standards
  - equipment accountability
---

# A Version Trail for a Building's Equipment

*Treating equipment history as a record accountable to a person, not a stream of readings*

> This paper is provided for engineering, operational, and research purposes and does not
> constitute investment advice or a solicitation to invest in any Woodfine direct-hold
> solution. Statements marked "planned," "intended," "targeted," "may," or "expected" are
> forward-looking and subject to change. Full disclosures appear at the end of this paper.

Working Paper PDS-011 · v0.1.0 · CC BY 4.0

Our thesis is that a building's equipment becomes accountable the moment its history is kept
the way a well-run business keeps its books — as an ordered, unalterable, timestamped record
attributable to a named responsible person — rather than as a stream of readings passing
through whichever vendor supplied the equipment. The difference is not a matter of software
quality. It is the difference between a pile of measurements and a record somebody can be
asked about.

Take an ordinary case. A building goes up in 2000. Its heating and cooling plant is replaced
in 2020. That is two vendors, two eras of technology, and two control systems that in practice
often cannot see each other at all. Add an access-control system from a third supplier, meters
from a fourth, and a lighting controller from a fifth, and the building's operating history
exists in five places in five shapes, three of which are only reachable through a portal
somebody else operates. Now ask the question an owner actually asks, usually at the worst
moment: who changed the setting on this plant, when, and on whose authority? In most buildings
the honest answer is that nobody knows, and the reason is not carelessness. It is that nothing
in the arrangement was ever a record.

Our position is that every device's history should be brought under one record-keeping
discipline, once, inside the building's own archive. A PropertyArchive is a Totebox OS archive
for a physical property, anchored to a Land Title parcel identifier or legal address,
containing permits, lifecycle records, building drawings, sensor data, the lease register, and
the maintenance history. Do that and the "who, when, on whose authority" question becomes
answerable for the whole building regardless of how mismatched its underlying equipment is —
and bringing a new device under the discipline is a one-time integration cost for that
building rather than another recurring licence. This paper is about ongoing operational and
equipment history specifically; where a building's *design* record should be hosted, and why
each building should have its own record server for it, is a separate question argued on our
building-information site. Two things are real and running: the append-only record store, and
a double-entry construction ledger that demonstrates the discipline against a live project.
The path that would carry equipment readings and work orders into a PropertyArchive is a
specified layout rather than a shipped component, and the paper says so where that matters.

## 1. The thesis

A sensor reading and a record are different things, and treating the first as though it were
the second is the whole of the problem.

A reading is a measurement at a moment: this coil was at eleven degrees at 4:02. It is
perishable, enormous in volume, and answers only one kind of question. A record is a statement
that something was done, by whom, when, and on what authority: the setpoint was lowered two
degrees on the fourteenth by the facilities contractor under work order 3391. A building
generates readings by the million and records by the hundred, and it is the hundred that
determine whether anyone can be held to account.

The discipline that turns statements into a usable history is not new and it is not
technological. It is bookkeeping. A business with good books can answer "who authorised this
expense and when" for any transaction, across years and across several bookkeepers, because
each entry was made in order, was never erased, referenced the authority for it, and can be
traced. Our claim is that a building's equipment history should be kept to exactly that
standard — ordered, unalterable, attributable — and that once it is, a pile of mismatched
building systems becomes an accountable whole without any of the equipment being replaced.

The composition is the claim, and each part of it is ordinary on its own. Append-only
bookkeeping is centuries old. Version control — software that records every change to every
file, by whom and when, and lets any earlier state be reconstructed — has been standard
practice among software engineers for decades. And open, text-based standards for building
information have been maintained by an international industry body since 1996 and published
through the International Organization for Standardization [ifc-4-3]. What we hold is that
assembling the three, inside a container that belongs to the building rather than to any
supplier, is what makes a fifty-year-old building with a five-year-old boiler accountable, and
that the cost of doing so should be a one-time project cost for that building rather than a
tax on every device in it.

## 2. The problem, in the reader's terms

Anyone who has run a business with properly kept books, or been asked a question by an
auditor, already knows the standard being proposed here.

Ask a well-run company who authorised a payment made four years ago and the answer takes
minutes, not because anyone remembers but because the books were kept. The entry exists in a
definite sequence. It was never erased — a correction, if one was needed, is a later entry that
refers back to the original, and both are still there. It records the authority: an approval, a
purchase order, an initial. And it can be traced forward and backward, because every entry
sits in the same ordered series as every other. Three bookkeepers may have come and gone in
the interval. The books did not go with them.

Now ask the same company who changed the temperature schedule in their building four years
ago. The answer, in almost every case, is that they cannot find out. The control system's own
log, if it has one, keeps a rolling window measured in weeks. The contractor who did the work
has an invoice, which records that a visit happened but not what was changed. The
building-management portal belongs to a supplier whose product has since been replaced, and
the historical data did not come across. And the reading data — the temperatures themselves,
which do exist somewhere in quantity — cannot answer the question at all, because a
temperature is not an authority.

This is the gap, and it is worth naming exactly what is missing rather than gesturing at poor
software. Three properties that any bookkeeper takes for granted are absent from almost every
building's operating history:

**Order.** Building data is usually timestamped but not sequenced. Two changes made minutes
apart by different parties may appear in a log in either order, or in two different logs, and
nothing settles which actually came first.

**Permanence.** Building data ages out. It is stored on the assumption that its value is
operational — useful this month for tuning, worthless next year — which is the correct
assumption for readings and precisely the wrong one for changes.

**Attribution.** Building data records that a value changed, not who caused it to change.
A shared login on a control panel is the normal case, not the exception, and it destroys
attribution entirely.

An owner who wants accountability from their building is asking for the same three properties
their accountant already provides, applied to a different subject. Nothing more exotic than
that is required, and nothing less will do.

## 3. What makes a record a record

### Readings, streams, and logs

Three words are used loosely in this field, and the distinction between them is where the
argument lives.

A **sensor** is a device that measures something and reports it — a thermometer, a meter, a
motion detector, a switch position.

A **stream** is what a sensor produces: a continuous flow of readings, typically sent
somewhere the moment each is taken. Streams are designed for immediacy. Their natural
destination is a dashboard or a control loop, and their natural fate is to be aggregated into
averages and then discarded, because storing every reading from every sensor in a large
building for decades would be both expensive and pointless. This is not a flaw. A stream is
the right shape for its job.

A **log** is a different thing: a sequence of entries, each appended in order and never
altered, kept because the sequence itself is the point. A ship's log, a visitor book, and a
general ledger are all logs. The essential property is not that they store information but
that they store it in an order that cannot be revised, so that "what happened, in what order"
has one answer rather than several.

Building automation, as an industry, is very good at streams and has almost no tradition of
logs. That is the asymmetry this paper is about.

### What an append-only record adds

An append-only record is a log with two additional properties that matter when the record may
need to be relied on by someone who was not there.

The first is **tamper evidence**. Each entry carries a short fingerprint computed from its
contents together with the fingerprint of the entry before it. A fingerprint of this kind — a
cryptographic hash — is a short string derived from data such that changing even one character
of the data produces an entirely different string, and such that nobody can work backward from
the string to the data. Because each entry's fingerprint depends on the previous entry's,
altering any past entry changes its fingerprint, which changes the next entry's, and so on to
the end of the record. The alteration is visible in every entry that follows. A bound ledger
with numbered pages achieves something similar by physical means; this achieves it by
arithmetic, and can be checked by anyone with a copy.

The second is a **signed checkpoint**: a dated, sealed statement that the record, as of this
many entries, has this fingerprint. A digital signature is a seal only the holder of a
particular private key can make and anyone holding the matching public key can check — like a
wax seal whose pattern everyone knows but whose stamp only one person owns. A checkpoint is
what lets a third party establish that nothing before a given date has been altered since,
without needing access to the live system and without trusting whoever runs it. The
checkpoint format used here is a small, plain-text public specification maintained by a working
group of engineers who build records of exactly this kind [c2sp-signed-note].

In this platform's record store, the append-only property is enforced three ways at once
rather than by convention. The programming interface exposes no operation that removes or
modifies an entry, so the capability is absent rather than discouraged. Completed portions are
marked read-only on the disk itself. And the fingerprint chain makes any retroactive change
detectable by arithmetic. A property maintained by policy can be waived by whoever sets the
policy. A property maintained these three ways cannot be waived without leaving evidence.

### Attribution, and the limit of all of this

An entry that says a setpoint changed is worth considerably less than one that says who
changed it. The discipline being argued for therefore requires that each entry carry the
responsible party — not a shared panel login, but the specific approved party whose
cryptographic key the entry was written under — and, where one exists, the work order the change
was made under.

The limit belongs here rather than in a section of its own, because it is the most commonly
overstated thing about records of this kind. An unalterable, attributed record says nothing
whatever about whether what was written into it was true. If a contractor records that a
filter was replaced and it was not, the record faithfully preserves that claim forever. What
the record gives is that the claim was made, by an identified party, at an identified moment,
and cannot later be quietly revised when the consequences arrive. That is a great deal less
than truth and a great deal more than a building's operating history normally offers.
Correctness is the job of the human review step at the point a record is committed, not of the
storage.

## 4. Where the history lives

### Why the building, and not the portfolio or the vendor

The container for this record should be the building's own, for the same reason a land title
office indexes ownership by the parcel rather than by whoever the current owner's lawyer
happens to be. A building outlives its architect, its builder, its first owner, every
contractor who has ever worked on it, and every piece of software used to design or manage it.
Buildings are ordinarily designed to stand for fifty to a hundred years. Design and
management software typically changes its file format with every major release and is often
unreadable by competing products within a decade. Anything organised around the software is
organised around the shortest-lived participant.

So: one archive per building, anchored to the building's own legal identity. A **Land Title
parcel identifier** is the number a land registry assigns to a specific parcel of land — the
same identifier a lawyer uses to establish what is being bought and sold — and anchoring the
archive to it, or to the legal address, means the record is organised around the thing that
persists rather than around a management arrangement that does not.

A PropertyArchive is one kind of Totebox Archive: a self-contained, portable, and encrypted
repository for data and applications, designed for long-term storage and secure access, of
which each is a single file that can be stored on any storage medium. People and companies get
their own; a building gets a PropertyArchive. The general case — what makes such a container
self-contained, why it boots and runs rather than merely being readable, and what a handover of
one involves — is argued in a companion paper on this site; here the point is only that the
container the equipment history belongs in is the building's, and the building's alone.

### What is inside, and what is not the record

The specified authoritative contents of a PropertyArchive are plain-text and standardised files
in a defined layout — specified being the operative word, as the close of this section sets out
exactly which parts of it exist as software today. The drawings are held in the international
building-information standard,
whose standard file encoding is line-oriented clear text: a person with a text editor can read
one, and an ordinary file comparison between two versions shows exactly which elements changed
[ifc-4-3]. Alongside each element that carries non-geometric operational data sits a small
companion file, named by that element's own stable identifier from the drawing standard — an
identifier that survives revisions of the model, which is what allows a fifteen-year history to
attach to a particular air handler rather than to whatever the air handler was called in the
2011 drawing set. Those companion files are where the equipment history goes:

- **Property values** for the element that the drawing itself does not carry.
- **Sensor readings**, timestamped, written as append-only entries rather than as a live stream.
- **Work orders** — references to maintenance tasks, inspection records, and repair history by
  work-order identifier.
- **Lease references** — which tenant holds the space the element serves, on what term.

Because a companion file is a plain text file held under version control in the same
repository as the drawings, every change to the sensor history or the work-order history lands
as a recorded commit: a dated, attributed, ordered change that can be reconstructed. That is
the design's central mechanical move — the building's operating history versioned alongside its
geometry, rather than in a separate system with a separate fate.

Equally important is what is explicitly *not* the record. The pictures a viewer draws on
screen — the three-dimensional visualisation, the two-dimensional sheets — are marked as
regenerable derivatives. They can be discarded and rebuilt from the authoritative files at any
time, and nothing depends on their survival. This matters more than it sounds: the usual reason
a building record is lost is that what everyone treated as the record was a rendering produced
by a tool that no longer exists.

Organised this way, the archive qualifies as what the international building-information
management standard calls a common data environment — the single agreed place where a
building's information is collected, managed, and shared [iso-19650]. That standard is
deliberately technology-neutral, and a version-controlled directory on a single workstation
with no network connection satisfies it as fully as a hosted platform does. A reader should
hold that fact steady against the sales proposition that only a cloud service can provide
governed building information. The standard does not say so.

### Where this stands

The record store underneath — append-only, fingerprint-chained, checkpointed — is real, tested,
open-source software with its tests passing, and the monthly publication of its checkpoints to
a public record runs today on a live schedule. What is not built is the equipment-history path
specifically: the companion-file layout above is a specification, and the software that would
take readings from a building's actual control systems and write them into a PropertyArchive as
attributed append-only entries does not exist yet. The building application in development
today is real code with no tests. And the record store's own storage shape is currently simpler
than its design calls for — a single file rewritten in full on each append, which is an
accepted trade-off at present volumes and will not remain one. No PropertyArchive is in service
in any building today.

## 5. One cost per building, not a cost per device

### What the current arrangement actually charges for

The prevailing commercial shape in building technology is a recurring charge tied to a count:
per device, per point, per seat, per building per month. It is a reasonable model from the
supplier's side and it has a specific consequence for the owner, which is that the cost of
knowing what your building is doing never ends and grows with the building's own
instrumentation. Adding twenty meters adds twenty recurring line items, and when a supplier
retires a product line the history held inside it can go with it.

It also has a subtler consequence that owners notice late. Because the charge is recurring and
the data lives with the supplier, the supplier's continued existence is a precondition of the
history's continued existence. An owner who stops paying does not merely lose new
functionality; they lose the archive, which was the part that took fifteen years to
accumulate.

### The shape we are arguing for

Integrating a building's mismatched equipment into that building's own archive is a project.
Somebody has to work out how each system reports, write the connection, and map its output into
attributed append-only entries. That work is real, it costs money, and we are not pretending
otherwise. What we hold is that it should be a **one-time project cost for that specific
building**, amortised across the building's life the way any other capital improvement is, and
not a recurring per-device licence.

Two structural things make that possible rather than merely desirable. The first is that the
archive holding the result belongs to the owner and runs on the owner's own equipment, so there
is no metered service in the path whose meter has to keep running. The reference appliance for
this sits in the three hundred to fifteen hundred dollar range depending on the size of the
business, with an intended monthly operating cost of zero: no subscription, no cloud fee, no
per-seat charge from us. The second is that the software holding the records is free. One
operator with one archive is a free deployment, published under licences that let anyone run,
inspect, and modify it, and we earn nothing from it. Our charge sits one level up, on the
component that answers a single question across many archives at once — which is a real
convenience for an owner with a portfolio and is not a precondition of any individual building's
record existing or remaining readable.

The candid version of the commercial claim: we are aiming at businesses whose whole annual
software budget for this kind of work runs in the five to fifty thousand dollar range, which is
too small for the enterprise building-technology sales motion and too regulated for consumer
tools. That is a deliberate position, not a modest one, and it is why the per-building
integration cost matters so much — it is the only cost in the arrangement large enough to be a
barrier, and it is a cost that gets paid once.

### The discipline is not hypothetical

There is a working demonstration of exactly this bookkeeping discipline applied to a building
project, and it is worth describing because it shows what the standard being argued for
actually produces.

A construction cost-and-schedule engine built on the same double-entry basis is real and
running against a live development project. It keeps two ledgers deliberately denominated
differently — one in physical quantities, hours and cubic metres and tonnes, and one in
dollars — as two named projections of a single journal rather than as separate books. Quantities
of different kinds are never added together: the engine refuses to sum hours with cubic metres
as a matter of construction, not convention. No running total is ever stored; every run
recomputes the whole ledger from its first entry, so the balancing identities are re-proved from
scratch each time rather than inherited from a saved figure that might have drifted. Its
correctness is checked against worked examples reproduced number for number, and on the live
project every balancing identity holds.

Two of its reporting rules are the point of mentioning it at all. It distinguishes a real zero
from an unmeasured figure and reports them differently: the money ledger currently reports
genuine zeros because no invoice or payroll record has entered it yet, and the progress columns
report nothing at all rather than a derived estimate, because no independent measurement of
installed quantity exists for that project yet. A system that would rather show an empty column
than a plausible guess is the one worth trusting with a building's history. Its own boundary is
equally plain: it runs as a set of command-line tools, and no operator-facing screen for it
exists or has been scheduled.

## 6. Where this construction comes from

The record-keeping machinery in Section 3 is not something we devised, and the honest account
of its origin is also the strongest argument for it.

Append-only records sealed with signatures and published so that anyone can check them were
developed to solve a specific public problem: how to police the issuance of the security
certificates that the entire web depends on, when the bodies issuing them cannot all be
individually trusted. The answer was to require every certificate to be entered in a public,
append-only log, and to define mathematically exactly what a party can prove about such a log —
that a particular entry is in it, and that a newer version of it merely extends an older one
without anything having been deleted or reordered. That work has been running in public since
the mid-2010s, and its current specification is a published internet standard [rfc-9162]. This
platform follows that specification's algorithms directly rather than inventing its own.

The same construction has since been applied to software supply chains, where a public log
records what was published and by whom so that anyone installing software can check it against
an independent record [sigstore-rekor-v2]. This platform's own checkpoints are published
monthly into that public log, on a live schedule, which means the claim "this record has not
been altered since that date" is independently checkable against something we do not operate.

What we are doing is applying the same machinery to physical building equipment rather than to
web certificates or software packages. The subject is different in one respect that matters: a
building's record has to remain readable for a great deal longer than a certificate's does. So
the design deliberately keeps its formats plain and its cryptography replaceable — the
fingerprint function and the signature scheme can both be changed for successors without
reformatting what already exists, which addresses the requirement, set out in European
preservation rules, that proof of a record's existence survive irrespective of future changes in
technology [eidas-qualified-preservation]. We hold no certification under those rules and have
not sought one; the alignment is a design choice, and stating it as anything more would be
false.

## 7. What this changes for the owner

The first change is that a question becomes answerable. Who changed this, when, under whose
authority, and under what work order — for any system in the building, at any point in its
history, however many contractors and however many product generations ago. That is not a
convenience. It is the difference between managing a building and reconstructing it after the
fact, and it is what an owner in a dispute, a purchaser's adviser, or an insurer actually
wants.

The second change is what an owner of an older building can do. The argument here requires no
equipment replacement. A building with a 2000 fabric, a 2020 plant, and three other vintages in
between can be brought under one coherent record without any of it being ripped out — what is
being upgraded is the record, not the hardware. For an owner who has been told that
accountability requires a wholesale controls replacement, this is a materially different
proposition and a very much cheaper one.

The third change is what happens when something ends. A supplier's failure, acquisition, or
discontinuation of a product changes who might be hired to work on the building. It does not
touch the record, because the record was never inside the supplier's system. And when the
building is sold, the intent is that the archive travels with the title: the buyer's adviser
begins from the building's complete attributed history rather than from whatever the seller's
various suppliers could be persuaded to export.

The trade-offs belong in the same paragraph. The integration project is real work with a real
cost, and for a small building with few systems it may simply not be worth doing. An
append-only record grows and never shrinks within a retention period, which is by design and is
also a cost in storage and in the discipline needed to keep it navigable. Attribution requires
that the parties touching the building's systems actually hold their own approved keys rather
than sharing a panel login, which is a change in working practice and is the part most likely
to be resisted on site. And the specific mechanism an owner of a building would most want — the
software that takes readings and work orders from real control systems and writes them into the
archive — is specified rather than shipped, so today this is a demonstrated discipline and a
working layout rather than a product a building owner can take delivery of.

## 8. An open invitation

The position in this paper is one we hold with confidence. Several of the problems it leaves
open belong to other people's professions, and we would rather work them with those professions
than around them.

To researchers in building automation and cyber-physical systems: the design assumes devices
that are merely heterogeneous — mismatched, old, uncooperative, but not lying. We have not
tested it against genuinely adversarial or malfunctioning equipment, and we do not know what an
attributed append-only record should do when a device reports readings that are internally
consistent and false, or when a compromised controller writes plausible entries at scale.
Whether the discipline degrades gracefully in that case or fails in an interesting way is a real
untested question.

To facilities managers and building operators: the attribution requirement asks the people who
actually work on a building to stop sharing a panel login. We think this is the single largest
practical obstacle in the whole design, larger than any technical one, and we would rather learn
from operators what would make it tolerable — or hear that it will not be — than design around a
guess. Similarly, what an operator would need to see on a screen before this record was useful
to them day to day, as opposed to useful to a lawyer in five years, is something we have not
established.

To records managers and archivists: a building's record has a retention horizon measured
against the building's own life rather than against a regulatory period, which is an unusual
case. What a fifty-year operational record should carry alongside its contents so that a reader
in 2080 can still interpret it — and what should be done about the readings, which cannot all be
kept and whose selective retention is itself a judgement — are questions we would rather put to
the profession than answer ourselves.

To insurers and forensic engineers: our claim is that an attributed append-only record makes a
building's operating history evidentially useful. Whether it actually would be — what an
adjuster or an expert witness would need in documentation, procedure, and independent
attestation before relying on such a record in place of a contractor's testimony — is a question
for people who do that work. We would value being told early if the answer is that it would
not.

And to anyone who has inherited a building with no usable history: the case we are least able to
address is the retrospective one. Everything above concerns a record started today and kept
well. What can honestly be done for a building whose first twenty years are already
irrecoverable, and whether a record that begins in the middle is worth what a complete one would
be, is a question we have not solved and would rather not pretend we have.

## 9. Conclusion

A building's equipment history should be a record, not a stream: ordered, unalterable,
timestamped, attributed to a named responsible party, and held inside the building's own archive
rather than inside whichever supplier happens to be current. Where that is true, the question
every owner eventually asks — who changed this, when, and on whose authority — has one answer for
the whole building, however many vendors and however many technology generations it contains, and
no equipment has to be replaced to get it. The cost of bringing a device under the discipline
should be a one-time project cost for that building, amortised like any other improvement,
rather than another recurring licence. What runs today is the append-only record store, its live
monthly publication to an independent public record, and a double-entry construction ledger that
demonstrates the standard against a real project. What does not yet run is the path that would
carry a real building's readings and work orders into a PropertyArchive, and no PropertyArchive
is in service. Building data has been treated as operational exhaust for as long as buildings
have had controls. We hold that the hundred entries that matter deserve a bookkeeper's
discipline, and we intend to build the record that gives them one.

## References

buildingSMART International. *Industry Foundation Classes (IFC) 4.3 — ISO 16739-1:2024.*
[https://ifc43-docs.buildingsmart.org/](https://ifc43-docs.buildingsmart.org/)

International Organization for Standardization. *ISO 19650 — Organization and digitization of
information about buildings and civil engineering works, including building information
modelling (BIM).* [https://www.iso.org/standard/68078.html](https://www.iso.org/standard/68078.html)

Laurie, B., Messeri, E., and Stradling, R. 2021. *RFC 9162 — Certificate Transparency Version
2.0.* Internet Engineering Task Force. [https://www.rfc-editor.org/rfc/rfc9162.html](https://www.rfc-editor.org/rfc/rfc9162.html)

C2SP working group. *signed-note — Signed checkpoint format for transparency logs.*
[https://github.com/C2SP/C2SP/blob/main/signed-note.md](https://github.com/C2SP/C2SP/blob/main/signed-note.md)

Sigstore. *Rekor — public transparency log for software supply-chain artifacts.*
[https://docs.sigstore.dev/logging/overview/](https://docs.sigstore.dev/logging/overview/)

European Commission. 2025. *Commission Implementing Regulation (EU) 2025/1946 — Qualified
electronic preservation services.* [https://eur-lex.europa.eu/eli/reg_impl/2025/1946](https://eur-lex.europa.eu/eli/reg_impl/2025/1946)

## Contributors

Prepared by Woodfine Management Corp.

## How this paper was produced

This paper is grounded in the operating and development work the preparing staff do themselves, and in what they have learned from the people they work with routinely: the graphic designers, web developers, and software developers and engineers who build the platform alongside them, and the architects and structural, building-services, and civil engineers they develop buildings with. No outside professional reviewed or approved this paper, and nothing in it is professional advice. It was drafted and edited with AI assistance under editorial direction, and the analysis and conclusions are Woodfine's own.

## Disclosures

Woodfine Capital Projects Inc. ("Woodfine") is the author of record. PointSav Digital Systems,
which builds the platform described, is currently a trade name of Woodfine, planned to become a
wholly-owned Woodfine subsidiary upon incorporation; PointSav does not itself offer, sell, or
solicit any security. Woodfine is a developer and owner of real property, which is the class of
asset this paper concerns, and the software described is our own, so this paper argues for an
approach we have a commercial interest in on both sides. The pricing and licensing arrangement
described in Section 5 is our own commercial model. This work was funded internally; no external
research funding was received. The discussion of retention in Sections 3 and 7, and the
alignment noted in Section 6 with a named European preservation instrument, describe a design in
general terms; they are not advice on any organisation's obligations under any regime, and we
hold no certification under any of the instruments referenced. This paper's content is provided
for engineering, operational, and research purposes and does not constitute investment advice or
a solicitation to invest in any Woodfine direct-hold solution. Some statements above describe
planned or intended future work; language such as "planned," "intended," "targeted," "may," and
"expected" marks this forward-looking content, which is subject to change and does not constitute
a commitment regarding future performance.

## Data and reproducibility

The specific version numbers, test counts, and file-layout names behind this paper's claims are
recorded in the platform's own engineering documentation rather than restated here in full; this
paper reports the shape of what exists rather than an inventory of the implementation. The
append-only record store described in Section 3 is an early-stage, independently tested
open-source component with its tests passing as of this paper's preparation, and its programming
interface was read directly for this paper: it exposes no operation that removes or modifies a
stored entry, which any reader with access to the source can confirm. Its current storage shape
was also read directly and is a single flat file rewritten in full on each append rather than the
segmented layout the design specifies — a real difference between the design and the running code,
stated here because a reader assessing durability should know it. A standalone program exists that
publishes the store's checkpoints monthly into an independent public record, and that schedule
runs today. The per-element companion files and the sensor-and-work-order ingestion path described
in Section 4 are a specified layout: the building application under development contains no such
ingestion code today, which we confirmed by reading it rather than by inference, and that
application is real code with no tests. The construction ledger described in Section 5 is real,
running, and checked against worked examples reproduced figure for figure on a live project; it is
a set of command-line tools with no operator-facing screen, and the empty columns in its current
reports reflect data that has genuinely not been measured rather than a computation that failed.
That engine is not among the published components: it is internal software, it is not offered for
inspection, and nothing in Section 5 should be read as an invitation to verify it — it is cited
there as evidence that the bookkeeping standard this paper argues for has been built and run
against a real project, not as a product a reader can obtain.
The hardware cost range in Section 5 is an estimate for the reference appliance class at the two
smallest business sizes, not a quoted price, and the stated zero monthly operating cost describes
the absence of any subscription or per-seat charge from us rather than the absence of electricity
and maintenance. The archive uses open, standards-governed file formats rather than a proprietary
database, so a person with an ordinary text editor can read the core file types directly and a
plain file comparison between two versions shows exactly what changed. The building-record
standards cited above are maintained by international bodies and are available for reference or
purchase through them. No independent party has audited this software, reproduced these
properties, or reviewed these claims.

Totebox Archive™, PointSav Digital Systems™, and Woodfine Capital Projects™ are trademarks of
Woodfine Capital Projects Inc.
