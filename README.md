<div align="center">

# PointSav Digital Systems — Working Papers
### *The numbered working-paper series behind home.pointsav.com, software.pointsav.com, and design.pointsav.com*

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg?style=flat-square)](https://creativecommons.org/licenses/by/4.0/)
[![Status: Working Papers](https://img.shields.io/badge/Status-Working_Papers-0075ca.svg?style=flat-square)](#)

<br/>

**[→ home.pointsav.com](https://home.pointsav.com/working-papers)** &nbsp;·&nbsp; **[→ software.pointsav.com](https://software.pointsav.com/working-papers)** &nbsp;·&nbsp; **[→ design.pointsav.com](https://design.pointsav.com/working-papers)** &nbsp;·&nbsp; **[→ Woodfine's papers](https://github.com/woodfine/media-knowledge-journals)**

</div>

---

## About this repository

This is the canonical, version-controlled source for PointSav Digital Systems's numbered
working-paper series (`PDS-NNN`, assigned sequentially and permanently — never reused, never
tied to a calendar year). Each site's own `/working-papers` page renders its assigned papers
from this same source — this repository, not any individual site, is the system of record.

**Institutional authorship, not individual.** Every paper is prepared and published by
Woodfine Management Corp. on behalf of PointSav Digital Systems. PointSav Digital Systems is
currently a trade name of Woodfine Capital Projects Inc., planned to become a wholly-owned
Woodfine subsidiary upon incorporation. No paper carries a named individual author, byline,
or contributor — the `## Contributors` section in every paper reads "Prepared by Woodfine
Management Corp." and nothing else.

**Working paper, permanently.** Every paper here is preliminary and subject to revision by
design — this is not a pre-publication staging area for a future peer-reviewed venue. A paper
stays a working paper, carries a version number (not a submission target), and is revised in
place rather than retracted and replaced when new evidence changes the picture.

**Zero outbound links, by editorial rule.** No paper in this series links to any external
site, product, or third party — including each other — anywhere in its body. Cross-references
between papers are recorded in machine-readable frontmatter (`draws_from:`) for tooling,
never rendered as a clickable link in the body. The `## References` section at the end of
each paper is the one exception: a bibliography entry with a real URL or DOI may render as a
link there, after the argument is finished. No named-competitor comparisons — commercial
products are described generically, by category, never by name.

**CC BY 4.0.** Every paper may be shared and adapted for any purpose, including commercially,
with attribution. See [LICENSE](LICENSE).

## Papers

| Imprint | Site | Paper |
|---|---|---|
| PDS-005 | home.pointsav.com | [Authority That Is Held, Not Looked Up](papers/capability-geometry.md) |
| PDS-008 | home.pointsav.com | [A Canonical Order for Decisions, None for Data](papers/no-source-of-truth-for-data.md) |
| PDS-009 | home.pointsav.com | [The Archive Is the Asset](papers/the-archive-is-the-asset.md) |
| PDS-010 | home.pointsav.com | [Keeping AI Out of the Write Path](papers/ai-as-the-optional-third-ring.md) |
| PDS-011 | home.pointsav.com | [A Version Trail for a Building's Equipment](papers/version-trail-for-buildings.md) |
| PDS-012 | software.pointsav.com | [Software That Is Sold, Not Rented](papers/buy-once-own-it.md) |
| PDS-013 | software.pointsav.com | [A Licence Boundary Drawn by Architecture, Not by Features](papers/aggregation-is-the-commercial-boundary.md) |
| PDS-014 | software.pointsav.com | [Ownership You Can Prove Without the Seller](papers/verifiable-ownership-without-vendor.md) |
| PDS-015 | software.pointsav.com | [Software for a Reporting Issuer, Not for a Multinational](papers/business-software-not-enterprise.md) |
| PDS-016 | design.pointsav.com | [The Shape of a Regulated Document Is Data](papers/token-contracts-for-regulated-disclosure.md) |
| PDS-017 | design.pointsav.com | [A Design System That Ships as a Binary, Not a Hosted Service](papers/design-system-ships-as-a-binary.md) |
| PDS-018 | design.pointsav.com | [Building Toward Type Nobody Can Take Back](papers/typeface-families-for-an-open-platform.md) |

## How this repository is used

Each paper is a plain Markdown file with a structured YAML frontmatter block (`schema:
journal-v2`) — title, thesis, abstract, citations, and version metadata — followed by a
masthead disclosure notice, a thesis-led opening, two to four numbered sections argued in the
paper's own terms, and a fixed back-matter sequence: `## References`, `## Contributors`,
`## How this paper was produced`, `## Disclosures`, and `## Data and reproducibility`.

This repository is the source; it is not itself a rendered website. Each paper's real
rendered form lives at its assigned site's own `/working-papers/<slug>` page.

## Disclosures

Nothing in this repository is an offer to sell, or a solicitation of an offer to buy, any
security. Forward-looking statements in any paper reflect current expectations as of that
paper's stated version date and are subject to change without notice.

---

<div align="center">

Copyright © 2026 Woodfine Capital Projects Inc. Licensed under [CC BY 4.0](LICENSE).

</div>
