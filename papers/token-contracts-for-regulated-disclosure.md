---
schema: journal-v2
slug: token-contracts-for-regulated-disclosure
title: "The Shape of a Regulated Document Is Data"
subtitle: "Treating a filing's sections, numbering, and cross-reference grammar as versioned, governed rules rather than a per-document formatting exercise"
site: design.pointsav.com
imprint: PDS-016
thesis: "The required shape of a regulated document — its sections, its numbering, its cross-reference grammar — should be governed, versioned data, decided once and reused, not re-decided document by document."
abstract: |
  Our thesis is that the required shape of a regulated document is itself governable
  data. A prospectus, a statutory year-end financial statement, a subscription
  agreement and a trust deed each have a form the law and professional practice
  constrain: which sections must appear, how headings are cased, how clauses are
  numbered, how one clause refers to another. In ordinary practice that form is
  reproduced by hand, document by document, usually by copying the last document that
  looked right. We hold that it should instead be recorded the way a design system
  already records a colour or a spacing value — as a named, typed, described entry in
  a file, with one shared base and a named set of differences for each document
  category. The platform's published print-and-document token set is built this way:
  a shared layer of page geometry, rule weights and type pairings, and a semantic
  layer of document families that select from it, including one cross-cutting legal
  drafting register of a single shared base plus five per-category variants. Two
  limits are stated plainly. Most values in that legal register are placeholders
  awaiting real measured values. And publishing a rule as data does not enforce it:
  the structural values are regenerated and checked automatically, while the
  qualitative drafting rules alongside them have no equivalent automatic check today.
state: draft
version: "0.1.0"
published:
updated: "2026-09-21"
cite_as:
license: CC-BY-4.0
cites:
  - dtcg-w3c
  - ni-51-102
  - np-51-201
  - bcsc-continuous-disclosure
  - ixbrl-esef
  - sec-17a-4-f
draws_from:
  - what-is-a-design-token
  - component-recipes-vs-raw-tokens
  - design-primitive-vocabulary
  - design-system-substrate
  - brand-typography
  - registry-driven-releases
  - theming-via-semantic-tokens
prepared_by: "Woodfine Management Corp."
keywords:
  - design tokens
  - regulated disclosure
  - document structure
  - legal drafting conventions
  - machine-readable documents
---

> This paper is provided for engineering, operational, and research purposes and does not
> constitute investment advice or a solicitation to invest in any Woodfine direct-hold
> solution. Statements marked "planned," "intended," "targeted," "may," or "expected" are
> forward-looking and subject to change. Full disclosures appear at the end of this paper.

Working Paper PDS-016 · v0.1.0 · CC BY 4.0

Our thesis is that the required shape of a regulated document should be recorded once, as
governed data, and reused — not reproduced by hand every time a new document of that kind
is needed. A prospectus has a shape. So does a set of statutory year-end financial
statements, a subscription agreement, a trust deed, a schedule appended to any of them.
Which sections must appear, in what order; how a heading is cased; whether clauses are
numbered plainly or carry the word "Section" in front of them; how a clause inside the
document refers to another clause, and how that differs from the way the same document
refers to a rule in a statute. None of this is decoration. Much of it is constrained by
law, by a regulator's filing requirements, or by drafting conventions old and settled
enough that departing from them is itself a signal to a professional reader.

In ordinary practice that shape is reproduced by hand. A firm produces its next
subscription agreement by opening its last one, or one it admired, and editing. The
governing rules live partly in a style memorandum, partly in a senior practitioner's
habits, and mostly in the previous document. We hold that this is the wrong place for
them, and that the right place is the same place a design system already keeps the rule
for what colour a warning is or how much space sits under a paragraph: a named entry in a
file, with a value, a type, and a written description of when it applies.

This paper takes four things in turn. What a token actually is, from the beginning,
because the argument does not work without it. What a regulated document's form is
actually required to do, and by whom. How the platform's own print-and-document token set
puts the two together, with one shared base and a named set of differences per document
category. And last, honestly, what happens when a governed rule is broken anyway —
including by us, in our own material — because a rule that cannot point at a real failure
has not yet earned its keep.

## 1. The thesis

There are two ways to hold a rule about how a document must look.

