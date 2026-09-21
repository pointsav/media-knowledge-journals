---
schema: journal-v2
slug: aggregation-is-the-commercial-boundary
title: "A Licence Boundary Drawn by Architecture, Not by Features"
subtitle: "One archive runs free; the layer that asks a single question of many archives at once is the part that costs money"
site: software.pointsav.com
imprint: PDS-013
thesis: "The line between the free and the paid parts of this platform should be a structural fact a reader can inspect — the presence of the multi-archive layer — not a feature list a vendor can quietly redraw."
abstract: |
  Our thesis is that a platform which is partly free and partly paid should draw the line
  between them at a place a customer can verify by looking at what is running, rather than
  at a list of features that can be revised. The line we draw is the presence of the layer
  that aggregates many archives together. One operator running one archive is a free
  deployment, and no paid capability exists inside a single unaggregated archive by
  construction — there is nothing there to sell. An organisation that wants to ask one
  question of a hundred archives at once needs a component that does not exist inside any
  of them, and that component is the paid one. This is a separate question from which
  open-source terms any given component carries, and we keep the two apart deliberately.
  On the second question we state both the destination and the current position honestly.
  The intended destination is specific: components that touch a customer's own kept
  records are intended to move to a permissive licence, because a delayed commercial gate
  on a customer's own records is incompatible with the commitment that records stay freely
  transferable; components with no kept-records role, where the real exposure is a
  competitor reselling our hosting without contributing back, are intended to move to a
  strong network copyleft licence that closes that exposure permanently. That destination
  is reasoned but not ratified. Today's actual position is mixed: a number of components
  carry no licence declaration at all, and at least one ships a declaration its own
  published classification does not match.
state: draft
version: "0.1.0"
published:
updated: "2026-09-21"
cite_as:
license: CC-BY-4.0
cites:
  - raymond-1999-cathedral-and-bazaar
  - benkler-2002-coases-penguin
  - lerner-tirole-2002-open-source-motivation
  - open-core-handbook
  - spdx-license-list
  - farrell-klemperer-2007-switching-costs
draws_from:
  - economic-model
  - legal-and-ip-structure
  - pointsav-overview
  - software-distribution-substrate
  - totebox-archives-as-the-asset
  - totebox-archive
  - customer-owned-graph-ip
  - customer-hostability
  - canadian-simple-copyright
  - contributor-model
  - three-ring-architecture
prepared_by: "Woodfine Management Corp."
keywords:
  - open core
  - software licensing
  - commercial boundary
  - copyleft
  - multi-archive aggregation
---

> This paper is provided for engineering, operational, and research purposes and does not
> constitute investment advice or a solicitation to invest in any Woodfine direct-hold
> solution. Statements marked "planned," "intended," "targeted," "may," or "expected" are
> forward-looking and subject to change. Full disclosures appear at the end of this paper.

Working Paper PDS-013 · v0.1.0 · CC BY 4.0

Our thesis is that the line between what a software platform gives away and what it charges
for should be a structural fact anyone can inspect, not a list of features the seller can
revise. Every prospective customer of a platform that is partly free asks the same practical
question sooner or later: where exactly does the free part stop? The usual answer is a
comparison table on a pricing page, with ticks in two columns. A table is not a boundary. It
is a statement of current intent, and it can be rewritten on any Tuesday.

Our answer is a single structural fact. A deployment is free when it consists of one archive
and the console used to work with it. It is commercial when a further layer is present — the
one that takes a question and asks it of many archives at once. That layer does not live
inside any archive. It cannot be reached from inside one. An operator running a single
archive is not running a limited edition of the paid product with parts switched off; they
are running the whole of what exists at that level, and there is no paid capability inside it
to withhold, because there is nothing at that level to sell.

This paper takes three things in turn. First, what open-source licensing actually is, stated
from the beginning, because the rest does not follow without it. Second, where the commercial
boundary sits and why an architectural boundary behaves differently over a decade than a
feature list does. Third, a separate question that is frequently confused with the first one:
which open-source terms each individual component carries. On that third question we state
both where we intend to arrive and where we actually are, and the two are not the same place.

## 1. The thesis

A company selling software that is partly free has to answer one question honestly, and most
of the difficulty in this field comes from answering it badly: what, precisely, does a
customer have to pay for?

