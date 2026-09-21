---
schema: journal-v2
slug: no-source-of-truth-for-data
title: "A Canonical Order for Decisions, None for Data"
subtitle: "How self-contained archives coordinate with one another without any central database at all"
site: home.pointsav.com
imprint: PDS-008
thesis: "A system needs one agreed order for its decisions, but it needs no central store for the records those decisions act on."
abstract: |
  Our thesis is that the central database exists because of a confusion between two needs.
  Decisions do need a canonical order — if two people act on the same record at the same
  moment, something must settle which act came first. The records themselves need no such
  centre. A Totebox Archive is a self-contained, portable, and encrypted repository for data
  and applications, designed for long-term storage and secure access, and each archive is a
  single file that can be stored on any storage medium. Two archives work together only
  through an explicit, approved connection; there is no shared central store either consults
  and no central list of who may do what. Each archive keeps its own ordered record of its
  own decisions,
  which is where the canonical order actually lives, and the component that answers a
  question across many archives at once holds nothing between questions. What exists as
  tested open-source software today is that per-archive ordered record, alongside an
  encrypted network with no
  central message broker on the path. Three limits belong beside the claim: the signed
  request that would make an archive's refusal mechanical is not yet committed to code; the
  cross-archive path that exists signs nothing on the way out; and the deepest enforcement
  layer this design points toward is a direction rather than a running system.
state: draft
version: "0.1.0"
published:
updated: "2026-09-21"
cite_as:
license: CC-BY-4.0
cites:
  - dennis-vanhorn-1966-capability-based-protection
  - capsicum-watson-2010
  - sel4-klein-2009-sosp
  - donenfeld-2017-wireguard
  - perrin-2018-noise
draws_from:
  - totebox-archive
  - totebox-archives-as-the-asset
  - source-of-truth-inversion
  - pairing-as-permission
  - machine-based-auth
  - app-orchestration-graph-federation
  - federation-via-content-mounts
  - sovereign-mesh
  - worm-ledger-architecture
  - customer-hostability
  - capability-geometry
  - three-ring-architecture
prepared_by: "Woodfine Management Corp."
keywords:
  - distributed coordination
  - self-contained archives
  - access control
  - append-only records
  - vendor independence
---

> This paper is provided for engineering, operational, and research purposes and does not
> constitute investment advice or a solicitation to invest in any Woodfine direct-hold
> solution. Statements marked "planned," "intended," "targeted," "may," or "expected" are
> forward-looking and subject to change. Full disclosures appear at the end of this paper.

Working Paper PDS-008 · v0.1.0 · CC BY 4.0

Our thesis is that a system needs one agreed order for its decisions and no central store
at all for the records those decisions act on. Almost every business computer system ever
built has assumed the opposite: that if many people and many machines are to work together
coherently, there must be one database in the middle that all of them ultimately read from
and write to. We hold that this conflates two genuinely different requirements. Settling
which of two conflicting acts happened first does require something authoritative. Holding
the records themselves does not, and the habit of putting them in the middle alongside the
decisions is the source of most of what people dislike about the software they depend on.

The alternative we are building is a system of self-contained archives. A Totebox Archive
is a self-contained, portable, and encrypted repository for data and applications, designed
for long-term storage and secure access, and each archive is a single file that can be
stored on any storage medium. A person gets one. A company gets one. A building gets one.
Two archives work together only through an explicit, approved connection established
between them — never by both consulting a shared store in the middle, and never by
checking a central list of who is allowed to do what. Each archive keeps its own strictly
ordered internal record of the decisions taken within it, and that per-archive order is the
only canonical order the design needs.

This paper is about the coordination model and nothing else. How a permission is
granted — what an approved connection actually consists of, cryptographically, and why
holding one is itself the authority rather than evidence of it — is Capability Geometry, the
subject of a companion paper on this site, and we treat it here as a fact this argument
depends on rather than re-deriving it. What exists as
tested software today is the per-archive ordered record and an encrypted private network
with no central message broker anywhere on the path. The pieces that are not finished are
named as they arise, in the sections where they belong.

