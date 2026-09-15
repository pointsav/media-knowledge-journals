---
schema: journal-v2
slug: verifiable-ownership-without-vendor
title: "Verifiable Ownership Without a Vendor in the Loop"
subtitle: "An architecture for license and payment proof that outlasts the vendor's own servers"
site: software.pointsav.com
imprint: PDS-2026-03
thesis: "For a license to actually mean 'perpetual,' verifying it cannot depend on the vendor's server still existing — the technical precondition, not just the contract language."
abstract: |
  Most software license verification requires a live call to the vendor's server, which means
  a "perpetual" license is only as permanent as the vendor's willingness, or ability, to keep
  that server running. This paper describes an alternative verification architecture already
  deployed on this site: a public, third-party-verifiable payment record, paired with an
  offline-verifiable license token checkable against a published cryptographic key with no
  network call, plus a per-binary, hash-chained ledger that lets a purchaser confirm the
  artifact they run is the one that was actually signed. Together these give a customer proof
  of purchase and proof of license that do not depend on the vendor's continued existence — the
  technical precondition, we argue, for licensing language like "perpetual" or "non-revocable"
  to mean what it says rather than what a terms-of-service update can quietly redefine. The
  paper's contribution is architectural: showing what verification without a vendor in the
  loop actually requires — a public payment record, an offline-checkable signature, an
  append-only artifact ledger — not a claim that any particular implementation is uncrackable
  or complete. Every product on this site is currently free during a beta period, so the
  payment-record component is not yet processing paid transactions at scale; the architecture
  — what gets verified, and how — is unchanged by the price charged, and we describe it as it
  will operate once pricing takes effect, not as a claim about transaction volume today.
state: draft
version: "1.0.0"
published:
updated: "2026-09-15"
doi:
license: CC-BY-4.0
cites:
  - nakamoto-2008-bitcoin
  - bernstein-2012-ed25519
  - haber-stornetta-1991-timestamping-digital-documents
draws_from: []
contributors:
  - name: Peter M. Woodfine
    roles: [Founding Contributor]
  - name: Jennifer M. Woodfine
    roles: [Founding Contributor]
  - name: Mathew Woodfine
    roles: [Founding Contributor]
keywords:
  - license verification
  - cryptographic provenance
  - offline verification
  - software distribution
  - hash-chained ledger
---

## 1. The question

A software license that describes itself as "perpetual" or "non-revocable" is making a
promise about the future: that the right to use the software will not expire and will not be
taken away. Most software distributed today enforces that promise, if it enforces it at all,
through a mechanism that quietly contradicts it — a license check that calls the vendor's own
server at startup, or periodically, to confirm the license is still valid. If that server
stops responding, because the vendor discontinued the product, was acquired and shut the
service down, or simply let the infrastructure lapse, the "perpetual" license the customer
paid for stops working, through no action or fault of the customer's own.

This is not a hypothetical edge case. Software vendors are acquired, pivot, and shut down
products routinely, and a license-verification architecture that depends on a live server call
inherits that risk directly, regardless of what the license agreement's text says. The word
"perpetual" in a contract describes an intention; whether that intention is actually
deliverable depends on a separate, technical question: can the license be verified without the
vendor's continued cooperation? If it cannot, "perpetual" is a promise the technical
architecture is not actually equipped to keep.

The question this paper asks is what a verification architecture would need to look like for
that promise to be technically, not just contractually, real — and whether such an
architecture can be built without asking the customer to trust the vendor any more than the
purchase itself already required. We describe one such architecture, already deployed on this
site, built from three specific pieces: a payment record the customer does not have to trust
the vendor to attest to, a license token the customer can verify without calling anyone, and
an artifact ledger that lets the customer confirm the software they are running is the
software that was actually licensed. None of the three pieces is novel cryptography. What we
argue is architectural: that combining these three specific, unglamorous pieces is what
"verification without a vendor in the loop" actually requires, and that most software
distribution today has none of them.

## 2. What we found

The verification problem splits cleanly into three separate questions, and a licensing
architecture needs an answer to each one that does not depend on the vendor still being
reachable.

**Did the customer actually pay?** Under most commercial software models, the answer lives
only in the vendor's own database — a customer disputing a payment, or trying to prove a
purchase after a vendor's records are unavailable, has no independent record to point to. This
site's payment flow instead records the transaction on a public blockchain ledger: the payment
itself is a public, timestamped, third-party-verifiable fact that exists independently of
whether the vendor's own systems are running, and independently of whether the vendor
attests to it. A customer, or any third party, can confirm the payment happened without
asking the vendor to confirm anything.

