---
schema: journal-v2
slug: the-archive-is-the-asset
title: "The Archive Is the Asset"
subtitle: "Toward bootable, freely transferable records built so a migration project never has to start"
site: home.pointsav.com
imprint: PDS-009
thesis: "If every person, company, and property has its own complete, bootable archive from day one, moving data between systems stops being a category of work."
abstract: |
  Our thesis is that records should be held in containers that boot and run on their own,
  one container per subject, from the first day — so that changing a software vendor,
  splitting a business in two, or selling one is a handover of a file rather than a
  migration project. A Totebox Archive is a self-contained, portable, and encrypted
  repository for data and applications, designed for long-term storage and secure access,
  and each archive is a single file that can be stored on any storage medium. "Bootable" is
  the load-bearing word: the file is not an export of a record held elsewhere, it is a
  complete small computer system holding the records, the identity that signs them, and the
  software that answers questions about them — so it can be stopped, copied to other
  hardware, and resumed unchanged. The idea is not ours: it descends from publicly
  documented work on separating a person's data store from the applications that use it,
  most prominently the Solid project associated with the web's inventor. What exists as
  early-stage, tested open-source software is the append-only record store and the free
  single-archive console. The main limit, stated plainly: the
  single command that would package an archive as a signed, transferable bundle is not
  built, and no licence we publish grants a portability guarantee — portability is a design
  commitment we are building toward, not a promise already made in a contract.
state: draft
version: "0.1.0"
published:
updated: "2026-09-21"
cite_as:
license: CC-BY-4.0
cites:
  - solid-project
  - farrell-klemperer-2007-switching-costs
  - shapiro-varian-1998-information-rules
  - sec-17a-4-f
  - eidas-qualified-preservation
  - ifc-4-3
draws_from:
  - totebox-archives-as-the-asset
  - totebox-archive
  - customer-owned-graph-ip
  - substrate-without-inference-base-case
  - customer-hostability
  - source-of-truth-inversion
  - economic-model
  - asset-anchored-bim-vault
  - machine-based-auth
prepared_by: "Woodfine Management Corp."
keywords:
  - data portability
  - bootable archives
  - switching costs
  - vendor independence
  - records handover
---

> This paper is provided for engineering, operational, and research purposes and does not
> constitute investment advice or a solicitation to invest in any Woodfine direct-hold
> solution. Statements marked "planned," "intended," "targeted," "may," or "expected" are
> forward-looking and subject to change. Full disclosures appear at the end of this paper.

Working Paper PDS-009 · v0.1.0 · CC BY 4.0

Our thesis is that records should be held in containers that boot and run on their own, one
container for each thing the records are about, from the first day rather than from the day
someone wants to leave. Where that is true, the work everyone in business has learned to
dread — moving records out of one system and into another — stops being a category of work at
all. Not faster. Not cheaper. Absent, because there is nothing to move: the records were
never inside the vendor's system to begin with.

Anyone who has changed accounting packages knows what the alternative costs. A business that
decides in March to move systems is often still reconciling in September. Anyone who has
split one company into two knows a harder version of it, because there the records must not
merely be moved but divided, and the division has to be defensible afterward to an auditor,
a tax authority, and possibly a court. And anyone who has ended a relationship with a
software supplier on poor terms knows the worst version: the negotiation over the export is
also a negotiation over how much the past is worth, conducted with the other side holding
it.

The container we are building is a Totebox Archive: a self-contained, portable, and encrypted
repository for data and applications, designed for long-term storage and secure access, in
which each archive is a single file that can be stored on any storage medium. A person gets
one, a company gets one, a property gets one. This paper takes three things in turn — what
"bootable" actually means and why the word is doing real work; where the idea comes from,
which is not from us; and what a handover looks like when the record is a file rather than a
subscription. Two things exist as early-stage, tested open-source software: the append-only
record store inside an archive, and the free console used to work with one archive at a time.
One thing does not, and the paper says so where it belongs rather than at the end: the single
command that would package an archive as a signed, transferable bundle has not been built, and
no licence we publish promises portability as a contractual right.

## 1. The thesis

There are two places a record can live, and the choice between them determines almost
everything else.

