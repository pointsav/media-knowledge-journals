---
schema: journal-v2
slug: typeface-families-for-an-open-platform
title: "Building Toward Type Nobody Can Take Back"
subtitle: "Why an open platform works toward typographic independence, and how far that work has actually got"
site: design.pointsav.com
imprint: PDS-018
thesis: "A platform meant to outlive its supplier should be built toward typographic independence from any single vendor, so that no document it produces can be broken by a licence lapsing."
abstract: |
  Our thesis is that a platform whose whole argument is that a customer should not depend
  on a supplier has to apply that argument to its own typefaces, and we are building
  toward that rather than reporting it as done. A typeface is licensed software, not a
  possession: a commercial font licence is typically counted by seats, by page views, or
  by the number of applications it is embedded in, and it can lapse, be renegotiated, or
  be breached by ordinary growth. A document whose typeface licence has lapsed is a
  document that cannot be reissued as it was. The direction we hold is that every face a
  document depends on should be one that nobody can withdraw. Real, completed work
  supports that direction. Every brand-facing typeface once specified from a proprietary
  vendor library has a named openly-licensed replacement recorded in the published
  typography rules, and the site publishing this paper serves its own body and monospaced
  faces as files from its own deployment, under a licence permitting redistribution, with
  the licence text shipped beside them and no request reaching an outside font service.
  Four limits are stated plainly. No document-generation tool consumes the print
  typography rules yet. The retired proprietary names still sit in the live style fallback
  chains, ahead of their open replacements in two of the three. This site's own heading
  face is named in its style variables with no font file behind it, so headings fall
  through to whatever serif the reader's machine provides. And where the platform does
  rely on ordinary system faces, that is a simplicity choice about speed and third-party
  requests, not the completion of an independence story.
state: draft
version: "0.1.0"
published:
updated: "2026-09-21"
cite_as:
license: CC-BY-4.0
cites:
  - sil-ofl-1-1
  - spdx-license-list
  - dtcg-w3c
draws_from:
  - brand-typography
  - wiki-typography-system
  - design-primitive-vocabulary
  - what-is-a-design-token
  - design-system-substrate
  - brand-family-swatch
  - design-tokens-and-accessibility
prepared_by: "Woodfine Management Corp."
keywords:
  - typography
  - open font licensing
  - design tokens
  - vendor independence
  - document longevity
---

> This paper is provided for engineering, operational, and research purposes and does not
> constitute investment advice or a solicitation to invest in any Woodfine direct-hold
> solution. Statements marked "planned," "intended," "targeted," "may," or "expected" are
> forward-looking and subject to change. Full disclosures appear at the end of this paper.

Working Paper PDS-018 · v0.1.0 · CC BY 4.0

Our thesis is that a platform built so that its customers do not depend on a supplier has
to apply the same standard to its own lettering — and that we are building toward that
rather than reporting it as finished. A typeface is not a possession. It is licensed
software, counted and metered like any other, and a document that depends on one depends
on that licence continuing to hold. When the licence lapses, or the terms change, or the
business simply grows past what it paid for, the document cannot be reissued as it was.
For most documents this is an irritation. For a document a person may need to produce
again, unaltered, years after it was signed, it is a real defect in a real thing.

The direction we hold is straightforward: every typeface a document of ours depends on
should be one that nobody can withdraw. Real work supports that direction and is worth
being specific about. Every brand-facing typeface once specified from a proprietary vendor
library now has a named openly-licensed replacement recorded in the published typography
rules. The site publishing this paper holds its own body face and its own monospaced face
as files in its own deployment, under a licence anyone may rely on, with the full licence
text shipped beside the files and no request going out to an outside font service when a
reader opens a page.

That work is evidence of a direction in progress, not proof the direction has been
travelled. Four things are not finished and this paper says so in its own section rather
than a footnote: no document-generation tool consumes the print typography rules yet; the
retired proprietary names are still sitting in the live style fallback chains, ahead of
their open replacements in two of three cases; this site's own heading face is named in its
style variables with no font file behind it, so headings fall through to whatever serif the
reader's machine has; and where the platform does rely on ordinary system faces, that is a
choice about speed and third-party requests rather than an independence achieved. Those are
different claims and conflating them would flatter us.

