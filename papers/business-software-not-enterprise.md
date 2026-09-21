---
schema: journal-v2
slug: business-software-not-enterprise
title: "Software for a Reporting Issuer, Not for a Multinational"
subtitle: "Comparable operational complexity, incomparable organisational scale — and why that distinction, not company size, is the design brief"
site: software.pointsav.com
imprint: PDS-015
thesis: "A mid-sized regulated company carries operational complexity comparable to a much larger one, on nothing like the same organisational scale — and software built for the larger one's scale cannot serve it."
abstract: |
  Our thesis is that "business software" and "enterprise software" solve genuinely
  different problems, and that the difference is not the amount of capability required.
  A mid-sized company with public reporting obligations carries much of the same
  operational complexity a far larger organisation carries: the same filing calendar, the
  same statutory record-keeping, the same auditor, the same categories of obligation.
  What it does not carry is the organisational scale that enterprise software silently
  assumes — an information-technology department, an implementation team, a multi-year
  rollout budget, and staff whose job is the software itself. Enterprise products are
  built for the second thing as much as the first, which is why a smaller company adopting
  one pays for and navigates complexity that exists to coordinate an organisation
  it will never become. The design brief that follows is specific and falsifiable: handle
  real, regulated complexity, assume none of the scale. In practice that has meant no
  enterprise tier above the free and paid tiers, a one-time purchase rather than a
  contract requiring renewal, and software that runs on the company's own hardware. We
  state the weakest point plainly: the installation experience does not yet match the
  claim, and most services are still brought up by hand rather than by a single script.
state: draft
version: "0.1.0"
published:
updated: "2026-09-21"
cite_as:
license: CC-BY-4.0
cites:
  - ni-51-102
  - np-51-201
  - idc-smb-2026
  - williamson-1979-transaction-cost-economics
  - shapiro-varian-1998-information-rules
draws_from:
  - economic-model
  - customer-hostability
  - pointsav-overview
  - totebox-archives-as-the-asset
  - totebox-archive
  - customer-owned-graph-ip
  - self-host-a-deployment
  - three-ring-architecture
  - software-distribution-substrate
  - legal-and-ip-structure
prepared_by: "Woodfine Management Corp."
keywords:
  - business software
  - enterprise software
  - mid-market
  - regulated small business
  - software positioning
---

> This paper is provided for engineering, operational, and research purposes and does not
> constitute investment advice or a solicitation to invest in any Woodfine direct-hold
> solution. Statements marked "planned," "intended," "targeted," "may," or "expected" are
> forward-looking and subject to change. Full disclosures appear at the end of this paper.

Working Paper PDS-015 · v0.1.0 · CC BY 4.0

Our thesis is that the useful distinction in business software is not between big companies
and small ones. It is between *operational complexity* and *organisational scale*, which are
ordinarily assumed to rise together and in one important class of company do not. A
mid-sized company with public reporting obligations carries a great deal of the complexity a
far larger organisation carries — the same filing calendar, the same statutory records, the
same auditor asking the same questions, the same categories of legal obligation, differing
in amount rather than in kind. What it does not carry is the scale: no information-technology
department, no implementation team, no project office, no multi-year rollout budget, and
nobody at all whose actual job is the software.

Enterprise software is built for both of those things at once, and this is rarely made
explicit. It handles genuine complexity, and it also assumes the organisational apparatus
that will install it, configure it, integrate it, train people on it, and keep it running. A
company that has the first requirement and not the second is offered a product built on the
assumption that it has both. What it gets instead is a great deal of
capability it does not need wrapped around the little it does — and an implementation project
that is larger than the department it is meant to serve.

This paper takes four things in turn: what "enterprise software" actually is and why it
became what it is; what the company we are building for actually looks like, described
concretely rather than as a market segment; the distinction between complexity and scale,
stated in the form that makes it a design brief rather than a slogan; and what follows from
it in what we have actually built, including the place where what we have built does not yet
match the claim.

## 1. The thesis

Software sold to businesses divides, in practice, into three markets that are rarely named as
three.