It can live inside the system that created it, arranged in whatever internal form that
system finds convenient, reachable only through that system's own doors. Or it can live in a
container of its own, in a form any competent reader can open, with the system that created
it treated as a visitor asking permission to read and write. Nearly all commercial software
takes the first path. We take the second, and we take it further than a file format goes: the
container is not merely a readable file, it is a complete running unit that carries its own
means of answering questions about its contents.

The reason to prefer the second shape is not that vendors hide data or that their export
tools are poorly made. Many are good. It is that a record designed to live inside one
system's internal arrangement cannot leave that system without leaving the arrangement
behind — and the arrangement was a large part of what gave the record meaning. Which field
refers to which. What a status code stands for. How one entry links to another. Which of two
similar numbers is the one the business actually relied on. An export carries the values and
leaves the arrangement at home. That is why a migration is never finished when the import
completes: what follows is months of discovering which pieces of meaning did not survive the
crossing.

So the claim is not "we have better export." It is that a record which never lived inside any
one system's arrangement has nothing to translate, and that the right time to arrange that is
at the beginning of a relationship rather than at the end of one. An archive that is complete
and bootable from its first day has nothing to migrate when its owner changes vendors, splits
one business into two, or sells. The record simply continues under new custody.

The composition is the claim, and each element of it is old. Self-contained portable
containers are as ordinary as a filing box, a shipping container, or a bound minute book.
Designating exactly one copy as the real record and treating every other as disposable is how
a careful bookkeeper has always worked. And the specific idea of separating a data store from
the applications that use it, so that the applications visit rather than own, has been
publicly developed on the web for years [solid-project]. What we hold is that these three,
applied together to an organisation's operating records, remove the migration project rather
than improve it.

## 2. The problem, in the reader's terms

Keep your company's records in a filing box and the box is yours. Change bookkeepers, and the
new bookkeeper takes the box. Sell the company, and the buyer takes the box. If the stationer
who sold you the box goes out of business, nothing at all happens to the papers inside. The
box was a container. The records were always yours, and handing them over is a single event
with a clear before and a clear after: at ten in the morning you had the box, at noon someone
else does, and there is no third state in which both of you half-have it.

Now suppose instead that your records are entries in a large ledger book belonging to your
bookkeeper, written in the bookkeeper's own shorthand, interleaved with the records of their
other clients. You may inspect your entries whenever you wish. But changing bookkeepers now
means someone must go through the book, find your entries, copy them out, and translate the
shorthand — and the new bookkeeper will keep them in a different shorthand in a different
book. Every change of bookkeeper is a copying-out. Some entries are missed. Some shorthand is
misread. And the oldest history becomes the least reliable, because it has been copied the
most times.

This is, almost exactly, how business software stores records: as rows in the vendor's
database, in the vendor's internal arrangement. The vendor's assurance that "you can export
your data" is the assurance of a copying-out. It is honest as far as it goes and it does not
go far enough, because the copying-out *is* the migration project. What is exported is a
translation of the record, not the record.

Two things follow that are worth separating, because they are often blurred together into an
accusation of bad faith that the situation does not require.

The first is that the cost of leaving is a source of pricing power entirely unrelated to the
quality of the software. This is not a suspicion; it is a well-developed result in the
economics of markets where customers face switching costs, which shows that the existence of
a cost to leave changes what a supplier can charge a customer who has already arrived
[farrell-klemperer-2007-switching-costs]. The same literature is clear that lock-in of this
kind is a structural feature of information markets rather than a failing of particular firms
[shapiro-varian-1998-information-rules]. A vendor need not intend anything for the incentive
to operate.

The second is that the cost compounds silently, in the customer's direction only. Every year
on the same system makes the eventual copying-out larger, because there is more history to
carry and more of the arrangement has been absorbed into daily habit. A business five years
in has a larger migration ahead of it than one five months in, which means the cheapest
moment to change is always the moment you have least reason to.

Buildings are the sharpest case of this, and we treat them only briefly here because a
companion paper on our building-information site argues the building case properly. The short
version: buildings stand for fifty to a hundred years, while the software used to design and
manage them changes its file format with every major release and is often unreadable by
competing products within a decade. The current standard for building design records is a
line-oriented text format maintained by an international industry body since 1996 and
published in its current revision as an ISO standard in 2024 [ifc-4-3], which is precisely
the sort of foundation a fifty-year record needs and precisely what a vendor's internal
format is not. Everything in this paper applies to a building with the numbers larger and the
horizon longer.

