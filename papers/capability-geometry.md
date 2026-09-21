---
schema: journal-v2
slug: capability-geometry
title: "Authority That Is Held, Not Looked Up"
subtitle: "Capability Geometry: a customer-held key, a public checkable record, and paired machines in place of a vendor's account database"
site: home.pointsav.com
imprint: PDS-005
thesis: "Authority over a system should be proven by a key its owner holds and a record anyone can check, not looked up in a vendor's account database."
abstract: |
  Our thesis is that the right to operate a system should rest on something the owner
  physically holds and something anyone can independently check, rather than on an entry
  in a vendor's account database that the vendor can read, alter, or lose. Capability
  Geometry is the name for that arrangement. It combines three parts: authorization tokens
  that work like physical keys, so that holding one is the permission and nothing is
  consulted at the door; a public, append-only record of every authorization decision,
  sealed with a signing key the customer holds, so that any third party can confirm what
  was granted and when without trusting the vendor; and a pairing step that binds authority
  to a specific approved machine rather than to a password a person remembers. The token
  type and the record-checking logic are implemented and tested today; a routine check
  against the record answers from memory in a fraction of the time the underlying signature
  check would take, which is what makes checking every request against the record
  practical rather than merely correct. The main limit: the kernel-level enforcement this
  design ultimately rests on is a direction, not a running service — today's platform
  services run on ordinary operating systems.
state: draft
version: "0.1.0"
published:
updated: "2026-09-15"
cite_as:
license: CC-BY-4.0
cites:
  - rfc-9162
  - c2sp-signed-note
  - sel4-klein-2009-sosp
  - capsicum-watson-2010
draws_from:
  - capability-geometry
  - pairing-as-permission
  - machine-based-auth
  - merkle-proofs-as-substrate-primitive
  - capability-ledger-substrate
  - sel4-capability-topology
  - sel4-microkernel-substrate
  - worm-ledger-architecture
  - os-console
  - three-binary-architecture
prepared_by: "Woodfine Management Corp."
keywords:
  - capability systems
  - transparency logs
  - customer-held keys
  - machine pairing
  - ownership transfer
---

> This paper is provided for engineering, operational, and research purposes and does not
> constitute investment advice or a solicitation to invest in any Woodfine direct-hold
> solution. Statements marked "planned," "intended," "targeted," "may," or "expected" are
> forward-looking and subject to change. Full disclosures appear at the end of this paper.

Working Paper PDS-005 · v0.1.0 · CC BY 4.0

Our thesis is that authority over a system should be proven by a key its owner holds and a
record anyone can check — never looked up in a vendor's account database. When you use almost
any online service today, the question "is this person allowed to do this?" is answered by
the service consulting its own list. That list belongs to the vendor. The vendor can read
it, change it, lose it, or be ordered to hand it over, and the customer has no independent
way to confirm what it says. We hold that this is the wrong shape for authority over
anything that matters, and that a better shape has existed in computer-science research for
decades and is now practical to build on.

Capability Geometry is the name for the arrangement we are building toward. It has three
parts, and this paper takes each in turn. The first is a form of permission that works like a
physical key: whoever holds it can open the door, and there is no doorman with a list to be
tricked or bribed. The second is a public, append-only record of every permission ever
granted or withdrawn, sealed with a signing key the customer — not the vendor — holds, so
that an outside party can confirm what was granted and when. The third is a pairing step
that binds authority to a specific, approved machine rather than to a password that a person
must remember and can be tricked into revealing.

Two of the three parts are running code today: the token type and the record-checking logic
exist as tested, open-source software, and the machine-pairing step is a live component. The
part that would make the whole arrangement a property of the computer's core rather than of
well-behaved application software — enforcement by a formally verified operating-system
kernel — is a direction, not a running service. This paper is written so that a reader with
no background in computing can follow why the three parts belong together, and so that a
specialist in any of the three can see exactly where we would welcome their help.

## 1. The thesis

A permission system has two possible shapes. In the first, authority is a fact recorded
somewhere central, and every request is answered by looking that fact up. In the second,
authority is a thing the requester holds, and a request either presents it or cannot be made
at all. Almost every commercial computer system uses the first shape. Capability Geometry is
the second shape, applied consistently, with a public record attached so that the holding of
authority can be independently confirmed.