At one end is software for individuals and very small businesses. It is bought with a credit
card, installed in minutes, and designed so that nobody has to be trained. It assumes almost
no complexity and almost no organisation, and it is excellent at what it does.

At the other end is enterprise software. It is bought through a procurement process, installed
over months or years by specialists, and configured to the organisation rather than the other
way round. It assumes both great complexity and a great deal of organisation.

Between them sits a market that both ends describe as an afterthought. The company in it is
genuinely complex — it may be regulated, it may have public obligations, it certainly has an
auditor and a lawyer and statutory records — and it is genuinely small as an organisation. It
has neither the simplicity the first market assumes nor the apparatus the second one requires.

Our position is that this middle market needs its own category rather than a discount on
either neighbour, and that the right name for that category is *business software* — the term
we use for what we build, deliberately and not as a synonym for enterprise software applied to
smaller firms. The design brief that follows is specific: handle enterprise-grade complexity,
assume none of the enterprise-grade organisation. Everything else in this paper follows from
those two clauses held at once.

We hold, further, that attempting to serve the enterprise market as well would prevent us from
serving this one properly. That is not modesty. A product that must also work for an
organisation of fifty thousand people acquires configuration surfaces, role hierarchies,
integration layers, and administrative depth that exist to coordinate the fifty thousand. Each
of those is correct for that customer and is pure cost for the company of two hundred. A firm
that tries to serve both will serve the larger customer, because that is where the money is,
and the smaller customer will get what is left over. That has already happened across most of
this industry, which is why the middle market is where it is.

## 2. The problem, in the reader's terms

Two pieces of vocabulary first, because the rest of this paper leans on them and because a
reader outside these fields is entitled to a plain gloss rather than an assumption.

A **reporting issuer** is a company that has formal, continuing obligations under securities
law to file information publicly — financial statements on a fixed timetable, disclosure of
material developments when they occur, and a range of related filings — because members of the
public may hold its securities. In Canada those obligations are set out in a national
instrument on continuous disclosure [ni-51-102], with separate guidance on how
forward-looking statements must be framed [np-51-201]. The obligations do not depend on how
big the company is. A company with two hundred employees and a company with two hundred
thousand face the same instrument.

**Enterprise resource planning** — the category usually abbreviated in conversation and almost
never explained — is the name for a single integrated system intended to run the whole of a
company's operations: accounting, purchasing, inventory, payroll, human resources, and
whatever else, all against one shared body of data. The appeal is obvious and real: one set of
numbers, one place to look, no reconciling between departments. The cost is equally real, and
is the subject of this paper.

Now the situation. Consider a company with perhaps a hundred million dollars of annual
revenue. It is a substantial business by any ordinary measure. It has real operations, real
staff, real obligations, and an auditor who arrives every year with real questions.

Ask where its records are, and the answer is frequently not what a reader would guess. It is
entirely unremarkable for a company that size to be running on a general-purpose word
processor and a spreadsheet, backing up by hand when somebody remembers, and relying on
outside advisers — the accountants, the lawyers, the consultants — to hold and maintain the
records that matter. This is not negligence. It is the result of a slow process that
accumulates: the company grew, each adviser brought their own systems, no single decision was
ever made to move the records anywhere, and so they stayed where they landed.

The consequence is worth sitting with, because it is the real problem underneath the software
question. In most cases the records of a mid-sized reporting issuer do not live at the
company. They live with the service providers who maintain them — and they live there for a
structural reason, not a lazy one. The advisers *have* enterprise systems. The company does
not. So the records accumulate wherever the capable system is, which is somebody else's.

That arrangement works until it is tested. It is tested when an adviser is replaced, when a
firm merges, when a person retires, when a dispute arises, or when a regulator or an acquirer
asks the company to produce its own history and the company discovers how much of it is held
by parties it no longer has a relationship with.

The obvious remedy — the company gets its own system — runs straight into the problem this
paper is about. The systems capable of holding those records are built for organisations with
an information-technology function, and the company does not have one. So the remedy costs
more than the problem, and nothing happens, and the records stay where they are. The gap is
not a gap in capability. It is a gap in what the available products assume about the buyer.

## 3. What enterprise software actually is

