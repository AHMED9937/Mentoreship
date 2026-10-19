# Use-Case Diagram — Vacation Tracking System

**Source of record:** [Lucidchart](https://lucid.app/lucidchart/d8e7b2e5-89a3-411d-9695-0f945f7aff0f/edit)

Shows **who** uses the VTS and **what** they can do. Mermaid has no native UML
use-case notation, so actors are rendered as `([actor])` nodes outside a system
boundary (the subgraph), with use cases as rounded nodes inside. `«include»`
dependencies (SSO auth, rules validation, logging, e-mail) are dashed, following
UML convention — these behaviours are pulled into many use cases rather than
triggered directly by an actor.

```mermaid
flowchart LR
    %% ---------- Actors ----------
    EMP([Employee])
    MGR([Manager])
    HR([HR Personnel])
    ADMIN([System Administrator])
    LEGACY([HR Legacy System])
    SYS([Internal System])

    %% ---------- System boundary ----------
    subgraph VTS["Vacation Tracking System"]
        direction TB
        UC1(["Submit vacation request"])
        UC2(["Edit / withdraw request"])
        UC3(["View request history<br/>(prev. year → +18 months)"])
        UC4(["Approve / reject request"])
        UC5(["Award personal leave<br/>(within system limits)"])
        UC6(["Override rule-restricted action"])
        UC7(["Maintain employee<br/>vacation data"])
        UC8(["Query vacation-request<br/>summary (Web service)"])

        %% included behaviours
        INC1(["Authenticate via portal SSO"])
        INC2(["Validate against rules engine"])
        INC3(["Send e-mail notification"])
        INC4(["Log transaction"])
    end

    %% ---------- Actor associations ----------
    EMP --- UC1
    EMP --- UC2
    EMP --- UC3
    MGR --- UC4
    MGR --- UC5
    HR  --- UC6
    HR  --- UC7
    ADMIN --- UC6
    SYS --- UC8
    LEGACY --- UC7

    %% ---------- «include» dependencies ----------
    UC1 -. include .-> INC1
    UC2 -. include .-> INC1
    UC4 -. include .-> INC1
    UC1 -. include .-> INC2
    UC1 -. include .-> INC3
    UC4 -. include .-> INC3
    UC6 -. include .-> INC4
    UC1 -. include .-> INC4

    classDef actor fill:#e8f0fe,stroke:#4472c4,stroke-width:1px;
    classDef inc fill:#fff4e5,stroke:#d9822b,stroke-dasharray:4 2;
    class EMP,MGR,HR,ADMIN,LEGACY,SYS actor;
    class INC1,INC2,INC3,INC4 inc;
```

## Actors

| Actor | Role |
|-------|------|
| **Employee** | Submits, edits, withdraws, and reviews their own leave requests. |
| **Manager** | Optionally approves/rejects requests; may award personal leave within limits. |
| **HR Personnel** | Maintains employee vacation data; may override rule-restricted actions (logged). |
| **System Administrator** | May override rule-restricted actions (logged). |
| **HR Legacy System** | External system supplying/receiving employee information. |
| **Internal System** | External consumer of the vacation-summary Web service. |