The reason to prefer the second shape is not that lookups are slow or that vendors are
dishonest. It is that a lookup requires a lookup table, and whoever controls the table
controls the authority. If the table lives on the vendor's computers, the customer's right
to operate their own system is, in practice, a courtesy the vendor extends and can withdraw —
by error, by a breach of the vendor's own systems, by a change in commercial terms, or by
simply going out of business. The second shape removes the table. There is nothing central
to control.

The composition is the claim. Each of the three parts is well understood on its own.
Key-like permissions have been studied since the 1960s and have shipped in production
operating systems. Public append-only records sealed with signatures are how the security of
the web's certificates has been policed since the mid-2010s. Machine-bound access is how
most engineers already reach their own servers. What has not been done, to our knowledge,
is to wire the three together so that a customer's own key is the root of every
authorization decision in a business system, the record of those decisions is theirs to
publish and anyone's to audit, and the transfer of the whole arrangement to a new owner is a
single sealed entry in that record rather than a months-long migration. That wiring is what
Capability Geometry names.

## 2. The problem, in the reader's terms

Consider how a bank branch used to verify a cheque before computers. The bank kept a
signature card for each account — a piece of paper with your signature on it, filed in a
drawer. When a cheque arrived, a teller compared the signature on the cheque against the
card. This is a lookup. It works as long as the drawer is honest, complete, and reachable.
If the card is lost, you cannot draw on your own account until the bank replaces it. If a
forger gets to the drawer and swaps the card, the bank will honour the forger's signature
and refuse yours. If the bank closes, the drawer closes with it. Your authority over your own
money is only as good as the bank's filing.

Nearly every online account you hold today is a signature card in a vendor's drawer. When
you sign in, the service looks up your record, checks the password or code you supplied
against what it has on file, and then consults a second list to decide what you are allowed
to do. Both lists are the vendor's. The industry's response to the obvious weaknesses of
this arrangement has been to add more checks in front of the drawer: a second code sent to
your phone, a firewall, a monitoring system that watches for unusual sign-ins, a "zero
trust" policy that re-checks you at every step. Each of these makes the drawer harder to
reach. None of them changes the fact that the drawer is where authority lives.

That matters because layered checks raise the cost of an attack without changing its
target. An intruder who learns to get past the newest layer arrives at the same drawer as
before. And every layer is itself a new piece of software that can fail, be misconfigured,
or be attacked — the maze gets longer, but it still leads to the same room. The structural
weakness is well known in the field under the name of the confused deputy: a trusted
intermediary that holds broad authority can be tricked by a less-trusted caller into using
that authority on the caller's behalf. Any system in which authority is looked up from a
table at request time has this weakness, no matter how carefully the table is maintained.

For an owner of a business system, the practical consequences are concrete. You cannot
independently verify who has been granted access to your own records. You cannot hand the
system to a successor — a buyer, a new operator, a family member — without the vendor's
cooperation in re-creating accounts. And if the vendor's own systems are breached, the
attacker's first prize is the drawer of signature cards for every customer at once.

## 3. A key that is the permission

### What a capability is

Start with a physical key. A locksmith cuts it, hands it to you, and from then on the lock
answers to the key — not to your name, your face, or a list posted beside the door. If you
lend the key to a neighbour, the neighbour can open the door; if you want them to stop, you
change the lock or take the key back. Nobody stands at the door checking a list, because
there is no list. The permission is the key.

In computing, a permission of this kind is called a capability: an unforgeable token that
names one specific thing — a file, a stretch of memory, a communication channel — and says
what may be done with it. A program that holds a capability can use it. A program that does
not hold one cannot even ask; there is no door to knock on. The idea dates from research in
the 1960s, and it has one property that lookup-based systems cannot have: the confused-deputy
trick does not work, because a program can only exercise authority it was explicitly handed,
never authority it happens to have lying around. A widely cited demonstration that this
model can be retrofitted into an ordinary operating system was published in 2010
[capsicum-watson-2010]; the model itself is far older.

The set of all such keys in a running system forms a map: each key is an arrow from the
program that holds it to the thing it opens. The map has a useful property — a program can
only obtain a new key by being handed one along an arrow it already has. Authority flows
along existing lines and is never conjured from nothing. Draw the map, and you have drawn
exactly what every program can ever reach. That is the "geometry" in Capability Geometry:
security is the shape of the map, not a policy consulted at the door.

