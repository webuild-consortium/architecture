# Architecture decision records

[WE BUILD](https://www.webuildconsortium.eu/) maintains a lightweight architecture decision record (ADR) for each software-related decision affecting interoperability.

## ADR overview

<!--BEGIN INDEX-->
1. [You could be first 🚀](_template.md)
<!--END INDEX-->

## ADR process for WE BUILD

```mermaid
stateDiagram-v2
    state "Pull request with new ADR" as pr
    state "Pull request ready to merge" as ready
    state "Consortium decision" as merged
    state "Proposal rejected" as rejected

    [*] --> pr: Any consortium participant proposes
    pr --> ready: Consortium participants review and share advice, authors improve the ADR including summarised advice

    ready --> merged: WP4 Architecture group merges
    merged --> [*]

    ready --> rejected: WP4 Architecture group rejects
    rejected --> [*]
```
