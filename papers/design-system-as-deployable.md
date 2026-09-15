---
schema: journal-v2
slug: design-system-as-deployable
title: "A Design System That Ships as a Binary, Not a Hosted Service"
subtitle: "Why treating a design system's build pipeline as a deployable artifact changes who can adopt it"
site: design.pointsav.com
imprint: PDS-2026-09
thesis: "A design system whose reference implementation compiles into one self-contained binary, rather than running only as a vendor-hosted service, is what actually makes it adoptable by a company that cannot depend on continued access to someone else's server."
abstract: |
  Most commercial design systems are consumed as a hosted documentation site plus a package a
  customer's own application imports — the underlying build pipeline, and any server the
  vendor runs to demonstrate the system, stay the vendor's own infrastructure. We built and run
  ours differently: the reference implementation compiles into a single binary that embeds its
  own templates and static assets at build time, generates its token stylesheet from the vendor
  export as part of that same build rather than by hand, and requires no live connection back to
  any vendor-operated service to run. We split the licensing to match: the tokens and component
  recipes are Apache-2.0, unconditionally, from the day they are published; the server binary
  that runs the reference site is source-available under the Functional Source License,
  converting automatically to Apache-2.0 two years after each release, with a narrow commercial
  grant available only to a customer who wants to build a competing product before that
  conversion date. We found a real instance of the failure this design guards against — a prior
  version of the same pipeline hand-synced its token stylesheet in three separate places and
  drifted — inside our own history, and treat that as evidence a self-hosted pipeline still
  needs real engineering discipline; it does not get that discipline for free just by not being
  a hosted service. The main limitation: this paper describes a real, running deployable, not a
  proven market — no customer has yet exercised the commercial license this model depends on.
state: draft
version: "1.0.0"
published:
updated: "2026-09-15"
doi:
license: CC-BY-4.0
cites:
  - dtcg-w3c
  - open-core-handbook
  - open-source-guides-leadership
  - spdx-license-list
  - farrell-klemperer-2007-switching-costs
  - williamson-1979-transaction-cost-economics
  - shapiro-varian-1998-information-rules
  - benkler-2002-coases-penguin
  - lerner-tirole-2002-open-source-motivation
  - raymond-1999-cathedral-and-bazaar
draws_from: []
contributors:
  - name: Peter M. Woodfine
    roles: [Founding Contributor]
  - name: Jennifer M. Woodfine
    roles: [Founding Contributor]
  - name: Mathew Woodfine
    roles: [Founding Contributor]
keywords:
  - design systems
  - self-hosted software
  - software licensing
  - switching costs
  - vendor independence
---

## 1. The question

A design system is usually delivered as a package a customer's build imports, plus a
documentation and reference site the vendor hosts and keeps running. The package is the part a
customer actually controls; the reference site, the build pipeline that produces it, and often
the token source itself stay the vendor's own infrastructure. For most customers this is a
reasonable division of labor. For a customer who specifically cannot depend on continued access
to someone else's server — because they operate somewhere connectivity is unreliable, because
their own compliance posture forbids depending on an external vendor's uptime for something
they consider core infrastructure, or simply because they want the option of running the whole
system themselves if the vendor relationship ever ends — that division is the whole problem.

Software-licensing economics gives a name to what a customer is actually buying in the
convenience version of this arrangement: not just a set of features, but a switching cost that
compounds the longer the relationship continues, because more of the customer's own workflow
comes to depend on infrastructure only the vendor operates. The question this paper asks is
narrower and more mechanical than "should software be self-hostable" in the abstract: can a
design system's own reference implementation — not just the tokens a customer's build already
imports, but the actual demonstration server and its build pipeline — be packaged as something
that runs entirely on infrastructure the adopter controls, with no live dependency on the
vendor, and does doing so cost the vendor a viable path to commercial revenue.

We answer both halves directly, because they are in real tension: making something fully
self-hostable and unconditionally reusable is what a customer in the position described above
actually needs, but a vendor that gives away everything unconditionally has no obvious way to
be paid for building it. Our answer is a license split, built and running today, not proposed —
described in full in §3.

## 2. What we found

**The reference server compiles into one self-contained binary, and this was verified directly,
not assumed.** The build pipeline embeds its HTML templates and static assets into the compiled
binary at build time, and generates its token stylesheet from the vendored design-token export
as part of the same build step, rather than requiring either to be hand-maintained or fetched
from a separate location at runtime. Running the compiled binary does not require a live
connection back to any vendor-operated service.

**We found a real occurrence of the exact failure mode this design guards against, inside our
own history, not a hypothetical one.** An earlier version of this same pipeline hand-synced its
token stylesheet by copying it into three separate places by hand. That copy drifted — the three
locations genuinely disagreed with each other — before the current build-time generation step
replaced the hand-sync entirely. This is direct evidence for a claim that is easy to state but
easy to get wrong in practice: a self-hosted pipeline does not inherit engineering discipline for
free just because nothing about it depends on a vendor's server. It still requires exactly the
same "single source of truth" discipline a hosted SaaS product would otherwise centrally enforce
on the vendor's side — the self-hosted version simply has to build that discipline into its own
pipeline instead of trusting a vendor to have done so.

