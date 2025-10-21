# Publish consortium trusted lists

**Authors:**

- Sander Dijkhuis, Cleverbase, the Netherlands

## Context

For the first usage of the interoperability testbed, and for the first increment, it is required to enable trust between issuers, wallets, and verifiers. EWC proposed a trust evaluation mechanism (see [EWC RFC 012](../ewc-rfcs/ewc-rfc012-trust-mechanism.md)) including an [Trusted List](https://github.com/EWC-consortium/ewc-trust-list).

As part of the Mapping Task Force, we’ve found that at least the QTSP group needs a similar approach for the first QEAAs to test. We need to specify who provides this.

At ETSI, the TS 119 612 series is being updated to support the European Digital Identity. This may require changes to the trust mechanism.

## Decision

The WP4 Trust Registry Infrastructure group provides trusted lists.

The issuers in the WP4 PID/LPID/QTSP/Wallet provider groups request registration on the trusted lists before testing.

The wallets in the WP4 Wallet provider group include validation with the trusted lists in their verification processes.

The relying parties in WP2/3/4 include validation with the trusted lists in their verification processes.

The starting point is EWC RFC 012. If changes are needed, these will be specified in new ADRs, potentially referencing new WE BUILD Drafts.

## Consequences

This decision makes interop between consortium members easier.

This decision makes it harder to test with ad-hoc pairwise trust relationships.

To address the risk of bottlenecks in implementing this decision, the Mapping Task Force pays extra attention to potential blockers for each involved WP4 group.

## Advice

Once merged, this is our consortium’s decision. This does not mean all
participants agree it is the best possible decision. In the decision
making process, we have heard the following advice.

- yyyy-mm-dd, Name, Affiliation, Country: OK or summary of advice
