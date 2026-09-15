---
schema: journal-v2
slug: token-contracts-for-regulated-disclosure
title: "Token Contracts for Regulated Disclosure Documents"
subtitle: "Encoding a compliance document's print and structural constraints as versioned, co-signed design tokens"
site: design.pointsav.com
imprint: PDS-2026-08
thesis: "A design-token schema can encode a regulated document's structural constraints — table alignment, mandatory notices, print geometry — as governed data, turning 'did we follow the format' into a schema check instead of an editor's manual re-read."
abstract: |
  Regulated financial documents carry structural constraints that are usually enforced by
  convention rather than by anything a machine can check: a multi-year statement's columns must
  align table to table, a forward-looking-statements notice must appear, a print layout must
  survive pagination without splitting a total row from its figures. This paper describes a
  design-token contract — a versioned, human-co-signed schema of CSS classes and page rules,
  not prose instructions — that encodes those constraints as data. We built one real component
  under this contract, a compliance financial-report layout, and validated its structural rules
  hold across two independent print-rendering engines. We also found the contract already
  generalizes in practice: a second, structurally distinct financial-statement format was built
  as a sibling under the same pattern language, not as a one-off. The mechanism does not verify
  a document's numbers are correct — only that its shape, notices, and accessibility properties
  are. That distinction, and how far the contract's governance already exceeds what any
  regulator currently requires of a document's presentation layer specifically, is this paper's
  main finding.
state: draft
version: "1.0.0"
published:
updated: "2026-09-15"
doi:
license: CC-BY-4.0
cites:
  - dtcg-w3c
  - w3c-aria-1-2
  - ixbrl-esef
  - sec-17a-4-f
  - eidas-qualified-preservation
  - etsi-ts-119-511
  - etsi-en-319-401
  - ni-51-102
  - np-51-201
  - bcsc-continuous-disclosure
  - mondaq-ni-51-102-summary
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
  - regulated disclosure
  - print CSS
  - compliance documents
  - accessibility
---

## 1. The question

A compliance financial document — a proforma, an income statement, a book valuation — has
structural requirements that have nothing to do with the numbers in it: the columns of a
multi-year statement must line up from one table to the next, a total row must read as a total
wherever it lands on the printed page, a forward-looking-statements notice must appear, and the
whole thing must survive being printed or exported to PDF without a table splitting across a
page break in a way that separates a figure from its label. Today, whether a new statement
actually satisfies those requirements is usually established the way most editorial standards
are: an editor compares the new document against the last one that was approved and re-checks
it by eye.

That works until the requirement itself needs to change, or until two people producing the same
document family drift apart in how carefully they check it. A design-token schema — the same
mechanism this workspace already uses to govern a button's color or a heading's type size — can
instead encode these structural requirements as versioned data: a semantic class for "this row
is a total," a page rule for "this table must not split," a metadata field for "this design
must clear WCAG 2.2 AA." Once the requirement is data rather than convention, whether a document
satisfies it becomes something a schema can check, not something an editor has to remember to
check.

The question this paper asks is whether that mechanism actually works for a real regulated
document, not just for ordinary interface chrome — and whether it generalizes across more than
one document in the same family, or only describes the first one anyone happened to build.
We answer both by describing a real component built under exactly this contract, and a second,
independently-built sibling that adopted the same pattern for a structurally different
statement type.

Two adjacent regulatory efforts are relevant context, not something this paper claims to
replace. The EU's ESEF regime already forces listed issuers to tag their financial statements'
actual data in structured, machine-readable form (inline XBRL) rather than free-form PDF, and
frameworks like the US SEC's electronic-recordkeeping rule and the EU's eIDAS qualified-
preservation standards already specify how a regulated record must be preserved over time.
None of these regimes reach the presentation layer specifically — how the document is laid out,
how it paginates, whether its accessibility properties survive print. That is the gap a design-
token contract can fill, and it is a narrower, more mechanical claim than "compliance," which
this paper is careful not to overstate.

## 2. What we found

**We built one real component under this contract, and its structural rules are enforced as
CSS classes and page rules, not as instructions written for a human to follow.** The component —
a compliance financial-report layout — expresses "this is a total row," "this is a section
banner," and "this column is the label column" as dedicated CSS classes rather than as ad hoc
inline styling, and expresses "do not split this table across a page" and "keep this heading
with the row that follows it" as `break-inside`/`break-after` rules rather than as a note in a
style guide telling an author to watch for it.

**The rules hold across two independent rendering engines, not just the one we happened to test
first.** The component was validated in Chromium's print-to-PDF path and, separately, in
WeasyPrint — a genuinely different rendering engine with a different implementation of CSS
print behavior. Both preserve the cross-table column alignment and the semantic-row fills. One
real, documented gap survived that comparison rather than being hidden: WeasyPrint does not
execute JavaScript, so a line-number gutter injected by script is present in Chromium's output
and absent in WeasyPrint's — a genuine, bounded limitation, not a claim of universal engine
parity.