**The licensing is genuinely split by what it governs, and both halves are real, not aspirational.**
The token set and component recipes are licensed Apache-2.0, unconditionally, with no waiting
period and no use restriction, from the day they are first published. The server binary that
runs the reference site carries a different, deliberately time-bound license: source-available
under the Functional Source License (FSL) from release, converting automatically to a full
Apache-2.0 grant two years after each release, with no action required and no re-licensing step
for that conversion to happen. A narrow commercial grant exists only for a customer who wants to
build a directly competing product or service before that two-year window closes — the source
itself never changes license to grant this; it is a separate permission layered on top, for the
purchaser only.

**The commercial-packaging decision made about this server so far treats it as a distribution
question, not a hosting question.** Rather than selling access to the server as a standalone
product, the decision made was to bundle it with an existing operating-system-tier license — a
real, already-made packaging choice, not a hypothetical option under consideration. That choice
is itself consistent with this paper's thesis: the server is being thought of as something a
customer installs and runs, priced and packaged the way installed software is, not the way
access to a hosted service is.

## 3. How we built and verified it

The build has two real, verifiable mechanisms behind the "no vendor dependency at runtime" claim.
First, a build-time step reads the vendored design-token export and this application's own
local override layer, and generates the final token stylesheet as part of every `cargo build` —
the generated file carries a comment marking it as produced output, not something to hand-edit,
and is regenerated fresh on every build rather than fetched or cached from anywhere external.
Second, the compiled binary embeds its markup templates and static assets directly, using a
standard Rust asset-embedding mechanism that reads the relevant directories at compile time —
so what ships is one binary, not a binary plus a directory of files it expects to find at a
particular path at runtime.

We verified the licensing terms directly against this workspace's own published licensing page
for the reference site, rather than describing the license from memory: Apache-2.0 for the
token set with no delay, FSL-1.1-ALv2 for the server source with an automatic two-year
conversion to Apache-2.0, and a separate commercial grant available only for the narrow
competing-product case, which does not alter the underlying source license itself.

What we have not yet built is an automated test that runs the compiled binary in a fully
network-isolated environment and confirms zero outbound calls of any kind — the claim that it
requires no live vendor connection rests on the build mechanism described above and on direct
inspection of what the binary does at startup, not yet on a dedicated isolation test. That gap is
stated plainly in §5, not glossed over.

## 4. What it changes

For a customer evaluating whether to adopt this design system's server component at all, the
practical change is what happens if the vendor relationship ends, degrades, or simply becomes
inconvenient. Under a purely hosted model, that scenario means migrating to a replacement
service, with the same compounding switching-cost dynamic that licensing economics describes for
any vendor-dependent infrastructure. Under this model, the customer already runs the actual
binary that was running the reference implementation — there is no separate migration step for
the infrastructure itself, only for any customer-specific configuration layered on top.

It also changes the shape of the vendor's own commercial incentive. A transaction-cost view of
why firms choose one governance structure over another suggests a vendor benefits from making
switching genuinely low-cost only when there is still a real, separate reason for a customer to
pay — here, the reason is not access to the server at all (that is unconditionally available),
but the narrow right to build a directly competing offering before the license would otherwise
convert on its own. The two-year automatic conversion is itself a real commitment device: it is
not a promise the vendor could quietly walk back later, because each release's conversion date,
once passed, is not something a future decision can retroactively undo.

It changes least, and this paper is direct about that: for a customer who has no interest in
running their own infrastructure at all, none of this changes anything about their day-to-day
experience of using the hosted reference site the way any other design-system documentation
site is used. This architecture is a structural option, not a requirement placed on every
adopter.

## 5. Where this could be wrong

**Being installable is not the same as being effortless.** Running the compiled binary still
requires an adopter to have the operational capacity to build, deploy, and update a Rust
service — a real, non-trivial cost this paper does not claim away. A customer without any such
capacity is not meaningfully better off than they would be under a purely hosted model, even
though the option to self-host exists.

**"Source-available" during the FSL window is not the same claim as "no restrictions," and
conflating the two would be dishonest.** For two years after each release, the server source
carries a real use restriction — a customer may not use it to build a directly competing
product or service without the separate commercial grant. Only the token set is unconditional
from day one; the server genuinely is not, until its own two-year window closes.

**The commercial-grant mechanism is described but untested — no customer has purchased one.**
The self-service purchase path for that grant is itself still a stated intention rather than a
live product; the entire revenue side of this license split remains a design, not yet a
result.

**Bundling the server with an existing operating-system-tier license, rather than selling it
standalone, is one packaging decision made once, not evidence the market specifically wants it
bundled.** A different customer segment, or more experience with actual demand, could reverse
this choice without changing anything else this paper describes.

## 6. Conclusion