This section explains where enterprise software's shape comes from. It is not a criticism —
the shape is a correct answer to a real question — and a reader who follows the argument here
will see why the same answer is wrong one segment down.

### Complexity of coordination, not complexity of work

The first thing to understand is that most of what makes a large organisation's software
complicated is not the work. Posting an invoice is the same operation in a company of two
hundred and a company of two hundred thousand. What differs is everything around it: who is
permitted to post it, who approves it, which of eleven subsidiaries it belongs to, which of
four accounting standards applies, how it appears in each of six reporting hierarchies, and
which of nine hundred cost centres absorbs it.

That is coordination complexity, and it is a direct function of organisational size. An
enterprise system's configuration depth exists to represent it. The system has to be told what
the organisation is before it can be useful, and describing an organisation of that size takes
a long time and specialised knowledge.

### The implementation project, and why it exists

This is why enterprise software arrives with an implementation project rather than an
installation. The project is not overhead attached to the software; in large part it *is* the
software, in the sense that the delivered value is the configured system rather than the
product as shipped. Consultants map the organisation, design the configuration, migrate data
from whatever came before, integrate adjacent systems, train staff, and run the change in
stages.

None of this is padding. It is the necessary work of making a general product fit one
particular large organisation. And it is priced accordingly, which is the second reason the
smaller company is poorly served: it must pay for a coordination problem it does not have.

### The sales motion shapes the product

There is a further effect, less visible and more consequential. Enterprise software is sold
through a long, expensive process — evaluations, proposals, procurement, negotiation — and a
sales process of that cost can only be justified by a contract large enough to cover it. That
places a floor under the contract value, and the floor is well above what a mid-sized company
will pay. A smaller buyer is therefore not merely expensive to serve; they are *structurally
unreachable*, because the cost of selling to them exceeds what they would pay.

The published analysis of this segment treats small and medium-sized businesses as a distinct
market with distinct adoption patterns rather than as scaled-down large ones
[idc-smb-2026], and the technology industry's own contract-value thresholds do the rest: a
platform built around a contract value in the high hundreds of thousands annually cannot
descend to one in the low tens of thousands by discounting, because the cost structure
underneath it does not descend.

### What the buyer is left holding

There is one more property of this arrangement that a reader should weigh, because it sits
underneath everything in this paper. Once the configuration, the integration, and the
migration are done, the buyer's investment is largely *specific to that supplier* — it has no
value anywhere else. Economists have a settled account of what happens to a relationship where
one party has made an investment that is worth much less outside it: the relationship has to
be governed rather than simply transacted, and governing it is itself costly
[williamson-1979-transaction-cost-economics]. In this industry the same result is usually
called lock-in, and it is treated as a structural feature of information markets rather than
a failing of particular firms [shapiro-varian-1998-information-rules].

For the large buyer, that is a known cost, absorbed by a procurement function that exists to
manage it. For the mid-sized buyer, it is the whole company's operational future decided by
a project it did not have the staff to supervise properly.

## 4. What the target company actually looks like

It is easy to write about a "segment" and never describe anyone. Here is the company this
platform is built for, concretely.

It has real revenue — enough that it is nobody's idea of a small business, with substantial
operations and staff. It has public obligations: a filing calendar it cannot miss, statutory
records it must keep, and an auditor who tests them annually. It operates in a field where a
regulator has views — securities, health, legal privilege, financial advice, real property —
so its records are not merely useful but evidentially important.

And it has no information-technology department. It may have one capable person who ended up
responsible for computers because they were good with them. It has no implementation budget,
no project office, and no appetite for a multi-year rollout, because there is nobody to run
one. Its actual technology estate is a general-purpose office suite, an accounting package,
and a filing structure that grew rather than being designed.

Two further properties matter as much as the first two.

Its records are distributed across its advisers, as described above, for the structural reason
described above. Getting them back is not a technical problem so much as a commercial and
relational one — which is precisely why a technical arrangement that never let them leave in
the first place is worth more than a better export.

