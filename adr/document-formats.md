# Specify digital document formats

**Authors:**

- Sander Dijkhuis, Cleverbase, the Netherlands

## Context

To issue PID, LPID, QeAA, PuB-eAA and eAA (“digital document” henceforth), it is necessary to specify a digital document format such as mdoc or a JWT-based one. While the EUDI implementing acts specify baseline standards, these specifications may not suffice for WE BUILD. For example, some specified standards need further profiling for interoperability. For some WE BUILD use cases, other standards may be necessary, for example to enable asynchronous interactions with EU Business Wallets, or to enable legal, technical and semantic interoperability with existing systems.

Several WP4 groups are stakeholders in this, for example:

- WP4 Architecture, for conformance to and efficient implementation of the EUDI framework
- WP4 PID and LPID Providers, for technical details of the provision of PID and LPID
- WP4 QTSPs, for technical details of the issuance and validation of QeAA
- WP4 Semantics, where the specification affects semantic interoperability

To ensure a streamlined process, the Mapping Task Force has evaluated the possible dependencies within WP4.

Out of scope of this evaluation were the dependencies with WP2 and WP3. After the use case stock taking, these should guide the decisions about formats made within WP4. If needed, the WP4 Architecture support teams can help gain input and feedback.

## Decision

The WP4 Architecture group specifies digital document formats.

The WP4 PID and LPID Providers and the WP4 QTSPs are expected to conform to these decisions.

The WP4 Semantics group delivers vocabularies, with mapping to the specified digital document formats.

## Consequences

This decision clarifies the decision process regarding digital document formats.

This decision creates an indirection between the vocabularies and the digital document formats, so that the extra translation is needed.

As an alternative, it has been considered to decide on WP4 Semantics specifying digital document formats, which would facilitate semantic interoperability, potentially at the cost of technical and legal interoperability. However, since these are cross-cutting decisions, the Mapping Task Force suggests that instead the WP4 Semantics group advices the WP4 Architecture group so that the latter sufficiently takes semantic interoperability into account.

## Advice

Once merged, this is our consortium’s decision. This does not mean all
participants agree it is the best possible decision. In the decision
making process, we have heared the following advice.

- yyyy-mm-dd, Name, Affiliation, Country: OK or summary of advice