The first is as prose in a style guide: "subscription agreements use flat numbered
headings in bold title case, with a terminal period; do not use all capitals." That
sentence is perfectly clear. It also has no mechanical relationship to any document. It
governs by being read and remembered. When it is not read, or is read and misremembered,
nothing announces the fact. The document that resulted looks confident and is wrong, and
the only detection mechanism is a person who happens to know better reading it closely.

The second is as data: an entry with a name, a value, and a description, sitting in a
file that a build tool reads. The rule is now addressable. It can be pointed at from more
than one place. It can be changed in one place and take effect everywhere it applies. It
can be compared against what a document actually did. It can be versioned, so that a
document produced last year can be shown to have followed the rule as it stood last year
rather than as it stands now — which matters a great deal when the question is asked by
someone examining the document years after it was signed.

Our position is that the second way is correct for regulated documents specifically, and
that the reason is not tidiness. It is that a regulated document's form carries
consequence. A misnumbered clause is a broken cross-reference. A cross-reference that
reads "Section 4" when the document's own divisions are called paragraphs is an ambiguity
a counterparty's counsel will find. A heading scheme that changes halfway through a
hundred-page instrument is the kind of thing that makes a careful reader wonder what else
changed halfway through. Form is not separable from substance in a document whose whole
purpose is to be precise.

The composition is the claim. Design systems have known for a decade how to hold a visual
decision as data. Legal drafting has known for far longer what the conventions are.
Financial reporting regulators have been pushing filings toward machine-readable structure
for years. What is less common is treating the *drafting conventions themselves* — the
heading form, the numbering scheme, the cross-reference grammar — as entries in the same
governed file as the page margin and the rule weight, so that one mechanism answers both
"how wide is the margin" and "does this family use the word Article."

## 2. The problem, in the reader's terms

Consider a law firm's precedent bank: the filing cabinet, physical or otherwise, holding
the firm's best previous versions of each kind of document it produces. It is an
enormously valuable thing. It is also, as a governance mechanism, exactly the weakness
this paper is about.

A precedent bank holds *documents*, not *rules*. The rule that every internal
cross-reference in a document must be capitalised the same way is not written anywhere in
the bank; it is merely true of the good documents in it, and quietly untrue of one or two
of them. When a junior drafter copies a document from the bank, they inherit whatever that
particular document happened to do — the rules it followed, the rules it broke, and the
accidents nobody noticed. Two documents copied from two different precedents diverge, and
the divergence is invisible until someone reads both side by side, which nobody does.

The remedy every firm tries first is a style memorandum. It is the right instinct and it
does not hold, for a reason that has nothing to do with discipline: the memorandum and the
documents are two separate things maintained by two separate acts. The documents change
constantly. The memorandum changes when somebody remembers. The gap between them widens on
its own, without anyone deciding anything. This is the same failure that makes software
documentation drift from software, and the remedy found there is structural rather than
disciplinary — keep one source, and generate everything else from it, so that the copy
which could drift does not exist as a separate thing to drift.

There is a second, sharper version of the problem, and it belongs to regulated documents
in particular. A regulated document is read by people who are entitled to rely on it. An
investor reading a prospectus, an auditor examining a set of statements, a securities
regulator reviewing a continuous-disclosure filing — a filing an issuer is required to
make on an ongoing basis after it becomes publicly accountable, rather than only once when
it first raises money [ni-51-102] [bcsc-continuous-disclosure]. Each of them is reading
for substance, and each of them uses form as a proxy for care. A document whose internal
references are inconsistent invites the question of whether the diligence behind its
numbers was any better. That inference may be unfair in a given case. It is not
unreasonable as a general reading habit, and a firm that wants to be read generously has
an interest in removing the grounds for it.

And the direction of regulatory travel makes the point for us. For listed issuers in the
European Union, the annual financial report must now be filed in a structured electronic
format in which the figures themselves carry machine-readable tags, not merely appear on a
page [ixbrl-esef]. In the United States, the rules governing how certain regulated firms
must preserve their records have for years specified properties of the record-keeping
*system* — that records be preserved in a non-rewriteable form, indexed, and reproducible
on demand — rather than merely instructing firms to keep good files [sec-17a-4-f]. The
regulator's expectation has already moved from "produce a document that looks right" to
"operate a mechanism whose output is right by construction." Our thesis applies the same
move one layer further in, to the document's own structural grammar.

