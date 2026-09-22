---
schema: journal-v2
slug: design-system-ships-as-a-binary
title: "A Design System That Ships as a Binary, Not a Hosted Service"
subtitle: "Open data under a permissive licence, and a single installable program the customer runs on their own machine"
site: design.pointsav.com
imprint: PDS-017
thesis: "A design system should be delivered as data a customer owns outright and a program they install and run themselves, so that nothing about it depends on the vendor continuing to operate a service."
abstract: |
  Our thesis is that a design system — the governed record of an organisation's design
  decisions — should be delivered as something the customer possesses, not something they
  log into. We split the delivery in two. The design decisions themselves are published
  as plain data files under a permissive open-source licence: anyone may take them, use
  them commercially, and never speak to us again. The program that stores, versions,
  documents and serves an organisation's own decisions is a single installed program,
  configured by three settings, running on the customer's own machine against a directory
  the customer controls, with no request-time call to us and no shared database between
  one customer's deployment and another's. It keeps working if the commercial
  relationship ends, because nothing in it asks us for permission to run. Two things are
  stated honestly rather than smoothed over. No customer has yet exercised the commercial
  licence; the only running deployment of the engine anywhere is our own. And the engine
  itself currently carries a delayed-conversion licence rather than the permissive one a
  companion paper on the platform's licensing argues belongs on anything sitting on a
  customer's own records path — a real gap between our stated destination and our present
  position, on the specific product this paper is about.
state: draft
version: "0.1.0"
published:
updated: "2026-09-21"
cite_as:
license: CC-BY-4.0
cites:
  - dtcg-w3c
  - spdx-license-list
  - open-core-handbook
  - farrell-klemperer-2007-switching-costs
  - lerner-tirole-2002-open-source-motivation
  - open-source-guides-leadership
draws_from:
  - design-system-substrate
  - self-hosting-customer-controlled-design-systems
  - registry-driven-releases
  - what-is-a-design-token
  - component-recipes-vs-raw-tokens
  - customer-hostability
  - legal-and-ip-structure
  - software-distribution-substrate
prepared_by: "Woodfine Management Corp."
keywords:
  - design systems
  - self-hosting
  - software licensing
  - installed software
  - vendor independence
---

> This paper is provided for engineering, operational, and research purposes and does not
> constitute investment advice or a solicitation to invest in any Woodfine direct-hold
> solution. Statements marked "planned," "intended," "targeted," "may," or "expected" are
> forward-looking and subject to change. Full disclosures appear at the end of this paper.

Working Paper PDS-017 · v0.1.0 · CC BY 4.0

Our thesis is that a design system should be something an organisation possesses rather
than something it logs into. The design decisions themselves — which colours mean what,
how far apart things sit, what a button is and what it must do for a reader using a screen
reader — should be plain data files the organisation holds, under terms that let it do
anything it likes with them. The program that stores, versions, documents and publishes
those decisions should be a program the organisation installs on a machine it controls and
runs for as long as it wants to, whether or not it is still paying anyone.

That is not how this category of software is normally delivered. The commercial tools that
do this job are, with very few exceptions, services the customer signs into: the
organisation's own design decisions live on the supplier's computers, and the supplier's
continued operation is a working dependency of every screen the organisation builds. This
arrangement is convenient and it is also a particular kind of exposure, and it is
disqualifying outright for a certain sort of buyer — a bank, a law firm, a government
department — whose rules about where its own material may live rarely make an exception for
design assets just because they seem unimportant.

This paper takes four things in turn. What "ships as a binary" actually means, from the
beginning, because the distinction between an installed program and a hosted service is
the whole argument and is not obvious to a reader who has never had to care. What the
design system is actually made of, and why its two halves are delivered under different
terms. Where that split is not yet as clean as the previous sentence implies, stated
plainly, on this specific product. And a real failure our own checking caught, included
because a paper about governed records that omits its own defects is not evidence of
anything.

## 1. The thesis

An organisation's design system is a record of decisions. Which blue is the one that means
"you can press this." How much space sits under a paragraph. What a warning looks like.
What a button must announce to someone who cannot see it. In a small organisation these
decisions live in people's heads and in the last file anyone edited. In a large one they
are written down, because otherwise every team re-decides them and the organisation's work
stops looking like one organisation's work.

Once they are written down, the question is where the writing lives and who controls it.
Our position is that the answer should be: in the organisation's own files, on the
organisation's own machine, under terms that give the organisation everything.