### Why the map needs a kernel underneath it

For the map to be trustworthy, something has to enforce it that cannot itself be talked
around. In a computer, the program that decides what every other program may touch is called
the kernel — the small core that sits between all software and the physical hardware. Most
kernels are very large, and a large program has bugs; a bug in the kernel can let a program
reach something the map says it should not.

One kernel, seL4, was built specifically to be small enough to prove correct. Its designers
wrote a precise mathematical description of what the kernel is supposed to do, then produced
a machine-checked proof that the actual code does exactly that and nothing else
[sel4-klein-2009-sosp]. "Machine-checked" means the proof is not an argument a reviewer
reads and nods at; it is verified line by line by a separate program built for the purpose,
in the way an accountant's totals can be re-added by a calculator rather than trusted on the
accountant's word. The proofs establish that the kernel enforces the capability map at all
times: a program cannot reach a resource it holds no key to, cannot forge a key, and cannot
retain a key after it has been revoked. The proofs rest on stated assumptions — that the
hardware behaves as specified, that the initial hand-out of keys at start-up was itself
correct — and they say nothing about the behaviour of software running above the kernel.
They are a proof about the lock, not about the tenant.

### Where this stands today

The token type that carries a permission through this platform is implemented and tested
open-source software, adopting the same terms the seL4 kernel itself uses for what a
permission opens and what it allows, and adding a lifetime, a renewal authority, and a place
in the auditable record described next.

The enforcement layer underneath is a direction, not a running service. No platform service
runs on seL4 today; the services that carry live traffic are ordinary programs on ordinary
operating systems. The platform's own seL4 work is a small number of standalone
demonstration programs, the most advanced of which brings up a virtual network card and
completes a single web request under emulation. The software above is written so that the
same code can eventually run inside a verified kernel, but the kernel-enforced version of
Capability Geometry is intended, not built.

## 4. A record anyone can check

### What a tamper-evident record is

A key answers "may this happen?" It does not answer "what was granted, to whom, and when?"
For that you need a record — and for the record to be worth anything, it must be one that
cannot be quietly rewritten after the fact.

The oldest tool for this is the bound ledger book with numbered pages. Entries are made in
ink, in order; nothing is erased; a correction is a new entry that refers back to the old
one. A missing page or an altered line is visible to anyone who inspects the book, because
the pages are numbered and the ink is permanent. A land title office works the same way: it
records each transfer of a property in sequence, and a buyer's lawyer can trace the chain of
ownership backward through the record without taking anyone's word for it.

Computers can make a stronger version of the numbered ledger using a tool called a
cryptographic hash. A hash is a fingerprint: a short, fixed-length string of characters
computed from any piece of data, such that changing even one letter of the data produces a
completely different fingerprint, and such that nobody can work backward from the
fingerprint to the data or construct a second piece of data with the same fingerprint. If
each entry in a ledger includes the fingerprint of the entry before it, then altering any
past entry changes its fingerprint, which changes the next entry's fingerprint, and so on
to the end — the tampering is visible in every entry that follows.

The construction this platform uses, called a Merkle tree, arranges the fingerprints so that
a single short fingerprint — the root — stands for the entire ledger. Two kinds of proof
follow from it. An inclusion proof shows that one specific entry is in the ledger that a
given root stands for, using only a handful of intermediate fingerprints rather than the
whole ledger. A consistency proof shows that a newer root stands for a ledger that merely
extends an older one — nothing before the old end was deleted, reordered, or altered. These
two proofs are the standardized machinery behind Certificate Transparency, the public system
that has policed the issuance of the web's security certificates since the mid-2010s, and
the current specification is RFC 9162 [rfc-9162]. This platform follows that specification's
algorithms directly.

One more piece is needed. A root fingerprint only means something if you know who vouches
for it. A digital signature is a seal that only the holder of a particular private key can
make, and that anyone holding the matching public key can check — like a wax seal whose
pattern everyone knows but whose stamp only one person owns. When the root of the ledger is
published together with the ledger's size and the signature of its owner, the result is a
signed checkpoint: a dated, sealed statement that "the record, as of this many entries, has
this fingerprint." The signed-checkpoint format this platform uses is a small public
specification maintained by a working group of transparency-log engineers
[c2sp-signed-note].

