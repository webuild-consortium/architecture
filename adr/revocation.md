# Revocation Method

**Authors:**

- George Fourtounis, GRNET, Greece

## Context

The EU Digital Identity Wallet (EUDI Wallet) follows the
issuer–holder–verifier model, to ensure user privacy and control of
their data. In this model, the issuer issues a credential bound to the
user (holder). This credential can then be presented to any verifier
without notifying the issuer, thus offering privacy and resistance
against monitoring user activity.

Credential issuance should also be matched with credential
revocation. Credentials expire, become obsolete, or are made invalid
in case of e.g., wallet deletion, security breaches, signing
certificate invalidation, or business logic upgrades. Revocation is
thus a necessary feature of issuance but has been problematic:

- Revocation must happen in the issuer but then propagate to the
holder wallet, making the latter less standalone, effectively
depending on the issuer during the credential lifetime. Moreover, the
timing of this propagation may be a further compromise to user
privacy.

- Revocation information must be available to the verifier,
introducing an information path between the issuer and the verifier,
clashing with the privacy requirements of the EUDI Wallet.

- Holding revocation information for too many documents can be a
technical challenge. For example, it can be too big to store locally
for some mobile verifiers.  Holders may object to revocation or wish
to be able to present revoked documents in particular scenarios.

- Wallet instances are registered in the wallet provider and can also
be revoked, a feature that interacts with PID revocation.

[Version 2.7.0 of the Architecture and Reference
Framework](https://eudi.dev/2.7.0/architecture-and-reference-framework-main/#6637-relying-party-verifies-that-the-pid-or-attestation-is-not-revoked)
defines "status lists" or "revocation lists", which can be used to
look up the revocation status of a credential.

The [Token Status List specification
(TSL)](https://datatracker.ietf.org/doc/draft-ietf-oauth-status-list/)
addresses revocation. TSL describes status lists that can be used with
JOSE/COSE token formats (which correspond to SD-JWT-VC/mdoc credential
formats).

TSL was chosen by
[EWC](https://eudiwalletconsortium.org/wp-content/uploads/2025/10/EWC-D3.1-List-of-available-compliant-wallets-in-EWC-and-documentation.pdf)
and was used by LSPs (e.g. by POTENTIAL in the UC4 Berlin Interop
Event.

The [EUDIW reference
implementation](https://github.com/eu-digital-identity-wallet/) also
supports TSL.

## Decision

The TSL (draft 13) MUST be used to implement status lists when revocation is
required (e.g., in long-lived credentials).

## Consequences

### Advantages

- Revocation is standardised for cross-border interoperability tests.

- Wallet providers that are using the reference implementation do not
  have to retrofit another revocation solution on that existing
  codebase.

### Disadvantages

- Privacy is not as good as revocation using Zero-Knowledge Proofs
  ([currently under discussion in the
  ARF](https://github.com/eu-digital-identity-wallet/eudi-doc-architecture-and-reference-framework/blob/main/docs/discussion-topics/g-zero-knowledge-proof.md)). A
  future ADR should address such a feature when it becomes available.

- There is tension between this method of revocation and short-lived
  credentials, which are available for 24 hours and may not be subject
  to revocation. There are cases where short-lived credentials require
  revocation (which is not clear how to do in this specification).

## Advice

Once merged, this is our consortium’s decision. This does not mean all
participants agree it is the best possible decision. In the decision
making process, we have heard the following advice.

- yyyy-mm-dd, Name, Affiliation, Country: OK or summary of advice