We split the delivery into two parts to make that true.

The first part is the decisions themselves, published as plain text files in a standard,
vendor-neutral format under a permissive open-source licence. "Permissive" here means
essentially unconditional: take it, use it, build a commercial product on it, change it,
never publish your changes, never tell us. Keep the copyright notice attached and do not
claim we endorsed you. That is the whole obligation. There is no account to open, no server
to reach, and no relationship with us of any kind. If this site stopped existing tomorrow,
every copy of the data would keep working, because the data was never attached to the
service that publishes it.

The second part is the program. An organisation that wants to govern, version, document and
publish *its own* decisions over time needs software to do it, and that software is
delivered as a single installed program rather than a login. The organisation puts it on a
machine, points it at a directory of its own files, and runs it. It answers to that
directory. It does not call us when a request arrives. It does not share a database with
anyone else's deployment. If the commercial relationship ends, the program continues to
run, because nothing in it was ever asking our permission.

The composition is the claim. Open data on its own is common and good; plenty of large
organisations publish their design tokens. An installed program on its own is ordinary;
most software used to be delivered that way. What is uncommon is doing both at once for
this particular job, so that the layer holding the customer's own material is the layer
they own outright, and the layer they might pay for is a tool sitting beside it rather than
a gate in front of it.

## 2. The problem, in the reader's terms

The suspicion this paper is addressed to deserves to be stated in its strongest form.

An organisation adopts a hosted tool because it is easy and it works. Over several years,
the organisation's design decisions accumulate inside it — hundreds of them, each
referenced by dozens of screens and documents, with a history of who changed what and why.
The tool has become the organisation's institutional memory for an entire discipline.

Now consider what the organisation's position actually is at renewal. Its own decisions are
on someone else's computers. Getting them out, if it is possible at all, produces a file
whose format only that supplier's software fully understands. The price can move; the terms
can move; the supplier can be acquired, change direction, or stop existing. None of this
requires anyone to behave badly. It requires only that the cost of leaving is high and
that both sides can see it. That is a well-developed piece of economics rather than a
grievance: the existence of a cost to switch changes what a supplier can charge a customer
who has already arrived, independent of anything about the product's quality
[farrell-klemperer-2007-switching-costs].

Compare two arrangements a business might have for its own books. In the first, the
bookkeeping lives in a service the business signs into. The ledgers are real and the
service is good, and if the business stops paying, it stops being able to open its own
ledgers. In the second, the business keeps its ledgers in its own filing cabinet and pays
an accountant for help with them. If it stops paying the accountant, it has lost the help.
It has not lost the books.

Both arrangements involve real software, real value and real money. The difference is
entirely in where the record sits when the relationship ends. A reader evaluating a
supplier is entitled to ask which of the two they are being offered, and to notice that
the answer is usually the first one and is usually not stated.

## 3. What "ships as a binary" actually means

This section establishes the distinction the rest of the paper rests on. A reader already
comfortable with the difference between installed software and a hosted service may go to
Section 4.

### A program is a file

Software written in the ordinary way begins as source code: text a person writes, readable
by anyone who can read that language. Before a computer can run it, a compiler translates
that text into machine instructions and packages them into a single file. That file is the
binary — sometimes called an executable, in the way a document produced by a typewriter is
a different object from the typist's shorthand.

The important properties of a binary, for this argument, are mundane. It is a file. You can
copy it. You can put it on a machine you own and it will run there. It does not need the
person who made it to still be in business, or reachable, or willing. Once you have it, you
have it — which is exactly the property the phrase "buying software" used to describe, and
mostly no longer does.

This design system's engine is a binary of that kind: one compiled program, installed on a
machine and started by the machine's ordinary startup arrangements, in the same way a
database or a web server is started. It is deliberately not packaged as a container — the
now-standard bundle that carries a program together with a small copy of an operating
system around it — because a container is another layer of machinery the customer has to
operate and another dependency between them and the thing running.

### What a hosted service is instead

A hosted service inverts the arrangement. The binary runs on the supplier's machines. What
the customer receives is not the program but the right to send requests to it — a login.
The customer's data is stored where the program runs, which is to say on the supplier's
machines, usually in one large shared database holding every customer's material with
software-enforced walls between them.