## 1. The thesis

Start with the word "database," because a great deal rides on it and it is used loosely.

A database, in the sense that matters here, is a program that holds records on behalf of
other programs and answers questions about them. Its distinguishing feature is not that it
stores things — a filing cabinet stores things — but that it is the single place the
records are held, so that every program needing them must go through it. When a company
runs a payroll system, a customer system, and an accounting system that all draw on one
database, the database is not merely storage. It is the place where the company's facts
actually live, and everything else is a window onto it.

That arrangement has one enormous advantage, which is worth stating plainly before arguing
against it. If there is one place the facts live, there is never any question about which
copy is right. Two clerks cannot produce two different answers, because both are looking at
the same record. Disagreement is impossible by construction. This is a real property and
the reason central databases became universal.

Our claim is that the property is being bought at a price nobody itemises, and that most of
it can be had for far less. The property people actually need is agreement about *order* —
that when two acts conflict, there is a definite answer about which one counted. What
central databases deliver alongside it, as an unpriced extra, is that every record in the
business now sits in one place, under one operator, reachable by anything that can reach
the database, and lost or frozen or surrendered as one unit. The order was the requirement.
The single location was a side effect of how the order was achieved.

Separate the two and the architecture changes shape. Give each archive its own strictly
ordered internal record, and each archive settles its own conflicts definitively, on its
own, with nothing in the middle. Let archives reach one another only through connections
that were explicitly approved, one pair at a time, and there is no central list of
permissions to compromise, and no central store whose loss cascades. Policies move; data
stays put. An archive can be handed a new rule, or brought into a new approved connection,
without a single one of its records travelling anywhere or being reconciled against anybody
else's copy.

The composition is the claim. Each part is unremarkable alone. Independently held records
that travel with their subject are how professions kept books for centuries. A strictly
ordered internal log is how any careful bookkeeper has always worked. Access granted by
holding a specific thing rather than by appearing on a list is an idea from computing
research of the 1960s [dennis-vanhorn-1966-capability-based-protection], and it has since
been demonstrated inside ordinary operating systems [capsicum-watson-2010]. What has not
been done, so far as we know, is to assemble the three into a business system where there
is no central record store at all and the coherence people rely on comes entirely from
per-archive ordering plus explicit pairwise connections.

## 2. The problem, in the reader's terms

Two firms of solicitors, in the era before computers, both kept their clients' files in
their own offices. When one firm needed something from the other, a clerk prepared a sealed
packet, entered it in the office's outgoing register with a date and a signature, and sent
it across. The receiving firm entered it in its own incoming register and filed it. Neither
firm ever read the other's cabinets. Neither firm's cabinets depended on the other's still
being there. And yet the two firms could transact perfectly well, because every exchange
between them was an explicit, dated, recorded event that both sides had written down in
their own books.

Notice what made that work. There was no central registry of all correspondence in the
city. There was no master list of which clerk was permitted to see which file. Each office
had its own register in its own strict order, which is what let it say with authority "we
sent this on the fourteenth and received the reply on the nineteenth." And a packet moved
between two offices because a particular person in one office was authorised to send to a
particular person in the other — a relationship established once, deliberately, between
those two parties.

Now consider the arrangement that replaced it. Both firms subscribe to a practice-
management service. Their files are rows in that service's database, on that service's
computers. Coordination is now easy in one sense — either firm can be given a view into a
matter with a few clicks. But the office register is gone. The authoritative account of what
happened and when is now a log inside a system neither firm operates. Permission is an
entry in a settings table, and whoever can edit that table can grant themselves anything.
If the service has an outage, both firms stop. If the service is breached, the prize is not
one firm's cabinets but every subscriber's at once. And if either firm leaves, what it takes
with it is an export — a copy of the rows, without the arrangement that gave them meaning.

