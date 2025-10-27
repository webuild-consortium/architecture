# ZKP-circuit optimized web tokens

* Version 0.1
* Author(s): Peter Altmann (peter.altmann@digg.se)

## Abstract

This document supports the adoption of ZKP-enabled attestations by presenting methods to reduce circuit complexity, thereby simplifying certification and auditing. Three approaches are outlined, each representing different trade-offs between protocol complexity and circuit auditability and certifiability.

## Background

Technical Specifications [TS4](https://github.com/eu-digital-identity-wallet/eudi-doc-standards-and-technical-specifications/blob/main/docs/technical-specifications/ts4-zkp.md) and [TS13](https://github.com/eu-digital-identity-wallet/eudi-doc-standards-and-technical-specifications/blob/main/docs/technical-specifications/ts13-zksnarks.md) under the ARF initiative focus on enabling Zero-Knowledge Proofs (ZKPs) for the European Digital Identity Wallet (EUDIW).

> **NOTE:** TS4 outlines the core approaches to ZKPs. One approach uses multi-message signatures with native ZKP support (expected to be detailed in TS14 using a BBS signature variant). The other, described in TS13, is based on circuit-defined ZKPs.

The high level requirements in Annex 2 are described first, followed by a background to TS13 and its focus on circuit-based approaches.

### High level requirements

Annex 2 outlines high-level requirements (HLRs) for ZKPs [here](https://github.com/eu-digital-identity-wallet/eudi-doc-architecture-and-reference-framework/blob/main/docs/annexes/annex-2/annex-2-high-level-requirements.md#hlrs--33). The most relevant are summarized below:

| REQ    | DETAILS                                                                                                                                                  |
|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| ZKP_01 | SHALL: ZKP of attribute value, expiration period, revocation check, key binding. SHOULD: Hide the provider.                                                     |
| ZKP_02 | SHALL: Prove possession of a specific attestation type.                                                                                                  |
| ZKP_03 | SHALL: Prove that two attestations share a common value. SHOULD: Prove binding of the attestation to a PID.                                             |
| ZKP_04 | SHALL: Request a user-unique secret attribute not revealed to the issuer. SHOULD: Enable pseudonym generation using a unique user ID and RP-specific context. |
| ZKP_06 | SHOULD: Generate proof of an already issued mdoc MSO or SD-JWT VC.                                                                                       |
| ZKP_08 | SHALL: Rely on standard algorithms.                                                                                                                      |
| ZKP_09 | SHALL: Support Level of Assurance (LoA) High.                                                                                                            |

Of the requirements listed, ZKP_04 presents a particular challenge without support for blind issuance. While some blind issuance schemes for ECDSA have been proposed (e.g., [2025/1827](https://eprint.iacr.org/2025/1827.pdf)), their applicability within TS13 remains uncertain. These approaches typically involve revealing all attributes except the user-unique secret in zero-knowledge, followed by the issuer performing a blind signature over the attestation.

ZKP_08 also presents challenges, as the standardization landscape for ZKP solutions is still rapidly evolving.

Additionally, this document addresses concerns related to ZKP_06, given that verifiable computation over formats such as mdoc MSO and SD-JWT VC is inherently complex.


### TS13 and circuit based approaches

A circuit-based approach currently under evaluation in TS13 is **longfellow-zk**, a zk-NARK based on the paper ["Anonymous Credentials from ECDSA"](https://eprint.iacr.org/2024/2010) with further details in the [IETF draft](https://datatracker.ietf.org/doc/draft-google-cfrg-libzk/).

Longfellow-zk does not require any changes to issuers, who can continue to issue attestations in formats such as mdoc MSO or SD-JWT VC. Users can then present a ZKP of valid signatures and attribute predicates, including equality, range proofs, and set membership for any subset of attributes in the original attestation. This adds a privacy-preserving layer to existing attestations, enabling fully unlinkable disclosures.

Some argue that a primary challenge with longfellow-zk is the complexity of the circuits when layered ontop of formats like mdoc MSO or SD-JWT VC. This complexity can hinder auditability and pose certification challenges, potentially creating barriers to adoption.

> **NOTE:** longfellow-zk was designed to minimize changes to issuer infrastructure and processes, optimizing performance within these constraints. The resulting circuit complexity is, in many ways, a consequence of these self-imposed limitations.

This document addresses these concerns by proposing ways to improve the auditability and certifiability of longfellow-zk circuits.

## Circuit complexity

longfellow-zk was designed to optimize performance when both SHA-256 and ECDSA are required, while avoiding changes to existing infrastructure or issuer workflows. This makes it an attractive privacy layer for formats like mdoc MSO or SD-JWT VC. However, these design constraints contribute to significant circuit complexity as the verifiable computation of formats like mdoc MSO and SD-JWT VC are non-trivial. As a result, there is a trade-off between minimizing issuer-side changes and achieving auditability and certifiability.

Since longfellow-zk is a circuit generation tool, there is substantial potential to reduce circuit complexity---particularly in the components validating attestation signatures and claim predicates. These reductions become more feasible if minor issuer-side modifications are acceptable, and if the set of supported features on the attestation side is constrained.

To optimize longfellow-zk circuits for auditability, it is important to understand the factors that make verifiable computation non-trivial.

### Sources of complexity

The following are among the sources of circuit complexity that can be targeted for optimization:

* Field depth
* Field type variability
* Format variability
* Variability in the number of claims
* Predicate diversity
* Decoding logic
* Dynamic control flows (e.g., optionality, conditional branching, interactions)
* Multi-field approaches requiring witness binding

> **Note:** Circuit complexity, in this context, does not refer to metrics like constraint count or gate depth typically used in performance evaluation. Instead, it denotes factors that make a circuit difficult to audit and certify. These factors are not well defined.

This document proposes three optimization strategies, each aligned with different levels of tolerance for issuer-side changes. This reflects the current uncertainty in the trade-off between auditability and the extent to which infrastructure or issuer processes can be modified.

1. **Optimized layering of current longfellow-zk:**
   Prioritizes minimal disruption to issuers. Suitable when certification and audit complexity are more acceptable than changes to attestation issuance. Focuses on adapting SD-JWT VC with minimal modifications.

2. **ZKP-optimized SD-JWT VC:**
   Targets significant circuit simplification. Assumes issuers are open to moderate changes, allowing the SD-JWT VC format to be streamlined for ZKP circuit friendliness.

3. **ZKP-optimized Web Token (ZWT):**
   Proposes a purpose-built format extending the ideas in (2), optimized explicitly for ZKP support and minimal circuit complexity.

> **Note:** mdoc MSO is not included in the optimization proposals. While certain techniques (such as a modified proof structure) could be adapted, the extent of required changes is substantial. This likely offsets any benefits of reusing the format compared to SD-JWT VC or a purpose-built alternative.

Each of the ideas are explored next.

### Minimally Disruptive SD-JWT VC Issuance

The SD-JWT VC specification permits several optimizations that can be applied without requiring changes on the issuer side:

1. **No `_sd` field:**
   The inclusion of digest values (`_sd`) is optional. Omitting it significantly improves performance and eliminates the need for multiple fields and, consequently, witness consistency tests.

2. **No `cnf` or KB-JWT:**
    A key insight is that the prover presents a proof of a verifiable computation over the presentation and **not** the SD-JWT VC itself. As a result, `cnf` and KB-JWT are not required for specification compliance. Their omission eliminates the need for token nesting and simplifies proof-of-possession logic. Instead, PoP is done using a new attribute `zk_cnf` that replicates `cnf` but uses a flat structure.

3. **Limited predicates**
   Initially focusing on simple predicates (e.g., equality and range) allows for simple and auditable circuit implementations. Most use cases can be supported this way. Range predicates (e.g., for age or expiration checks) can be added incrementally as circuits are audited.

4. **Issuer-specific circuits:**
   Supporting issuer-specific canonical JSON simplifies parsing and reduces variability, thereby minimizing circuit complexity.

The primary trade-off in this approach is that reducing circuit complexity often requires fixed structures (e.g., default values for unspecified attributes). This increases the size of the SHA-256 input blocks, which can degrade performance.

A pragmatic mitigation is to restrict ZKP usage to attributes where disclosure carries low re-identification risk. For example, it is generally unnecessary to prove knowledge of uniquely identifying values (e.g., national ID numbers) using ZKPs.

### ZKP optimized SD-JWT VC

The ZKP optimized SD-JWT VC applies the above optimizations but targets a few additional ones. Specifically, it introduces an inner-proof + outer-proof approach where the longfellow-zk circuit verifies only the issuer signature over the witness (inner-proof), and where the verifier uses an issuer signed commitment to validate user attributes (outer-proof). This way, most of the complexity sources are moved outside of the circuit to where they are much easier to audit and certify. Concretely, we now do the following:

1. Reduce the number of user attributes that the circuit needs to handle to one. This single one is an issuer signed Pedersen commitment, $C$, of either:
    * Attribute values. Here $C = H_0 + m_1H_1 + ... + m_n H_n$
    * Polynomial coefficients. Here $C$ is computed based on polynomial coefficients of the polynomial that allows for claims inclusion tests.
2. Use fixed length and type data fields in a mimimal SD-JWT VC that includes only the following (three SHA256 blocks):
    * 32 byte Pedersen commitment
    * 65 byte `zk_cnf` claim for user PoP
    * 5 byte of expiration information
    * 16 byte of token identifier for revocation
3. Use RFC 7797 for un-encoded payload. This may be an option to consider to avoid decoding.

### ZKP optimized web token (ZWT)

This approach builds on the ZKP-optimized SD-JWT VC, but introduces a compact, purpose-built attestation format—conceptually similar to a TCP header.

An example of such a format could use the following fixed-size byte encoding:

- **64 bytes**: Pedersen commitment
- **64 bytes**: Uncompressed proof-of-possession (PoP) key
- **5 bytes**: Expiration data
- **32 bytes**: Token identifier (used for revocation)

The total payload fits within three SHA-256 blocks, maintaining acceptable performance for circuit evaluation.

Additional proposals include the use of 9-bit bytes to enable features such as single-byte keys, escape characters, and extended encoding schemes. This can simplify circuit logic as MSB tagging is relatively easy. But it will likely not be useful if we can agree on a commit-and-prove model.