## 3. What a token is

This section establishes the vocabulary the rest of the paper needs, from the beginning. A
reader already at home with design tokens may go to Section 4.

### A decision written down as data

A token is a design decision recorded as data: a name, a value, and — in a mature system —
a type and a written description of when to use it. That is the whole idea, and it is
smaller than it sounds.

Take the most ordinary example. A company's primary colour is a particular blue. In the
usual arrangement, that blue appears as a code — a short string of letters and numbers —
typed directly into every stylesheet, template and slide master that needs it. The value is
duplicated dozens of times, each copy silently independent of the others. When the blue
changes, every copy must be found. Worse, nothing distinguishes the copies that meant
"this is our primary colour" from the copies that happened to use the same blue for an
unrelated reason, so a search-and-replace changes both.

Recording the decision as a token means the blue exists in exactly one place, under a name.
Everything that needs it refers to the name. The name carries the intent: a stylesheet
that says "the colour for things a person can act on" is making a different statement from
one that says "the specific blue number." Change the one entry and every surface that meant
the first thing follows; surfaces that meant something else are untouched, because they
referred to a different name.

The description field is the part most easily overlooked and, for this paper's argument,
the most important. In the platform's own published token set, a timing value is not merely
a number of milliseconds; its description records what it is for — the quick beat of a
button press or a focus outline fading. A spacing value records that it is the floor for
the rhythm between paragraphs. The rule for using the value travels with the value. It is
not in a separate guide that a person has to remember to open.

### Three tiers, and why the middle one matters

The design-system field has converged on arranging tokens in three tiers, each answering a
different question, and the platform's published set follows that convention rather than
inventing one.

**Primitive tokens answer "what values exist?"** They are the raw inventory: a numbered
scale of greys, a set of spacing steps, a handful of durations. A primitive has no opinion
about where it is used. It is a swatch in a case, not an instruction.

**Semantic tokens answer "what does this value mean here?"** A semantic token points at a
primitive and attaches a role — "the surface a page sits on," "the colour of text that is
secondary to the main text," "the outline that shows which control has focus." This is the
tier where meaning lives, and it is the tier that makes the whole arrangement portable: a
different organisation adopting the system re-points the semantic names at its own
primitives, and every document and screen follows, without a single component being
rewritten.

**Component tokens answer "what does this specific part use?"** This button, this surface,
nothing else. Scoping one more name to one component costs a line and buys the ability to
change that one thing later without disturbing anything else.

The discipline that keeps the arrangement coherent is the direction of reference.
Components refer to semantics; semantics refer to primitives; nothing refers the other
way. A component that reaches past the middle tier to grab a raw value directly has
re-embedded exactly the duplication the arrangement exists to remove.

### One format, so the file is portable

For most of the last decade, every tool that handled tokens used its own file shape, which
meant a token file was a private convention rather than something you could hand to
someone else. That changed when the Design Tokens Community Group — a community group
operating under the World Wide Web Consortium, the body that maintains the web's core
standards — published the first stable version of its format, announced in October 2025
[dtcg-w3c]. The format is a plain, vendor-neutral text file: each entry declares its value,
its type, and its description; entries nest into groups; and one entry can refer to another
by name.

The practical effect is that a token file stops being a thing your tooling understands and
becomes a thing anyone's tooling understands. That is what makes the next section possible.
A document-structure rule recorded in this format is not a rule inside our software. It is
a rule in a file, readable by a build tool, an auditor's script, or a person with a text
editor.

## 4. What a regulated document's form is required to do

Before describing the mechanism, it is worth being concrete about what is actually being
governed, because "document formatting" sounds like a matter of taste and this is not one.

### The document families are real and specific

The platform's print-and-document token set covers a set of named document families, and
they are not generic categories invented for tidiness. They are the real kinds of document the work
produces.

