---
schema: journal-v2
slug: content-as-governed-tokens
title: "The Same Mechanism That Governs a Color Can Govern a Sentence"
subtitle: "Encoding banned vocabulary, audience voice, and section length as versioned design tokens"
site: design.pointsav.com
imprint: PDS-2026-10
thesis: "Encoding vocabulary, register, and structural rules as versioned, co-signed design-token data — rather than as prose in a style guide — makes a voice violation something a cross-check can find, but only if something actually runs the check; the data alone does not enforce itself."
abstract: |
  A design-token schema is usually described as a way to govern visual properties — color,
  spacing, type. This paper describes the same mechanism already governing something else in
  this workspace: editorial voice. Two structured token files retire specific vocabulary by
  name, with a stated reason and suggested replacements, for two different audiences; separate
  schema tokens govern a document's required section order, its word-count range, and its
  audience-appropriate voice profile. We found a real test of whether this actually works: a
  workspace protocol file is currently named, and internally uses vocabulary, that directly
  violates this workspace's own banned-vocabulary tokens — a genuine self-contradiction that has
  been on record as an open item since 2026-07-15 and remains unresolved as of this paper. That
  finding is the honest core of this paper's contribution: encoding a voice rule as data makes it
  possible to check against, but a rule sitting in a token file that nothing actually runs a
  check against is not meaningfully different from a rule sitting in a style guide nobody
  rereads. The mechanism is real and useful; the enforcement gap it currently has is just as
  real, and this paper reports both rather than only the part that reflects well on the system.
state: draft
version: "1.0.0"
published:
updated: "2026-09-15"
doi:
license: CC-BY-4.0
cites:
  - dtcg-w3c
  - json-ld-schema-org
  - spdx-license-list
  - keep-a-changelog
  - cff-spec
draws_from: []
contributors:
  - name: Peter M. Woodfine
    roles: [Founding Contributor]
  - name: Jennifer M. Woodfine
    roles: [Founding Contributor]
  - name: Mathew Woodfine
    roles: [Founding Contributor]
keywords:
  - design tokens
  - editorial voice
  - content governance
  - controlled vocabulary
  - structured metadata
---

## 1. The question

A design-token schema is normally scoped to the visual layer: a color primitive, a spacing
scale, a type ramp, versioned and governed so that a change to any of them is a deliberate,
recorded act rather than one designer's local override. Editorial voice — which words a company
allows itself to use, how differently it should write for a financial audience versus an
internal engineering one, how long an article is allowed to run before it should be split —
is usually governed the opposite way: a style guide, written in prose, that an editor is
expected to remember and re-apply by judgment each time.

This workspace already blurs that line in one direction: two of its own content-schema token
files retire specific vocabulary terms by name, each with a stated reason and a set of suggested
replacements, in the same structured, versioned YAML format used for a color token. The question
this paper asks is whether treating voice as data this way actually delivers what the visual-
token version of the same mechanism delivers — the ability to check a real document against a
rule mechanically, rather than trusting an editor's memory of a style guide they may not have
reread recently.

We do not answer this in the abstract. We answer it by describing what a real self-check against
this workspace's own governed vocabulary data actually found, and being direct about what it
found: the mechanism works as a source of truth, but it is not yet wired to anything that runs
automatically, and a real violation sat unresolved in this workspace's own files for months as a
direct result.

## 2. What we found

**Two governed vocabulary files retire specific terms as structured data, not prose advice, and
this is real, existing infrastructure, not a proposal.** One file retires 16 terms from
corporate- and projects-wiki content; a second retires 27 terms from documentation-wiki content
(16 of which overlap with the first — the same term can be banned for one audience and, in a
handful of cases, explicitly permitted with a caveat for another). Each entry carries a plain-
language reason the term is retired and a list of replacement phrases, rather than a bare
"don't use this" instruction.

**We found a real, currently-unresolved self-violation of this exact data, inside this
workspace's own files.** A protocol file governing optical-presentation rules is literally
titled "Optical Preservation & Sovereign Presentation Protocol" and repeatedly refers to a
"PointSav Sovereign Engine" throughout its body — while the banned-vocabulary tokens explicitly
retire the term "sovereign" for precisely this reason: internally the word is used to mean
"operator-controlled," but a financial audience reads "sovereign" as "government-backed," and
the two meanings conflict in exactly the way that makes a retired-vocabulary rule necessary in
the first place. This is not a hypothetical example constructed for this paper — it is a real,
live inconsistency, flagged internally as an open item since 2026-07-15, still unresolved as of
this paper being written.