There are three usual answers. The first is *features* — the free version omits capabilities
the paid version has. The second is *capacity* — the free version is the same software with a
ceiling on users, records, or machines. The third is *support* — the software is entirely
free and the company sells help with it.

Each has a known failure. A feature boundary drifts, because every commercial pressure pushes
capability from the free column to the paid one, one item at a time, each move individually
defensible. A capacity boundary is arbitrary: nothing about the software explains why the
ceiling is at ten and not fifty, so the number becomes a pricing dial rather than a fact. And
a support boundary puts the seller in the position of benefiting when the software is
difficult, which is a quiet incentive nobody intends and everybody eventually notices.

We propose a fourth: an *architectural* boundary. The paid thing is a component that exists
at a level above the free thing and does something the free thing structurally cannot do. It
is not a version of the free product with more switches turned on. It is a different
component, answering a different question, and its absence from a free deployment is not a
restriction applied to that deployment — it is a description of what that deployment is.

The reason to prefer this shape is not that we are more principled than firms that chose
differently. It is that this boundary is *checkable by the customer*, and the others are not.
A customer inspecting their own running system can see whether the aggregation layer is
present. They do not need to trust a pricing page, and they do not need to trust us. And a
boundary that is checkable is much harder to move quietly, because moving it means changing
what the software is, in public, in code that is published.

## 2. The problem, in the reader's terms

The suspicion this paper is addressed to is well founded and widely held, and it deserves to
be stated in its strongest form rather than a convenient one.

A customer adopts a platform because the free version does what they need. Over some years,
the business built around that platform has to grow. Capability moves across the line — not
in one visible act, but in a series of individually reasonable decisions. A feature that was
free becomes a paid add-on at the next release. A limit that was generous becomes tight as the
customer's own use grows. A new capability that everyone will eventually need arrives in the
paid column only. None of this requires bad faith. It requires only that the company needs
revenue and that the line is drawn somewhere a company can move it.

The customer's position deteriorates in a particular way as this happens. They have not merely
been asked to pay more. They have been asked to pay more *after* building their operations on
the thing, which is the moment at which their ability to decline is at its weakest. The
economics of this are well developed: the existence of a cost to leave changes what a supplier
can charge a customer who has already arrived, independent of anything about product quality
[farrell-klemperer-2007-switching-costs]. A customer who has read that literature, or who has
simply lived it twice, is right to want a boundary that does not move.

Consider the difference between two arrangements a tenant might have with a landlord. In the
first, the lease says the tenant may use the building "subject to the rules posted in the
lobby," and the landlord posts the rules. In the second, the tenant owns the freehold of their
own unit and the landlord owns the lift and the loading bay. Both arrangements involve an
ongoing relationship and both involve the tenant paying for something. The difference is that
in the second, what the tenant holds is not subject to revision by the other party, and both
sides can see precisely where one thing ends and the other begins. A boundary drawn at the
walls behaves differently over twenty years than a boundary drawn in a posted notice, even if
the two describe the same arrangement on the day they are signed.

## 3. What open-source licensing actually is

This section establishes the vocabulary the rest of the paper needs. A reader already at home
with software licences may go straight to Section 4.

### Copyright is the starting point, not the licence

The first thing to understand is that software is protected by copyright automatically, from
the moment it is written, without any registration or notice. The default position, if nobody
does anything, is that nobody may copy, modify, or distribute it but the author. Everything
else is a permission the author grants on top of that default.

So an "open-source licence" is not a giving-up of ownership. The author still owns the
copyright. What the licence does is grant everyone a standing permission to use, copy, modify,
and redistribute, on stated conditions. Which conditions distinguishes one open-source licence
from another, and there are essentially two families.

### Permissive and copyleft

A **permissive** licence says: do what you like, including building a commercial product on
this and never showing anyone your changes; just keep our copyright notice attached and do not
pretend we endorsed you. The most widely used example is the Apache licence, which adds an
express grant of patent rights — meaning the contributors promise not to sue users over patents
covering their own contributions. Permissive licences maximise adoption, and they accept that
some adopters will take and never give back.

A **copyleft** licence says: do what you like, but if you distribute a modified version, you
must publish your modifications under these same terms. It is a reciprocity condition. The
purpose is to keep the commons growing rather than being quietly enclosed.

