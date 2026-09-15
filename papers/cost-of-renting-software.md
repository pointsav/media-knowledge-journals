---
schema: journal-v2
slug: cost-of-renting-software
title: "The Cost of Renting Software You Could Own"
subtitle: "A total-cost-of-ownership model for subscription versus perpetual licensing"
site: software.pointsav.com
imprint: PDS-2026-01
thesis: "A subscription's real price is not the invoice — it is the exit cost the arrangement manufactures over time, which a perpetual, self-hostable license does not create."
abstract: |
  Subscription pricing is usually compared to perpetual licensing on sticker price alone — a
  lower monthly figure against a larger one-time figure — and that comparison misses the
  asymmetry that actually determines total cost. A subscriber who has integrated a tool into
  daily work faces real switching costs — retraining, data migration, process rework — that
  the vendor did not have to build and does not bear. Those costs are the subscription's real
  price. They compound for as long as the arrangement continues, and the vendor can revise the
  terms of that arrangement unilaterally at any renewal. A perpetual, self-hostable license
  with no forced update cycle and no remote kill-switch cannot manufacture that same exit
  cost, because there is no renewal point at which terms can be revised — the cost of owning
  the software is bounded the day it is purchased. We work through this asymmetry as a
  cost-of-ownership model, using this site's own distribution terms — no automatic updates,
  no remote kill-switch, an expired license key that never halts an already-running binary —
  as the worked example, not as a sales pitch. We make no comparison to any named competitor;
  the argument is structural, about what a licensing model can and cannot do to a customer
  over time, not about who currently does it better. The main limitation: the model describes
  a structural asymmetry in what each licensing form can do, not a claim about which one costs
  less for any specific buyer in any specific year.
state: draft
version: "1.0.0"
published:
updated: "2026-09-15"
doi:
license: CC-BY-4.0
cites:
  - shapiro-varian-1998-information-rules
  - farrell-klemperer-2007-switching-costs
  - williamson-1979-transaction-cost-economics
draws_from: []
contributors:
  - name: Peter M. Woodfine
    roles: [Founding Contributor]
  - name: Jennifer M. Woodfine
    roles: [Founding Contributor]
  - name: Mathew Woodfine
    roles: [Founding Contributor]
keywords:
  - software licensing economics
  - subscription pricing
  - total cost of ownership
  - switching costs
  - self-hosting
---

## 1. The question

Buyers evaluating software licensing usually compare two numbers: a subscription's monthly or
annual fee, and a perpetual license's one-time price. Whichever number is smaller, over
whatever time horizon the buyer happens to be using, looks like the cheaper option. This
comparison is the one vendors want made, because it is the one where subscription pricing
almost always wins in the short run — a smaller number today beats a larger number today,
regardless of what happens after today.

The comparison is also incomplete in a specific, structural way that has nothing to do with
which vendor is more honest or which product is better. A one-time purchase and a recurring
subscription are not the same kind of financial commitment priced differently — they are
different kinds of commitment. A perpetual license is a completed transaction: the buyer pays
once, receives a working artifact, and the vendor's ongoing cooperation is not required for
that artifact to keep working. A subscription is an incomplete, continuously renewing
transaction: the buyer's access depends on the vendor's continued willingness to provide it,
on terms the vendor can change at the next renewal, for as long as the buyer wants to keep
using what they have already integrated into their work.

That second fact — the buyer's use, not the vendor's product, is what has been integrated —
is where the real cost lives. The question this paper asks is not "which licensing model is
cheaper." It is: what does each model allow the vendor to do to the price, the terms, or the
availability of the software, after the buyer has already built real, hard-to-reverse
dependence on it? And does the answer to that question show up anywhere in the sticker-price
comparison buyers are actually shown?

We think the answer is no, and that this is not a minor omission. The economics of switching
costs are well understood in general — a buyer who has sunk cost into learning, integrating,
and depending on a specific tool faces a real cost to leaving it, separate from and often
larger than the tool's own price [farrell-klemperer-2007-switching-costs]. What is specific to
software, and specific to subscription licensing in particular, is that the vendor controls
both sides of that switching cost at once: they set the ongoing price, and they control
whether the tool keeps running at all if the buyer stops paying it. A perpetual license
structurally cannot do the second thing. This paper works through why that structural
difference is the real price comparison, using a real, currently-deployed licensing model as
the concrete case rather than a hypothetical.

## 2. What we found

The asymmetry has three parts, and each one is a real, checkable property of a licensing
model — not a matter of vendor intent or reputation.

**First: who bears the cost of a renewal decision.** Under a subscription, the buyer faces a
recurring decision point — renew, or lose access — and the vendor sets the terms of that
decision each time it recurs. Under a perpetual license, the decision happens once, at
purchase, and there is no recurring point at which the vendor can revisit the terms of
something the buyer already owns. This is not a claim that subscription vendors behave badly
at renewal time. It is a claim about what the licensing structure *permits*, independent of
whether any specific vendor exercises that permission. A term a vendor is structurally
permitted to revise is a term a buyer should price as revisable, whether or not it has been
revised yet.