A **preliminary prospectus** prepared under the Canadian securities rules for prospectus
form. A **statutory year-end financial statement set**, prepared in the compilation register
a Canadian accountant issues under a Notice to Reader — portrait, symmetric margins, pure
black on white, because that is what the register looks like and departing from it signals
something the document does not mean. A **projection and proforma reporting layout**, which
is a deliberate sibling of the statutory set rather than the same thing: landscape, wide
multi-period tables, a different density and a different tone, because a projection is not
a statutory statement and should not be dressed as one. A **subscription agreement** in two
variants that share a recipe and differ in their schedules. An **engagement-letter suite**
with its memorandum of understanding and lettered schedules. Two **Mexican trust-vehicle
instruments** — a trust deed and an offering document for a listed property trust, drafted
in Spanish under civil-law notarial convention, governed by that country's income-tax and
securities statutes and its securities regulator's registry. A **print-safe corporate
relationship diagram** for the ownership chart such an offering document carries. And an
**interactive binder-navigation layer** for assembled document sets.

Two of those families are worth dwelling on together, because their relationship is the
whole argument in miniature. The Canadian prospectus family and the Mexican offering
family do the same job in two jurisdictions. They are siblings and they are deliberately
not the same: different language, different section taxonomy, no running header on one,
noticeably narrower side margins on one because a fixed-width ownership diagram sets them,
a different body type size matched to its companion trust deed. A single "prospectus
template" covering both would be wrong in both. Five hundred separately hand-built
documents would drift. What is wanted is a shared base and a named, deliberate, written
list of the differences — which is precisely what a semantic tier is.

### The shared base is genuinely shared

Underneath those families sits a primitive layer they all draw from, and the sharing is
real rather than nominal.

The **rule-weight ladder** is four steps — a hairline, a light rule, a standard rule, and
an emphasis rule — and it is identical across every legal and financial-statement family.
A hairline draws the border of a key-terms table, the line under a running header, and a
statutory subtotal. A standard rule draws a form cell, a signature line, and the rule above
a grand total. Two families extend the ladder rather than redefining it: a prospectus
data-table total row takes a doubled rule heavier than the ladder's top step, and an
engagement-suite form note takes a heavier accent bar still. The extension is recorded as
an extension. It is not a fifth private ladder.

The **typography rule** is one sentence and it is a real drafting protection: every
document family pairs a serif reading face for body and heading text with a *different*
sans face reserved for form-fill zones. A blank line a person is meant to write on should
never be mistaken for printed text they are meant to rely on. That is not a preference.
That is the difference between a subscriber filling in a blank and a subscriber believing
a term was already agreed.

The **page geometry** is per family and real: bound margins wider on the binding edge, a
reduced top margin on a cover page, a landscape page for the wide projection tables. These
are production values measured from documents that were actually produced, not defaults
carried in from a template.

## 5. How a document becomes a token contract

The structural values above — margins, rule weights, type sizes — are the easy half. They
are measurements, and a design system has always known how to hold a measurement. The
harder and more interesting half is the part that has no number.

### One shared base and five named differences

Alongside the concrete per-document families, the token set carries a cross-cutting
register for legal drafting conventions. Its structure is one shared base plus five
per-category variants: a commercial agreement, a constitutional agreement, a schedule or
exhibit, a letter, and a preliminary instrument such as a memorandum of understanding or a
term sheet.

What it governs is heading form, numbering, and cross-reference grammar — the three things
a precedent bank transmits by accident. Each cell in the register is marked with how firmly
it binds: some rules never vary, some are the strong default drawn from the weight of filed
precedent, and some are an accepted house alternative where genuine practice differs. That
grading is itself the useful part. It distinguishes "this is how it is done" from "this is
how we have chosen to do it," which a style memorandum almost never does.

The content is specific. A commercial agreement takes a flat numbered heading — the bare
number, a bold title-case title, a closing period, left-aligned, not capitals. It does not
put the word "Section" in front of the number; putting it there is the house alternative,
not the default. Its internal cross-references are capitalised and its references to
outside instruments are not, so that a reference to a clause in this agreement is visibly a
different kind of thing from a reference to a rule in a securities instrument. A
constitutional agreement — a shareholders' agreement, a partnership agreement, a
constating document — uses a centred article line in capitals with a title-case sub-level
beneath it, and the two levels are always distinguishable by case; that one is a rule that
never varies. A schedule's own label is its heading, and whichever word the document chose
— schedule, exhibit, or annex — it holds that word throughout, without exception. A letter
matches its cross-reference word to whatever its divisions are actually called: sections if
it has headed sections, paragraphs if it has bare numbered paragraphs.