### Who holds the seal

Here is the part that distinguishes this design from a vendor's audit log. The private key
that seals the checkpoints is held by the customer. The vendor cannot produce a valid
checkpoint. Every permission the system honours carries an anchor to a specific checkpoint,
and the system refuses any permission whose anchor cannot be proven against a checkpoint the
customer sealed. The customer's own key is therefore the root of every authorization
decision — not because the vendor promises to consult it, but because a permission without
a provable anchor is refused by the same code that would honour a valid one.

This has an immediate consequence for auditors. An auditor is an independent professional
who examines a business's records and states whether they can be relied on; the word is
used here in that ordinary sense. To confirm that a particular permission was granted, an
auditor needs only the signed checkpoint, the permission, and its inclusion proof — not
access to the ledger itself, and not the customer's private key. To confirm that the ledger
has not been rewritten between two dates, an auditor needs only the two signed checkpoints
and a consistency proof. Neither check requires trusting the vendor, the customer, or the
computer the ledger runs on.

### Handing the whole system to a new owner

A sealed record whose seal belongs to the customer raises the natural question: what
happens when the customer changes? A business is sold; an operator retires; a property with
its systems passes to an heir. In a lookup-based system this is a migration project — new
accounts are created, old ones are closed, and there is an uncomfortable period when both
the old and new operators can act, with no independent record of exactly when control
passed.

This design makes the handover a ceremony recorded in the ledger it secures. The outgoing
owner seals a final ordinary checkpoint, then seals an entry revoking their own authority.
The next checkpoint is sealed by both the outgoing and the incoming owner together — two
seals on one statement, the way a safety-deposit box opens only with the bank's key and the
customer's key turned together. From the following checkpoint on, only the incoming owner's
seal is accepted; a checkpoint bearing only the old seal is refused, by the same logic that
refuses an expired permission. The transfer is one self-contained event in a public record.
There is no overlap window, and anyone examining the record can point to the exact entry at
which authority changed hands. This is tested behaviour, not aspiration: the complete
sequence, start to finish, is exercised directly by the software's own tests.

### What it costs

The check "is this permission's anchor valid against a sealed checkpoint?" has to happen
before every operation the system performs, so its cost decides whether the design is
practical. Verifying a seal outright is the expensive part of the two — it involves real
cryptographic arithmetic and takes a small number of milliseconds on ordinary server
hardware. The design's practical answer is to keep a small memory of the most recently
verified checkpoints: when a permission's anchor points to one already held in that memory,
the check is answered almost instantly instead, at a cost measured in nanoseconds rather
than milliseconds — several hundred thousand times faster — and the expensive verification
is skipped. In steady operation nearly every check is answered this way, and the costly
signature check runs only when the customer actually publishes a new checkpoint. We measured
this directly rather than assuming it, and the ratio is what makes checking every single
request against the record affordable rather than merely correct.

The record's cost of proving one entry among many also grows only slowly as the record
grows — the underlying mathematics guarantees this, and direct measurement confirms it holds
in practice. The durable, tile-based storage this design specifies for the record is a
direction, not a shipped component; today's measurements were taken against an in-memory
version of the same logic.

## 5. The machine as the holder of authority

### What a machine-held key is

A key is only as safe as the pocket it sits in. If the key to your system is a password, the
pocket is a human memory — and a human can be persuaded, over the phone or by a convincing
email, to read the password out to a stranger. The entire industry of remote credential
theft exists because the credential is something a person knows.

The alternative is to make the key something a specific machine holds and never reveals. In
public-key cryptography, a key comes in two halves: a private half that stays on the device
and is never transmitted, and a public half that can be given to anyone. The device proves
it holds the private half by producing a signature that only the private half could have
made; the other side checks the signature against the public half. The private key is never
typed, never sent, and never seen. There is nothing for a caller to talk a person out of.

Compare the bank's signature card once more, but now imagine the card holds not a
signature to be imitated but the pattern of a seal, and the seal's stamp never leaves your
desk. A forger who steals the card gains nothing — the card was always public. The only way
to forge your seal is to physically take your stamp.

### How a machine is admitted