## 1. The thesis

A platform can be open in its code, open in its data, and open in its licence, and still
have one thread running out of it to a supplier who can pull. Typography is a common place
for that thread to be, precisely because it looks like a matter of aesthetics rather than
of dependency.

Our position is that it is a dependency, and it should be removed the same way every other
dependency on this platform is meant to be removed — not by promising to behave well, but
by arranging things so that nobody has a lever to pull. A document set out in a typeface
that anyone may use and redistribute cannot be broken by a commercial decision taken
somewhere else. A document set out in a licensed commercial face can be.

The reason to care is not the appearance of the page. It is the reproducibility of the
document. A great deal of what this platform is for is producing records that are meant to
outlast the software that produced them: agreements, statements, filings, records attached
to a building. A record you cannot reproduce in its original form is a weaker record than
one you can. Type is part of the original form.

The composition is the claim, and it is a modest one. Openly licensed typefaces are
ordinary and widely used; there is nothing novel about choosing one. Holding font choices
as named entries in a governed file rather than as strings scattered through stylesheets is
also ordinary. What we are arguing is that the two together should be treated as a
*dependency question* rather than a design question — that "which face" belongs in the same
conversation as "which licence" and "who runs the server," and should be reasoned about
with the same seriousness.

## 2. The problem, in the reader's terms

Most people have never bought a typeface and reasonably assume that a font is something
that comes with a computer, the way a ruler comes with a pencil case. It is worth being
concrete about what a commercial typeface actually is, because the exposure is not obvious
until you see the meter.

A typeface is a design; a font is the software file that draws it. Selling that file is a
licensing business, and the licence is metered in ways that surprise people the first time
they read one. A desktop licence is commonly counted by the number of people who may
install it. A web licence is commonly counted by page views per month or per year. An
application licence is counted by the number of applications the file is embedded in. A
licence to embed the face inside a document that will be widely distributed — a printed
report, a filed prospectus — is often a separate grant again. Exceeding a count is a
breach, and the counts are the kind that ordinary business growth exceeds without anyone
deciding anything.

Now think about what that means for a document. A set of statutory financial statements is
typeset in a licensed face. Five years later, the business needs to reissue that document —
because a regulator asked, because a buyer is conducting due diligence, because a dispute
turns on what the original said. If the licence has lapsed, or the seat count has moved on,
or the supplier has been acquired and the terms have changed, the business is in the
peculiar position of not being permitted to reproduce its own document in its own form. The
content is theirs. The lettering is not.

The traditional comparison is exact and old. A printer setting metal type owned the type.
The trays of sorts sat in the shop and were the shop's property; a printer who kept his
type could reprint a job in twenty years. Photo-typesetting and then digital typesetting
turned the trays into a subscription — which brought enormous benefits and also quietly
converted a durable asset into a recurring permission. An openly licensed typeface returns
the tray to the shop. Not because the open face is better than the commercial one, which
it often is not, but because it is *held* rather than *permitted*.

There is a second, quieter version of the problem, and it belongs to the web rather than to
print. A great many sites do not hold their fonts at all. They load them, when a reader
opens a page, from a large third-party font service. That is convenient and free and it means every
reader's browser makes a request to a company that is not the one whose page they thought
they were reading. Two things follow: the page stops working the way it should if that
service is unreachable, and the reader's visit is visible to a party they did not choose.
Holding the font files on the same server as the page removes both, and costs a few hundred
kilobytes.

## 3. What is actually being governed

This section sets out the mechanics plainly. A reader comfortable with font licensing and
fallback chains may go to Section 4.

### The licence is the thing that matters, and it has a standard name

The openly licensed typefaces used throughout this platform are published under the SIL
Open Font License, version 1.1 [sil-ofl-1-1]. It is worth reading what that licence
actually does, because "open" is a word that covers a range.