Then there are the rules that apply across the whole family, and these are the ones a style
memorandum tends to leave out because nobody thinks to write them down. Never a lone
sub-clause with no sibling — a section with only one block stays bare under its heading
rather than acquiring a decimal it does not need. Subdivide only where two or more parallel
provisions actually exist; uniform depth throughout a document is not required and forcing
it produces the orphan the previous rule prohibits. Keep the "of such-and-such instrument"
qualifier on every external reference, so a clause numbered the same inside and outside the
document cannot be confused. An unnumbered lead-in paragraph under a subdivided section is
legitimate and is cited as the whole section. Do not formally define the words "Section" and
"Article" in the definitions clause; capitalise them and carry a short construction clause
instead. And one rule marked as binding absolutely across the entire family, which is
notable precisely because it is so small: never two internal cross-reference pointers in
different case within the same document.

### The rule that exists because it was broken

One rule in that register deserves its own paragraph, because of how it got there.

The token set also carries a number-display rule for financial reporting output —
decimal precision, whether to round or truncate, how to scale a per-unit figure against an
aggregate. It is a sensible rule for a financial report, where consistent presentation of
figures is the whole point of the register.

It was applied to a document that was not a financial report. It was a corporate
resolution: an instrument whose operative content includes a figure the parties are
agreeing upon. The rule did exactly what it was written to do, and in doing so it changed
that figure — in every place the figure appeared. Nobody decided to change a number. The
renderer changed it, correctly, according to a rule written for a different kind of
document.

The answer was not a reminder to be careful. The answer was a new rule, binding across all
five legal variants without exception: every operative figure in a legal instrument — a
stated price, a consideration amount, a share count, any number the document resolves upon
— renders exactly as it appears in the source, with no rounding, no truncation, and no
rescaling applied by the machinery. The scope of the financial-reporting rule was narrowed
in the same change, so that it can no longer reach a signable instrument at all. That
correction is in the published token file, with its reasoning, where anyone can read it.

This is what it looks like when a rule is data rather than prose. The defect was a rule
applied outside its scope; the fix was a change to the scope, recorded once, in the place
the machinery actually reads. In a style memorandum the same fix is a sentence somebody
must remember.

### What is honestly not finished

Most of the values in the legal drafting register are placeholders. The structure is
decided — the shared base, the five variants, the qualitative lock table — and the real
measured values for the categories are being delivered a category at a time, commercial
agreements first, from a reference implementation. The token file says so on its face. The
concrete per-document families beside it — the subscription agreement, the prospectus, the
engagement suite — already ship real production stylesheets; the cross-cutting drafting
register does not yet.

## 6. When the rule itself is broken

A rule earns its keep when it can point at a real failure. Until then it is a plausible
opinion, and a platform arguing for governed rules ought to say so about its own.

The failure described above is the strongest version of that test we can offer within this
subject: a real rule, correctly written for its own domain, causing a real problem by
being applied outside it. But there is a second and more uncomfortable version, and
leaving it out would make this paper less honest than the token file it describes.

The platform's published rules include a vocabulary register — a list of terms retired from
public writing, each with the reason and each with a stated plain-language substitute. One
entry on that list is a word that carries a completely ordinary meaning in finance,
describing growth that accumulates on itself, and a second, unrelated meaning in this
platform's own technical usage. The rule does not ban the word outright. It requires that
where the technical sense is meant, a plain-language translation precede it on first use,
so that a reader arriving with the financial meaning in mind is not silently handed the
other one. That is a good rule, written for exactly the reader this corpus is written for,
and it is published as data alongside the colours and the margins.

Here is the honest limit. Publishing a rule as data is not the same as enforcing it. The
platform's structural token values have a real, automatic check: a gate in the repository
regenerates the derived token files whenever a source file changes, stages the result into
the same change, and refuses the change outright if regeneration fails — so the exported
file and its sources cannot silently drift apart. The qualitative rules sitting in the same
token set have no equivalent. They are strings, not measurements. Nothing today reads a
finished document and reports that its cross-references are inconsistently cased, or that a
retired term appeared without its translation. That check is intended and it is not built,
and until it is, conformance rests on a person reading carefully — which is the mechanism
this paper opened by criticising.