Nothing about this is dishonest, and for many purposes it is the right trade: the supplier
handles the operating, updating, backing up and securing, which is real work the customer
would otherwise do. The trade is specific and it is worth naming: convenience now, in
exchange for the supplier's continued operation becoming a working dependency of the
customer's own records.

### What this one does instead

The engine is installed and run by the customer, and its entire configuration surface is
three settings: which directory holds their material, which brand identity within that
directory to serve, and which network address to listen on. One running copy serves one
organisation's directory. There is no shared database and no shared infrastructure between
one organisation's deployment and another's, because there is no shared anything — they are
separate copies of a program on separate machines.

Two consequences follow, and they are the practical substance of the whole thesis.

There is no export step, because there was never an import. The material is files in a
directory the organisation already controls. Moving to a different hosting provider, or
taking the whole thing off the network entirely for a review, means moving a directory and
restarting a program.

And governance — who may change what, what changed when, who approved it — comes from the
organisation's own version control rather than from permissions inside our software. A
change to a design decision is a commit. Edit rights are branch protections. The history is
the repository's log. Review is a pull request. These are the same mechanisms the
organisation's engineering department already runs and, in a regulated business, has
already had audited. Nothing new has to be trusted.

### Why publish the source at all

It is worth saying plainly why a commercial firm publishes source code, since a reader
meeting this for the first time may reasonably assume charity or naivety. The published
literature identifies a set of unsentimental commercial motives: attracting skilled
contributors, establishing a format others build on, lowering the cost of a customer's
evaluation, and obtaining review from people who are not on the payroll
[lerner-tirole-2002-open-source-motivation]. The governance practices that make an open
project usable by outsiders — a stated licence, a contribution process, a visible decision
record — are themselves a well-documented discipline rather than an afterthought
[open-source-guides-leadership].

We publish for those reasons and for one more that is particular to this product. An
organisation is being asked to believe that the program does not phone home, holds nothing
back, and will keep working without us. Those are claims about behaviour. The only way to
check a claim about behaviour is to read the thing that behaves.

## 4. The two parts, and the terms on each

### The data: permissive, and genuinely so

The design decisions — colours, spacing, typography, motion, the document-structure rules a
companion paper on this site describes, and the component recipes that compose them into
working elements — are published as plain files in the standard interchange format
maintained by the Design Tokens Community Group under the World Wide Web Consortium, whose
first stable version was published in October 2025 [dtcg-w3c]. That matters because it is
what makes the files portable: a token file in this format is not a thing our software
understands, it is a thing anyone's software understands.

The licence on that data is Apache-2.0 — a permissive open-source licence, one of the most
widely used, which grants unconditional permission to use, modify, distribute and sell,
adds an express promise not to sue users over patents covering the contributors' own
contributions, and asks in return only that the copyright notice travel with the files and
that nobody imply an endorsement. Licences of this kind are identified by short standard
codes maintained in a public registry, so a reader can look up exactly what any named
licence permits without taking a vendor's characterisation of it on trust
[spdx-license-list].

Using the data requires nothing. No account, no server, no fork, no relationship. For a
great many readers that is the entire transaction, and the paragraphs that follow are not
relevant to them.

### The program: an installed binary, with a commercial alternative beside it

The engine is version 0.3.0 and is a single compiled executable. Its source is published
and readable, under a licence that permits most uses immediately and converts automatically
to the same permissive licence as the data after a fixed period following each release.
Each release carries its own clock. A customer who cannot wait for that clock — or who
wants terms without the intervening condition at all — may obtain a commercial licence
instead; that offer is stated in the repository's own licence notice with a real contact
address, not buried in a sales process.

Two honest facts about that arrangement belong here rather than in a footnote.

No customer has yet exercised the commercial licence. Our own instance is the only
deployment of this engine anywhere. The five-step procedure for running your own copy is
documented, and every step of it uses ordinary tooling any competent systems administrator
already operates — clone a repository, edit a directory, run a program, put a reverse proxy
in front of it — but no organisation outside ours has run that procedure end to end in
production. Every claim in this paper about what an external deployment would be like is
therefore architectural rather than observed.

And the delayed-conversion licence on the engine is a real, present condition rather than a
formality. Until the clock runs out on a given release, one particular use of that release
requires our permission. That permission has never been asked for and has never been
refused. But the gate exists, and the next section is about why that is a problem we have
named rather than a detail we would rather not mention.

## 5. Where the split is not yet clean

