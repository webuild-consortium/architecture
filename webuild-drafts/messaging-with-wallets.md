# WE BUILD Draft: Messaging with European wallets

**Authors:**

- Sander Dijkhuis, Cleverbase, the Netherlands

## Context

European Digital Identity and Business Wallets have well-defined interfaces and protocols for interactive processes, such as document issuance and presentation over the Web.

However, several WE BUILD require system-to-system message interchange on behalf of natural or legal persons, that is not necessarily interactive. This technical report describes how to leverage existing European infrastructure to support these use cases. It ends with proposed next steps to manage related general cross-border interoperable capabilities within WE BUILD.

Example use cases include:

| Example | Description                                                                                                                                      |
| ------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| BU1     | Issuance of business eAttestation of attributes                                                                                                  |
| BU3     | Attribute verification at public sector authentic sources                                                                                        |
| BU6     | Government-to-government data sharing ([Once-Only](https://ec.europa.eu/digital-building-blocks/sites/spaces/OOTS/pages/565379323/OOTSHUB+Home)) |
| SC5     | Invoicing and procurement                                                                                                                        |
| N/A     | Government-to-business notifications (EUBW area of focus)                                                                                        |

## Requirements

Always:

- Sender identification with a high level of confidence.
- Recipient identification with certainty before delivering the data.
- Protection of the integrity and confidentiality of data.
- Interoperability and freedom of choice: sender and recipient may choose their own implementation.
- European governance of standards.

In some cases:

- Timestamped evidence of delivery events in case of disputes.
- High availability of infrastructure, even if the sender or the recipient is unavailable.

## Applicable standards

### eDelivery stack

The [eDelivery](https://ec.europa.eu/digital-building-blocks/sites/spaces/DIGITAL/pages/467110114/eDelivery) building block in the Digital Europe programme consists of technical specifications and open source reference implementation, and is applied under various EU regulations and global networks such as [Peppol](https://peppol.org/). This section describes several characteristics.

The eDelivery specifications include interoperability profiles of several standards for information interchange:

| Global standard  | Free-of-charge source                                                                                                                  | Topic                            |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------- |
| ISO 15000-1:2021 | [OASIS ebMS v3.0](https://docs.oasis-open.org/ebxml-msg/ebms/v3.0/core/os/ebms_core-3.0-spec-os.html)                                  | Core features                    |
| ISO 15000-2:2021 | [OASIS AS4 profile v1.0 of ebMS v3.0](https://docs.oasis-open.org/ebxml-msg/ebms/v3.0/profiles/AS4-profile/v1.0/AS4-profile-v1.0.html) | HTTP-based interface             |
| ISO 15000-3:2023 | [OASIS ebXML RegRep v4.0](https://www.oasis-open.org/standard/ebxmlregrep/)                                                            | Registry and repository messages |
| ISO 15000-5:2014 | [UN/CEFACT-CCTS v3.0](https://unece.org/trade/documents/2009/09/uncefact-core-components-technical-specification-version-30)           | Common semantics                 |
Typically, eDelivery is explained in a four-corner model, such as in this example which connects two wallet instances:

```
 Corner 1            Corner 2              
┌─────────┐         ┌─────────┐            
│Sender   │ ──────► │Sender   │ ─────┐     
│EU wallet│         │access   │      │     
│instance │         │point    │      ▼     
└─────────┘         └─────────┘  ┌────────┐
                          │      │Common  │
                eDelivery │      │services│
                          ▼      │        │
┌─────────┐         ┌─────────┐  └────────┘
│Recipient│         │Recipient│      ▲     
│EU wallet│         │access   │      │     
│instance │ ◄────── │point    │ ─────┘     
└─────────┘         └─────────┘            
 Corner 4            Corner 3              
```

In eDelivery, the C2-C3 interaction is standardised, and supports several message exchange patterns (see [illustrations by IBM](https://www.ibm.com/docs/en/wm-b2b?topic=agreements-message-exchange-patterns)): one-way/push, one-way/pull, two-way/sync (i.e. HTTP request-response), two-way/push-pull, two-way/push-push. Between submission and retrieval of messages, the access points can store them. This enables dealing with various expectations about availability of the sender, the recipient, and their access points. For example, while some natural or legal persons may be able to deploy a highly-available access point server for inbound HTTP requests, others may just be able to make outbound HTTP requests using a client with limited internet connectivity.

This is a similar issue as addressed in DC4EU for document issuance with the [Datastore REST API](https://github.com/dc4eu/vc/blob/main/standards/api_specification.md). However, where the Datastore REST API requires a centralised service provider for both sender and recipient, the 

The C1-C2 and C3-C4 interactions are not standardised in eDelivery. Example interfaces are:

- [OpenID4VC](https://openid.net/sg/openid4vc/) when the access point is at an eAA Provider
- national government information exchange standards, such as [Digikoppeling](https://www.logius.nl/onze-dienstverlening/gegevensuitwisseling/digikoppeling) for the Dutch government
- HTTP-based API when the access point has a web server
- [Webhook](https://en.wikipedia.org/wiki/Webhook)-based API when the recipient has a web server
- local software APIs when the access point is part of the wallet instance

The user messages over C1-C2 and C3-C4 do not need to have the same document format as the messages over C2-C3. That is, the sender and recipient may trust their access points to perform translation while assuring that the meaning is preserved.

Various interfaces and protocols apply to the common services. For example, [Once-Only common services](https://ec.europa.eu/digital-building-blocks/sites/spaces/OOTS/pages/615481586/Common+and+Supporting+services) provide an ISO 15000-3 RegRep interface.

## eDelivery as a trust service

Under [eIDAS (EU) 910/2014](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A02014R0910-20241018), Art. 3(16) defines as trust services:

> (k) the provision of electronic registered delivery services;
> (l) the validation of data transmitted through electronic registered delivery services and related evidence;

And Art. 3(36) defines the electronic registered delivery service (eRDS), which can be qualified (QeRDS):

> ‘electronic registered delivery service’ means a service that makes it possible to transmit data between third parties by electronic means and provides evidence relating to the handling of the transmitted data, including proof of sending and receiving the data, and that protects transmitted data against the risk of loss, theft, damage or any unauthorised alterations;

So the eRDS provider provides:

1. an access point as a service to senders or recipients;
2. relevant evidence, for example to other access points.

In Art. 43 the legal effect of eRDS and QeRDS is specified:

 > 1. Data sent and received using an electronic registered delivery service shall not be denied legal effect and admissibility as evidence in legal proceedings solely on the grounds that it is in an electronic form or that it does not meet the requirements of the qualified electronic registered delivery service.
 > 2. Data sent and received using a qualified electronic registered delivery service shall enjoy the presumption of the integrity of the data, the sending of that data by the identified sender, its receipt by the identified addressee and the accuracy of the date and time of sending and receipt indicated by the qualified electronic registered delivery service.

In Art. 44 the requirements for QeRDS are specified, where compliance is presumed for QTSPs which conform to [(EU) 2025/1944](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=OJ:L_202501944), which is based on the ETSI EN 319 522 set of standards.

So this means that implementers can choose between:

- self-provided eDelivery access
- eDelivery access through a non-federating service provider
- eDelivery access through a federating trust service provider
- eDelivery access through a qualified trust service provider

### Alternatives considered

[OpenID4VC](https://openid.net/sg/openid4vc/) and [ISO/IEC 18013-7](https://www.iso.org/standard/91154.html) also provide messaging to and from wallets, but only in the case of “verifiable credentials”, and the protocols are optimised for interactive connections.

[DIDComm](https://identity.foundation/didcomm-messaging/spec/v2.1/) also provides messaging between wallets, but not using EU standards.

Alternatively, use cases could specify ad hoc APIs between the systems of various natural and legal persons. However, this means that each ad hoc API brings additional work of specifying connectivity and security requirements, and dealing with technical challenges that are already solved with eDelivery.

## Architectural challenges

The following challenges may need to be addressed by WP4 groups.

### Interoperability profiles

There are several interoperability profiles, such as eDelivery v1 (adopted by Once-Only and Peppol), eDelivery v2 (specified by the Commission), ETSI EN 319 522-4-1 (potentially different from eDelivery v1 and v2, under revision in STF 705), [OpenPeppol eDEC Specifications](https://docs.peppol.eu/edelivery/). Even the profiles may contain too many degrees of freedom for efficient implementation in WE BUILD.

### End-to-end security

With EU wallets, natural and legal persons obtain means for authentication and encryption at C1 and C4. While eDelivery specifies C2-C3 end-to-end authentication and encryption at the message delivery layer, EU wallets provide natural and legal persons with means for C1-C4 end-to-end security. Especially the interchange of (sensitive) personal data or economic data prone to fraud or theft may benefit from standardising this on the message payload layer.

### Access point service APIs

When the access point is provided as a service, interoperability across service providers may be desirable to avoid vendor lock-in. Similar to the [Cloud Signature Consortium API](https://cloudsignatureconsortium.org/resources/download-api-specifications/), this could be provided using an OAuth-protected HTTP/JSON API to which EU wallets can implement a client. At the moment of writing, no such standardisation initiative is known. The [Domibus WS Plugin](https://docs.edelivery.tech.ec.europa.eu/domibus/5.1.9/#wsplugin) interface could be a starting point.

### Open interop network

The two most common interop networks are Once-Only (only accessible to EU Member States) and Peppol (only applicable for eProcurement). To support more use cases, such as registered eDelivery use cases, either one of these networks could be extended, or a separate network could be put in place. This includes putting in place trust registry infrastructure (e.g. public key infrastructure) and service metadata locator functionality.

## Next steps for WP4

For proper interoperable connectivity between WE BUILD consortium partners, WP4 needs to take some focused action towards a common eDelivery implementation. Below are suggested components that the WP4 groups can take into their tasks and deliverables.

- **WP4 Architecture**
	- Raise awareness at WP2/WP3 use cases and WP4 groups about the ability to include four-corner eDelivery models in their specifications.
	- Decide on the application of eDelivery to common architectural patterns, e.g.:
		- communication between PID and eAA Providers and authentic sources, leveraging the ETSI TS 119 478 interface based on ISO 15000;
		- communication with and between EU Business Wallets;
		- communication with voluntarily enrolled EU Digital Identity Wallet users.
	- Specify a common C2-C3 interoperability profile for eDelivery.
- **WP4 Trust Registry Infrastructure**
	- Provide eDelivery common service for use within WE BUILD.
	- Govern access of eDelivery implementations to the common WE BUILD network.
- **WP4 Semantics**
	- Govern semantic models based on ISO 15000-5.
- **WP4 QTSPs**
	- Specify a common C1-C2 and C3-C4 interoperability profile for eDelivery services.
	- Provide generic eDelivery services to all WP2/WP3 use cases and to WP4 PID/LPID/Wallet Providers.
	- Raise awareness at WP2/WP3 use cases about considerations for using qualified versus non-qualified eDelivery.
- **WP4 Testing**
	- Support cross-provider and cross-border testing of eDelivery implementations.
- **WP4 Wallet Providers**
	- Implement eDelivery in EU Business Wallets, relying on the WP4 QTSPs for efficiency.
- **WP4 PID/LPID Providers**
	- Implement eDelivery for access to authentic sources for natural and legal person registries.
