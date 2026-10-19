# Flowchart — Submit a New Vacation Request

**Source of record:** [Lucidchart](https://lucid.app/lucidchart/8b88e3e0-78ac-4eeb-a3b5-63b824c1d8e3/edit)

The core domain journey: *the employee wishes to submit a new request for vacation
time.* Follows flowchart best practice — one start and one end terminator, every
decision is a diamond with labelled Yes/No exits, and the rules engine / optional
manager approval / e-mail / logging requirements from the spec are shown explicitly.

```mermaid
flowchart TD
    START([Start]) --> AUTH["Employee opens VTS<br/>(authenticate via portal SSO)"]
    AUTH --> ENTER["Enter request:<br/>leave type, dates, hours"]
    ENTER --> RANGE{"Dates within allowed window?<br/>(prev. year → +18 months)"}
    RANGE -- No --> REJRANGE["Show out-of-range message"]
    REJRANGE --> ENTER
    RANGE -- Yes --> VALIDATE["Rules engine validates<br/>against company & facility policy"]
    VALIDATE --> VALID{Request valid?}
    VALID -- No --> SHOWERR["Show policy reason<br/>(e.g. insufficient balance)"]
    SHOWERR --> FIX{Employee edits & retries?}
    FIX -- Yes --> ENTER
    FIX -- No --> LOGABORT["Log cancelled request"]
    LOGABORT --> END

    VALID -- Yes --> NEEDAPP{Manager approval required?}
    NEEDAPP -- No --> APPROVED["Status = Approved<br/>(auto)"]
    NEEDAPP -- Yes --> PENDING["Status = Pending"]
    PENDING --> MAILMGR["E-mail manager:<br/>approval requested"]
    MAILMGR --> DECIDE{Manager decision}
    DECIDE -- Approve --> APPROVED
    DECIDE -- Reject --> REJECTED["Status = Rejected"]

    APPROVED --> LOG["Log transaction"]
    REJECTED --> LOG
    LOG --> NOTIFY["E-mail employee:<br/>status change"]
    NOTIFY --> END([End])

    classDef term fill:#e6f4ea,stroke:#34a853;
    classDef decision fill:#fef7e0,stroke:#f9ab00;
    class START,END term;
    class RANGE,VALID,FIX,NEEDAPP,DECIDE decision;
```

## Notes

- **Rules engine (NFR1).** All validation is centralised — the employee never needs
  to know the policy; the engine enforces it.
- **Optional approval (F1).** When approval is not required, the request is
  auto-approved; the Yes branch covers the manager-approval path.
- **E-mail (F3)** is sent both to request manager approval and to notify the
  employee of any status change.
- **Logging (F6)** happens on every terminal outcome — approved, rejected, or
  cancelled.
