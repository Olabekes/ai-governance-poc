# Architecture Diagram

## Workflow Flow
┌─────────────────────────────────────────────────────────┐
│ USER QUERY                                              │
└────────────────────┬────────────────────────────────────┘
│
▼
┌─────────────────────────────────────────────────────────┐
│ COPILOT STUDIO AGENT                                    │
│ (Generates initial response)                            │
└────────────────────┬────────────────────────────────────┘
│
▼
┌─────────────────────────────────────────────────────────┐
│ QC WORKFLOW (Power Automate)                            │
│ Evaluates response using AI prompt                      │
└────────────────────┬────────────────────────────────────┘
│
▼
┌─────────────────────────────────────────────────────────┐
│ SCORING LOGIC                                           │
│ Score response 1-10 based on:                           │
│ • Grounding (knowledge base)                            │
│ • Scope (answers question)                             │
│ • Confidence (appropriate level)                        │
└────────┬───────────────────────────────┬────────────────┘
│                               │
Score ≥ 8                        Score < 8
│                               │
▼                               ▼
┌─────────┐                    ┌──────────────┐
│ APPROVE │                    │ HUMAN REVIEW │
│ (Log)   │                    │    QUEUE     │
└────┬────┘                    └──────┬───────┘
│                                │
│                     ┌──────────┴──────────┐
│                     │                     │
│                 Approved            Escalate
│                     │                     │
▼                     ▼                     ▼
┌──────────────────────────────────────────────────┐
│ SEND TO USER (or appropriate queue)              │
│ + Log all decisions (timestamp, score, reason)   │
└──────────────────────────────────────────────────┘
## Data Flow

Input: User Query + Copilot Response
↓
Process: AI Evaluation (structured prompt)
↓
Output: JSON Score + Reasoning
↓
Decision: Route based on score threshold
↓
Logging: Record all decisions for audit
## System Components

| Component | Technology | Purpose |
|-----------|-----------|---------|
| Copilot | Copilot Studio | Generates initial response |
| QC Engine | Power Automate + AI | Evaluates response quality |
| Scoring | Logic Apps | Calculates 1-10 score |
| Routing | Power Automate Conditional | Routes based on score |
| Logging | SharePoint/Database | Audit trail |
| Alerts | Power Automate Notifications | Alerts on failures |
