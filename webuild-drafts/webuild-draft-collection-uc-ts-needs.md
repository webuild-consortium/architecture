## WE BUILD Draft: Collection of use cases' needs in terms of QES/QEAA 

* Version: 0.1  
* Authors: Sander Dijkhuis (sander.dijkhuis@cleverbase.com), Iris van der Wel (iris.van.der.wel@cleverbase.com), Svilena Rakshieva (svilena.rakshieva@evrotrust.com)

# Abstract

This document announces the approach by the QTSP group for collecting WE BUILD user stories and use case needs related to Qualified Electronic Signatures and Seals (QES) and (Qualified) Electronic Attestation of Attributes (QEAA). We suggest other WP4 groups to also consider this template.

# Background

The purpose of the WE BUILD project is to further the development of the EUDI wallet ecosystem by piloting a set of use cases. In order to support the stocktaking, specification and development of trust services in the WE BUILD use cases, and more specifically in terms of QES/QEAA at this stage, the QTSP group is collecting insights and feedback on what the use cases' needs will be.

The purpose of the collection of QES and QEAA user stories and needs with the templates, particularly in the earlier phases of WE BUILD, is to:
- Gather insights from group members on trust services in use cases.
- Share knowledge with use cases regarding the possibilities of trust services.
- Prepare for the roadmap of the QTSP group.

This document introduces the the approach by the QTSP group for capturing both QEAA/QES user stories and needs.

# Collection of use cases' needs

Input for user stories and needs is collected in two tables. These tables can be reused by using the following columns in the preferred format specified to the considered service.

1. **User stories QES/QEAA**  
   This table captures use cases in the form of user stories. The user stories are written from the perspective of the user, and not the technology provider. This allows us to focus on what the user wants to achieve, not on how the technology should implement it.  

   Columns:  
   - **Responder's organization** – Identifies the organization providing the input.
   - **Use case #** – Identifier for each use case.
   - **As a [...]** – Defines the user.
   - **[will/ could/ will not] pilot** – Indicates whether the user story is planned to be piloted.
   - **User story** (“As a [...] I want to [create/ validate/ enable] QES/QEAA of document type [...] so that [...]”) – captures the usage of the trust service. When re-using the template, QES/QEAA can be replaced by the considered service. 
     
   Reference working document of QTSP group: [User stories QES/QEAA](https://docs.google.com/spreadsheets/u/1/d/1djcCeJJbmnMvfWQ2htW0bjEErrrELmfemJ4pG5Qh-aU)

2. **Use cases’ QEAA needs**  
   This table captures the needs for QEAA in more detail, elaborating on the required roles and technology for the use cases.  

    Columns:  
   - **Responder's organization** – Identifies the organization providing the input.
   - **Use case #** – Identifier for each use case.
   - **QEAA scheme name** – Identifies the specific scheme involved. Aligned with data schemes from [Attestation Rulebooks Catalog](https://github.com/eu-digital-identity-wallet/eudi-doc-attestation-rulebooks-catalog) where possible.
   - **Authentic source** – Indicates the repository or system, held under the responsibility of a public sector body or private entity, that contains and provides attributes about a natural or legal person or object and that is considered to be a primary source of that information or recognised as authentic in accordance with Union or national law, including administrative practice
   -  **Issuer** – Shows which organization issues the electronic attestation, can be a role (such as QTSPs for QEAAs) or a specific organization.
   -  **Wallet unit** – means a unique configuration of a wallet solution that includes wallet instances, wallet secure cryptographic applications and wallet secure cryptographic devices provided by a wallet provider to an individual wallet user.
   -  **Relying party instance** – Identifies the software and/or hardware module with the capability to interact with a Wallet Unit and to perform Relying Party authentication, that is controlled by a Relying Party.
   -  **Relying party** – Identifies the natural or legal person that relies upon electronic identification, EUDI Wallets or other electronic identification means, or upon a trust service - QEAA in the QTSP working document.

   Reference working document of QTSP group: [Use cases’ QEAA needs](https://docs.google.com/spreadsheets/d/1rAqVdg3GGjuWVZqy0thjKPg6PG-qNGAeldjiPRhPens)
   
# References

- User stories QES/QEAA: https://docs.google.com/spreadsheets/u/1/d/1djcCeJJbmnMvfWQ2htW0bjEErrrELmfemJ4pG5Qh-aU
- Use cases’ QEAA needs: https://docs.google.com/spreadsheets/d/1rAqVdg3GGjuWVZqy0thjKPg6PG-qNGAeldjiPRhPens
- Attestation Rulebooks Catalog: https://github.com/eu-digital-identity-wallet/eudi-doc-attestation-rulebooks-catalog
