# Pseudonyms for the EUDI Wallet

## Background

Pseudonyms are addressed in the legal framework. Their use is permitted when user identification is not required (see Regulation 2024/1183, Articles 5 and 5b.9), and pseudonym management is a mandatory EUDI Wallet function (Article 5a.4(b)). Additionally, CIR 2024/2979 Article 14 mandates compliance with Annex V, which specifies WebAuthn, and requires support for site-specific pseudonyms.

Two primary concerns arise with CIR 2024/2979 as written: the first is a syntactic ambiguity in Article 14(2); the second is the mandated use of WebAuthn.

## Ambiguity in Article 14

Article 14 Point 2 states:

> Wallet units shall support the generation, **upon the request of a wallet-relying party**, of a pseudonym which is specific and unique to that wallet-relying party and provide this pseudonym to the wallet-relying party, either standalone or in combination with any person identification data or electronic attribute attestation requested by that wallet-relying party. [emphasis added]

This provision contains a syntactic ambiguity due to the placement of “upon the request of a wallet-relying party.” It is unclear whether pseudonym generation is conditional or if site-specificity is conditional. Neither interpretation is satisfactory without mature (possibly ZKP) mechanisms that allow the wallet to generate pseudonyms autonomously and verifiably.

Thus, pseudonym generation likely requires a trusted service or limiting the functionality of pseudonyms and forcing reuse across sites. No implementation guidance is currently available to resolve tradeoffs and guide optimization efforts. Therefore, clarification of Article 14 is necessary. In the interim, the following clarifications are proposed:

* Pseudonym generation may occur prior to any RP request.
* The user can choose whether to present a site-specific pseudonym.
* The RP may request a site-specific pseudonym, that the wallet must be able to present.
* No single pseudonym mechanism can satisfy all use case requirements. Consequently, either multiple pseudonym constructions must be supported, or an interim solution must be adopted until suitable ZKP-based approaches become viable.
* User chosen reuse of pseudonyms is acceptable.

WebAuthn related concerns are explored next.

## WebAuthn

A second concern is the mandated use of WebAuthn. A detailed critique of its unsuitability for pseudonym use is available [here](https://github.com/eu-digital-identity-wallet/eudi-doc-architecture-and-reference-framework/discussions/375#discussioncomment-13638807). The core problem is that WebAuthn is an authentication protocol and not a pseudonym solution. Binding pseudonyms to the authentication mechanism adds unnecessary complexity and is hard to reconcile with emerging ZKP based solutions.

Despite this, WebAuthn is referenced in the implementing acts as the mechanism for enabling pseudonym functionality. However, technical details are undefined, and no coherent mapping exists between WebAuthn semantics and pseudonym requirements.

One proposed workaround involves linking a WebAuthn credential to a PID during registration. The user first registers with a PID, then provisions a WebAuthn public key for passwordless login. The RP may associate a local identifier with the key and is expected to delete PID-related data. It is unclear why deletion is required rather than requiring presentation of a minimal or empty PID. A potential benefit of this model is that passkeys could be registered independently of the wallet.

In any case, public-key-based pseudonyms are ill fit for a long-term pseudonym solution. The remainder of this text focuses on alternative approaches.

## Alternatives to Explore in WeBuild

One alternative models pseudonyms as disclosable attributes in issuer-signed attestations. "Disclosable" may refer to either direct representations (e.g., salted digests) or zero-knowledge predicates. This section outlines two concrete proposals based on conventional cryptography (explained also here). Both using a high-entropy pseudonym seed (`nym_seed`) and a pseudonym generation pseudorandom function `F()`, keyed with `nym_seed`. A third option based on zero-knowledge proofs (ZKPs) is also considered.

The objective is to evaluate each approach empirically to assess how theoretical tradeoffs manifest in real-world use cases.

### Alias-based pseudonyms

In the alias-based model, pseudonyms are not site-specific by default. Instead, users select an alias, which determines the disclosed pseudonym during presentation. The wallet maintains two internal mappings:

1. Alias → index / pseudonym value
2. Alias → Relying Party (service)

Pseudonyms are computed as `F(key=nym_seed,data=index)`. With an issuer managed `nym_seed`, the issuer can precompute a bounded array of such values. During presentation, the user selects an alias, and the wallet discloses the corresponding pseudonym.

Properties:
* Requires no new ecosystem actors or protocol changes.
* May support ban evasion resistance (will likely require fixing an index and forcing pseudonym reuse).
* Pseudonym reuse is user-controlled.
* Limited by the number of pre-issued pseudonyms; reuse becomes unavoidable.

The alias-based approach minimizes disruption but is limited by the number of pre-issued pseudonyms and does not scale well for high-privacy scenarios. It is less functional but operationally simple.

### Directed pseudonyms

In the directed model, pseudonyms are specific to each RP and computed as `F(nym_seed,rp_identifier || context)`. This directionality improves unlinkability but introduces privacy and architectural tradeoffs:

* If the issuer generates the pseudonym, it must do so at presentation time, exposing the target RP and increasing operational complexity.
* If a separate pseudonym service performs generation, it learns the target RP and disclosed attributes but not the user’s identity.

The pseudonym service can issue a signed pseudonym attestation that includes:

* The RP-specific input (identifier + context).
* The resulting pseudonym value.
* A reference to the source PID.

The pseudonym attestation can be presented either to the issuer for inclusion in the PID (requires slight changes to issuance flows and issuer availability during presentation) or directly to the RP alongside the PID in a combined presentation.

Properties:

* Enables strong unlinkability and site-specificity.
* Supports advanced use cases like ban evasion resistance.
* Requires new roles (e.g., pseudonym service) and support for combined or multi-round presentations.

The directed approach enables robust pseudonym guarantees but requires additional infrastructure and coordination, complicating deployment.

### ZKP-based Pseudonyms

ZKP-based models offer flexible support for pseudonym semantics. Both circuit-based and commitment-based constructions are possible, enabling:
* Site-specificity
* Ban evasion resistance
* Optional re-identification
* Total unlinkability

This remains an active research area. While high-level requirements are well understood, practical instantiations are still under development. ZKP-based pseudonyms are likely the most complete and future-proof and thus well worth considering.
