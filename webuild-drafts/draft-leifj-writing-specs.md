## WEBUILD Draft: guidelines for webuild drafts and specifications 

* Version: 1.0
* Authors: Leif Johansson <leifj@sunet.se>

# Abstract

This document contains a set of guidelines for the WeBuild specification series.

# Terminology

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119](#RFC2119).

# Background

The purpose of the WEBUILD project is to further the development of the EUID wallet ecosystem by piloting a set of use cases. The purpose of the WE BUILD specification series is to provide written guidance for implementers and deployers involved in those pilots.

# WeBuild Drafts

The WeBuild Draft series represent proposals under discussion. Each draft has a set of authors that own change control for the document in question. The authors are expected to consider all bona fide PRs presented on github for review and SHOULD process (either by accepting or rejecting) them in a timely fashion.

Discussion about PS should be done in the PR itself or in any associated issues.

# WeBuild ADRs

The WeBuild ADR series are accepted proposals and represent the consensus of the architecture work package.

# Publication process

A WeBuild ADR starts its life as a WeBuild Draft. When the workpackage leadership determines that consensus has been reached a Draft is ready to become an ADR. When a Draft is turned into an ADR it is assigned a sequence number by the workpackage leadership and published under the new name in the webuild-adr folder of the github repository. The original draft SHOULD be removed from the webuild-drafts folder when it is publised as an ADR.

Changes to existing ADRs MUST NOT be done unless the change represent the consensus of the workpackage. The work package leadership is responsible for making the determination of consensus. Changes to ADRs should be done by reviewing a PR representing the change. Anyone can open a PR against an ADR but only work package leadership can approve such PRs.

# Writing WeBuild Drafts

WebBuild Drafts (aka "drafts" below) are markdown documents placed in the webuild-drafts folder of the github repository. Drafts MUST identify authors, topic and SHOULD contain at least the following sections:

* Abtract: a short summary of the topic covered
* Background: introduction to the topic covered
* References: a list of references

In addition to these the author may structure the text in the best way to present the topic. 

Additionally, authors SHOULD include

* Security considerations 
* Privacy considerations

These should be included only if there are signifficant security and/or privacy considerations that are not covered by the main body of the text.

In general WeBuild drafts SHOULD profile existing standards and MUST clearly reference any standards referenced. Authors SHOULD avoid duplicating normative language from other specifications. The primary objective of a WeBuild draft should be to explain how existing standards apply to WeBuild, rather than creating new standards. 

If it becomes necessary to create completely new standards in WeBuild that work should happen in an existing standards-body and the work can then be referenced in a WeBuild draft.

# References

* <a href="RFC2119">RFC 2119</a>: https://datatracker.ietf.org/doc/html/rfc2119