**Is the license the customer holds actually valid?** Under a server-call model, validity is
whatever the vendor's server currently says it is — which is precisely the property that
makes "perpetual" unenforceable if the server disappears. This site's license tokens are
signed with an Ed25519 keypair and verified entirely offline: the customer's software checks
the token's signature against a published public key, with no network call and no dependency
on any server being reachable at verification time. The mathematics of the signature check are
the same whether the vendor's infrastructure is fully operational, temporarily down, or
permanently gone. A license issued this way is only as revocable as the customer's own choice
to stop using it — the vendor cannot silently invalidate an already-issued token by taking a
server offline, because there is no server in the verification path to take offline.

**Is the software the customer is running the software that was actually licensed?** This is
the question most licensing architectures skip entirely, and it matters because a license
token verified against the wrong binary — a tampered build, a stale version with a since-fixed
vulnerability, an unauthorized redistribution — is not actually proof of anything useful. This
site maintains a per-binary, hash-chained ledger: each released artifact's cryptographic hash
is recorded in an append-only chain, where each new entry incorporates the previous entry's
hash, making the history tamper-evident — altering any past record would break the chain in a
way that is detectable by re-verifying it. A customer can confirm the specific binary they
downloaded matches a hash that was actually published by the vendor at a specific point in
time, using the same append-only-ledger logic that underlies public timestamping systems
generally [haber-stornetta-1991-timestamping-digital-documents], rather than trusting a
vendor's live claim that "this is the official build."

Put together, these three answers give a customer something a server-call model structurally
cannot: proof of purchase, proof of license validity, and proof of artifact authenticity, none
of which requires the vendor's infrastructure to still exist at the moment the customer needs
to check any of them.

## 3. How we worked through it

None of the three components described in §2 is a novel cryptographic primitive. Public,
third-party-verifiable transaction records are the foundational property of public blockchain
ledgers generally [nakamoto-2008-bitcoin]. Offline-verifiable digital signatures using
published public keys are standard practice, and Ed25519 specifically is a well-studied,
widely deployed signature scheme chosen for its combination of strong security properties and
fast, simple verification [bernstein-2012-ed25519]. Append-only, hash-chained record-keeping
for tamper-evidence is a decades-old technique in digital timestamping
[haber-stornetta-1991-timestamping-digital-documents]. The contribution here is not inventing
any of these mechanisms. It is recognizing that a licensing architecture needs all three
together, because each one closes a different specific way a vendor-dependent system fails,
and a system missing any one of the three still has a vendor-dependency somewhere in the
chain.

A payment record alone, without an offline-verifiable license token, still requires the
customer to trust the vendor to correctly translate "payment happened" into "access is
granted" — the payment can be public and verifiable while the access decision remains a
private, server-side judgment the vendor can revise. A license token alone, without a public
payment record, gives the customer an offline-verifiable credential but no independent proof
they are entitled to it if a dispute ever arises. And either of the first two without an
artifact ledger leaves open the question of whether the software actually running is the
software that was actually licensed — a valid license checked against a compromised or
incorrect binary verifies nothing useful. The architecture only delivers on the "no vendor in
the loop" claim when all three pieces are present and each is independently checkable by the
customer, not merely asserted by the vendor.

We tested this architecture against the specific failure mode it is meant to prevent: what
happens to a customer's access if the vendor's own infrastructure becomes unavailable, whether
through business failure, acquisition, or simple neglect. Under this architecture, the answer
is: nothing changes for a license that has already been issued and a binary that has already
been downloaded, because neither the payment record, nor the license check, nor the artifact
verification requires the vendor's servers to be running at the moment the customer needs
them. This is the specific, checkable property the paper claims — not a general claim that the
architecture prevents all forms of vendor misbehavior or business failure.

## 4. What it changes

For a buyer evaluating a "perpetual" license claim, the practical change is knowing which
question to ask before taking the word at face value: does verifying this license require a
live call to the vendor's server? If it does, the license is perpetual in name only — its
actual permanence is bounded by the vendor's infrastructure lifespan, not by the contract
language. If verification is offline and cryptographic, checkable against a published key with
no network dependency, the perpetual claim has a technical foundation matching its contractual
one. This is a concrete, answerable due-diligence question a buyer can put to any vendor
making a perpetual-license claim, regardless of whether that vendor uses this specific
architecture.