The industry's answer to the obvious fragility here has been to put more locks in front of
the room: a second code sent to a phone, a network boundary, continuous monitoring, a
policy of re-checking every request rather than trusting a session. Each of these is real
and each of them helps. None changes the fact that everything is in one room. An intruder
who defeats the newest lock arrives at the same room as an intruder who defeated the oldest
one, and every additional lock is itself another piece of software that can be
misconfigured or fail.

There is a name in the field for the deeper weakness this arrangement carries. It is called
the confused deputy: a trusted intermediary holding broad authority can be talked by a
less-trusted caller into exercising that authority on the caller's behalf. Any system where
authority is fetched from a table at the moment a request arrives has this weakness,
however carefully the table is maintained, because the intermediary's authority exists
independently of who asked it to act. A system where authority is a thing the requester must
actually be holding does not, because a program can only exercise what it was handed.

For the owner of a business, the practical consequences of the central room are specific
and unglamorous. You cannot independently establish who has had access to your own records,
because the access log belongs to the same party as the records. You cannot hand the
business to a successor without the vendor's cooperation in re-creating accounts. And the
history you would most want in a dispute — the dated, ordered account of what was done and
by whom — is held by someone whose interests in the dispute are not necessarily yours.

## 3. What makes an archive self-contained

### The unit, and why the unit matters

An archive in this design is assigned to one subject — a person, a company, a building, or
any other unit the operator chooses to define — and it holds everything about that subject:
the records, the cryptographic identity that signs them, and the small operating system that
answers questions about them. It is packaged as a single file that boots and runs, so it can
be stopped without anything being lost or expiring, copied the way any file is copied, moved
to a different machine, and resumed exactly where it left off. The machine that receives it
knows nothing whatever about what is inside; it lends the archive processing capacity and
memory and nothing more.

The reason to insist on one subject per archive, rather than one archive holding a whole
portfolio, is that it makes the boundaries of any question obvious. "Who touched this
building's records" is a question with one place to look. "What happens if this company's
archive is lost" has an answer that involves exactly that company. When records for
hundreds of subjects share one store, every such question becomes a query against a store
that also contains everything else, and the honest answer to "what did this affect" is
always "we would have to check."

Inside an archive, every write appends. No record is altered in place. A record that must be
corrected is followed by a correction entry that refers back to it, and the original stays
permanently visible. This is the office register made structural: the archive accumulates a
complete account of what its subject knew and when. Every record carries its own retention
class, fixed when the record is created — either a bounded period matching whatever rule
governs that kind of record, or permanent — and within that period the record cannot be
changed or deleted at all. After the period elapses the record becomes eligible for
deletion, but deletion is never automatic; it is a deliberate, individually authorised,
logged act, and it is blocked outright while a legal hold is in force. A legal hold is an
instruction, usually from a lawyer or a court, that records bearing on a dispute must be
preserved regardless of the ordinary schedule.

### Who is allowed to ask

An archive does not answer questions from whoever happens to reach it. It holds a short list
of exactly which parties may query it and at what level. There are four levels, and they are
coarse on purpose: full administrative authority; read and write, which is the ordinary
setting for active data entry; read only; and metadata only, which can see that records
exist without seeing their contents.

The consequence that matters most is a separation people find counterintuitive at first. A
party with no entry on an archive's list cannot query it *even from a machine that can reach
it over the network.* Being able to reach something and being allowed to ask it anything are
two different planes with no shared authority. This is why running the network confers no
access to the data moving over it — a property that matters to us specifically, since we run
network infrastructure for our own deployments and would otherwise be asking customers to
take our restraint on trust.

One honest qualification belongs with that. The list and its four levels are the design's
access model, and they are how an archive is addressed. The mechanism intended to enforce
them — a signed request that names exactly which records it is entitled to, which the archive
checks before answering — is specified and not yet committed to code, and no particular
protocol for carrying such a request has been settled on. What that means in plain terms is
that the separation described above is currently a property of how the software is arranged
rather than a refusal a stranger could provoke and observe.

### What the archive is not