We would rather state that plainly than let the preceding sections imply a completeness
that does not exist. The structure is right, the structural half is enforced, and the
qualitative half is currently a well-written rulebook in a filing cabinet that happens to
be machine-readable.

## 7. What this changes for the reader

The first change is what "consistent" can mean. Today a firm claiming its documents follow
a consistent house standard is asking to be taken at its word, because the standard exists
as prose and the documents exist separately. Under this arrangement the standard exists as
a file. Two documents of the same family either drew on the same entries or they did not,
and that is a question with an answer rather than an impression.

The second change is for whoever examines the documents later. An auditor — an independent
professional who examines a business's records and states whether they can be relied upon —
or a buyer's counsel reading a stack of agreements in diligence, can be told not merely
"these follow our house style" but "these were produced from this version of this rule set,
and here is the rule set." The rules are versioned, so a document produced two years ago
can be assessed against the rules as they stood two years ago rather than against today's.
That is a materially different conversation from producing four documents and inviting
someone to notice they match.

The third change is about correcting a mistake. When a drafting convention turns out to be
wrong — as the number-display scoping was wrong — the fix is a change to one entry, with a
written reason attached, and it applies to everything produced afterward. It is not a
circulated note that some people read.

The trade-offs are real and belong in the same paragraph. Encoding a convention requires
first deciding what it is, and legal drafting practice genuinely differs between
jurisdictions and between good firms; the register handles this by marking what is settled
and what is a house choice, but marking a disagreement is not resolving it. A rule held as
data is enforced only where a machine actually checks it, and today half of this rule set
has no such check. Placeholder values are placeholders. And there is a failure mode
specific to this approach: a rule correct in one domain, applied by machinery to a document
in another, does the wrong thing faster and more uniformly than a careless person would. We
have seen that happen once, which is why the scope of a rule is now treated as part of the
rule rather than as context a reader supplies.

## 8. An open invitation

This paper states a position we hold and a set of problems we cannot settle from inside one
firm.

To researchers in legal informatics and computational contract drafting: the register
described in Section 5 grades each convention by how firmly it binds — never varies, strong
default, accepted alternative. We derived those gradings from the weight of filed precedent
and from standard drafting references, which is a defensible method and not a rigorous one.
Whether the gradings survive a proper corpus study of filed instruments, and whether the
three-way grading is even the right shape for this kind of rule, is a question we would
rather have answered than assumed.

To regulatory-technology researchers: the structured-filing requirements now in force for
listed issuers in several jurisdictions govern the tagging of *figures*. The register in
this paper governs the *structure* — headings, numbering, references. Whether these two
should eventually be one mechanism, so that a document's structural grammar and its tagged
content are governed together rather than by unrelated tools, is an open design question
with real consequences for anyone who has to produce both.

To practitioners of comparative drafting practice: this register has been tested against
two jurisdictions in depth and touches a third. Whether a shared base plus per-category
differences holds up across jurisdictions whose formatting requirements diverge more
sharply than these — or whether it quietly becomes a base that is shared by nobody and five
variants that are really five separate systems — is the question we would most like a
specialist to break.

And to anyone who has built a conformance check for qualitative drafting rules at scale: we
would be glad to learn what actually works. We know how to check a margin. We do not yet
have a reliable way to check, across a long document, that internal cross-references are
consistently cased and that every retired term arrived with its translation, without
producing so many false reports that people stop reading them.

## 9. Conclusion

The required shape of a regulated document should be governed, versioned data, decided once
and reused — not re-decided document by document out of whichever previous document was
nearest to hand. A prospectus, a statutory statement set, an agreement and a schedule each
have a real form with real consequences, and that form is exactly the kind of thing a
design system has spent a decade learning to hold as named entries in a file rather than as
habits in a precedent bank.

The platform's print-and-document token set is built that way: a shared base of geometry,
rule weights and type pairings; a set of real document families selecting from it; and one
cross-cutting legal drafting register of a single shared base and five named variants,
covering heading form, numbering, and cross-reference grammar. Most of that register's
values are still placeholders, and the qualitative rules in it have no automatic check
today, which is why a rule in it was able to be applied outside its scope and alter an
operative figure before anyone noticed. We publish that rather than omit it, because a
paper arguing that governed rules are better than remembered ones has no business implying
its own are already finished.

