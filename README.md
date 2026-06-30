# Responsible AI Workflow

A production-grade system that evaluates AI-generated outputs for quality and compliance before they reach users.

## Overview

This workflow was built in Power Automate to monitor Copilot Studio agent responses in an enterprise environment. It demonstrates how to integrate AI with governance built in from the start—not bolted on afterward.

## The Problem

Copilot agents can:
- **Hallucinate** information not in the knowledge base
- **Generate out-of-scope** responses that don't answer the user's question
- **Provide confident-sounding but incorrect answers**

Without governance, these errors reach users and damage trust.

## The Solution

An automated workflow that evaluates each response BEFORE it reaches the user:
User Query
↓
Copilot Agent (Generates Response)
↓
QC Workflow (AI Evaluation)
↓
Scoring Logic (1-10 scale)
↓
Score ≥ 8?
├─ YES → Send to User (Logged)
└─ NO → Human Review Queue → Approved/Escalated

## Key Features

✅ **Automated evaluation** using structured AI prompts  
✅ **Governance built-in** (not bolted on)  
✅ **Human-in-the-loop** for low-confidence responses  
✅ **Full audit logging** for compliance  
✅ **Incident tracking** and alerts  
✅ **Scalable** across teams  

## How It Works

1. **Copilot** generates a response to a user query
2. **QC Workflow** runs the response through an evaluation prompt
3. **Scoring Logic** scores the response 1-10 based on:
   - Is it grounded in our knowledge base?
   - Does it answer the actual question?
   - Is the confidence level appropriate?
4. **Routing Logic**:
   - Score ≥ 8: Send to user (logged)
   - Score < 8: Route to human reviewer
5. **Logging & Alerts**: Track all decisions for audit + pattern detection

## Governance Guardrails

| Guardrail | Why It Matters |
|-----------|---|
| **Specific prompts** | AI evaluator only follows structured instructions, not free-form |
| **Clear scoring criteria** | Consistent evaluation across all responses |
| **Mandatory human review** | Low-confidence responses always get a human check |
| **Audit logging** | Every decision logged: timestamp, user, response, score, reasoning |
| **Incident tracking** | Alerts if >10% of responses fail; patterns reviewed monthly |

## Prompts

See [prompts.md](prompts.md) for:
- The evaluation prompt used to score responses
- Sample responses and what they mean
- Guardrails applied at evaluation

## Implementation

To build this in Power Automate:

1. Create workflow with trigger: "When Copilot response is generated"
2. Add AI evaluation step using the prompt from prompts.md
3. Add scoring logic based on response
4. Add conditional: If score < 8, route to human queue
5. Add logging to database/SharePoint
6. Add alert if failures exceed threshold
7. Test in staging environment
8. Deploy and monitor

## Why This Matters

For media organizations like Postmedia:
- **Risk mitigation**: Catch AI errors before they damage credibility
- **Compliance**: Audit trail for governance and regulatory needs
- **Trust**: Users get reliable, verified information
- **Scale**: Automation handles volume; humans review exceptions

---

Built by: Ola Balogun  
Last updated: July 2026