It is worth being exact, because the word "archive" invites two wrong pictures.

It is not a backup. A backup is a second copy kept against the loss of an original held
somewhere else; the whole point here is that there is no other original.

And it is not a shared drive. There is no file-sharing protocol into an archive and no
general-purpose programming interface. The intended query shape follows from that: a request
names what it wants and receives only the matching result, never the underlying records
wholesale. As above, that shape is specified rather than built.

## 4. Coordination without a centre

### Why an aggregator is not a database in disguise

The obvious objection to independent archives is practical. A business with one archive per
building, one per company, and one per member of staff will constantly need to ask questions
that span them: which of our properties has an expiring lease, which of our entities holds
which asset. If answering those questions requires a component that has gathered all the
archives' data into one place, then the central database has simply been rebuilt under
another name, and nothing has been gained.

The design's answer is that the component that spans archives holds nothing. When a
cross-archive question arrives, it asks each archive in turn, in parallel, assembles the
replies in working memory, returns them, and discards them. Nothing is cached between
questions. There is no synchronisation step, no scheduled copy, and no accumulated
mirror — so if an archive's contents changed a second ago, the next question returns the
new answer without anything having had to be reconciled.

Two further properties keep this from drifting back into a centre by degrees. The
cross-archive path runs only when an authorised party explicitly asks: no background process
sweeps archives on its own initiative, because an unsolicited read of a self-contained
archive would require a standing permission to read it whenever one liked, and the design
does not grant permissions of that shape. And the failure behaviour is deliberately honest
rather than convenient. If one archive cannot be reached, it is left out of the answer and
the reply reports both how many archives were asked and how many replied, so the caller can
see the difference rather than receiving a confident-looking partial result.

There are two real limits here. The cross-archive path that exists today sends its outbound
requests without a signed statement of what it is entitled to ask for; the version that
signs each request, and lets each archive refuse a query whose signed scope does not match
what it was asked under, exists as a working scaffold rather than a running service. And
because the aggregator is where the commercial value of the design sits, it is also the
component we do not give away: querying a single archive directly is free software; fanning
a query across many of them is the paid tier. We think that is the honest place to put a
price, since it is the one part of the arrangement that is genuinely ours rather than the
customer's, but a reader should know the boundary is there and where we drew it.

### The connection is the permission

An archive becomes reachable by another party through an explicit approval step, not by
being added to a central directory. The step binds authority to a specific approved machine
holding a specific cryptographic key, rather than to a password that a person has to
remember and can be talked into repeating. The deeper mechanism — what the resulting
permission consists of, and what public record makes the grant independently checkable — is
the subject of the Capability Geometry paper mentioned earlier, and we will not re-derive it
here.

What matters for the coordination argument is narrower and can be stated in one line: the
question "may this party reach that archive?" has a structural answer rather than a looked-up
one. Either an approved connection exists, in which case a request can be made, or it does
not, in which case there is no path along which to make one. This is not a request that gets
refused. It is a request that cannot be formed. Systems built this way have been
demonstrated at the level of an operating system's own internals and shown to be
retrofittable into conventional systems [capsicum-watson-2010]; the design here applies the
same shape to the connections between whole archives.

The underlying network follows the same logic. Every node in the private network brings up
an encrypted link to its authorised peers, using a well-studied key-agreement pattern
[perrin-2018-noise] inside a transport designed for exactly this kind of always-on private
mesh [donenfeld-2017-wireguard]. No plaintext ever leaves a node. And — the point for this
argument — there is no central message broker on the path. A relay node exists to pass
packets between nodes that have no direct route to each other, but it is intended to be a
stateless relay rather than a place anything is stored, and it carries the lowest trust
rating of any node role precisely because the hardware it runs on belongs to somebody else.
Closing that residual trust gap in the hardware itself is a direction rather than a running
system, and we say so in the same breath as the claim.

### One more instance of the same shape