There is a well-known hole in ordinary copyleft, and it matters here. Copyleft's obligation is
triggered by *distribution* — handing someone a copy. If a company takes copyleft software,
modifies it, and runs the modified version on their own servers as a service that customers
reach over a network, they have distributed nothing. Customers use the software without ever
receiving a copy. The reciprocity condition never fires. A stronger variant of copyleft — the
network-service variant — closes this by treating "makes it available over a network" as
equivalent to distribution. That variant is the answer to one specific threat: a competitor
taking the software and selling it as hosting without contributing anything back.

### Delayed-conversion licences, and the problem with them

A third arrangement has become common in the last several years. The source code is published
and readable, and most uses are permitted immediately, but one use — competing commercially
with the original author — is withheld for a fixed period, two years in the form most widely
used, after which
that release converts automatically to a fully permissive licence. Each release carries its own
clock.

The appeal is obvious: the author gets a window of commercial protection and the public
eventually gets permissive code. The objection is equally real, and it is not mainly about
whether the arrangement is fair. It is that during the delay period, using the software for
certain purposes requires the author's permission. The permission may never be asked for and
may never be refused. But the *gate exists*, and a gate that exists can be used.

That distinction — between a permission that is unlikely to be exercised and a permission that
cannot be exercised — is the hinge of Section 5.

### Why firms use open source at all

It is worth saying why a commercial firm publishes source code, since a reader encountering
this for the first time may reasonably assume charity or naivety. Neither is the usual reason.
The published literature on open-source production identifies a set of hard commercial
motivations: recruiting and signalling to skilled contributors, establishing a standard that
others build on, reducing the cost of a customer's evaluation, and obtaining review from people
who are not on the payroll [lerner-tirole-2002-open-source-motivation]. The organisational
argument — that an open development model can coordinate production outside both the firm and
the market, at a scale that neither manages well — was set out at length two decades ago
[benkler-2002-coases-penguin], following an earlier and more practical account of why the open
method produces more reliable software than a closed one [raymond-1999-cathedral-and-bazaar].

We publish source for those reasons and for one more, particular to what we build: a customer
whose business records live inside our software cannot verify our claims about it unless they
can read it. The publishing is not a gift to the commons. It is the only way the central claim
of this platform can be checked.

## 4. Where the boundary actually sits

### The free level, described plainly

A free deployment is one archive and one console.

An archive here is a self-contained, portable, encrypted repository for data and applications,
designed for long-term storage and secure access — a single file that can be stored on any
storage medium, holding the records, the identity that signs them, and the software that
answers questions about them. A companion paper on the home site argues what that construction
is for and why it is built to be complete from its first day. A console is the terminal program
an operator uses to work with one archive.

We earn nothing from a deployment at this level. The console is published under a network
copyleft licence — free software in the full sense, modifiable and redistributable by anyone
who accepts the reciprocity condition. The archive operating system is published under the
delayed-conversion arrangement described in Section 3, which means its source is readable and
most uses are permitted now, with the remaining permission arriving on a clock. That is not
where we intend it to stay, for reasons Section 5 sets out, and the distinction is real enough
that it should not be blurred by calling both components the same thing. What is true of both
today is that running one archive costs nothing. That is not a loss leader in the ordinary
sense, where the seller expects to recover the cost from the same customer later. A person or a business running one
archive may run it for twenty years and never pay us anything, and the design intends that to
be a perfectly ordinary outcome rather than a failure of conversion.

### The paid level, and why it is not inside the free one

Now consider a firm that holds not one archive but four hundred — one for each property it
manages, or each entity it administers, or each client whose records it keeps. The question
such a firm needs answered is not answerable inside any single archive: *which of my four
hundred archives contain a lease expiring this quarter?* No archive can answer that, because no
archive knows the others exist. Each is complete and each is sealed, and that is the entire
point of the construction.

Answering it requires a component that sits above them all, holds the ability to reach each
one, asks each the same question, and assembles the answers. That component is the
orchestration layer, and it is the commercial product. Its family of applications is
distributed under proprietary terms and does not convert.

Three properties of that arrangement are worth stating explicitly, because they are what make
the boundary structural rather than declared.

The first: the paid capability is not absent from a free deployment by policy. It is absent
because the thing it does is a relationship between archives, and a deployment with one archive
has no relationships. There is nothing to switch off. A customer who inspects a free deployment
looking for disabled paid features will not find any, because none was ever compiled in.