A companion paper on the platform's software site argues that the line between the free and
the paid parts of this platform should be drawn by architecture rather than by a feature
list, and it is careful to separate that question from a second one: which open-source
terms each individual component carries. On that second question it states a destination
and admits the present position falls short of it. The destination is specific. Anything
sitting on the path a customer takes to reach their own kept records is intended to carry
permissive terms, because a permission gate on somebody's own records is incompatible with
the commitment that those records stay freely transferable — and an unexercised gate is
still a gate. Components with no kept-records role, where the real commercial exposure is a
competitor reselling our hosting without contributing anything back, are intended to carry
strong network copyleft instead, which closes that exposure permanently.

This paper's own product falls on the first side of that line, and does not yet carry the
terms that side calls for.

The engine serves an organisation's own vault: their decisions, their rationale documents,
their brand. If anything on this platform is on a customer's own records path, this is. Its
current licence is the delayed-conversion one described above. By the destination that
companion paper sets out, it should be permissive now rather than permissive on a schedule.
Moving it is a change we are able to make, because the code is ours alone and relicensing
our own work does not require anyone else's agreement — a project with many outside
contributors generally cannot change its licence at all without collecting permissions.
It is an intended action that has not been taken, and stating it as already done would be
untrue.

There is a second gap, smaller and more embarrassing, and it is the same class of defect
that companion paper reports across the wider codebase. The source tree contains a second
component reserved for this work which is, today, an empty placeholder — one stub function
and nothing else — and whose build manifest declares no licence identifier at all. The
repository-wide rule assigns terms to it by the directory it sits in, so it is not
unlicensed in substance; but a reader or an automated tool looking where such things are
normally declared finds nothing there, and the placeholder's own descriptive text asserts a
reservation posture that does not sit comfortably beside the repository-wide assignment
covering it. One of those two statements is the operative one. Both are published.

A third inconsistency is worth reporting because a reader checking our claims will hit it
before they hit anything else. Two of the platform's own published articles about this
engine, both written in August 2026, describe its licence as the platform's previous
default rather than the tier a licensing decision ratified on 1 September 2026 assigns it.
The shipped code and the repository's own licence notice agree with each other and with the
September decision; the two articles have not been updated to match. That is a
documentation lag rather than a disagreement about what the licence is, and it is precisely
the kind of drift the next section is about.

None of this is presented as a scandal. It is presented because a paper whose argument is
"you can check this yourself rather than trusting us" has no business implying that
everything a checker will find is already tidy. A reader who checks will find what is
described here. We would rather they find it here first.

## 6. A real failure, used as evidence

The argument that a governed record beats a set of parallel hand-maintained copies is easy
to assert. What makes it worth believing is that this system has violated it, twice, in its
own working history, and that the violations were found by checking rather than by
accident.

The first is small and instructive. A page whose central diagram argued that the site's
navigation and its machine-readable index cannot disagree, because both are read from one
file, carried a worked example in which they disagreed. The visible navigation listed eight
sections. The index alongside it listed seven, omitting one that the navigation plainly
included. The reason is exactly the failure mode the page was describing: in a hand-built
mock-up, both the navigation and the "index" are typed by hand, so the structural guarantee
the page described did not yet protect the page describing it. One edit had been applied to
one copy and not the other.

The second is larger. The repository carried two files of design-token data with the same
name — one at the top level, one inside the vault — with overlapping contents and no
declared relationship between them. Resolving the question required a full reconciliation
in which every reference was followed to the literal value it eventually resolves to on
both sides, rather than comparing the text as written. That found 107 token paths present
in both files. Of the fifty apparent disagreements in value, forty were not disagreements
at all: one side referred to a name where the other had written out the value that name
points to, so the two agreed and merely said so differently. Ten were real conflicts. And
five colours existed only in the copy nobody was maintaining any more.

Two details make this worth reporting rather than quietly fixing. Neither copy actually fed
the live site, which resolves its tokens through a separate compiled export — so the
divergence was invisible in production while remaining a live hazard for any outside tool
that picked the wrong file. And the fix was not "clean up both copies." It was: declare one
copy canonical, fold the five genuinely-new values into it, and replace the other with a
stub pointing at the canonical one. The second copy was eliminated as a thing that can
drift, rather than improved as a thing that will.

