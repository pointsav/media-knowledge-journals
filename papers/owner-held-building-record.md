---
schema: journal-v2
slug: owner-held-building-record
title: "Building Data Should Live With Whoever Holds the Title"
subtitle: "Why this platform's portability commitment is an ownership-duration argument, not just a technical feature"
site: home.pointsav.com
imprint: PDS-2026-07
thesis: "Across a building's life, the party with the longest-lasting interest in its data is whoever holds title to the property, not whichever software vendor's platform happened to originate the file — this platform's own portability commitment exists because that mismatch in time horizon is real, and because a software architecture that ignores it is asking an owner to accept a structural risk with no technical necessity."
abstract: |
  This platform states, as a plain product commitment, that a customer's records move with
  them if they change technology providers, with nothing re-shaped and nothing requiring this
  platform's own cooperation. This paper makes the case for why that commitment matters,
  using the vocabulary an asset manager, a lender, or an acquiring buyer actually uses, rather
  than the vocabulary of a product feature list. Across a building's full life — design,
  construction, operation, refinancing, resale — the party with the most durable interest in
  the building's data is whoever holds title at any given moment, and that interest typically
  spans decades. The party who originated the digital record — a software vendor operating
  under a contract term measured in years, not decades — has a structurally shorter time
  horizon than the asset the record describes. We restate the case for owner-held building
  records in the terms that actually matter at a transaction: how cleanly the record
  transfers at a sale, how the record survives a change of vendor or a vendor's own business
  failure, and how readily a lender or regulator can independently verify what it contains.
  We make no claim about cost savings or any specific transaction outcome — this paper's
  contribution is a framework for evaluating building-data custody arrangements by
  ownership-duration, of which this platform's own portability commitment is one concrete
  instance, not a technology endorsement for any particular project.
state: draft
version: "1.0.0"
published:
updated: "2026-09-15"
doi:
license: CC-BY-4.0
cites:
  - iso-19650
  - ifc-4-3
draws_from:
  - flat-file-bim-substrate
  - aec-data-layers
contributors:
  - name: Peter M. Woodfine
    roles: [Founding Contributor]
  - name: Jennifer M. Woodfine
    roles: [Founding Contributor]
  - name: Mathew Woodfine
    roles: [Founding Contributor]
keywords:
  - building data ownership
  - asset lifecycle records
  - data portability
  - vendor risk
  - real property transactions
---

## 1. The question

This platform's own portability commitment states, in plain terms, that a customer's records
move with them if they change technology providers — nothing is re-shaped, and nothing
requires this platform's own cooperation. That is a specific, checkable design choice, not a
marketing phrase, and this paper makes the case for why it is the correct choice rather than
simply asserting it.

A building's digital record — its as-built drawings, its equipment schedules, its
maintenance history — is typically created by whichever software the design or construction
team happened to be using at the time, and stored on whatever platform that software's vendor
operates. That arrangement works fine for the duration of one project. It becomes a real
liability across the building's actual operating life, because a commercial building
routinely stays in service, under one or more owners, for fifty years or more, while the
software vendor that originated its digital record operates under a contract term measured in
single-digit years, and has no obligation — commercial, legal, or otherwise — to remain in
business, keep the format unchanged, or keep the owner's access uninterrupted for anything
approaching the building's own lifespan.

This is a mismatch in time horizon, not a mismatch in technology quality. The party with the
longest-lasting interest in the building's data — whoever holds title to the property at any
given time — depends on the party with the shortest-lasting interest in that same data — the
current software vendor. This paper asks a narrow question directly relevant to anyone who
owns, lends against, or is considering acquiring commercial real estate: when should building
data custody itself be treated as a due-diligence item, the same way title, zoning, and
environmental condition already are?

## 2. What we found

**The party who should hold a building's authoritative digital record, by any reasonable
ownership-duration standard, is whoever holds title — not whoever's software created the
file.** A lender underwriting a forty-year mortgage does not expect the borrower's insurance
broker of the day to retain custody of the policy documents indefinitely; the documents move
with the asset and its owner of record. The same logic applies with more force to a building's
core operating data, which — unlike an insurance policy — has no natural renewal point that
forces a custody decision. Left unaddressed, custody defaults silently to whichever platform
originated the file, for as long as that platform exists.

**Three transaction-relevant properties follow directly from where the record actually
lives, independent of any specific vendor's contract terms.** Portability at sale: a record
that is a set of open, plain files transfers with a property deed the same way physical
documents do; a record locked inside a vendor's subscription-gated platform requires
re-onboarding the buyer into that vendor's own account structure before the buyer has any
access at all. Continuity across vendor changes: a plain-file record remains readable
regardless of which specific software tool an owner or operator chooses to use next; a
vendor-hosted record's usability ends when that specific vendor relationship ends, for
whatever reason. Auditability: a lender or a regulator reviewing a building's operating and
compliance history can inspect a plain-file record directly; a vendor-hosted record requires
that lender or regulator to obtain access through the vendor, introducing a third party into
what is otherwise a two-party relationship between owner and reviewer.

**None of this requires a specific cost claim or a specific vendor comparison to be true.**
The argument holds purely on the mismatch between the building's operating life and any single
vendor's realistic business lifespan — a structural fact about time horizons, not a claim
that a particular vendor's product is deficient or that switching custody models produces a
specific dollar saving.

## 3. How this framework applies