The second: a customer who stops paying does not lose an archive. They lose the ability to ask
one question of all of them. Every archive continues to hold every record, readable by the free
console, exactly as before. The dependency runs on the convenience, not on the records — and
that is the whole reason for putting the price where we put it. A platform whose customers
depend on their *records* remaining reachable has a standing incentive to make leaving
expensive, whatever it intends. Removing the incentive means removing the dependency, which
means not charging for the layer that holds the records.

The third is the sharpest evidence available for the whole argument of this paper, because it
is a fact about the code rather than about our intentions: the paid layer checks its own
licence, and nothing else does. When the commercial component starts, it verifies its licence —
offline, against a public key built into itself, with no call to us — and if that licence is
absent, invalid, or lapsed past a grace period of thirty days, it continues to run but withdraws
the paid service it offers. The free components contain no such check at all; a search of the
archive operating system and the console for any licence, token, or entitlement check returns
nothing. The commercial gate sits exactly on the architectural line, on the paid side of it,
and a reader can confirm both halves of that sentence in the published source.

### The honest present tense

Two limits belong here rather than in a footnote.

The orchestration layer is early. Parts of its application family exist as real, running
services; others exist as scaffolds with a name and a plan. A reader should understand the
commercial boundary as a settled design commitment with a partially built paid side, not as a
mature product line.

And the boundary as described governs *this* platform's own deployments. Nothing in it stops
somebody else from writing their own aggregation layer against the same free archives and
selling it, or giving it away. We think that is a feature — a platform that could prevent it
would be one where the archives were not really the customer's — but it is also, plainly, a
commercial exposure we are choosing to accept.

## 5. Which licence each component carries — a different question

It is easy to assume that the free-versus-paid boundary and the open-source-licence question
are the same question. They are not, and conflating them produces confusion in both directions.

The first question is about *deployments*: is a given installation free or commercial? Answer:
does it include the aggregation layer.

The second question is about *components*: what terms govern a given piece of source code —
who may copy it, modify it, redistribute it, and under what conditions. That question is
answered per component, and it applies equally to components on the free side of the first
boundary. A component being free to run does not settle whether a competitor may fork it, or
whether someone who modifies it must publish their changes.

Licensing here is assigned per directory rather than per commercial tier, which means the two
questions genuinely do have different answers in different places, and a reader tracing one
should not assume they have traced the other.

### Where we intend to arrive

Our intended destination for the second question is specific, and it follows from one governing
commitment rather than from a preference among licences.

The commitment is that nothing on the path a customer takes to reach their own kept records —
their own archive, their own source code, their own data — may carry a permission gate, even an
unexercised one. Records that are meant to be freely transferable cannot sit behind a door
somebody else holds a key to, and the fact that the key has never been turned does not change
where the door is. That is the argument set out at the end of Section 3, applied.

From that commitment, two intended assignments follow.

Components that touch a customer's own kept records are intended to carry a permissive licence.
The archive operating system, the console, and the private source-control system all fall here.
The archive operating system and the source-control system carry the delayed-conversion licence
today, which means that for a period after each release a particular use of the customer's own
records path requires our permission. We intend to remove that, and a permissive licence removes
it outright rather than on a clock. The console already carries network copyleft, which imposes
a condition on redistribution but is not a permission gate — nobody has to ask us anything — so
moving it to permissive terms is a smaller change made for consistency rather than to close an
exposure.

Components with no kept-records role are intended to carry the network copyleft licence instead.
The infrastructure and network-administration systems fall here, and so does the publishing
system. No customer's records live inside them, so the commitment above does not bind. What
does apply to them is the specific exposure described in Section 3: a competitor taking the
code, running it as a hosted service in competition with us, and contributing nothing back.
Network copyleft closes that permanently. A delayed-conversion licence only postpones it, at the
cost of not being a recognised open-source licence in the meantime.

Both assignments are our reasoned intention and neither is a ratified company decision. They are
stated here as direction, not as current fact, and they may change.

### Where we actually are

Today's position is not the destination, and we would rather say so plainly than let the
paragraph above imply a tidiness that does not exist.

We counted directly, in preparing this paper, rather than repeating a published summary. Most
components carry a licence declaration that is what it should be. A meaningful number carry no
licence declaration at all — not a wrong one, none — so their terms fall back to a
repository-wide notice rather than being stated in the place a reader or an automated tool would
look. That notice is itself out of date: our own published documentation records that it
predates the most recent licensing decision and has not been regenerated to match. A reader
trying to establish what terms govern one of those components therefore has to reason from a
stale general statement instead of reading a specific one. That is the opposite of what we
intend, and it is a housekeeping failure rather than a decision.