The mechanism that came out of that is the closest thing this paper has to proof rather
than argument. The design-system repository now carries a gate that runs on every change:
if a change touches any source token file, the derived export files are regenerated
automatically and added to the same change, and if regeneration fails the change is
refused. The gap it closes is named in the gate's own text — generation used to be a manual
step somebody had to remember after editing, and the export went stale because nobody
remembered. There is now nothing to remember.

What that gate does not cover is stated in the companion paper on this site about
regulated-document structure, and it applies here too: the structural values are
regenerated and checked automatically; the qualitative rules that sit beside them are
strings rather than measurements, and nothing checks a finished document against them
today. Half of this discipline is enforced by machinery. The other half is enforced by
people reading carefully, which is the mechanism whose failure this section just described.

## 7. What this changes for the reader

The first change is what "we will still have this in ten years" can be based on. A
prospective customer can evaluate this the way they would evaluate any installed software:
if we stop paying, does it keep running? Here the answer is yes, and the reason is
structural rather than promissory — the program runs on the customer's machine against the
customer's directory and makes no request-time call to us, which is a fact about the
program rather than a commitment in a contract, and can be verified by reading it or by
watching what it does on the network.

The second change is what happens to the customer's own material. Under a hosted
arrangement the material is the supplier's to hold and the customer's to request. Here the
material never leaves a directory the customer already controls, in a plain-text format
maintained by a standards body rather than by us. There is no migration project waiting at
the end of the relationship, because there was never a migration at the start.

The third change is for a reader assessing not the price but the supplier's incentives. A
company that has put its commercial layer beside a customer's records rather than around
them has given up a particular kind of leverage, permanently and visibly. That is a weaker
commercial position than the alternative, and it is the position we want to be in, because
a customer should not have to depend on our forbearance to open their own files.

The trade-offs are real and belong in the same paragraph. An installed program means the
customer operates it — updates, backups, the certificate that secures the connection — work
a hosted supplier would otherwise absorb, and work a very small organisation may genuinely
not want. Publishing the data under permissive terms means anyone may build a competing
product on it, which we have accepted rather than solved. The standard guidance on drawing
a commercial boundary in an open-source business is written mostly for firms whose product
is a hosted service, where the boundary naturally follows what the supplier operates
[open-core-handbook]; ours is drawn inside software the customer runs, which changes the
problem in ways we have not fully mapped. And the honest headline of this whole paper is
that nobody outside us has yet run the thing in production, so the reader is weighing a
design and its published source rather than a track record.

## 8. An open invitation

This paper states a position we hold and several questions we cannot settle alone.

To researchers in open-source business models: the arrangement described here gives away
the layer holding the customer's material and charges, if at all, beside it. We believe
that is the right place for the line. We do not know whether a firm can sustain it at scale,
and the honest test is comparative — real firms, real decades — rather than an argument
from first principles. We would rather see that study run than keep asserting the
conclusion.

To practitioners who operate design systems inside regulated organisations: the claim that
version-control governance is a full substitute for a hosted tool's permissions, history
and review is ours, and it is untested outside our own use. Where does it actually fall
short? A designer who does not use version control daily is a real person with a real job,
and "it is just a pull request" may be the wrong answer for them. We would value hearing
where this shape has been tried and how it failed.

To licence-compliance specialists: Section 5 rests on the distinction between a permission
that is never exercised and a permission that cannot be exercised. We hold that the
distinction matters a great deal to a customer whose own material sits on the other side of
it. We do not know whether it matters to a procurement officer filling in a supplier
questionnaire, to an auditor, or to a court — and the answer changes how much the intended
licence change is actually worth.

And to anyone who keeps licence and provenance metadata correct across a large codebase:
the gaps in Section 5 were found by counting, not by a tool that told us. We would be glad
to learn what practices genuinely hold this straight at scale, as distinct from the
practices that are supposed to.

## 9. Conclusion

A design system should be something an organisation possesses. The decisions themselves are
published as plain, standard-format data under a permissive licence that asks for nothing
in return but attribution, so that using them requires no account, no server, and no
relationship with us. The software that governs an organisation's own decisions over time
is a single installed program, configured by three settings, running on a machine the
organisation controls against a directory it already owns, with no shared database, no
request-time call to us, and no permission to withdraw.

