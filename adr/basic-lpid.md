# Provide LPID as a stable minimal basis

**Authors:**

- Sander Dijkhuis, Cleverbase, the Netherlands

## Context

In BU3 on foreign tax declaration, an issue on [Identifiers in LPID](https://portal.webuildconsortium.eu/group/5/files/3645/collabora-online/edit/974) was raised to WP4 Architecture. In this context, LPID is *legal person identification data*. Should the LPID just be a “bootstrap identity” with a stable minimum attribute set, or should LPID be a “dynamic reference framework” containing many relevant attributes registered by competent bodies?

In the Annex of [(EU) 2024/2977](https://data.europa.eu/eli/reg_impl/2024/2977/oj), Table 3 specifies mandatory PID for the legal person in line with the “bootstrap identity”, and Table 4 specifies optional PID for the legal person that leans more towards the “dynamic reference framework”.

The implementation choice affects what other electronic attestations of attributes may be needed for use cases such as BU3.

Under EU Digital Identity, EU Member States may take different decisions with regard to this. The upcoming EU Business Wallet legislation may affect these decisions.

To achieve cross-border interoperability within WE BUILD, several options are possible:

- basic LPID everywhere (minimum attributes from a single source)
- extended LPID everywhere (attributes such as the VAT registration number)
- basic LPID in some EU Member States, extended LPID in others

## Decision

Rely on basic LPID everywhere. Develop use cases under the assumption that other attributes require additional electronic attestations.

## Consequences

With this decision, it becomes easier to reason about the minimum set of additional electronic attestations.

With this decision, it becomes more difficult to test the extended LPID case, which may be relevant to some EU Member States. But note that the decision does not preclude testing with extended LPID as well.

To manage the risk that this approach differs from EU Business Wallet legislation, WE BUILD should take the definition of LPID in account in its upcoming definition of an EU Business Wallet.

## Advice

Once merged, this is our consortium’s decision. This does not mean all
participants agree it is the best possible decision. In the decision
making process, we have heard the following advice.

- yyyy-mm-dd, Name, Affiliation, Country: OK or summary of advice