## 3. What "bootable" actually means

### Three ordinary words: file, image, operating system

The claim in this section rests on a technical distinction that is easy to state once three
words are in place, and it is worth putting them in place rather than assuming them.

A **file** is a named lump of data on a storage device — a document, a photograph, a
spreadsheet. Copying a file is the most ordinary operation a computer performs.

An **operating system** is the software that manages a computer: it decides which programs
run, what each may touch, and how anything reaches the storage and the network. Every
computer has one. It is the layer between the programs a person cares about and the machine
underneath.

A **disk image** is a file whose contents are the entire contents of a disk — not a document
stored on a disk, but a copy of everything a disk holds, the operating system included,
packaged as one file. Given the right instruction, a computer can be pointed at a disk image
and told to start it as if it were a real disk with a real machine attached. When it does,
the thing inside begins running. That is what **bootable** means: not "readable," not
"importable," but *able to start up and run*.

### Why the distinction is load-bearing

Most claims about data portability concern the first word only. A vendor's export produces a
file. The file is readable by whoever can interpret it, and interpreting it is the receiving
system's problem. Portability of that kind is real but thin: you hold a description of the
record, and turning the description back into a working record requires another system,
another vendor, and another arrangement to absorb it into.

An archive in this design is a disk image, and the disk image and the archive are the same
thing. There is no external database, no storage bucket in a data centre, and no central
register holding the archive's contents. The single file contains the records, the
cryptographic keys that are the archive's identity, and the small operating system that
serves questions about what is inside. Four consequences follow directly, and none of them is
available to an export:

It can be **stopped.** The running archive is shut down. Nothing is lost and nothing expires.
There is no subscription that lapses while it is off, because the archive was never a
subscription.

It can be **copied.** It is a file. Copying it is the operation every computer already
performs a thousand times a day.

It can be **relocated.** The copy is started on different hardware, which may belong to
someone else entirely. The machine receiving it lends it processing capacity and memory and
knows nothing whatever about what is inside.

It can be **resumed.** It continues from exactly the state it was in when it stopped, because
the state was inside the file.

Put those four together and "handing over the records" becomes the same operation as handing
over a filing box: a single event, with a clear before and after, and no intermediate period
in which the record exists in two half-versions.

### What is inside, briefly

Inside an archive, records are kept as plain files, and every write appends. Nothing is
altered in place. A record that must be superseded is followed by a correction entry that
points back to the original, and the original remains permanently visible. Each record
carries its own retention class, fixed when it is created, and within that period it cannot
be changed or deleted at all; afterwards it becomes eligible for deletion, but deletion is
always a deliberate, individually authorised, logged act, and is blocked outright while a
legal hold — an instruction, usually from a lawyer or a court, that records bearing on a
dispute must be preserved — is in force. This shape is deliberately aligned with what
regulators already ask of electronic records they expect to be unalterable
[sec-17a-4-f], and with the European framework for services that undertake to preserve
digital records over long horizons [eidas-qualified-preservation]. Neither of those requires
certification of us today, and we have not sought any; the alignment is a design choice, not
a credential.

The archive also holds a short list of exactly which parties may query it and at what level,
and a party with no entry on that list cannot query it even from a machine that can reach it.
The mechanism by which such a party is approved, and why holding an approved key is itself
the authority rather than evidence of it, is the subject of a separate paper on this site.

### What this is not

It is not a backup. A backup is a second copy kept against the loss of an original held
elsewhere. Here there is no other original.

And it is not an export feature. Export implies the record's native home is inside a platform
and a copy is prepared on request. An archive's native home is the archive. There is nothing
for an export to convert, because the format never changed.

## 4. Where this idea comes from

We did not invent this, and a paper that implied otherwise would be worth less than one that
says so.

The clearest public expression of the underlying principle is the Solid project, an effort
led by the inventor of the web to return control of personal data to the individual
[solid-project]. Its central construction is a personal data store — a pod — that belongs to
the individual, with applications requesting permission to read from or write to it rather
than holding their own copy inside their own database. The application is the visitor. The
store is the resident. That inversion is the same inversion this paper argues for, and it has
been publicly developed, documented, and implemented by others for years.

