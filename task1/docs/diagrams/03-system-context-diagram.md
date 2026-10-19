# System Context Diagram — Vacation Tracking System

**Source of record:** [Lucidchart](https://lucid.app/lucidchart/d45b8374-fe33-4ad1-95e8-91574aae2253/edit)

Places the VTS in its environment: the people who use it and the external systems
it depends on or serves. This reflects the integration constraints in the spec —
VTS is an **extension of the existing intranet portal** (F5), reuses existing
infrastructure (F4), and talks to e-mail, the HR legacy systems, and internal
consumers over a Web service (F3/F9/F10).

```mermaid
flowchart TB
    EMP([Employee])
    MGR([Manager])
    HRU([HR / System Admin])

    subgraph CORE[" "]
        VTS["<b>Vacation Tracking System</b><br/>rules engine · requests · audit log"]
    end

    PORTAL[["Intranet Portal<br/>(Single Sign-On)"]]
    EMAIL[["E-mail / Notification Server"]]
    LEGACY[("HR Legacy Systems")]
    INTERNAL[["Internal Systems<br/>(Web-service consumers)"]]

    EMP   -->|"submit / view requests"| VTS
    MGR   -->|"approve · award leave"| VTS
    HRU   -->|"maintain data · override"| VTS

    VTS -->|"authenticate users"| PORTAL
    VTS -->|"send notifications"| EMAIL
    VTS <-->|"employee info & changes"| LEGACY
    VTS -->|"vacation-summary query"| INTERNAL

    classDef sys fill:#e8f0fe,stroke:#4472c4,stroke-width:2px;
    classDef ext fill:#f1f3f4,stroke:#80868b;
    classDef actor fill:#fff,stroke:#5f6368;
    class VTS sys;
    class PORTAL,EMAIL,LEGACY,INTERNAL ext;
    class EMP,MGR,HRU actor;
    style CORE fill:#ffffff,stroke:#4472c4,stroke-width:0px;
```

## External dependencies

| System | Direction | Purpose |
|--------|-----------|---------|
| **Intranet Portal (SSO)** | VTS → Portal | All authentication; VTS is an extension of the portal (F5). |
| **E-mail Server** | VTS → E-mail | Approval requests and status-change notifications (F3). |
| **HR Legacy Systems** | VTS ↔ Legacy | Retrieve/receive employee information and changes (F10). |
| **Internal Systems** | VTS → Consumers | Serve vacation-request summaries via Web service (F9). |