**The contract already generalizes in practice, not just in theory.** A second, structurally
distinct compliance format — a year-end financial statement, portrait rather than landscape,
denser in narrative and lighter in period-column count — was built as a deliberate sibling under
the same pattern language: the same semantic-row classes, the same print-engine cautions, a
different geometry and density where the document genuinely differs. Two real recipes exist
under one shared vocabulary, not one recipe and a hope that it would generalize.

**The contract's governance already exceeds anything a regulator currently asks of a document's
presentation layer.** Every structural change to this token contract requires a named human
co-sign recorded in the change's own frontmatter before it can be committed — a real, enforced
mechanism, not a proposed one. Regimes like SEC Rule 17a-4(f) and the EU's eIDAS preservation
standards specify rigorous requirements for how a regulated record's data must be preserved and
verified over time; none of them require a named sign-off on a change to how the document is
laid out on the page. This workspace already applies that discipline to presentation, one level
above where any of these regimes currently look.

## 3. How we built and verified it

The contract has three real parts. First, a DTCG-format token vocabulary — the same open,
W3C-track token format this design system uses for every other visual property — defines the
semantic classes (`tr.total`, `tr.subtotal`, `tr.section-banner`, `td.lbl`) and the print
mechanics (`table-layout:fixed` restated inside `@media print`, forced page-break utility
classes) as named, versioned values rather than one-off CSS an author reinvents per document.

Second, an accessibility contract travels with the component as metadata rather than as
separate documentation an implementer might skip: explicit WCAG 2.2 AA and print-contrast
targets, and a "no color alone" rule — every emphasized row (total, subtotal, section banner)
carries a non-color signal (border weight, font weight, case) so the distinction survives both
grayscale printing and color-vision deficiency, not just a themed screen render.

Third, we tested the specific cross-engine gotcha that makes or breaks this kind of contract:
some print engines re-resolve table layout at print time and silently revert a `table-layout:
fixed` rule set on screen, which would break the exact column alignment the contract exists to
guarantee. Restating the rule inside `@media print` — rather than assuming a screen rule
survives into print unchanged — was verified necessary, not precautionary, by testing without
the restatement first and observing the alignment actually break in at least one engine before
adding it back.

We did not build an automated conformance checker that scans a finished document and confirms
it satisfies every rule in the contract. What exists today is the token/class vocabulary itself,
validated by direct testing of the two real components built under it — a real foundation for
such a checker, not the checker itself.

## 4. What it changes

For a team producing a new regulated statement, the practical change is what "does this follow
the format" actually means. Under the convention model, it means an editor holds the new
document up against the last approved one and re-checks it by eye, a check that scales linearly
with editor attention and drifts differently depending on who is doing the checking. Under a
token contract, a new statement inherits the structural rules by construction — the total-row
fill, the page-break behavior, the label-column width — because it is authored against the same
class vocabulary, not re-derived by an editor per document.

It also changes what "extending the family" costs. Building the second, structurally distinct
statement format did not require reinventing print mechanics, accessibility rules, or semantic-
row conventions from zero — those already existed as shared, versioned tokens; the work that
remained was the genuinely new part, the different page geometry and density that statement
type actually needed. A design-token contract turns "we need a new regulated-document type" into
mostly a data-population exercise plus a bounded design delta, not a full redesign each time.

Most directly, it changes who is accountable for a structural change and when. Because every
edit to the contract itself requires a recorded human co-sign, there is a durable, checkable
answer to "who approved this layout change and on what date" that does not depend on anyone's
memory of a conversation — closer to the kind of accountability regimes like eIDAS's
preservation-policy requirements already demand of a record's data integrity, applied here to
the record's presentation instead.

## 5. Where this could be wrong