Machine-based authorization on this platform grants access to a device's key rather than to
a person's password. A new device becomes known through a pairing ceremony that works like a
locksmith registering a new key with a building's owner: the device presents its public key,
the service shows it a short code and holds the request as pending, and an administrator,
reached by a separate channel, compares the same code and approves or denies. Approval binds
the key to the user. There is no password stored anywhere in the arrangement — a fact any
reader of the platform's own source can confirm. Revocation is exact: removing one machine's
key removes that machine's access without disturbing the same person's other devices or
resetting anyone else's credentials.

Pairing sits at the application boundary, independent of the network. Reaching a machine at
all requires membership of the platform's private encrypted network, which is one layer;
even a party that can reach the machine is refused at the application unless its key is
paired, which is the other. The two layers are granted by different mechanisms and held by
different people — which is what prevents whoever runs the network, the vendor included,
from thereby gaining access to the data running on it.

In the intended full arrangement, pairing is also where a machine's capabilities are minted:
approving a device would hand it the specific keys for the services it is permitted to
reach. That step is planned and not built. Two further present-tense limits belong here.
Host access over the public internet currently runs through an encrypted tunnel that does
not verify the identity of the server at the far end, so the promise that the vendor cannot
read a customer's data in transit is not delivered over that specific path until verified
two-way encryption lands. And what role a paired machine is recorded under is not yet an
enforced permission tier; what a paired machine may then do is governed by a separate
permission model.

## 6. What this changes for the owner

The immediate change is where authority lives. Under Capability Geometry the right to
operate your system is a key you hold and a record you seal. The vendor cannot lock you out
by losing, altering, or being compelled to surrender an account database, because there is
no such database in the path. A breach of the vendor's own systems does not yield a drawer
of every customer's signature cards; the vendor holds public keys, which were never secret.

The second change is what an outside party can verify. Due diligence — the examination a
buyer, lender, or regulator performs before relying on a business's records — today
requires taking the vendor's word about who had access to what. Under this design, an
examiner can be handed a signed checkpoint and a set of proofs and confirm the history of
authorization on their own desk, with no access to the live system and no trust in anyone
who operates it.

The third change is the handover. Selling the business, appointing a new operator, or
passing the system to a successor becomes a sealed ceremony in a public record — a single
event with a visible before and after, rather than a project with an overlap window.

The trade-offs are real and belong in the same paragraph. Holding the key means being
responsible for the key: lose the private key that seals your checkpoints and no vendor can
recover it for you, which is why key custody for an owner who is not a technologist is one
of the open questions below. A public record is public: what is sealed is a history of
permissions, not the contents of your records, but the shape of who was authorized to do
what is visible to anyone you give a checkpoint to. And the design's strongest property —
enforcement by a verified kernel — is the part not yet built, so today's guarantees are
properties of well-tested application code, not of the machine's core.

## 7. An open invitation

The composition in this paper is a position we hold with confidence and a set of problems we
do not claim to have solved. Several of them belong to specialist fields, and we would rather
work them with those specialists than around them.

To researchers in capability systems and formal methods: the token type adds an expiry time
and a renewal authority to a bare kernel capability. We have not proven that time-bound,
renewable capabilities preserve the confinement properties the kernel proofs establish for
capabilities without them, and we do not know whether that is a small extension of existing
proofs or a hard problem. We would welcome a collaboration that treats it as a question
rather than assuming the answer.

To transparency-log engineers: a customer-rooted log is a different creature from a
web-certificate log with a handful of large operators. A log with one owner and few
readers is exposed to the split-view attack, in which the owner shows different histories to
different parties; the standard defence is a network of independent witnesses who gossip
checkpoints to one another. What that witness ecosystem looks like when the log owners are
thousands of ordinary businesses rather than a few certificate authorities is an open design
question, and the answer determines how much the "anyone can check" claim is worth in
practice.

To specialists in hardware security and key custody: the owner this design serves may be a
retiree who holds a building and its systems, not an engineer. Where their sealing key
lives, how it is backed up, how it is recovered if the device holding it is lost, and how a
successor obtains it on the owner's death are questions with no purely technical answer. The
handover ceremony assumes both owners can act; the case where the outgoing owner cannot is
unsolved.

To auditors and records professionals: an inclusion proof is mathematically conclusive, but
it is not yet a recognised form of evidence in an audit standard or a courtroom. We would
value help understanding what an examiner would need — in documentation, in procedure, in
independent attestation — before a proof against a customer-sealed checkpoint could stand in
for the vendor's word in a professional opinion.