It grants permission, free of charge, to use, study, copy, embed, modify, redistribute and
sell copies of the font — with no fee, no seat count and no page-view meter. Three of its
conditions matter here. The font files may not be sold on their own, though they may be
bundled, embedded, redistributed and sold inside any software. A modified version may not
use the original's reserved name, so an altered face cannot be passed off as the original,
which protects a reader's expectation that a named face is the face they think it is. And
each copy distributed must carry the copyright notice and the licence text with it, which
is a small housekeeping duty rather than a restriction.

Two absences matter as much as the conditions. There is no clock and no conversion date;
the permission is not withdrawn later and does not require renewing. And the licence says
in terms that the requirement for the font to stay under this licence does not reach any
document created with it — so a document set in such a face carries no licence obligation
of its own, which is exactly the property a record meant to be reissued years later needs.

Licences of this kind are identified by short standard codes maintained in a public
registry, so an organisation's compliance team can look up exactly what any named licence
permits rather than taking a supplier's characterisation of it on trust
[spdx-license-list]. That matters for the thesis: "this face is safe to depend on" is a
checkable statement, not an assurance.

### A font choice is a token

The platform records its font choices the way it records every other design decision: as a
named entry in a governed file, with a value and a written description of when it applies,
in the standard vendor-neutral interchange format maintained by the Design Tokens Community
Group under the World Wide Web Consortium [dtcg-w3c]. A companion paper on this site
explains that mechanism in full.

The practical consequence is that a font decision is addressable. There is a name for "the
formal serif for institutional print," a name for "the condensed sans for dense financial
tables," and a name for "the workhorse body face." Documents and stylesheets refer to the
name. The face behind the name can be changed in one place, and everything that meant that
role follows — which is precisely the mechanism that made the substitution described in the
next section a change to a handful of entries rather than a hunt through every document
ever produced.

### What a fallback chain is, and why the order in it is a fact

One more piece of mechanics, because the honest limit in Section 6 turns on it.

A stylesheet rarely names a single face. It names a list — a fallback chain — and the
machine displaying the page walks the list from left to right and uses the first face it
actually has available. The list exists because the machine showing the page may be any
machine, and the author cannot know what is installed on it.

The order of that list is therefore not decorative. It is an instruction about preference,
evaluated on the reader's own computer. A name sitting first in the list is the face that
will be used wherever it is present. A name sitting third is a face that will be used only
where the first two are missing. Which means that removing a face from a design and
removing its name from the chain are two different acts, and only the second one is
mechanically true.

There is a second, separate instruction that matters just as much, and the two are easy to
confuse. Naming a face in the chain says which face is *wanted*. A different instruction
elsewhere in the stylesheet says where the file for that face may be *fetched from*. If the
second instruction is missing, the first is merely a wish: the browser looks for the named
face on the reader's own machine, does not find it, and quietly moves down the chain to
something it does have. Nothing announces the substitution. The page looks entirely
reasonable, and it is set in a face nobody chose. Both halves of the honest accounting in
Section 6 turn on this distinction.

## 4. What has actually been replaced

The substitution is real, completed as a decision, and recorded where anyone can read it. It
is presented here as evidence supporting a direction, not as a claim that the direction has
been fully travelled.

The platform's brand typography was originally specified from a well-known proprietary
vendor library — the kind of collection an agency licenses and a corporate identity is
built on. Four roles were involved, and each now names an openly licensed face instead.

The **formal serif** — the face for a white-paper cover, a legal block heading, the title of
a formal document — was a slab serif from that library. Its replacement is Zilla Slab, a
humanist slab serif under the open licence described above, carrying the same institutional
weight the role was chosen for.

The **condensed sans for dense data** — the face for a financial ledger, a tight table, a
capitalised micro-heading where horizontal room is scarce — was a condensed grotesque from
the same library. Its replacement is Barlow Condensed.

The **body face** — the workhorse behind ordinary paragraphs, memoranda and operational
text — was a geometric sans from that library. Its replacement is Nunito Sans.

And a fourth role, a high-contrast **editorial serif** for pull quotes and secondary
markers, is filled by Sahitya, which was openly licensed from the start rather than
replacing anything.