We evaluate building-data custody arrangements against three questions, asked at the point a
building's data architecture is chosen or reviewed, not only at the point of a transaction.
**Who can access the record with no active relationship to any specific software vendor?**
A record that requires an active subscription, account, or vendor relationship to open at all
fails this test regardless of how good the vendor's product is while that relationship holds.
**Does the record transfer with the property, or does it require a separate onboarding step
with a third party?** A record bound to a vendor's own account structure requires the buyer to
independently establish a relationship with that vendor before gaining any access; a record
held as open files transfers as part of the same closing that transfers the deed. **Can a
party outside the owner-vendor relationship — a lender, a regulator, a future buyer's own
consultants — verify the record's contents directly, or only through the vendor's own
interface?**

Applying these three questions is a due-diligence exercise, not a technology-procurement
decision. A building owner does not need to operate the underlying open-standard technology
described in a companion engineering paper to apply this framework — the framework applies
at the level of "who can open this file, under what conditions, five, twenty, or fifty years
from now," a question any asset manager can evaluate without technical expertise in the
underlying data formats. This platform's own architecture is one concrete instance of a
system built to pass all three questions by construction, rather than by relying on
contractual promises about future behavior.

## 4. What it changes

For an owner or an acquiring buyer, the practical change is treating building-data custody
as a named line item in due diligence, the same way title condition, zoning status, and
environmental assessment already are — rather than as an unexamined default that happens to
follow from whichever vendor the design or construction team used. A building with an
open-format, owner-held record is, on this framework, a lower-risk asset from a data-custody
standpoint than an otherwise-identical building whose operating record is locked inside a
single vendor's platform — not because the vendor's product is worse, but because the
locked-in building's future usability depends on a company remaining in business on a
timescale the building itself does not require.

For a lender, the same framework applies directly to loan underwriting: a building whose
compliance and maintenance history can be independently verified without going through a
third-party vendor is more straightforwardly auditable over the life of a long-term loan.

## 5. Where this could be wrong

**This paper makes no claim about cost.** Adopting an owner-held record architecture has real
implementation costs of its own — building or commissioning the technical substrate, in-house
or through a consultant, is not free — and this paper does not claim those costs are lower
than continuing with a vendor-hosted arrangement. The argument here is about risk allocation
over time, not about which option is cheaper.

**This paper makes no claim about any specific transaction outcome.** We do not claim that
building-data custody has historically affected a specific sale price, financing term, or
closing timeline for any real transaction; the argument is prospective and structural, not a
report of an observed market effect.

**The framework assumes a multi-decade holding horizon.** For an owner with a genuinely
short holding period — a merchant builder selling within one to two years of completion, for
example — the custody-duration mismatch this paper describes is smaller by construction, and
the framework's practical weight is correspondingly reduced.

## 6. Conclusion

Building data is routinely created and held by whichever vendor's software happened to be in
use at the time, with no deliberate decision about where the record should live across the
building's actual operating life. Evaluated on ownership-duration grounds — the same grounds
a lender already applies to every other long-lived asset attribute of a building — the party
who should hold the authoritative record is whoever holds title, not whoever's platform
originated the file. This is not a claim that any specific vendor's technology is deficient;
it is a claim about a structural mismatch in time horizon between a building's decades-long
life and any single vendor's realistic business lifespan, and a recommendation to treat
building-data custody as its own explicit due-diligence question rather than an unexamined
default.

---

## 7. Claims and what would count against them

**Portability claim.** An owner-held, open-format building record transfers to a new owner at
a property sale with no separate vendor-onboarding step required before the new owner has
full access to the record.

**Auditability claim.** A lender or regulator can independently verify the contents of an
owner-held, open-format building record without requiring access mediated through a software
vendor.

| Test | What it checks | Status |
|---|---|---|
| Sale-transfer test | Whether an owner-held record opens for a new owner immediately at closing, with no vendor account step | Verified structurally: the record format requires no vendor account by construction |
| Third-party audit test | Whether a lender or regulator can open and verify the record without vendor mediation | Verified structurally: the record format is openable by any standards-compliant tool |
| Cost-comparison test | Whether owner-held custody is cheaper than vendor-hosted custody over a multi-decade horizon | Not tested — this paper makes no cost claim |
| Transaction-outcome test | Whether custody model has measurably affected a real sale price or financing term | Not tested — this paper makes no outcome claim |

The portability and auditability claims are falsified if a real owner-held, open-format
record is found to require vendor mediation for either transfer or third-party verification.
This paper's remaining statements are explicitly framed as structural argument, not
empirical findings — the last two rows record what this paper deliberately does not claim,
not tests it failed.

## References

International Organization for Standardization. *ISO 19650 — Organization and digitization
of information about buildings and civil engineering works, including building information
modelling.*

International Organization for Standardization. 2024. *ISO 16739-1 — Industry Foundation
Classes for data sharing in the construction and facility management industries.*

---

## Contributors

Peter M. Woodfine, Jennifer M. Woodfine, and Mathew Woodfine are credited as founding
contributors to PointSav Digital Systems's systems-architecture research programme.

## How this paper was produced

This paper was prepared with AI assistance under human editorial direction; all analytical
claims and conclusions are the responsibility of the named institutional author.

## Disclosures

This paper contains forward-looking statements about the intended benefits of a building-
data custody approach; such statements reflect current intentions and are not a claim about
any specific transaction outcome, cost saving, or valuation effect.

## Data and reproducibility

This paper is a framework argument, not an empirical study; it makes no claim requiring a
dataset for reproduction. The technical architecture referenced as the owner-held-record
approach is documented in full in a companion paper (`flat-file-bim-substrate`).