**The rule existed as governed data well before the violation was ever flagged, which is the
finding that actually matters.** The banned-vocabulary token retiring "sovereign" is not a new
addition made in response to finding the violation — the rule predates the flag by months. That
means the token data alone, sitting correctly written in its file, did not prevent or surface the
violation on its own. It took a direct human-and-AI review, cross-reading the protocol file
against the vocabulary tokens, to notice the two disagreed. No automated process made that
comparison first.

**Structural rules beyond vocabulary are already governed the same way, with the same open
question about enforcement.** A GUIDE article's required section order and its word-count range
are schema-token fields, not conventions an editor holds in their head; a document's audience-
appropriate voice register is a named, enumerated field (one of three fixed profiles) rather than
a paragraph of prose describing "write differently for different readers." A newly-added
cross-reference field connecting JOURNAL papers back to the wiki articles they draw from — added
as a content-schema token this same session — follows the identical pattern: a relationship that
used to be implicit, made explicit as queryable, versioned data.

## 3. How we built and verified it

Each vocabulary-retirement entry is a structured record — the retired term, a reason, and a list
of replacements — rather than free text, which is what makes it something a tool could check
against mechanically, in principle, even though no such tool exists yet for it. The two files are
scoped by audience rather than merged into one list, because the two audiences do not always
agree: the same word can be correctly retired for one wiki and correctly permitted, with a
documented exception, for another.

The structural tokens follow the same shape: a document schema's required-section order, its
word-count range, and its audience-voice-profile enumeration are all named fields in a versioned
schema file, changeable only through the same governed-token-change process (including the
human co-sign requirement) that governs a visual token. This is the same governance path
described in this paper's companion piece on regulated-document tokens, applied here to
linguistic and structural rules instead of print and layout rules.

We verified the self-violation directly rather than taking the earlier internal flag at face
value: reading the protocol file's own title and body text, and separately reading both
vocabulary-retirement files' entries for "sovereign," confirmed the conflict is real, specific,
and exactly the kind the retirement rule's own stated reason describes — not a stretch or a
different sense of the word carved out by either file's own exception language.

We did not build, and are direct about not having built, any automated process that reads a
changed or new file and checks its text against either vocabulary file or the structural schema
tokens. What exists is the governed data itself, verified as internally consistent in its own
terms; what does not yet exist is anything that runs the comparison this paper's own finding in
§2 had to perform by hand.

## 4. What it changes

For an editor working on a real document, the practical change so far is narrower than "voice
mistakes get caught automatically" — it is closer to "there is now one specific, versioned file
to check a word against, instead of a memory of a style conversation from months ago." That is a
real improvement over pure convention, but this paper's own central finding shows it is not yet
the same thing as automatic enforcement: the file existing correctly did not, by itself, prevent
or catch a real violation elsewhere in the same workspace.

It changes what a future fix actually requires, which is now a scoped, specific engineering
task rather than an open-ended "improve our style discipline" goal: something that reads new or
changed content and checks it against the two vocabulary files and the structural schema tokens
already exists as the missing piece, not as a redesign of how voice rules are recorded in the
first place. The data model this paper describes does not need to change for that gap to close.

It also changes the audit trail for a voice or structure change specifically. Because a change
to either vocabulary file or either schema file goes through the same governed-token-change
process as a color token, there is now a recorded answer to "who approved retiring this term, or
changing this section order, and when" — even though, as §2 shows, that governance covers
changes to the rule itself, not yet enforcement of the rule against everything else in the
workspace that should already be following it.

## 5. Where this could be wrong

**Encoding a rule as data does not enforce the rule — this paper's own central finding is direct
proof of that, not a hedge added out of caution.** The sovereign-vocabulary self-violation sat
unresolved for months with the correct rule already written down in governed, versioned form.
Any claim that structuring voice as tokens "solves" editorial consistency on its own would be
contradicted by this paper's own evidence.

**The fixed three-profile voice enumeration (corporate, documentation, projects) may not
generalize cleanly to a genuinely new audience or register later.** Adding a fourth profile is a
schema change, with its own governance step, not a casual addition — this is a real, if modest,
rigidity the enumerated-token approach accepts in exchange for the checkability a free-text voice
description would not offer.