The stated reason for the exercise is the one this paper is about, and it is recorded in the
rules themselves rather than reconstructed here: every asset embedded in a document the
platform produces must be freely distributable, so that no font-licensing review can ever
stand between the platform and producing a document. The replacements were not chosen
because they were free. They were chosen because a licence that cannot be withdrawn removes
a dependency.

The same principle runs through the site serving the pages you are reading. Its body face
is Inter, in five weights; its face for code, command examples and identifiers is JetBrains
Mono, in two. Both are published under the same open licence described above. Both are held
as files inside the deployment's own static assets rather than fetched from an outside font
service when a reader opens a page, so no request leaves for a third party. And the full
text of the licence for each ships in the same directory as the files it covers, naming the
face's own authors — which is precisely the housekeeping duty described in the previous
section, done in the most ordinary way available.

That arrangement is also, in its small way, the second kind of evidence this paper can
offer, because it replaced something broken. The stylesheet that now declares those faces
records on its own face what it corrected: the two faces named there previously were named
and never loaded. There was no instruction anywhere to fetch them, so every reader had been
seeing a substitute all along while the file confidently declared otherwise. A font name in
a stylesheet with nothing behind it is not a typographic decision. It is a decision that
looks like one.

## 5. Where ordinary system faces are used on purpose

Not every surface on this platform carries a brand typeface, and some deliberately carry
none. The design system's own global typography rules name only generic categories — the
reader's system interface sans, the reader's system monospace — and no custom face at all.
Several of the document families in the print rules do the same, specifying ordinary system
or metric-compatible faces for their body text rather than a brand face.

It is worth being precise about why, because it would be easy and wrong to present this as
independence achieved.

The reason is speed and the absence of a third-party request. A generic system face is
already on the machine. Nothing is downloaded, nothing is waited for, and no text flashes
invisible while a file arrives. On an operator's working screen — a console, a panel, a tool
somebody uses all day — that is simply better, and it would be better even if brand
typefaces cost nothing and carried no licence at all. The print families follow the same
logic for a different reason: a set of statutory financial statements is meant to look like
a set of statutory financial statements, and the plain, universally available faces that
register uses are the correct answer rather than a compromise.

So this is a simplicity choice, made for its own reasons. It happens to carry no font
dependency, which is a welcome side effect. It is not the same thing as having removed a
dependency that was there, and it should not be counted twice. A platform that used only
system faces everywhere would have no typographic dependency and would also have made no
typographic decision; that is not the position we are arguing for, and it is not the
position we are in.

## 6. What is not finished

Four things, stated plainly.

**No document-generation tool consumes the print typography rules yet.** The open
substitutions described in Section 4 specify what a print and PDF pipeline should use once
one exists. They are not, today, a live mechanism embedding those faces into shipping
documents. The platform's own published documentation says so in as many words, and that is
the accurate description: a decision made and recorded, waiting on the machinery that will
act on it.

**The retired names are still in the live fallback chains.** The platform's live style
variables name three font roles, and each chain still contains the proprietary name it was
meant to leave behind. In two of the three — the display role and the serif role — the
retired name sits *ahead* of its own named open replacement in the order. Since a fallback
chain is evaluated left to right on the reader's own machine, a machine with the retired
face installed will use it in preference to the open substitute that was chosen to replace
it. The first name in each chain is an openly licensed face, so the common case is
unaffected; but the retired names have not been removed, and the ordering means the
substitution is not yet mechanically complete in the place that decides what a reader
actually sees. We found this by reading the file while writing this paper, which is roughly
the point of writing it.

**This site's own heading face has no file behind it.** The previous section described a
correction: two font names declared with nothing instructing a browser to fetch them.
Exactly one instance of that defect is still present on this site, and it is in the
paragraph above's own subject matter. The style variable for display and heading text names
a serif face; there is no rule anywhere in the stylesheet telling a browser to load it, and
no file for it in the directory holding the others. The heading you are reading is
therefore set in whatever serif the machine in front of you happens to provide, by way of
the fallback the same variable declares. Nothing is broken and nothing is misrepresented to
a reader, but a named face that is never loaded is a decision recorded and not taken, and it
is the sort of thing a paper of this kind should say rather than leave for a reader to
discover.