For a vendor, the practical change is that building this kind of architecture is a genuine
constraint on future business decisions, not just a marketing claim. A vendor whose license
verification is fully offline cannot later add a remote kill-switch to already-issued licenses
without visibly changing the architecture in a way customers or auditors could detect — the
commitment is structural, not merely stated. This is a real cost to the vendor (less future
flexibility to change the terms of already-sold licenses) traded for a real benefit to the
buyer (confidence that "perpetual" actually describes what they are buying), and making that
trade-off explicit and inspectable is itself part of what this architecture is for.

## 5. Where this could be wrong

**Offline verification does not prevent all forms of vendor misbehavior.** A vendor could
still, for example, stop releasing security patches, decline to provide support, or otherwise
make continued use of the software impractical without technically revoking the license. This
architecture addresses one specific failure mode — the license or artifact becoming
unverifiable because the vendor's infrastructure disappeared — not the general question of
vendor good faith.

**The public payment record and the license token are only as trustworthy as their initial
issuance.** If a vendor issues a fraudulent or mistaken license token in the first place, the
offline-verification property does not detect that error after the fact — it confirms the
token is authentic, not that it was correctly issued. The architecture protects against
post-issuance vendor disappearance, not against errors made at issuance time.

**We have not benchmarked this architecture against alternative approaches at scale.** The
claims here describe what the architecture is designed to do and the specific mechanism by
which it does it; we have not compared its real-world robustness against other
vendor-independent verification schemes, because we are not aware of directly comparable
deployed alternatives to benchmark against.

**The payment-record component is not yet operating at commercial volume.** This site's
products are currently offered free during a beta period, so the public-payment-ledger piece
of this architecture has not yet been exercised by a large number of real, paid transactions.
The signature-verification and artifact-ledger components do not depend on price and are
fully exercised today regardless; the payment-record claim specifically should be read as a
description of how the mechanism is designed to operate once pricing takes effect, not as a
report of transaction volume already observed.

## 6. Conclusion

The question was what a license-verification architecture needs, technically, for a
"perpetual" or "non-revocable" license claim to be actually deliverable rather than a promise
the underlying system cannot keep. The answer is three specific, individually unglamorous
pieces, used together: a public, third-party-verifiable payment record; an offline-verifiable,
cryptographically-signed license token; and an append-only, hash-chained artifact ledger
confirming the software running is the software that was licensed. None of the three is novel
on its own. Combined, they remove the vendor's own continued existence from the customer's
verification path — which is the specific, checkable precondition for a perpetual-license
claim to mean what its contract language says.

---

## 7. Claims and what would count against them

**Claim.** A license architecture combining a public payment record, an offline-verifiable
signed license token, and a hash-chained artifact ledger does not require the vendor's
infrastructure to remain available for a customer to verify purchase, license validity, or
artifact authenticity.

**This claim would be wrong if:** any of the three verification steps is shown to actually
depend, directly or indirectly, on a live vendor-controlled service at the moment of
verification — for example, if the "offline" signature check silently calls out to a vendor
endpoint, or if the published public key itself can only be retrieved from a vendor server
with no independent distribution channel. An auditor finding such a dependency should treat it
as a real defect in the implementation, not a detail to work around.

**What this claim does not say.** It does not claim this architecture prevents vendor bad
faith at issuance time, does not claim it substitutes for ongoing support or security
maintenance, and does not claim to be the only possible approach to vendor-independent
verification — only that it is a real, deployed one that closes the specific failure mode
described in §1.

## References

Bernstein, D. J., N. Duif, T. Lange, P. Schwabe, and B.-Y. Yang. 2012. High-speed
high-security signatures. *Journal of Cryptographic Engineering* 2(2): 77–89.

Haber, S., and W. S. Stornetta. 1991. How to time-stamp a digital document. *Journal of
Cryptology* 3(2): 99–111.

Nakamoto, S. 2008. *Bitcoin: A Peer-to-Peer Electronic Cash System.* bitcoin.org.

---

## Contributors

Peter M. Woodfine, Jennifer M. Woodfine, and Mathew Woodfine are credited as founding
contributors to PointSav Digital Systems's software-economics research programme.

## How this paper was produced

This paper was prepared with AI assistance under human editorial direction; all analytical
claims and conclusions are the responsibility of the named institutional author.

## Disclosures

The architecture described is this site's own deployed licensing and distribution mechanism,
disclosed directly because the paper uses it as its worked example. No named competitor or
specific competing product is referenced or compared. This paper contains forward-looking
language about the architecture's intended guarantees; such statements reflect current design
choices and are subject to change without notice.

## Data and reproducibility

This is an architectural paper describing a real, deployed system rather than reporting an
empirical dataset. The public payment ledger and the per-binary artifact hash chain are, by
design, independently verifiable by any third party without vendor cooperation.