**Vocabulary exceptions still require human judgment the data cannot make by itself.** Both
vocabulary files carve out legitimate uses of otherwise-retired terms (for instance, "sovereign"
in its ordinary political or financial sense) — a simple string match against the banned-term
list cannot distinguish a correct use from a violation on its own; a human, or a more capable
check than string matching, still has to apply the exception.

**This mechanism governs vocabulary and structure, not sentence-level register.** It does not
detect hedging, jargon density, or tone at the level real editorial judgment currently handles —
extending it that far, if ever warranted, is a materially different and harder problem than the
lookup-table mechanism described here.

## 6. Conclusion

The question was whether the token mechanism that governs a color or a spacing value can do the
same job for editorial voice — vocabulary, audience register, structural length — and whether
doing so actually changes anything in practice. It does encode real rules as real, versioned,
co-signed data, and that data is more specific and more checkable than a prose style guide would
be. What it does not yet do, proven by a real, currently-unresolved self-violation found in this
workspace's own files during the writing of this paper, is enforce itself. The honest answer to
"does content-as-tokens work" is: the data model works; the missing piece is something that
actually reads that data and checks it against everything else, and that piece does not exist
yet.

---

## 7. Claims and what would count against them

**Claim.** Structuring editorial vocabulary, audience-voice register, and document-length rules
as versioned, co-signed design-token data — rather than as prose style-guide advice — makes
those rules more specific and more checkable in principle, but does not by itself prevent a real
violation without something that actively runs the check.

**This claim would be wrong if:** a full sweep of this workspace's own governance files against
the vocabulary tokens found zero violations beyond the one already identified — which would
suggest the sovereign case was an isolated slip rather than evidence of a systemic gap between
"rule exists as data" and "rule is actually checked."

**What this claim does not say.** It does not say the vocabulary/schema token files are
incorrectly designed, does not say a full enforcement tool would be trivial to build, and does
not claim every workspace file has been audited against these rules — only the one instance
this paper directly verified.

| Test | What it checks | Status |
|---|---|---|
| Full-corpus vocabulary cross-check | Whether other governance/protocol files also violate the retired-vocabulary tokens beyond the one found | Designed; not yet run beyond the single confirmed instance |
| Build-time/CI vocabulary lint | Whether an automated check against the vocabulary and schema tokens would have caught the sovereign violation before it persisted for months | Not yet built or run |
| Exception-carve-out precision test | Whether a simple string-match approach would false-positive on the documented legitimate exceptions (e.g., "sovereign debt") | Not yet tested |
| Cross-reference field utility (`journal_refs`) | Whether the newly-added bidirectional field is actually populated and used by any real tool | Schema landed this session; population explicitly deferred, not yet exercised |

## References

Design Tokens Community Group (DTCG). 2026. *W3C Design Tokens Format Module.*
https://tr.designtokens.org/format/

JSON-LD and Schema.org. *Semantic web data format for structured content markup.*
https://json-ld.org/

Linux Foundation. *SPDX License List — standardised licence identifier registry.*
https://spdx.org/licenses/

*Keep a Changelog 1.1.0 — changelog format convention.* https://keepachangelog.com/en/1.1.0/

*Citation File Format (CFF) — Specification.* https://citation-file-format.github.io/

---

## Contributors

Peter M. Woodfine, Jennifer M. Woodfine, and Mathew Woodfine are credited as founding
contributors to PointSav Digital Systems's design-systems research programme.

## How this paper was produced

This paper was prepared with AI assistance under human editorial direction; all analytical
claims and conclusions are the responsibility of the named institutional author.

## Disclosures

The token files, schema fields, and the self-violation described are this workspace's own,
currently-real content. The self-violation named in §2 was unresolved at the time of writing and
is reported as such — this paper does not claim the issue has been fixed. Any reference to a
future enforcement tool is stated in planned or intended terms only, in accordance with
continuous-disclosure practice under NI 51-102 and CSA National Policy 51-201.

## Data and reproducibility

The vocabulary-retirement files and content-schema token files described are versioned YAML in
this workspace's design-system repository; the self-violation finding is independently
reproducible by reading the named protocol file's title and body against either vocabulary
file's "sovereign" entry directly.