What we are doing differently is the level it is applied at. Solid's subject is a person and
their personal data on the web. Ours is an organisation's operating records — a company's
books, a property's history, a member of staff's personnel file — and the unit is an archive
per subject rather than a pod per person. We also make the container bootable rather than
merely readable, which is a stronger commitment than the pod model requires and, we would
argue, the commitment that actually removes the migration project rather than relocating it.

Being honest about the lineage has a second use beyond credit. The user-controlled data store
idea has been pursued for over a decade and has not displaced the central-database
arrangement. Any reader entitled to be persuaded by this paper is also entitled to ask why we
expect a different outcome, and the answer is not that we are cleverer. It is that we are
attacking a narrower problem — one organisation's operating records, entered by its own staff,
in a market segment too small for the enterprise software industry to serve well — and that
the bootable container is a materially different mechanism from a permissioned web store.
Whether that is enough is a genuinely open question, and it is the first one in the invitation
below.

## 5. What a handover replaces

### Ending a vendor relationship

Consider a business that has decided to stop using its current software. Under the ordinary
arrangement, this begins a project: agree an export format, extract, transform, load into the
new system, reconcile, discover what did not come across, decide what to do about it, and
maintain read-only access to the old system for some period because the reconciliation is
never quite complete. The project has a budget, a timeline, and a risk register.

Under this design there is nothing to begin. The archive is where the records already were.
Changing software means running different software against the same archive — approving the
new party at the appropriate level on the archive's own list, and removing the old one. The
archive does not move. Nothing is extracted, because nothing was ever inside the thing being
replaced.

### Splitting one business into two

This is the harder case, and the one we think makes the argument best, because it is where an
export-based approach fails most visibly. When a business divides, the records must divide
too, and the division has to be intelligible afterward to people who were not in the room:
which entity holds which contract, which liability, which history. Done by export and
re-import, the division is performed by whoever writes the transformation, and the evidence
that it was done correctly is that transformation's own correctness.

Done as archives, the division is a division of containers. Each resulting entity has its own
archive, holding its own complete history, including the history that preceded the split and
the entry recording the split itself. The append-only discipline means neither entity's
archive has had anything removed from it; what changes is which archive is authoritative for
which subject going forward. An examiner reconstructing the event afterward reads two ordered
records rather than auditing a transformation script.

This is the direction. It is not yet a completed mechanism, and this is the place to say so
rather than at the end. The single command that would package an archive as a signed,
self-contained bundle — its records, its ordered history, its configuration, and the
identity that signs it — is designed and not built. There is no export command today. Nor
does any licence we publish grant a portability right: the commitment to portability is
architectural, expressed in how the archive is built, and it is not a contractual promise
anyone could enforce against us. A reader assessing this should weigh the architecture, not a
guarantee, because the guarantee does not exist.

### Selling the thing the records are about

The case we care about most, because it is the business our own group is in, is the sale of a
property. A building changes hands and the record of what it is, what was approved, who
occupies it, and what has been repaired should change hands with it. That the record travels
with the title is the design intent, and it is an intent rather than a settled legal
mechanism — how an archive should be referenced in a purchase agreement, whether it forms
part of the property or is conveyed alongside it, and what a seller warrants about its
completeness are questions for the conveyancing profession rather than for us. No archive has
yet passed to a buyer with a deed. The companion paper on our building-information site treats
the building record in the detail it deserves.

### Why we give away the part that holds the records

One structural point belongs here because it is the difference between a commitment and a
slogan. A platform whose customers depend on their records staying inside its systems has a
reason to make leaving expensive, whatever its intentions. Removing that reason means
removing the dependency, which means not charging for the layer that holds the records.

So the archive operating system and the single-archive console are free software. The console
is published under a licence requiring anyone who modifies it and offers it as a network
service to publish their changes as well. The archive operating system is under a
source-available licence that converts automatically to a permissive open-source licence two
years after each release. One operator with one archive is a free deployment, and we earn
nothing from it.