And its complexity does not grow with its market value. This is the observation that makes the
whole argument turn, and it is worth stating in its sharpest form. Take one of the largest
listed companies in the world by market value and ask what it must actually publish under its
continuous-disclosure obligations: financial statements, a description of the business, a
handful of biographies of its directors and officers, and a modest set of related filings.
The list is short. It does not become long because the company is valuable. A reporting issuer
a thousandth of the size publishes a list of substantially the same shape. What changes with
size is the volume flowing through each item and the number of people involved in producing
it — not the number of distinct things that must exist.

If that is right, then the amount of *kinds* of complexity a company faces is set mostly by
what it does and how it is regulated, and only weakly by how big it is. The amount of
*organisation* available to handle that complexity, by contrast, is set almost entirely by
size. The two quantities come apart, and the middle market is where they come apart furthest.

## 5. Comparable complexity, incomparable scale

Here is the claim in the form that makes it a design brief.

It is *not* that a mid-sized reporting issuer needs less than a large organisation. That
version is the intuitive one and it argues against everything above: if the smaller company
simply needed less, the answer would be a cut-down enterprise product, and cut-down enterprise
products exist and do not work.

The claim is that its **operational complexity is genuinely comparable** — the same categories
of obligation, the same statutory records, the same audit, the same evidentiary standard for
what it keeps — while its **organisational scale is not remotely comparable**. It must handle
enterprise-grade complexity with none of the enterprise-grade apparatus: no department to run
the system, no team to implement it, no budget to absorb a multi-year rollout, and no ability
to make the software somebody's full-time job.

Enterprise software resolves the tension the other way round. It assumes that if a customer
has the complexity, they must have the organisation, and it builds accordingly. Business
software, as we mean the term, is the product category that takes the complexity seriously and
refuses the assumption about the organisation.

That refusal has consequences that are easy to state and hard to honour.

It means the system must be installable by a competent generalist rather than a specialist,
because there is no specialist. It means configuration has to be mostly *absent* rather than
mostly *guided*, because a configuration wizard still assumes somebody who knows what the
answers should be. It means capability that only makes sense at large organisational scale
should not be built at all, rather than built and hidden, because hidden capability is still
surface a buyer must understand enough to ignore. And it means the price and the sales motion
have to be small enough that the buyer can simply decide, which rules out the process that
funds enterprise selling.

What the company actually needs, stripped to its shortest form, is a private network and
reliable record-keeping, with ordinary software on top. What it is currently offered is a
public cloud and complicated software. The distance between those two sentences is the whole
market.

## 6. What follows in what we build

### No tier above the two

There are two tiers — one free, one paid — and no enterprise tier above them, and the absence
is a decision rather than a stage we have not reached.

The reasoning is the one set out in Section 3. A platform that adds an enterprise tier
acquires an enterprise sales motion, an enterprise cost structure, and an enterprise product
roadmap, and each of those pulls the product away from the customer described in Section 4.
The segment we target runs annual technology contracts in the low tens of thousands of dollars,
against an enterprise floor at least an order of magnitude above that. Those are not two ends of one
market that a single company can span by discounting; they are two cost structures.

The free tier — one archive and one console — exists as the way in, and we earn nothing from
it. The paid tier adds the layer that asks a single question across many archives at once. A
companion paper on this site argues that boundary and why it is drawn by architecture rather
than by a feature list.

### Records held by the company, not by the system

The second consequence is structural rather than commercial. If the problem in Section 2 is
that a mid-sized company's records live with its advisers, then the answer cannot be a better
system for the advisers. It has to be an arrangement in which the records are the company's
own object, held by the company, which advisers are given access to.

That is what an archive is: a self-contained, portable, encrypted repository for data and
applications, designed for long-term storage and secure access, and held as a single file
that can be stored on any storage medium. A companion paper on the home site argues that
construction properly. Its relevance here is narrow and important: it is the piece that lets a
company with no technology department still be the party that holds its own history. Changing
an adviser becomes a change to who is permitted to reach the archive, rather than a project to
recover records from somebody's system.

### Bought once, run on the company's own hardware

The third consequence is that the software is sold outright rather than rented, and runs on
the customer's own machines with the customer's own data and the customer's own keys. A
companion paper on this site argues the pricing model; the reason it belongs here is that a
company without a technology department is exactly the company least able to manage a
dependency that can be switched off, and least able to negotiate when it is.

