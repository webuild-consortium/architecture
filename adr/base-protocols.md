# Baseline protocols

**Authors:**

- Leif Johansson, Sunet, Sweden
- Sander Dijkhuis, Cleverbase, the Netherlands
- Sarah Amandusson, Digg, Sweden

## Context
The EUDI Wallet ecosystem is mandated by eIDAS to ensure secure, interoperable cross-border digital identity.
This implementation is guided by the Architecture and Reference Framework (ARF), which translates legal mandates into technical specifications.
To achieve mandatory interoperability for Issuance and Presentation of Person Identification Data (PID) and Electronic Attestations of Attributes (EAA), implementing regulations require compliance with foundational standards.
OID4VCI (Issuance) and OID4VP (Presentation) are adopted as the ARF-recommended baseline protocols for technically implementing the required data models and transport mechanisms in the pilot.

## Decision

Each recognized role in the WE BUILD project - PID/LPID Providers, EAA Providers (including QEAA, Pub-EAA), Relying Parties, Wallet Providers, and Trust Service Providers — is REQUIRED to implement the corresponding technical profiles described here.
Actors performing multiple roles MUST meet all requirements relevant to those roles.

* PID Providers (including LPID) MUST implement [OpenID4VCI version 1.0](https://openid.net/specs/openid-4-verifiable-credential-issuance-1_0.html)
* EAA Providers (including QEAA, PuB-EAA) MUST implement [OpenID4VCI version 1.0](https://openid.net/specs/openid-4-verifiable-credential-issuance-1_0.html)
* Relying Parties MUST implement [OpenID4VP version 1.0](https://openid.net/specs/openid-4-verifiable-presentations-1_0.html)

## Consequences

Implementations following this profile ensure interoperability between actors within the WE BUILD ecosystem.
Actors can verify conformance through testing against other implementations.

## Advice

Once merged, this is our consortium’s decision. This does not mean all participants agree it is the best possible decision. In the decision making process, we have heard the following advice.
- yyyy-mm-dd, Name, Affiliation, Country: OK or summary of advice