**Second: what happens if the vendor's business changes.** A subscription's continued value to
the buyer depends on the vendor continuing to run the infrastructure that enforces access —
a license server, an authentication check, a kill-switch that can be triggered remotely.
If the vendor is acquired, discontinues the product, or simply decides to sunset a tier, the
buyer's access can end regardless of how much the buyer has integrated the tool into their
own operations. A perpetual license that does not depend on a live server call to keep
running does not have this failure mode: the software the buyer already has continues to run
whether or not the vendor's business does. This site's own distribution terms are built this
way deliberately — no automatic updates that could silently change behavior, no remote
kill-switch that could halt a running installation, and an expired license key that stops
future purchases from that key without touching a binary that is already running. We
describe this as the worked example specifically because it is a real, checkable design
decision, not a theoretical possibility.

**Third: where the switching cost actually accumulates.** The retraining, data-migration, and
process-rework costs of leaving a tool accumulate on the buyer's side, in proportion to how
long and how deeply the tool has been used — not on the vendor's side, and not in proportion
to what the vendor charges. This means the buyer's real exposure to a subscription's future
price and term changes *grows* the longer the relationship continues successfully, which is
the opposite of what a simple "lower monthly cost" comparison implies. The tool a buyer has
used longest, integrated most deeply, and depends on most is exactly the tool where a
subscription's future terms matter most — and exactly the tool a sticker-price comparison,
run once at purchase time, is least equipped to price correctly.

None of these three properties describes anything a subscription vendor is doing wrong.
Subscription pricing is a legitimate, often genuinely lower-cost model for buyers whose
switching costs really are low, or whose usage horizon really is short. The finding here is
narrower and structural: the sticker-price comparison buyers are typically shown does not
distinguish between a licensing model that can revise its own terms against an
already-dependent buyer and one that structurally cannot, and that distinction is the one
that determines a license's real cost over a multi-year horizon.

## 3. How we worked through it

The model here is a total-cost-of-ownership comparison, not an empirical study — there is no
dataset of buyer behavior to measure, because the object being compared is a contractual
structure, not an observed outcome. The method is to make explicit what each licensing form
allows and does not allow, then show that the allowed set, not the sticker price, is what
should be priced.

We treat a license as allocating a bundle of specific rights and exposures, following the
general framework in the property-rights and transaction-cost literature on incomplete
contracts [williamson-1979-transaction-cost-economics]: the right to keep using the artifact
without further vendor cooperation, the right (or absence of a right) to modify contractual
terms unilaterally after the fact, and the exposure (or absence of exposure) to a
counterparty's future business decisions. A perpetual, self-hostable license allocates the
first right fully to the buyer and the second right to neither party, because there is no
mechanism by which either party revisits the terms after the sale. A subscription allocates
the first right conditionally — contingent on continued payment and continued vendor
cooperation — and allocates the second right to the vendor, who sets the terms of each
renewal.

We then apply this allocation to a concrete, currently-deployed case: this site's own binary
distribution model. License verification is offline-checkable rather than dependent on a live
server call, meaning an already-issued license continues to function even if the vendor's own
infrastructure is unavailable. There is no forced-update mechanism that could change a
running binary's behavior without the buyer's action. An expired license key blocks future
purchases and updates under that key; it does not, and structurally cannot, reach into an
already-running installation and stop it. Each of these is a specific, checkable design
choice that closes off a specific way a vendor could otherwise revise the terms of an
already-completed sale — and each has a directly corresponding subscription-model
counterpart that leaves that same door open.

We do not attempt to quantify a dollar figure for the switching-cost asymmetry, because that
figure depends on buyer-specific facts — how deeply a given buyer integrates a given tool,
over what horizon — that vary too widely to generalize. What can be stated in general is the
direction and mechanism of the asymmetry, which is the paper's actual claim.

## 4. What it changes

For a buyer evaluating a licensing decision, the practical change is what question to ask.
The sticker-price question — which option costs less per month or per year — is answerable
immediately and is often genuinely useful for short-horizon, low-integration use cases. The
question this paper argues is more often the one that matters is different: if I am still
using this tool in three years, having built real dependence on it, what can the vendor do to
the terms of my access at that point, and what can I do about it? A perpetual, self-hostable
license answers that question with "nothing, and nothing needs to be done, because the terms
do not change." A subscription answers it with "whatever the vendor's terms say at that
renewal, and the buyer's only recourse is the switching cost they have already accumulated."