### Where this does not yet hold

One limit belongs here, stated plainly, because it is the weakest point in the whole argument
and a reader should have it from us rather than find it themselves.

The claim in Section 5 is that the system must be installable without a specialist. That is
the claim, and it is not yet the practice. The intended shape — every service installable from
a single script, in the customer's own language, with a manifest declaring what it provides —
is real intent and not uniform reality. Today exactly one service has a full install script.
Most are brought up by hand-applying a system configuration file, which is precisely the kind
of task that requires the specialist this platform's entire positioning says the customer does
not have.

That is a real gap between what we argue and what we ship, and it is the gap most likely to
determine whether the argument survives contact with a real customer. It is also, mercifully,
engineering work rather than a design flaw.

## 7. What this changes for the reader

The first change is that a prospective buyer has a better question to ask before evaluating
anything else. Not "does this product have the features I need" — most products of any
seriousness will — but "was this built for a company of my actual size, or for one I am
expected to grow into?" The tell is not the feature list. It is what the product assumes about
the buyer: how long the implementation takes, who has to run it, what the configuration
expects the buyer to already know, and whether the price can be decided by a person rather
than a process.

The second change is that a company can stop treating the distributed-records problem as
permanent. The reason a mid-sized company's history sits with its advisers is that the advisers
had the capable systems. If the company can hold a capable record of its own without an
information-technology department, the reason dissolves — and with it the awkwardness that
arises when an adviser relationship ends.

The third change is in what a buyer should expect to pay for. Under the enterprise arrangement,
a large share of the cost is the implementation, and the implementation is what locks the buyer
in. If the implementation is small, that cost is small and so is the lock-in, and the
relationship stays a transaction rather than becoming something that has to be governed.

The trade-offs are real and belong in the same paragraph. Refusing to build for large
organisations means genuinely refusing them: a customer who grows past this shape will outgrow
the product, and we would rather say so than pretend otherwise. Absent configuration means
opinionated defaults, and a company whose practice differs from the default has less room to
adjust than an enterprise customer would. Declining the enterprise sales motion means declining
the revenue that funds deep, specialised support, so a buyer who wants somebody accountable at
three in the morning is buying that separately if at all. And the installation gap in Section 6
is live today: a buyer evaluating this platform right now should assume more hands-on setup
than this paper's own argument says they should need.

## 8. An open invitation

This paper states a position and raises questions we cannot answer from inside one firm.

To researchers in enterprise software and organisational technology adoption: the claim in
Section 5 is the one we would most like tested. Does operational complexity really decouple
from organisational scale in the way we describe, across industries, or is that an artefact of
the regulated sectors we happen to know? A study that measured *distinct kinds* of obligation
and record rather than volume, across firms of very different sizes in the same industry, would
settle it. We have a strong intuition, formed from one vantage point, and no dataset.

To practitioners who have implemented systems in mid-sized regulated companies: our claim that
configuration should be absent rather than guided is a design opinion that has not survived
many real deployments. We would genuinely like to know where opinionated defaults break — which
practices vary so much between companies of this size that a default is worse than a question.

To economists working on switching costs and vendor relationships: Section 3 argues that a
small implementation produces small lock-in, which is intuitive and may be wrong. It is
possible that lock-in in this segment is driven less by implementation investment than by staff
familiarity and adviser relationships, in which case reducing implementation cost changes less
than we expect. That is a testable proposition and we have not tested it.

And to people who run technology in a company of this size — the one capable person who ended
up responsible for the computers: you are the reader whose judgement matters most to Section 6,
and the gap admitted there is exactly the thing you would notice first. We would rather hear
what actually stops you than guess at it.

## 9. Conclusion

