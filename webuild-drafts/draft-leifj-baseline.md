# Baseline implementation profile for WE BUILD

** Authors: **
 - Leif Johansson <leifj@sunet.se>

## Abstract

This note specifies the baseline implementation profile for WE BUILD particpants.

## Normative language

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL
NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and
"OPTIONAL" in this document are to be interpreted as described in
RFC 2119.


## Roles and Interoperability Requirements

The following roles are recognized in the WE BUILD project:

* Issuers
* Wallet Providers
* Verifiers (aka Relying Parties)
* Trust Service Providers

Each role is REQUIRED to implement the set of technical profiles described in this note. Actors that provide multiple roles are REQUIRED to implement all requirements for all such roles. Each actor MUST demonstrate interoperability with at least two other actors for relevant roles. For instance; an actor providing a Wallet MUST demonstrate interoperability with issuers belonging to at least one other Actor to be deemed interoperable.

This document provides an implementation profile, not a deployment profile. This means that an implementation MAY choose to provide mechanisms for turning on and off features in a way that makes it possible for a single instance of a software component (eg an issuer) to provide only a subset of the implementation profile at a given time. For instance a verifier component MUST implement support for mutually exclusive specification A and B but may choose to only support A for a given set of tests.

## Implementation Profile

In brief:

* All roles MUST implement validation of X509 credentials using ETSI TS 119 612
* Issuers MUST implement OpenID4VCI version 1.0
* Verifiers MUST implement OpenID4VP version 1.0
* Trust Service Providers MUST provide signed trust status list based on ETSI TS 119 612 v2.3.1 (2024)

TODO: add more normative language about trust status validation and publication OR reference future draft based on EWC RFC012

## References

[OpenID4VCI] https://openid.net/specs/openid-4-verifiable-credential-issuance-1_0.html
[OpenID4VP] https://openid.net/specs/openid-4-verifiable-presentations-1_0.html