The pattern recurs in a place that is easy to check, because the software it runs in is the
same software serving this platform's own public documentation. That software can present
articles drawn from more than one source directory at once, and a reader browsing the result
cannot tell which source produced any given article. Each running instance reads only the
sources declared in its own configuration. Two instances could point at directories drawn from
the same upstream material and still present entirely different article sets, because what
each instance shows is a property of its own configuration and not of anything coordinating
them. Misconfiguring one instance cannot leak content into, or pull content out of, another.
There is no central content registry; there are instances, each complete in itself.

The honest boundary here is worth a sentence, because it is the same drift risk described
above. Pointing an instance at a local directory works today. The further step — the software
going out and fetching content from a remote repository on its own schedule, rather than
reading a directory somebody else keeps populated — is a design direction and is not built. An
operator adopting this today keeps those directories current themselves.

## 5. Where a canonical order is genuinely required

### What "order" buys, and what it costs

Suppose two people are working on the same set of records at the same time, and both act.
One approves a document; the other withdraws it. Both acts are legitimate. Somebody has to
be able to say which came first, because the record that results is different depending on
the answer, and "it depends who you ask" is not an acceptable state for a business record to
be in.

This is the requirement that central databases are usually reached for. It is a real
requirement and we are not arguing it away. Our argument is about its scope. The order has
to be settled *within the set of records the two acts touch*. It does not have to be settled
across every record in the business, and it certainly does not have to be settled across
every customer of a software vendor.

So each archive keeps its own ordered record and settles its own conflicts. Within an
archive, every event is appended in a definite sequence, and that sequence is authoritative.
Two parties working the same queue at the same moment cannot produce a corrupted or
ambiguous outcome, because the order in which their acts landed is a fact the archive
records rather than a race whose outcome depends on timing. Neither party has to coordinate
with the other in advance; the ordering does that work after the fact.

The ordering is enforced in three ways at once rather than by convention. The programming
interface to the record store exposes no operation that removes or changes an entry — the
capability is absent, not merely discouraged. Completed portions of the stored record are
marked read-only on disk. And each entry carries a fingerprint computed from the entry
before it, so altering any past entry would visibly break every entry that follows. A
property maintained by policy can be waived. A property maintained this way cannot be waived
without leaving evidence.

### What ordering does not give you

Two honest limits belong here rather than in a separate section at the end.

An ordered, unalterable record says nothing about whether what was written was true. If an
incorrect figure is entered, the record faithfully preserves the incorrect figure forever,
along with any correction that follows. Correctness is the job of the human review step
before a record is committed, not of the storage. We think that division is right — a store
that quietly fixed things would be far worse — but a reader should not mistake tamper
evidence for accuracy.

And the ordered record as built today is stored in a simpler shape than the design
calls for: a single file rewritten in full on each append, which is an accepted trade-off at
the volumes involved and will not remain acceptable at larger ones. The segmented layout
that replaces it, and which would make the cost of an append independent of how much history
exists, is specified and not yet built.

### The enforcement layer underneath

One further piece of honesty belongs in this section because it bears directly on how much
the structural claims above are worth.

Everything described so far is enforced by well-tested application software running on
ordinary operating systems. The strongest version of this design would have the boundaries
enforced by the small core program that decides what every other program on a machine may
touch — and specifically by one that has been mathematically proven to enforce exactly those
boundaries and nothing else [sel4-klein-2009-sosp]. That is the direction the software is
written toward. No platform service runs on seL4 today; the services that carry live traffic
are ordinary programs on ordinary operating systems. Until that changes, the guarantees here
are properties of code we wrote and test, not properties of the machine's core.

## 6. What this changes for the owner

The first change is what a failure costs. Because no archive depends on a central store,
there is no single point whose loss stops everything. If a connected party's archive becomes
unreachable, questions that span it come back incomplete and say so, and every other
archive carries on unaffected. If our own aggregating component is unavailable, single-
archive work continues, because that component was never in the path between an archive and
its own records. There is no arrangement in which losing one thing loses everything, because
there is no one thing.