This does not mean perpetual licensing is always the right choice. A buyer with a genuinely
short usage horizon, or one who values a vendor's ongoing active development and support more
than the certainty of unrevisable terms, may rationally prefer a subscription even after
pricing the asymmetry correctly. What changes is that the choice becomes an informed one,
made against the real structure of what each model allows over time, rather than a
sticker-price comparison that treats the two as differently-priced versions of the same
commitment.

For a vendor, the practical change is that the design choices described in §3 — no forced
updates, no remote kill-switch, offline license verification — are not incidental technical
details. They are the concrete mechanism by which a perpetual license actually delivers the
property a subscription cannot: terms that do not become revisable simply because the buyer
has stayed a customer long enough to be worth revising terms against.

## 5. Where this could be wrong

**The model assumes the buyer's switching cost is real and material.** For a tool with low
integration depth — used occasionally, easily replaced, holding no buyer-specific data or
workflow — the asymmetry this paper describes is real in structure but small in practice,
and a sticker-price comparison may be perfectly adequate. The argument is strongest exactly
where integration is deep, which is not every purchase.

**A perpetual license is not free of its own risks.** A buyer who owns a perpetual license to
software that stops receiving security updates, compatibility fixes, or vendor support faces
a different kind of cost — obsolescence risk — that a well-maintained subscription can manage
better. This paper's claim is about who controls the terms of the relationship, not a claim
that perpetual licensing eliminates all forms of ongoing cost.

**We have not modeled vendor-side incentives to behave well under either structure.** A
subscription vendor with strong competitive pressure or reputational stakes may never in
practice revise terms adversarially, in which case the structural exposure this paper
describes goes unrealized. The paper's claim is about what the structure permits, not a
prediction that every subscription vendor will use that permission.

## 6. Conclusion

The question was whether comparing subscription and perpetual licensing on sticker price
alone captures the real cost difference between them. It does not, because the two models
allocate a different bundle of rights and exposures, and the exposure that matters most —
whether the vendor can revise the terms of an already-completed relationship — does not show
up in either number. A perpetual, self-hostable license with no forced updates and no remote
kill-switch closes off that exposure structurally; a subscription leaves it open by design,
regardless of whether any given vendor chooses to use it. The real price of a subscription is
not the invoice. It is the exit cost the arrangement builds over time, priced against terms
the buyer does not control.

---

## 7. Claims and what would count against them

This is a structural argument, not an empirical one, so there is no regression to run — but
the claim is still meant to be checkable, and stating what would count against it matters as
much here as a falsification test does for an empirical paper.

**Claim.** A perpetual, self-hostable license with offline verification, no forced updates,
and no remote kill-switch cannot manufacture a revisable-terms exposure against an
already-completed sale; a subscription can, by design, regardless of whether any specific
vendor exercises that design.

**This claim would be wrong if:** a perpetual license of this kind is shown to carry an
equivalent mechanism for revising terms against an existing buyer after sale — for example, a
mandatory update that silently narrows usage rights, or a verification step that can be
remotely disabled after the fact. We are not aware of such a mechanism in the model described
here; a buyer or auditor who finds one should treat it as a real defect in the argument, not
a detail to route around.

**What this claim does not say.** It does not say subscription pricing is worse in every
case, that any specific subscription vendor behaves badly, or that perpetual licensing
eliminates obsolescence risk (see §5). It says the two models allocate a specific, checkable
risk differently, and that difference belongs in a buyer's cost comparison.

## References

Farrell, J., and P. Klemperer. 2007. Coordination and lock-in: Competition with switching
costs and network effects. In *Handbook of Industrial Organization,* vol. 3. Amsterdam:
Elsevier.

Shapiro, C., and H. R. Varian. 1998. *Information Rules: A Strategic Guide to the Network
Economy.* Boston: Harvard Business School Press.

Williamson, O. E. 1979. Transaction-cost economics: The governance of contractual relations.
*Journal of Law and Economics* 22(2): 233–261.

---

## Contributors

Peter M. Woodfine, Jennifer M. Woodfine, and Mathew Woodfine are credited as founding
contributors to PointSav Digital Systems's software-economics research programme.

## How this paper was produced

This paper was prepared with AI assistance under human editorial direction; all analytical
claims and conclusions are the responsibility of the named institutional author.

## Disclosures

The licensing model described in §3 and §4 is this site's own distribution model, disclosed
because the paper uses it as a worked example, not because the disclosure changes the
structural argument being made. No named competitor or specific competing product is
referenced or compared. This paper contains forward-looking language about licensing
philosophy and intent; such statements reflect current design choices and are subject to
change without notice.

## Data and reproducibility

This is a conceptual/structural paper; no dataset underlies its claims. The licensing
mechanism described (offline Ed25519 verification, no forced updates, no remote kill-switch)
is the mechanism actually in production for this site's own binary distribution as of this
paper's posting date.