**The independence claim is a direction and should be read as one.** What is true today is
that the decisions have been made, recorded and published; that the platform serving these
papers holds its own faces rather than borrowing them; and that the roles that would
otherwise depend on a proprietary library have named open replacements waiting. What is not
true is that a document produced by this platform today has been demonstrated end to end,
from source text to finished file, using only faces nobody can withdraw — because the tool
that would produce that file does not exist yet. We intend to build it. Saying it is done
would be the easiest sentence in this paper to write and the one a reader could most simply
disprove.

## 7. What this changes for the reader

The first change is what a reader can check. Typography is unusual among the independence
claims a platform might make, because it is inspectable without any special access: the
licences of the named faces are public, the font files served by a page can be seen by
anyone who looks at what a page loads, and the rules recording the choices are published
text files. A reader who wants one concrete, verifiable instance of whether this platform's
independence talk is real can start here, and will find both the substitution and its
unfinished edges.

The second change is about the durability of documents. A record produced entirely from
openly licensed faces can be reproduced in its original form indefinitely, by anyone, with
no permission needed from anyone. For a class of record meant to outlive the software that
made it — an agreement, a statement, a filing — that is a property worth having and cheap to
obtain, and it costs a reader nothing to ask their own suppliers about.

The third change is for readers of the pages themselves. A page whose fonts come from its
own server does not report the visit to a third party and does not stop looking right when
that third party is unreachable. That is a small benefit, freely available, that a great
many sites decline for convenience.

The trade-offs are real and belong in the same paragraph. Openly licensed faces are
genuinely constrained: the commercial libraries are deeper, better hinted in places, and
carry weights and widths that do not always have an open equivalent, and a designer who
needs a specific one is being asked to give something up. Holding font files yourself means
carrying a few hundred kilobytes and updating them by hand rather than having a service do
it. And the honest headline of this whole paper is that the completed part of the work is a
set of recorded decisions and a self-hosted web platform, while the document pipeline those
decisions were made for has yet to be built.

## 8. An open invitation

This paper states a position we hold and several questions we would rather have answered
than assumed.

To researchers in digital typography and type design: the replacements in Section 4 were
chosen for aesthetic correspondence to the faces they replace and for licence terms. Whether
they hold up as *durable* choices over a ten- or twenty-year horizon — actively maintained,
covering the character sets that bilingual and multi-jurisdictional documents need,
rendering well on the kinds of hardware a printed regulatory document eventually passes
through — is a genuinely open assessment we are not qualified to make about our own choices.

To specialists in document preservation and archival practice: the argument that an openly
licensed face makes a document more reproducible assumes the font file itself remains
available and unchanged. Fonts are versioned; metrics shift between versions; a document
reproduced with a later version of the same named face is not necessarily identical. What
the right practice is — embed the exact file with the document, record a fingerprint of it,
something else entirely — is a question the preservation field has thought about far longer
than we have.

To font-licensing and compliance specialists: we would value a rigorous reading of what an
organisation actually has to do to stay clean when it redistributes openly licensed faces
inside its own product and inside the documents that product generates. We believe the
obligations are light. We would rather be told precisely where they are not than assume it.

To anyone who maintains typography across a large body of published material: both defects
in Section 6 are the same shape — a name recorded in a file that does not match what a
reader's machine actually does — and both were found by a person reading the file rather
than by anything that reports it. We would be glad to learn what genuinely catches this
class of drift in practice: a face named but never fetched, or a retired name still sitting
ahead of its replacement in a preference list.

And to designers who have moved a real brand identity off a commercial library: we are
interested in what was lost, not what was gained. The gains are easy to list and we have
listed them. The losses are the part a paper written by the party making the change is least
likely to see clearly.

## 9. Conclusion

A platform built so that its customers do not depend on a supplier should be built toward
typographic independence too, and that is the direction we hold. The reason is not
aesthetic. It is that a document whose typeface licence can lapse is a document that may
one day be impossible to reissue in its original form, and a great deal of what this
platform exists to produce is records meant to outlast the software that made them.