The question was whether a design system's own reference server, not just the tokens a
customer's build imports, can be packaged as something that runs entirely on infrastructure the
adopter controls, without costing the vendor a viable way to be paid for building it. It can:
the server compiles into one self-contained binary with no live dependency on the vendor at
runtime, the licensing is genuinely split — unconditional for the tokens, time-bound and
source-available for the server — and a real instance of the failure this design exists to
prevent, three-way hand-sync drift, already happened once in this pipeline's own history before
the current build-time mechanism replaced it. What remains open is commercial, not technical:
whether a real customer ever exercises the license split this model depends on.

---

## 7. Claims and what would count against them

**Claim.** Packaging a design system's reference server as a self-contained, build-time-
assembled binary under a split, time-bound license removes the vendor-dependency-at-runtime
problem for an adopter who needs that, without requiring the tokens themselves to carry any
restriction.

**This claim would be wrong if:** the compiled binary is found to make any live call back to a
vendor-operated service at runtime (undermining the "no live dependency" claim directly), or if
the FSL/commercial-grant split is shown in practice to suppress adoption of the unconditionally
licensed token set specifically (which would mean the split is costing the paper's other stated
goal rather than serving both).

**What this claim does not say.** It does not claim self-hosting is effortless, does not claim
the commercial-grant mechanism has generated any revenue yet, and does not claim every adopter
should prefer the self-hosted path over the hosted reference site.

| Test | What it checks | Status |
|---|---|---|
| Network-isolated runtime test | Whether the compiled binary makes zero outbound calls to any vendor-operated service | Not yet run; claim currently rests on build-mechanism inspection, not an isolation test |
| Hand-sync drift recurrence check | Whether the build-time token generation step actually prevents the three-way drift that occurred under the prior hand-synced version | Confirmed structurally (generation replaced the hand-sync entirely) |
| Commercial-grant uptake | Whether any customer purchases the FSL commercial grant | Not yet exercised — zero purchases to date |
| Token-adoption rate under the split license | Whether adoption of the Apache-2.0 token set is measurably unaffected by the server's separate, more restrictive license | Not yet measured |

## Appendix A — Licensing terms as currently published

| Artifact | License | Restriction | Conversion |
|---|---|---|---|
| Design tokens, component recipes, research documents | Apache-2.0 | None | N/A — unconditional from publication |
| Reference server (`app-privategit-design`) | FSL-1.1-ALv2 | May not be used to build a directly competing product/service | Converts automatically to Apache-2.0, two years after each release |
| Commercial grant (optional, per release) | Separate commercial permission layered on the FSL source | Lifts the competing-product restriction early, for the purchaser only | Does not change the published source license itself |

## References

Design Tokens Community Group (DTCG). 2026. *W3C Design Tokens Format Module.*
https://tr.designtokens.org/format/

Open Core Ventures. *Open Core Ventures Handbook — Licensing & Distribution.*
https://handbook.opencoreventures.com/commercial-mvp/licensing-and-distribution/

GitHub. *Open Source Guides — Leadership and Governance.*
https://opensource.guide/leadership-and-governance/

Linux Foundation. *SPDX License List.* https://spdx.org/licenses/

Farrell, J., and Klemperer, P. 2007. Coordination and lock-in: Competition with switching costs
and network effects. In *Handbook of Industrial Organization*, vol. 3. Elsevier.

Williamson, O. E. 1979. Transaction-cost economics: The governance of contractual relations.
*Journal of Law and Economics* 22(2): 233–261.

Shapiro, C., and Varian, H. R. 1998. *Information Rules: A Strategic Guide to the Network
Economy.* Harvard Business School Press.

Benkler, Y. 2002. Coase's Penguin, or, Linux and the nature of the firm. *Yale Law Journal*
112(3): 369–446.

Lerner, J., and Tirole, J. 2002. Some simple economics of open source. *Journal of Industrial
Economics* 50(2): 197–234.

Raymond, E. S. 1999. *The Cathedral and the Bazaar: Musings on Linux and Open Source by an
Accidental Revolutionary.* O'Reilly Media.

---

## Contributors

Peter M. Woodfine, Jennifer M. Woodfine, and Mathew Woodfine are credited as founding
contributors to PointSav Digital Systems's design-systems research programme.

## How this paper was produced

This paper was prepared with AI assistance under human editorial direction; all analytical
claims and conclusions are the responsibility of the named institutional author.

## Disclosures

The build pipeline, licensing terms, and packaging decisions described are this workspace's own
work and current policy. This paper describes the commercial-grant purchase path and specific
future licensing/marketplace mechanics in planned or intended terms only; no revenue has yet
been realized through that mechanism, in accordance with continuous-disclosure practice under
NI 51-102 and CSA National Policy 51-201.

## Data and reproducibility

The build mechanism (token generation, asset embedding) and the licensing terms described are
directly inspectable in the reference server's own source repository and its published
licensing page. No proprietary measurement tooling was used; the one open verification gap
(network-isolated runtime testing) is stated as such in §5 and §7, not represented as complete.