At least one component ships a declaration that does not match its own published classification.
The orchestration operating system — described in our own published documentation as the
proprietary commercial layer, never distributed under an open tier — carries in its own manifest
a delayed-conversion source-available licence, while the application family sitting on top of it
correctly carries the proprietary identifier. One of those two is wrong. Separately, three
desktop applications declare a European public licence that appears nowhere in the published
classification at all.

Several components on the customer's own records path still carry the delayed-conversion licence
that the commitment above is meant to remove. Moving them is an intended action on code we wrote
ourselves and therefore may relicense, but it is an execution step that has not been taken, not a
change already made.

None of this is presented as a scandal. Licence metadata drifts in every codebase of any size,
and the reason this one drifted is mundane: a default was carried forward in new components
without anyone re-deciding it. It is presented because a paper arguing that a boundary is
trustworthy *because it is checkable* has no business implying that the adjacent bookkeeping is
already clean. A reader who checks will find what we have described. We would rather they find it
here first.

## 6. What this changes for the reader

The first change is that the free-versus-paid question has an answer a reader can obtain without
asking us. Inspect a running deployment. If the aggregation layer is not present, the deployment
is free, and it is free because of what it is rather than because of what we currently charge
for. A pricing page is a claim about the present. The architecture is a claim that has to be
rewritten in public to change.

The second change is what happens to a customer who stops paying. Under a feature-boundary
arrangement, stopping payment removes capability from a system holding the customer's records,
and the customer's exposure is proportional to how much of their operation runs through it. Here,
stopping payment removes one thing: asking a single question across many archives. Every archive
and every record in it remains exactly as it was, reachable with free software.

The third change is for a reader assessing a supplier's durability rather than its price list. A
company that has put its commercial layer above the customer's records rather than around them
has given up a particular kind of leverage, permanently and visibly. That is a weaker position
for us, and it is the position we want to be in, because a customer should not have to rely on
our forbearance for access to their own books.

The trade-offs are real and belong in the same paragraph. An architectural boundary is rigid: a
capability that genuinely belongs at the archive level cannot be moved into the paid column later
just because we need revenue, which removes a lever most software companies rely on. Giving away
the records layer means the free tier can be large and produce nothing, indefinitely. Publishing
the source of the free components means a competitor can build their own aggregation layer
against them, which we have accepted rather than solved. And the intended licence changes in
Section 5 are intentions: a reader weighing this paper should weigh the architecture, which is
real today, more heavily than the licensing destination, which is not yet a ratified decision and
not yet executed.

## 7. An open invitation

This paper states a position we hold and several questions we cannot settle from inside one firm.

To researchers in open-source licensing and the economics of open core: the claim we most want
tested is comparative and falsifiable. Over a multi-year product life, does a boundary defined by
architecture actually resist the drift that feature-defined boundaries show, or does it merely
relocate the drift — for instance into the question of which capabilities get built at which
level in the first place? Both of us could be right about the first boundary and wrong about the
second. The study that would settle it compares real dual-licensed platforms over a decade rather
than reasoning from the licences alone, and we do not have the standing to run it.

To practitioners who have set commercial boundaries in real firms: the standard guidance on this
question is written mostly for firms whose product is a hosted service, where the boundary is
naturally drawn around what the vendor operates [open-core-handbook]. Ours is drawn inside
software the customer runs on their own machines, which we think changes the problem
substantially and may change it in ways we have not anticipated. We would value hearing where
this shape has been tried and how it failed.

To lawyers and licence-compliance specialists: the argument in Section 5 rests on a distinction
between a permission gate that is never exercised and one that cannot be exercised. We believe
that distinction matters to a customer whose records are on the other side of it. We do not know
whether it matters to a court, to an auditor, or to a procurement officer filling in a supplier
questionnaire, and the answer changes how much weight the intended licence change actually
carries.

And to anyone who maintains licence metadata across a large codebase: the drift described at the
end of Section 5 was found by counting, not by a tool that told us. We would be glad to learn
what practices actually keep this correct at scale, as opposed to the practices that are supposed
to.

## 8. Conclusion

