# Hermes Kanban Integration

Author: Elyazer Emmanuel  
Compatible with: Hermes Agent (Nous Research) multi-agent Kanban board

## Purpose

Turns the Content Lifecycle (IDEA → RESEARCH → DRAFT → REVIEW → APPROVED → SCHEDULED → PUBLISHED → MONITORING → ANALYZED → LEARNED) into a real shared board. One board per managed X account.

## Board Structure

```
Board name: x-growth-{account-name}

Columns:
  Idea Bank → Research → Draft → Review → Approved
  → Scheduled → Published → Monitoring → Analyzed
```

## Agent Roles (Hermes profiles)

| Role              | Claims from          | Responsibilities |
|-------------------|----------------------|------------------|
| Scout             | — (creates tasks)    | Trend Detection + Relevance Filter; creates tasks in Idea Bank |
| Writer            | Draft                | Human Writing Engine + Voice DNA; calls request_review when done |
| Reviewer          | Review               | Brand Guardrails + Quality Gates; request_changes or approve |
| Scheduler/Publisher | Approved / Scheduled | Sets target time; **only role that loads the persistent session**; executes publish when due |
| Analyst           | Published (after dwell) | Performance Benchmarking + Attribution; attaches findings via comment |

## Tool Mapping

| Hermes tool                  | Implements |
|------------------------------|------------|
| kanban_create                | New idea enters Idea Bank |
| kanban_request_review / kanban_request_changes | Approval autonomy + Quality Gates |
| kanban_block / kanban_unblock | “Do Not Post” intelligence (visible reason) |
| kanban_link                  | Campaign phase sequencing |
| kanban_attach / kanban_attach_url | Visual briefs, dry-run previews, analytics |
| kanban_comment               | Audit trail for gates and human feedback |
| kanban_heartbeat             | Reliability — reclaim Scheduled tasks if Publisher dies |

## Scheduling

A task in Scheduled carries target publish time as metadata.  
Dispatcher (or lightweight poller) claims it when the time arrives and hands it to the Publisher role.  
Publisher loads the persistent encrypted session, performs the action (or dry-run), then moves the task to Published.

## Review Policy Default

Tied to Autonomous Mode in the Account Profile:

- Manual / Assisted / Approval → human approval required at Review column  
- Autonomous → Reviewer agent may self-approve inside guardrails  

Safe default is human approval.

## Worked Flows

**Single post**  
Scout creates task → Writer drafts + request_review → Reviewer approves → Scheduled with time → Publisher posts → Analyst attaches data after dwell period.

**Multi-phase campaign**  
Phase tasks created up front and linked so later phases cannot advance until earlier ones show Published.

**Rejected idea**  
Scout creates task → Reviewer runs relevance filter → kanban_block with reason as comment (visible record).

## Security Note

Only the Publisher role ever loads the persistent browser session. All other roles operate on public data only.