The charge sits one level up, on the component that fans a question across many archives at
once. That component is proprietary and does not convert. We think this is the honest place
to put a price — it is the part that is genuinely ours rather than the customer's, and a
customer who stops paying keeps every archive and every record in it, losing only the
convenience of asking one question of all of them. A reader should still know the boundary
exists and where we drew it, because a claim of independence from a party with a commercial
interest deserves to be checked rather than accepted.

## 6. What this changes for the owner

The first change is what an owner actually holds. Under this design the record of a person, a
company, or a property is a file in the owner's possession, complete with the means of
reading it, rather than an entitlement to query someone else's system for as long as a
commercial relationship lasts. A supplier's failure, acquisition, price increase, or decision
to discontinue a product changes who might be hired to work on the archive. It does not touch
the archive.

The second change is what a change of hands costs. Replacing a bookkeeper, a property
manager, or a software supplier becomes a change to one list: the new party is approved at the
level appropriate to their role and begins work on the same archive. Dividing a business
becomes a division of containers rather than a transformation to be audited. Selling the asset
is intended to carry the record with it.

The third change is what an outside party can rely on. Because the record is append-only and
ordered, an auditor, a lender, or a purchaser's adviser can be handed a copy and establish for
themselves that nothing has been removed since a stated point, without access to any live
system and without trusting whoever operated it.

The trade-offs belong in the same paragraph. Holding the archive means holding the
responsibility: backups, the custody of the keys, and the decision to dispose of a record when
its retention period ends all fall to the owner, and no vendor stands behind any of them.
Append-only storage grows and never shrinks within a retention period, which is by design and
is also a real cost in storage and in the discipline required to keep it navigable. The first
wave of this work covers three kinds of archive — people, companies, and real property — and
records are entered directly by operating staff rather than imported in bulk from older
systems, which makes the earliest archives accurate by construction and also means adoption
begins with data entry rather than with a conversion. And the part a reader of this paper most
wants — a single command that hands the whole thing over as a signed bundle — is the part not
built.

## 7. An open invitation

This paper states a position we hold and a set of problems we cannot resolve alone. Several of
them belong to professions other than ours.

To researchers and practitioners in the user-controlled data store tradition this design draws
from: you have more experience than we do of where this idea meets resistance. Our honest
question is whether making the container bootable rather than merely permissioned solves
problems that earlier attempts struggled with — application developers' reluctance to write
against a store they do not control, the absence of a business model for the store itself, the
difficulty of getting anyone to hold one — or whether it simply moves those problems into a
new shape. We would rather be told than find out slowly.

To records managers and archivists: the retention model described in Section 3 is our reading
of ordinary practice. Whether it is adequate across jurisdictions whose retention floors
conflict, how a disposal should be evidenced inside a store that never removes anything, and
what an archive ought to do when one record falls under two regimes with different rules, are
questions we would rather work through with practitioners than settle by assumption.

To conveyancing lawyers and land title professionals: the claim that an archive travels with a
deed is design intent, not a settled mechanism, and we said so above. What we would value is
the shape of the answer — whether such a thing is best treated as a fixture, a chattel, a
schedule to the agreement, or something with no existing category — and whether it differs
enough between jurisdictions to make a single design impossible.

To auditors and assurance professionals: an ordered, append-only archive is conclusive about
whether anything was removed, and it is not yet a recognised form of evidence in any assurance
standard. What documentation, procedure, and independent attestation an examiner would need
before relying on one, in place of a management representation, is a question for that
profession.

And to anyone with long experience of records that had to outlive their custodians: the
durability claim here rests on open standards continuing to be maintained, and standards are
also abandoned. What an archive should carry alongside its contents so that a reader fifty
years from now can still open it — and what that reader will actually have to hand — is
something we would rather learn from people who have watched formats survive or fail than
reason about from first principles.

## 8. Conclusion

A record should be a container that boots and runs on its own, one container per subject, held
by the subject's owner from the first day. Where that is true, changing vendors is a change to
a list, dividing a business is a division of containers, and selling an asset carries its
record along with it — none of which is a migration project, because there is nothing to
migrate. The idea is not ours; it descends from a decade of public work on separating a data
store from the applications that visit it, and our contribution is to apply it to an
organisation's operating records and to make the container bootable rather than merely
readable. What runs today is the append-only record store and the free single-archive console.
What does not is the one command that would package an archive for handover, and no licence we
publish promises portability as a right. The migration project has been treated as an
unavoidable cost of changing software for as long as businesses have used software. We hold
that it is a consequence of where records were kept rather than a law of nature, and we intend
to build records that never need one.