**The contract verifies form, not substance.** A document can satisfy every rule in this token
contract — correct column alignment, the mandatory notice present, print-safe fills — and still
contain a wrong number. This mechanism is not, and does not claim to be, a substitute for the
data-tagging and audit regimes (like ESEF's iXBRL mandate) that actually govern a disclosure
document's underlying figures.

**"Cross-engine" means two engines, not every engine.** Chromium's print-to-PDF path and
WeasyPrint are two real, independently-implemented rendering engines, and testing both is a
genuinely stronger claim than testing one — but it is not a claim that the contract behaves
identically in every browser or PDF tool a reader might use.

**The co-sign requirement is workspace governance, not regulatory attestation.** It demonstrates
this workspace treats a structural change to a regulated document's presentation with real,
recorded seriousness. It is not, and should not be described as, compliance with any BCSC,
SEC, or EU disclosure requirement — none of which currently reach the presentation layer at all,
which is exactly the gap this paper describes, not a gap this paper claims to have closed on a
regulator's behalf.

**The contract has been tested on two sibling document types within one family** (compliance
financial statements), not on a genuinely different regulated-document category — a legal
instrument or a prospectus, for instance, where the structural constraints might not decompose
into the same semantic-row/page-rule vocabulary at all.

## 6. Conclusion

The question was whether a design-token contract can actually encode a regulated document's
structural requirements as machine-checkable data, and whether that mechanism generalizes past
the first document anyone happens to build under it. It does: a real compliance financial-report
component enforces its own structural rules as versioned classes and page rules rather than
editorial convention, those rules were validated across two independent rendering engines, and
a second, genuinely different statement type was built as a sibling under the same shared
vocabulary rather than from scratch. What the contract does not do — verify a document's actual
figures, or stand in for any regulator's own data-integrity requirements — is exactly the
boundary that makes its real claim, encoding presentation as governed data, an honest one
instead of an overreaching one.

---

## 7. Claims and what would count against them

**Claim.** A structural token contract for a regulated-document family reduces "does this
follow the format" from an editor's manual re-check to a schema-conformance property, and this
mechanism generalizes across more than one document type within the family without being
reinvented per document.

**This claim would be wrong if:** extending the contract to a third, structurally distinct
document within the same family required inventing new structural primitives rather than
reusing the existing token vocabulary — which would mean the "one recipe reused, not
reinvented" finding in §2 was an artifact of only two examples existing so far, not a real
property of the mechanism.

**What this claim does not say.** It does not say the contract verifies a document's factual
correctness, does not say it satisfies any specific regulator's presentation requirements
(none currently impose any), and does not say the mechanism has been tried outside the
compliance-financial-statement family.

| Test | What it checks | Status |
|---|---|---|
| Cross-engine print validation (Chromium, WeasyPrint) | Structural rules hold across two independently-implemented print engines | Tested and confirmed; one bounded limitation found (JS-dependent line numbers absent in WeasyPrint) |
| Sibling-format reuse (financial-report-layout → financial-statement-yearend) | Whether a second document type in the same family reuses the token vocabulary rather than reinventing it | Built and confirmed for one sibling pair |
| Third-family extension (a non-financial regulated document) | Whether the mechanism generalizes past the compliance-financial-statement family | Not yet attempted |
| Automated schema-conformance check against a finished document | Whether the contract can be verified mechanically rather than by direct component testing only | Not yet built |

## Appendix A — Token/class vocabulary referenced

| Class / rule | Encodes |
|---|---|
| `tr.total` / `tr.subtotal` / `tr.section-banner` | Structural row role, with a non-color signal on each |
| `td.lbl` / `th.lbl` | The one left-aligned label column in a wide table |
| `table.wide` + `table-layout:fixed` (restated in `@media print`) | Cross-table column alignment, including under print-engine re-resolution |
| `.page-break-before` / `.page-break-after` | Manual, opt-in forced pagination |
| `accessibility_targets` metadata (`wcag-2-2-aa`, `table-semantics-scope`, `print-contrast-exact`, `no-color-only-meaning`) | Accessibility contract carried as component metadata, not separate documentation |
| `master_cosign_required` | Governance: a named human sign-off recorded before a structural change to the contract lands |

## References

Design Tokens Community Group (DTCG). 2026. *W3C Design Tokens Format Module.*
https://tr.designtokens.org/format/

World Wide Web Consortium. 2026. *Accessible Rich Internet Applications (WAI-ARIA) 1.2 — W3C
Recommendation.* https://www.w3.org/TR/wai-aria-1.2/

European Securities and Markets Authority. *European Single Electronic Format (ESEF) —
inline-XBRL mandatory tagging for EU-listed issuers' annual financial reports.*
https://www.esma.europa.eu/policy-activities/corporate-disclosure/european-single-electronic-format

U.S. Securities and Exchange Commission. *Rule 17a-4(f) — Records to be Preserved by Certain
Exchange Members, Brokers and Dealers.* 17 C.F.R. § 240.17a-4.

European Commission. 2025. *Commission Implementing Regulation (EU) 2025/1946 — Qualified
electronic preservation services (eIDAS).*

ETSI TS 119 511. *Policy and security requirements for trust service providers providing
long-term preservation of digital signatures or general data using digital signature
techniques.*

ETSI EN 319 401 v3.2.1. *General Policy Requirements for Trust Service Providers.*

British Columbia Securities Commission. *National Instrument 51-102 — Continuous Disclosure
Obligations.*

Canadian Securities Administrators. *National Policy 51-201 — Disclosure Standards for
Forward-Looking Information.*

British Columbia Securities Commission. *Continuous Disclosure Obligations Overview.*

Mondaq. *Continuous Disclosure Obligations — Amendments to National Instrument 51-102.*

---

## Contributors

Peter M. Woodfine, Jennifer M. Woodfine, and Mathew Woodfine are credited as founding
contributors to PointSav Digital Systems's design-systems research programme.

## How this paper was produced

This paper was prepared with AI assistance under human editorial direction; all analytical
claims and conclusions are the responsibility of the named institutional author.

## Disclosures

The token contract, component, and cross-engine validation described are this workspace's own
engineering work. This paper describes existing, built artifacts rather than a plan; where it
refers to work not yet attempted (extension to a third document family, an automated
conformance checker), that is stated in plain terms as not yet done, in accordance with
continuous-disclosure practice under NI 51-102 and CSA National Policy 51-201.

## Data and reproducibility

The component and its token contract are DTCG-format design tokens plus HTML/CSS/JavaScript
source, versioned in this workspace's design-system repository. Cross-engine validation was
performed directly against the rendered output of both engines described in §3; no proprietary
tooling outside Chromium's print pipeline and WeasyPrint was used.