## References

Design Tokens Community Group. *Design Tokens Format Module.* World Wide Web Consortium
Community Group. [https://tr.designtokens.org/format/](https://tr.designtokens.org/format/)

British Columbia Securities Commission. *National Instrument 51-102 — Continuous Disclosure
Obligations.*
[https://www.bcsc.bc.ca/securities-law/law-and-policy/instruments-and-policies/5-ongoing-requirements-for-issuers-insiders/current/51-102](https://www.bcsc.bc.ca/securities-law/law-and-policy/instruments-and-policies/5-ongoing-requirements-for-issuers-insiders/current/51-102)

British Columbia Securities Commission. *Continuous Disclosure Obligations — overview.*
[https://www.bcsc.bc.ca/industry/issuer-regulation/continuous-disclosure-obligations](https://www.bcsc.bc.ca/industry/issuer-regulation/continuous-disclosure-obligations)

Canadian Securities Administrators. *National Policy 51-201 — Disclosure Standards for
Forward-Looking Information.*

European Securities and Markets Authority. *European Single Electronic Format (ESEF) —
inline XBRL requirements for annual financial reports.*
[https://www.esma.europa.eu/policy-activities/corporate-disclosure/european-single-electronic-format](https://www.esma.europa.eu/policy-activities/corporate-disclosure/european-single-electronic-format)

United States Securities and Exchange Commission. *Rule 17a-4(f) — Records to be Preserved
by Certain Exchange Members, Brokers and Dealers.*
[https://www.ecfr.gov/current/title-17/chapter-II/part-240/section-240.17a-4](https://www.ecfr.gov/current/title-17/chapter-II/part-240/section-240.17a-4)

## Contributors

Prepared by Woodfine Management Corp.

## How this paper was produced

This paper is grounded in the preparing staff's own development and operating work, and in their standing engagement with the designers, software engineers, architects, engineers, and legal and accounting advisers the business works with. It was drafted and edited with AI assistance under editorial direction, and the analysis and conclusions are the author's own.

## Disclosures

Woodfine Capital Projects Inc. ("Woodfine") is the author of record. PointSav Digital
Systems, which builds the platform described, is currently a trade name of Woodfine,
planned to become a wholly-owned Woodfine subsidiary upon incorporation; PointSav does not
itself offer, sell, or solicit any security. The token set described in this paper is our
own work, so this paper argues for an approach we have a commercial interest in. This work
was funded internally; no external research funding was received. The descriptions of
drafting conventions, filing requirements, and disclosure obligations are given in general
terms to explain a design and are not legal advice on any party's obligations under any
instrument or in any jurisdiction. This paper's content is provided for engineering,
operational, and research purposes and does not constitute investment advice or a
solicitation to invest in any Woodfine direct-hold solution. Some statements above describe
planned or intended future work; in particular, the conformance check described in Section
6 as intended is not built, and most values in the drafting register described in Section 5
are provisional. Language such as "planned," "intended," "targeted," "may," and "expected"
marks this forward-looking content, which is subject to change and does not constitute a
commitment regarding future performance.

## Data and reproducibility

Everything this paper reports about the token set was read directly from the published
files in preparing it, rather than from a summary. The print-and-document token set is
published as ordinary text files in a public repository under a permissive licence, in the
standard interchange format described in Section 3, which means a reader can open them
without any of our software. The named document families, the four-step rule weight ladder
and its two extensions, the reading-face and form-fill-face pairing rule, the shared base
and five variants of the legal drafting register, its per-category heading and
cross-reference rules, the family-wide drafting rules, and the numeric-precision rule
described in Section 5 are all present in those files with their own written descriptions
attached. The correction described in Section 5 — the narrowing of a number-display rule so
that it can no longer reach a signable instrument — is recorded in the file itself,
including its reasoning; the document involved, and the figure it affected, are not
described here and are not in the published file either. The automatic regeneration gate
described in Section 6 is a short script in the same public repository. The document
families' real production stylesheets are referenced from the token entries that describe
them. No independent party has audited this token set, reviewed these drafting conventions,
or verified these claims.

PointSav Digital Systems™ MCorp™, and Woodfine Capital Projects™ are trademarks of Woodfine
Capital Projects Inc.