## References

Solid Project. *Solid — Your data, your choice.* [https://solidproject.org/](https://solidproject.org/)

Farrell, J., and Klemperer, P. 2007. Coordination and lock-in: Competition with switching
costs and network effects. *Handbook of Industrial Organization,* vol. 3. Elsevier.

Shapiro, C., and Varian, H. R. 1998. *Information Rules: A Strategic Guide to the Network
Economy.* Harvard Business School Press.

US Securities and Exchange Commission. *Rule 17a-4(f) — Records to be preserved by certain
exchange members, brokers and dealers (electronic recordkeeping).* 17 CFR §240.17a-4.
[https://www.ecfr.gov/current/title-17/chapter-II/part-240/section-240.17a-4](https://www.ecfr.gov/current/title-17/chapter-II/part-240/section-240.17a-4)

European Commission. 2025. *Commission Implementing Regulation (EU) 2025/1946 — Qualified
electronic preservation services.* [https://eur-lex.europa.eu/eli/reg_impl/2025/1946](https://eur-lex.europa.eu/eli/reg_impl/2025/1946)

buildingSMART International. *Industry Foundation Classes (IFC) 4.3 — ISO 16739-1:2024.*
[https://ifc43-docs.buildingsmart.org/](https://ifc43-docs.buildingsmart.org/)

## Contributors

Prepared by Woodfine Management Corp.

## How this paper was produced

AI assistance was used in preparing and revising this paper.

## Disclosures

Woodfine Capital Projects Inc. ("Woodfine") is the author of record. PointSav Digital
Systems, which builds the platform described, is currently a trade name of Woodfine, planned
to become a wholly-owned Woodfine subsidiary upon incorporation; PointSav does not itself
offer, sell, or solicit any security. The architecture described is our own, and the licensing
and pricing arrangement described in Section 5 is our own commercial model, so this paper
argues for an approach we have a commercial interest in. Woodfine is also a developer and
owner of real property, which is the class of asset the building example concerns. This work
was funded internally; no external research funding was received. Section 3 describes
records-retention and legal-hold concepts in general terms in order to explain a design; it is
not advice on any organisation's obligations under any regime, and the alignment noted there
with named recordkeeping and preservation instruments is a design choice rather than a
certification, none of which we hold. This paper's content is provided for engineering,
operational, and research purposes and does not constitute investment advice or a solicitation
to invest in any Woodfine direct-hold solution. Some statements above describe planned or
intended future work; language such as "planned," "intended," "targeted," "may," and
"expected" marks this forward-looking content, which is subject to change and does not
constitute a commitment regarding future performance.

## Data and reproducibility

The specific version numbers and test counts behind this paper's claims are recorded in the
platform's own engineering documentation rather than restated here; this paper reports the
shape of what exists (tested; open source; early-stage) rather than an inventory of the
implementation. The archive operating system, the single-archive console, and the append-only
record store described in Section 3 are all early-stage, independently tested open-source
components, with the record store's tests passing as of this paper's preparation; the
application under development for the building case is real code but is not yet tested
software. The record store's programming interface was read directly and exposes no operation
that removes or modifies a stored entry, which any reader with access to the source can
confirm. The licence terms were read from the components' own published declarations: the
console requires anyone who modifies it and runs it as a network service to publish their
changes; the archive operating system is source-available and converts automatically to a
permissive open-source licence two years after each release, under the licence's own terms;
and the multi-archive aggregation component is proprietary and does not convert. Moving the
first two to a permissive licence sooner is an intended direction, already approved
internally, held back by a remaining dependency on more restrictively licensed code elsewhere
in the platform. The building-record standard cited above is maintained by an international
standards body and is publicly available through it. No independent party has audited this
software, reproduced these properties, or reviewed these claims.

Totebox Archive™, PointSav Digital Systems™, and Woodfine Capital Projects™ are trademarks of
Woodfine Capital Projects Inc.
