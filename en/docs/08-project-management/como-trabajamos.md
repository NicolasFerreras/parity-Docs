---
title: "How We Work"
---

# How We Work (agents)

> How Parity is built: specialized AI agents, coordinated by an orchestrator and supervised by people at every major step.

```mermaid
flowchart TD

    subgraph SG0["Input and routing"]
        U["Person writes a request<br/>in natural language"]
        ORCH{"Orchestrator<br/>interprets the request"}
        AMBIG{"Ambiguous across<br/>2+ workflows?"}
        ASK["Ask the user<br/>which one applies"]
    end

    subgraph SG1["Mandatory plan mode"]
        PLAN["Implementation brief<br/>(what / what not / files / risks)"]
        GATE0[["🔒 Human gate<br/>Approved?"]]
    end

    subgraph SG2["New feature"]
        IDEA["Idea / Need"]
        AN["Analysis"]
        NEC{"Is it needed?"}
        DESCARTADO["Discarded"]
        REQ["Product/BA agent<br/>Requirement"]
        US["Product/BA agent<br/>User story"]
        AC["Product/BA agent<br/>Acceptance criteria"]
        UX["UX/UI agent<br/>Flow and wireframes"]
        RFD["Ready for development"]
    end

    subgraph SG3["User story development"]
        BE["Backend agent<br/>API + logic"]
        FE["Frontend agent<br/>Interface"]
        BRANCH["Own branch<br/>(never straight to main)"]
        TESTDB[("Test<br/>database/fixture")]
        BUGCHECK{"Unrelated bug<br/>shows up?"}
        BUGWF["Fire nested Bug workflow<br/>— escalate to user first"]
    end

    subgraph SG4["Quality"]
        QA["QA agent<br/>Tests"]
        CR["Code reviewer agent"]
    end

    subgraph SG5["Pull request"]
        CI["CI: tests + build +<br/>lint + security checks"]
        APPROVED{"Approved?"}
        FIXES["Fixes"]
    end

    subgraph SG6["Merge and release"]
        SYNC["Update branch with<br/>latest main before merging"]
        GATEM[["🔒 Human gate<br/>confirm merge"]]
        MERGE["Merge to main"]
        REL["Staging → smoke tests<br/>→ production → monitoring"]
        FEEDBACK["Feedback"]
    end

    subgraph SG7["Outside the pipeline"]
        TUTOR["Mentor<br/>direct questions, explains only"]
    end

    MCP[("External integrations")]

    U --> ORCH
    ORCH --> AMBIG
    AMBIG -->|Yes| ASK --> ORCH
    AMBIG -->|No| PLAN
    ORCH -.->|when needed| MCP

    PLAN --> GATE0
    GATE0 -->|No| PLAN
    GATE0 -->|Yes| IDEA

    IDEA --> AN --> NEC
    NEC -->|No| DESCARTADO
    NEC -->|Yes| REQ --> US --> AC --> UX --> RFD

    RFD --> BE
    RFD --> FE
    BE --> BRANCH
    FE --> BRANCH
    BRANCH -.-> TESTDB
    BRANCH --> BUGCHECK
    BUGCHECK -->|Yes| BUGWF --> BRANCH
    BUGCHECK -->|No| QA

    QA --> CR --> CI --> APPROVED
    APPROVED -->|No| FIXES --> BRANCH
    APPROVED -->|Yes| SYNC --> GATEM
    GATEM -->|Yes| MERGE --> REL --> FEEDBACK
    FEEDBACK -.->|new cycle| IDEA

    classDef gate fill:#ffe0e0,stroke:#c0392b,stroke-width:2px,color:#000
    classDef decision fill:#fff4cc,stroke:#d4a017,color:#000
    classDef tutor fill:#f0f0f0,stroke:#888888,stroke-width:2px,stroke-dasharray: 5 5,color:#000
    classDef mcp fill:#e8e0f5,stroke:#8e44ad,color:#000

    class GATE0,GATEM gate
    class AMBIG,NEC,BUGCHECK,APPROVED decision
    class TUTOR tutor
    class MCP mcp
```

How to read it: every request enters in natural language and gets routed (asking when ambiguous); nothing is built without an approved plan; each specialty (product, UX, backend, frontend, QA) has its agent; no sensitive transition moves without human approval; and a direct mentoring channel outside the pipeline only explains, never decides or executes.