The work supporting that direction is real and specific: every brand-facing role once
filled from a proprietary library now names an openly licensed replacement in the published
rules, and the site serving these papers holds its own body and monospaced faces under a
licence nobody can withdraw, in its own deployment, with the licence text beside them and no
outside request. The work remaining is equally specific: no document-generation tool
consumes those print rules yet; the retired proprietary names are still sitting in the live
fallback chains ahead of their replacements in two of three roles; this site's own heading
face is named with no file behind it and resolves to whatever serif the reader already has;
and using ordinary system faces on an interface is a choice about speed rather than an
independence achieved. We would rather publish a direction with its distance still to run
than a completion a reader could disprove by opening one file.

## References

SIL International. *SIL Open Font License, Version 1.1.*
[https://openfontlicense.org/](https://openfontlicense.org/)

Linux Foundation. *SPDX License List — standardised licence identifier registry.*
[https://spdx.org/licenses/](https://spdx.org/licenses/)

Design Tokens Community Group. *Design Tokens Format Module.* World Wide Web Consortium
Community Group. [https://tr.designtokens.org/format/](https://tr.designtokens.org/format/)

## Contributors

Prepared by Woodfine Management Corp.

## How this paper was produced

AI assistance was used in preparing and revising this paper.

## Disclosures

Woodfine Capital Projects Inc. ("Woodfine") is the author of record. PointSav Digital
Systems, which builds the platform described, is currently a trade name of Woodfine,
planned to become a wholly-owned Woodfine subsidiary upon incorporation; PointSav does not
itself offer, sell, or solicit any security. The typography rules and the platform
described are our own work, so this paper argues for an approach we have a commercial
interest in. This work was funded internally; no external research funding was received.
The descriptions of how font licensing operates are given in general terms to explain a
design and are not legal advice on any party's rights or obligations under any font licence.
No claim is made or implied about the terms, conduct or quality of any typeface supplier;
the faces replaced are described by role rather than by vendor because the argument is about
dependency structure, not about any particular firm. This paper's content is provided for
engineering, operational, and research purposes and does not constitute investment advice or
a solicitation to invest in any Woodfine direct-hold solution. Some statements above describe
planned or intended future work; in particular, the document-generation pipeline that would
consume the print typography rules is intended and does not exist, and the removal of the
retired proprietary names from the live fallback chains is intended and has not been done.
Language such as "planned," "intended," "targeted," "may," and "expected" marks this
forward-looking content, which is subject to change and does not constitute a commitment
regarding future performance.

## Data and reproducibility

Everything this paper reports was read directly from the published files in preparing it,
rather than from a summary. The four typeface roles, the faces they now name, and the
proprietary faces each replaced are recorded together in one short published document in the
design-system repository, along with the stated reason for the exercise. The platform's own
global typography rules, which name only generic system categories and no custom face, are a
separate published file in the same repository. The live style variables reported in Section
6 are three lines in a single published stylesheet file, and the ordering described there —
the retired name sitting ahead of its open replacement in two of the three chains — can be
confirmed by reading those three lines. The font files this site serves are in its own
static assets directory, visible to anyone who inspects what a page loads, and the full
licence text for each sits in that same directory as an ordinary text file naming the
face's authors; the licences are also public documents identified by standard registry
codes [spdx-license-list], so a reader can confirm what each one permits without relying on
this paper's description. The heading-face gap reported in Section 6 is confirmable the same
way and in the same stylesheet: the variable naming that face is present, the instruction
that would fetch it is not, and no file for it exists among the others. That stylesheet's
own comments record the earlier version of the same defect, described in Section 4, in its
own words. The statement that no document-generation tool consumes the print rules is the
platform's own published current-state description, not an inference drawn here. No
independent party has audited these typeface choices, verified these licence terms, or
reviewed these claims.

PointSav Digital Systems™ and Woodfine Capital Projects™ are trademarks of Woodfine
Capital Projects Inc.