The second change is what a breach yields. An intruder who compromises one archive has
compromised one subject's records — serious, and bounded. There is no drawer holding every
customer's records at once, because the drawer was never built. And an intruder who
compromises the network gains the ability to reach machines, which is not intended to be the
ability to question them: an archive is designed to answer only parties on its own approved
list, so reachability without an approval is reachability to a door that will not open. With
the qualification from Section 3 attached — that the signed request which makes the refusal
mechanical is not yet built — this is today a property of how the software is arranged rather
than one a stranger could test.

The third change is what a handover involves. Because each archive is one self-contained
unit with its own approved-connection list, changing who works on it is a change to that
list rather than a project. A new property manager, bookkeeper, or operator is approved at
the appropriate level and begins work on the same archive; the previous party is removed and
loses access to that archive without anybody else's access being disturbed and without
anyone's credentials being reset.

The trade-offs belong in the same paragraph rather than in a footnote. Asking a
cross-archive question costs more work than asking a central database the same question,
because the answer has to be assembled from several places each time instead of read from
one index — we accept that cost deliberately, and at very large numbers of archives it is
not yet known to be acceptable. Holding your own archive means holding responsibility for
backing it up and for the custody of its keys, and no vendor stands behind either. The
approved-connection list is coarse, with four levels rather than finely tuned per-record
rules, which is simple to reason about and less expressive than some organisations will
want. And the strongest structural claims here rest on application software today, not on a
verified machine core.

## 7. An open invitation

The position in this paper is one we hold with confidence. Several of the problems it leaves
open belong to specialist fields, and we would rather work them with the people in those
fields than around them.

To researchers in distributed systems: the claim that a per-archive order suffices, and that
no order across archives is ever required, is the load-bearing assumption of this whole
design. We have exercised it against a handful of archives, not against thousands
independently operated by parties with no relationship to one another. Whether there is a
class of genuinely useful business question that cannot be answered without a cross-archive
order — and whether the honest partial answers this design returns instead are adequate for
that class, or merely tolerable — is a question we would put to people who have spent
careers on it.

To specialists in access control and authorisation: four coarse levels per archive is a
deliberate simplification, chosen because a model an owner can hold in their head is worth
more to us than one that expresses every conceivable rule. We do not know where that trade
becomes wrong. What a small, comprehensible set of levels cannot express that organisations
genuinely need, and whether finer grain can be added without reintroducing the lookup table
this design exists to remove, is real unsolved design work.

To network-security researchers: the arrangement places a relay at the centre of the
encrypted mesh, running on hardware we do not physically control, and relies on that relay
being stateless for the trust argument to hold. Stateless is an architectural intention
supported by the current shape of the code rather than a checked invariant, and we would
value help working out what a positive mechanism — something that refuses to retain, rather
than merely not retaining — would look like at that position.

To auditors and records professionals: an archive can demonstrate its own internal order
conclusively. What it cannot currently demonstrate is a single order across several archives
at a moment in time, which is exactly what an examiner reconstructing an event sequence
across a group of entities would want. What such an examiner would actually need — in
documentation, in procedure, in independent attestation — before a set of independently
ordered archives could substitute for one consolidated log is a question for that profession
rather than for us.

And to anyone who has operated systems of this shape at scale: the failure mode we are most
wary of is not a dramatic one. It is the gradual reintroduction of a centre by convenience —
a cache added here, a scheduled copy there, each individually reasonable, until the
aggregator has quietly become the database again. What disciplines actually prevent that
drift, as opposed to merely forbidding it in a document, is something we would rather learn
from experience than discover.

## 8. Conclusion