The line between what this platform gives away and what it charges for is the presence of the
layer that aggregates many archives into one question. One archive and one console are free,
permanently, and contain no paid capability to withhold. Aggregation is a component that exists
above the archives and cannot be reached from inside one, so its absence from a free deployment
describes what that deployment is rather than what has been taken from it. That boundary is a
structural fact a customer can check in their own running system, which is the only property that
makes it more durable than a comparison table. Which open-source terms each component carries is a
separate matter with a separate answer, and on that one our intended destination — permissive
terms on everything touching a customer's own records, network copyleft where the real exposure
is hosted resale — is reasoned, unratified, and not yet executed, while today's position still
contains components with no licence declared and at least one whose declaration and published
classification disagree. We hold that a boundary worth trusting is one the customer can verify
without us, and that a company arguing so had better say where its own bookkeeping falls short.

## References

Raymond, E. S. 1999. *The Cathedral and the Bazaar: Musings on Linux and Open Source by an
Accidental Revolutionary.* O'Reilly Media.

Benkler, Y. 2002. Coase's Penguin, or, Linux and the nature of the firm. *Yale Law Journal*
112(3): 369–446.

Lerner, J., and Tirole, J. 2002. Some simple economics of open source. *Journal of Industrial
Economics* 50(2): 197–234.

Farrell, J., and Klemperer, P. 2007. Coordination and lock-in: Competition with switching costs
and network effects. *Handbook of Industrial Organization,* vol. 3. Elsevier.

Open Core Ventures. *Handbook — Licensing and Distribution.*
[https://handbook.opencoreventures.com/commercial-mvp/licensing-and-distribution/](https://handbook.opencoreventures.com/commercial-mvp/licensing-and-distribution/)

Linux Foundation. *SPDX License List — standardised licence identifier registry.*
[https://spdx.org/licenses/](https://spdx.org/licenses/)

## Contributors

Prepared by Woodfine Management Corp.

## How this paper was produced

AI assistance was used in preparing and revising this paper.

## Disclosures

Woodfine Capital Projects Inc. ("Woodfine") is the author of record. PointSav Digital Systems,
which builds the platform described, is currently a trade name of Woodfine, planned to become a
wholly-owned Woodfine subsidiary upon incorporation; PointSav does not itself offer, sell, or
solicit any security. The commercial boundary and the licensing arrangement described in this
paper are our own, so this paper argues for an approach we have a direct commercial interest in.
This work was funded internally; no external research funding was received. The descriptions of
how copyright and open-source licences operate are given in general terms to explain a design and
are not legal advice on any party's rights or obligations under any licence. This paper's content
is provided for engineering, operational, and research purposes and does not constitute investment
advice or a solicitation to invest in any Woodfine direct-hold solution. Some statements above
describe planned or intended future work; in particular, the licence assignments described in
Section 5 as intended are a reasoned direction and not a ratified decision, and have not been
executed. Language such as "planned," "intended," "targeted," "may," and "expected" marks this
forward-looking content, which is subject to change and does not constitute a commitment
regarding future performance.

## Data and reproducibility

The licensing position reported in Section 5 was established by reading the platform's own
component declarations directly in preparing this paper, rather than from a published summary,
and by comparing what each component declares against what our own published documentation says
it should carry. Every component in the codebase carries — or, in a number of cases, fails to
carry — a machine-readable licence identifier in its own build manifest and in a header at the top
of its source files. Those identifiers follow the standard public registry maintained by the
Linux Foundation [spdx-license-list], so a reader can look up exactly what each named licence
permits. Both counts reported in Section 5 — the components with no declaration at all, and the
component whose declaration disagrees with its published classification — are reproducible by
anyone reading the published source, and we have deliberately reported their shape rather than a
precise tally, because the tally changes with every commit and a stale number would be worse than
none. The commercial boundary described in Section 4 is verifiable two further ways. A reader can
confirm that the aggregation component is a separate component with its own source tree, rather
than a set of disabled capabilities inside the free ones. And they can confirm the enforcement
asymmetry reported there by searching the published source: licence-checking code exists in the
paid components, where it is documented at its own definition site as an offline check against a
built-in key with a thirty-day grace period, and returns nothing at all in the free ones. Our code is sole-authored, which is why
relicensing it is a decision available to us at all; a project with many outside contributors
generally cannot change its licence without their agreement. No independent party has audited this
software, verified these licence declarations, or reviewed these claims.

Totebox Archive™, Totebox Orchestration™, PointSav Digital Systems™, and Woodfine Capital
Projects™ are trademarks of Woodfine Capital Projects Inc.