The honest present tense is smaller than the thesis. No customer has yet exercised the
commercial licence, and ours is the only deployment of the engine anywhere. The engine
itself sits on a customer's own records path while carrying a licence with a
delayed-conversion condition, which is exactly what our own stated destination says should
not be there; a placeholder component beside it declares no licence at all; and two of our
own published articles still describe the engine's licence as the tier it was assigned
before September 2026. We hold that a supplier whose argument is "check this yourself"
earns nothing by reporting only the parts that survive checking.

## References

Design Tokens Community Group. *Design Tokens Format Module.* World Wide Web Consortium
Community Group. [https://tr.designtokens.org/format/](https://tr.designtokens.org/format/)

Linux Foundation. *SPDX License List — standardised licence identifier registry.*
[https://spdx.org/licenses/](https://spdx.org/licenses/)

Open Core Ventures. *Handbook — Licensing and Distribution.*
[https://handbook.opencoreventures.com/commercial-mvp/licensing-and-distribution/](https://handbook.opencoreventures.com/commercial-mvp/licensing-and-distribution/)

GitHub. *Open Source Guides — Leadership and Governance.*
[https://opensource.guide/leadership-and-governance/](https://opensource.guide/leadership-and-governance/)

Lerner, J., and Tirole, J. 2002. Some simple economics of open source. *Journal of
Industrial Economics* 50(2): 197–234.

Farrell, J., and Klemperer, P. 2007. Coordination and lock-in: Competition with switching
costs and network effects. *Handbook of Industrial Organization,* vol. 3. Elsevier.

## Contributors

Prepared by Woodfine Management Corp.

## How this paper was produced

This paper is grounded in the operating and development work the preparing staff do themselves, and in what they have learned from the people they work with routinely: the graphic designers, web developers, and software developers and engineers who build the platform alongside them, and the architects and structural, building-services, and civil engineers they develop buildings with. No outside professional reviewed or approved this paper, and nothing in it is professional advice. It was drafted and edited with AI assistance under editorial direction, and the analysis and conclusions are Woodfine's own.

## Disclosures

Woodfine Capital Projects Inc. ("Woodfine") is the author of record. PointSav Digital
Systems, which builds the platform described, is currently a trade name of Woodfine,
planned to become a wholly-owned Woodfine subsidiary upon incorporation; PointSav does not
itself offer, sell, or solicit any security. The design system, its engine and its
licensing arrangement are our own, so this paper argues for an approach we have a direct
commercial interest in. This work was funded internally; no external research funding was
received. The descriptions of how copyright and open-source licences operate are given in
general terms to explain a design and are not legal advice on any party's rights or
obligations under any licence. This paper's content is provided for engineering,
operational, and research purposes and does not constitute investment advice or a
solicitation to invest in any Woodfine direct-hold solution. Some statements above describe
planned or intended future work; in particular, the licence change described in Section 5
as intended is a reasoned direction that has not been ratified or executed, and every
statement about how an external self-hosted deployment would behave is architectural rather
than observed, because no such deployment exists. Language such as "planned," "intended,"
"targeted," "may," and "expected" marks this forward-looking content, which is subject to
change and does not constitute a commitment regarding future performance.

## Data and reproducibility

Everything this paper reports was read directly from the published files in preparing it,
rather than from a summary. The engine's version number, its single executable target, its
three configuration settings and their defaults, and the licence identifier it carries are
all in its own build manifest and at the top of each of its source files; the
repository-wide licence notice states which terms apply to which directory, names the date
that mapping was ratified, and carries the commercial-alternative offer with a real contact
address. The placeholder component described in Section 5 can be confirmed as a stub in the
same way — one function, and a build manifest with no licence line where the others have
one. The licence identifiers used throughout follow the standard public registry
[spdx-license-list], so a reader can look up precisely what each one permits rather than
relying on our description of it. The token and component data is published in full under
permissive terms in a separate public repository, in the standard interchange format, and
the gate described in Section 6 is a short script in that repository whose own text states
the problem it was written to close. The two worked defects in Section 6 were verified
against the repository's own history before they were first published, and the figures
reported — the shared paths, the apparent disagreements, the ones that were real, and the
colours that existed in only one copy — are those of that reconciliation as recorded at the
time; a reader repeating the exercise today would be measuring a different, since-corrected
state. The two stale licence statements reported in Section 5 are in live published
articles and can be compared against the repository notice directly. No independent party
has audited this software, verified these licence declarations, or reviewed these claims.

PointSav Digital Systems™ and Woodfine Capital Projects™ are trademarks of Woodfine
Capital Projects Inc.