A system needs one agreed order for its decisions. It needs no central store for the records
those decisions act on, and the long habit of providing both at once has cost owners more
than it has given them. Our position is that the two requirements should be met separately:
each archive self-contained, holding its own subject's records and its own strictly ordered
account of what was done to them; archives reaching one another only through connections
approved one pair at a time; and the component that spans them holding nothing and keeping
nothing. What runs today is the per-archive ordered record and an encrypted network with no
broker in the middle. What does not yet run is the signed request that would make an
archive's refusal mechanical rather than structural, the signed cross-archive path, and the
verified machine core beneath all of it.
The database in the middle has been the shape of business computing for as long as business
computing has existed. We hold that it was never the requirement, only one way of meeting
it, and we intend to build the other way.

## References

Dennis, J. B., and Van Horn, E. C. 1966. Programming semantics for multiprogrammed
computations. *Communications of the ACM* 9(3): 143–155.

Watson, R. N. M., et al. 2010. Capsicum: Practical capabilities for UNIX. *USENIX Security
Symposium.* [https://www.usenix.org/conference/usenixsecurity10/capsicum-practical-capabilities-unix](https://www.usenix.org/conference/usenixsecurity10/capsicum-practical-capabilities-unix)

Klein, G., et al. 2009. seL4: Formal verification of an OS kernel. *ACM Symposium on
Operating Systems Principles.* [https://doi.org/10.1145/1629575.1629596](https://doi.org/10.1145/1629575.1629596)

Donenfeld, J. A. 2017. *WireGuard: Next generation kernel network tunnel.* Network and
Distributed System Security Symposium. [https://www.wireguard.com/papers/wireguard.pdf](https://www.wireguard.com/papers/wireguard.pdf)

Perrin, T. 2018. *The Noise Protocol Framework* (Revision 34).
[https://noiseprotocol.org/noise.html](https://noiseprotocol.org/noise.html)

## Contributors

Prepared by Woodfine Management Corp.

## How this paper was produced

AI assistance was used in preparing and revising this paper.

## Disclosures

Woodfine Capital Projects Inc. ("Woodfine") is the author of record. PointSav Digital
Systems, which builds the platform described, is currently a trade name of Woodfine, planned
to become a wholly-owned Woodfine subsidiary upon incorporation; PointSav does not itself
offer, sell, or solicit any security. The architecture described is our own; the components
discussed are software we wrote or intend to write, and the paid tier named in Section 4 is
our own commercial model, so this paper argues for an approach we have a commercial interest
in. This work was funded internally; no external research funding was received. Section 3
describes records-retention and legal-hold concepts in general terms in order to explain a
design; it is not advice on any organisation's obligations under any particular regime. This
paper's content is provided for engineering, operational, and research purposes and does not
constitute investment advice or a solicitation to invest in any Woodfine direct-hold
solution. Some statements above describe planned or intended future work; language such as
"planned," "intended," "targeted," "may," and "expected" marks this forward-looking content,
which is subject to change and does not constitute a commitment regarding future
performance.

## Data and reproducibility

The specific version numbers, test counts, and route names behind this paper's claims are
recorded in the platform's own engineering documentation rather than restated here; this
paper reports the shape of what exists (tested; open source; early-stage in the places it
says so) rather than an inventory of the implementation. The record store described in
Sections 3 and 5 is an early-stage, independently tested open-source component, with its
tests passing as of this paper's preparation; its programming interface was read directly and
exposes no operation that removes or modifies a stored entry, which any reader with access to
the source can confirm for themselves. The cross-archive query path described in Section 4
exists on the component that today also routes inference requests; the separate,
request-signing version of that path exists as a working scaffold and is not running in
production. The console used to work with a single archive is published under a licence that
requires anyone who modifies it and offers it as a network service to publish their changes
as well; the archive operating system is under a source-available licence that converts
automatically to a permissive open-source licence two years after each release; and the
cross-archive aggregation component is proprietary and does not convert. Moving the first two
to a permissive licence sooner is an intended direction, already approved internally, held
back by a remaining dependency on more restrictively licensed code elsewhere. No independent
party has audited this software, reproduced these properties, or reviewed these claims.

Totebox Archive™, Capability Geometry™, PointSav Digital Systems™, and Woodfine Capital
Projects™ are trademarks of Woodfine Capital Projects Inc.