The distinction that matters is not size. It is that operational complexity and organisational
scale, normally assumed to rise together, come apart in the middle market: a mid-sized company
with public reporting obligations carries much of a large organisation's complexity on almost
none of its scale. Enterprise software is built for both at once and cannot be discounted into
serving only the first, because the implementation project, the configuration depth, and the
sales motion that carry it are all functions of the scale it assumes. Business software, as we
use the term, is the category that takes the complexity seriously and refuses the assumption:
no enterprise tier, records held by the company rather than by its advisers' systems, software
bought once and run on the company's own hardware, and configuration that is mostly absent
rather than merely guided. The most honest thing we can say about our own position against that
brief is that the installation experience does not yet meet it. We hold that the category is
real, that it is badly served, and that building for it properly means declining the customer
above it rather than serving both badly.

## References

Williamson, O. E. 1979. Transaction-cost economics: The governance of contractual relations.
*Journal of Law and Economics* 22(2): 233–261.

Shapiro, C., and Varian, H. R. 1998. *Information Rules: A Strategic Guide to the Network
Economy.* Harvard Business School Press.

British Columbia Securities Commission. *National Instrument 51-102 — Continuous Disclosure
Obligations.*
[https://www.bcsc.bc.ca/securities-law/law-and-policy/instruments-and-policies/5-ongoing-requirements-for-issuers-insiders/current/51-102](https://www.bcsc.bc.ca/securities-law/law-and-policy/instruments-and-policies/5-ongoing-requirements-for-issuers-insiders/current/51-102)

Canadian Securities Administrators. *National Policy 51-201 — Disclosure Standards for
Forward-Looking Information.*

IDC. *The SMB 2026 Digital Landscape.*
[https://www.idc.com/resource-center/blog/the-smb-2026-digital-landscape-how-ai-is-redefining-growth/](https://www.idc.com/resource-center/blog/the-smb-2026-digital-landscape-how-ai-is-redefining-growth/)

## Contributors

Prepared by Woodfine Management Corp.

## How this paper was produced

This paper is grounded in the preparing staff's own development and operating work, and in their standing engagement with the designers, software engineers, architects, engineers, and legal and accounting advisers the business works with. It was drafted and edited with AI assistance under editorial direction, and the analysis and conclusions are the author's own.

## Disclosures

Woodfine Capital Projects Inc. ("Woodfine") is the author of record. PointSav Digital Systems,
which builds the platform described, is currently a trade name of Woodfine, planned to become a
wholly-owned Woodfine subsidiary upon incorporation; PointSav does not itself offer, sell, or
solicit any security. The market positioning argued here is our own commercial position, so
this paper argues for an approach we have a direct commercial interest in. Woodfine is itself a
company of the kind described in Section 4 and is the platform's first and reference customer,
which means our picture of that customer is drawn substantially from our own operations rather
than from an independent survey; a reader should weigh that accordingly. This work was funded
internally; no external research funding was received. The description of continuous-disclosure
obligations is given in general terms to explain who this software is for and is not legal
advice on any issuer's obligations under any instrument. This paper's content is provided for
engineering, operational, and research purposes and does not constitute investment advice or a
solicitation to invest in any Woodfine direct-hold solution. Some statements above describe
planned or intended future work; language such as "planned," "intended," "targeted," "may," and
"expected" marks this forward-looking content, which is subject to change and does not
constitute a commitment regarding future performance.

## Data and reproducibility

This paper argues a position rather than reporting a measurement, and the distinction matters
for how its claims should be weighed. The claim in Section 5 — that operational complexity and
organisational scale come apart in this segment — is reasoning from our own operating
experience and from the structure of public disclosure obligations, which apply to a company
regardless of its size. It is not a measured finding, and no dataset behind it exists; the study
that would test it is named in Section 8 as an invitation precisely because we have not run it.
The illustrative picture of a company in Section 2 is drawn from what we observe in this market
and is offered as a representative case rather than a surveyed average. The commercial facts in
Section 6 are checkable: the two tiers and the stated absence of any tier above them, and the
present state of installation tooling, are both set out in the platform's own published
operating documentation, which states directly that one service today has a full install script
and that most services are brought up by hand. That documentation is public, and a reader can
confirm the gap admitted in Section 6 there rather than taking our word for it. The platform's
own code is open source and published in full. No independent party has audited this software,
surveyed this market segment on our behalf, or reviewed these claims.

PointSav Digital Systems™ and Woodfine Capital Projects™ are trademarks of
Woodfine Capital Projects Inc.