And to practitioners of usable security: the pairing ceremony is simple, but it still asks
two people to compare a short code over a separate channel. Whether that step holds up when
the person at the device is unfamiliar with computers, and whether it can be made simpler
without reopening the door it closes, is something we would rather learn from field study
than assume.

## 8. Conclusion

Authority over a system should be proven by a key its owner holds and a record anyone can
check, not looked up in a vendor's account database. Capability Geometry is our name for the
arrangement in which that is true: a permission that is a key rather than an entry in a
list, a public append-only record of every grant and revocation sealed by the customer, and
authority bound to an approved machine rather than a memorised secret. Two of the three
parts run today as tested open-source code; the third, kernel-level enforcement, is the
direction the code is written toward. The lookup table has been the shape of authority in
commercial computing for as long as commercial computing has existed. We hold that it is the
wrong shape for anything a person owns, and we intend to build the alternative.

## References

Klein, G., et al. 2009. seL4: Formal verification of an OS kernel. *ACM Symposium on
Operating Systems Principles.* [https://doi.org/10.1145/1629575.1629596](https://doi.org/10.1145/1629575.1629596)

Watson, R. N. M., et al. 2010. Capsicum: Practical capabilities for UNIX. *USENIX Security
Symposium.* [https://www.usenix.org/conference/usenixsecurity10/capsicum-practical-capabilities-unix](https://www.usenix.org/conference/usenixsecurity10/capsicum-practical-capabilities-unix)

Laurie, B., Messeri, E., and Stradling, R. 2021. *RFC 9162 — Certificate Transparency
Version 2.0.* Internet Engineering Task Force. [https://www.rfc-editor.org/rfc/rfc9162.html](https://www.rfc-editor.org/rfc/rfc9162.html)

C2SP working group. *signed-note — Signed checkpoint format for transparency logs.*
[https://github.com/C2SP/C2SP/blob/main/signed-note.md](https://github.com/C2SP/C2SP/blob/main/signed-note.md)

## Contributors

Prepared by Woodfine Management Corp.

## How this paper was produced

This paper is grounded in the preparing staff's own development and operating work, and in their standing engagement with the designers, software engineers, architects, engineers, and legal and accounting advisers the business works with. It was drafted and edited with AI assistance under editorial direction, and the analysis and conclusions are the author's own.

## Disclosures

Woodfine Capital Projects Inc. ("Woodfine") is the author of record. PointSav Digital
Systems, which builds the platform described, is currently a trade name of Woodfine,
planned to become a wholly-owned Woodfine subsidiary upon incorporation; PointSav does not
itself offer, sell, or solicit any security. The architecture described is our own; two of
the three components discussed are software we wrote, and the third is a design direction
we intend to pursue, so this paper argues for an approach we have a commercial interest in.
This work was funded internally; no external research funding was received. This paper's
content is provided for engineering, operational, and research purposes and does not
constitute investment advice or a solicitation to invest in any Woodfine direct-hold
solution. Some statements above describe planned or intended future work; language such as
"planned," "intended," "targeted," "may," and "expected" marks this forward-looking content,
which is subject to change and does not constitute a commitment regarding future
performance.

## Data and reproducibility

The specific figures behind this paper's claims — exact test counts, benchmark timings, and
source-line counts — are recorded in the platform's own engineering documentation rather
than restated here in full; this paper reports the shape of the results (tested; a several-
hundred-thousand-times speed difference between a cached check and a full signature check;
a small number of demonstration kernel programs) rather than an inventory of the
implementation. Two open-source software components carry the token type and the
record-checking logic described in Sections 3 and 4, both independently tested, with all
tests passing as of this paper's preparation; the timing figures were measured on ordinary
server hardware against an early release of the same components, and signature operations
of this kind are expected to run substantially slower on small embedded hardware. The
pairing component described in Section 5 stores no password anywhere in its data, which a
reader with access to its source can confirm directly. The code is open source, published
in full including its tests and performance measurements, under a license that requires
anyone who runs a modified version of it as a network service to publish their changes as
well. No independent party has audited this software, reproduced these measurements, or
reviewed these claims.

Capability Geometry™, PointSav Digital Systems™, MCorp™, and Woodfine Capital Projects™ are
trademarks of Woodfine Capital Projects Inc.
