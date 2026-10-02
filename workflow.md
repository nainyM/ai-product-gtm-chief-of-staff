# GTM Chief of Staff — Workflow

## High-Level Architecture
```
Signal Collection → Context Assembly → Claude Processing → Review → Ship
```

## Detailed Workflow Steps

### 1. Signal Collection (Automated)
**Trigger:** Daily at 9:00 AM
**Duration:** 2-3 minutes

Pull raw signals from each connector:
- **Calendar API:** Fetch today's events + next 7 days
- **Gmail API:** Fetch emails from last 24 hours, filter by priority/sender
- **Slack API:** Fetch mentions, thread activity from last 24 hours
- **Jira API:** Fetch open tickets assigned to user, filter by due date and status
- **Notion API:** Fetch recently updated docs and action items

**Output:** Raw JSON/structured data with timestamps

### 2. Context Assembly (Automated)
**Duration:** 1-2 minutes

Enrich signals with context:
- **Calendar:** Extract meeting purpose, attendee list, agenda links
- **Gmail:** Classify by sender (C-level, customer, team), extract action items
- **Slack:** Identify thread context, resolve mentions to full names
- **Jira:** Link tickets to roadmap items, identify dependencies
- **Notion:** Extract task status, owner, due dates

**Output:** Enriched signal bundle with relationships and context

### 3. Claude Processing
**Model:** Claude Opus (or Sonnet)
**Prompt:** See `prompt.md`

Claude receives the enriched signals and:
1. **Reads** all signals in context
2. **Identifies** key themes and patterns
3. **Prioritizes** by business impact (not just urgency)
4. **Flags** blockers and dependencies
5. **Extracts** decisions that need human input
6. **Drafts** structured briefing with reasoning

**Output:** Draft briefing with priorities, blockers, decisions + Claude's reasoning

### 4. Human Review (Manual)
**Duration:** 5-10 minutes
**When:** PM reads briefing at 9:15 AM

The PM reviews:
- Are priorities correct? (Adjust if needed)
- Are blockers accurately identified? (Add context if needed)
- Are decisions flagged correctly? (Approve or remove)
- Missing anything? (Add gaps manually)

**Action:** PM approves or edits briefing

### 5. Ship (Manual or Automated)
**Options:**
- **Option A:** Email briefing to self + team
- **Option B:** Post to Slack channel
- **Option C:** Save to shared dashboard/doc
- **Option D:** Schedule meetings for flagged decisions

## Fallback Logic
If any step fails:
- **Missing data source:** Use cached data from previous briefing
- **Claude timeout:** Send previous day's briefing with update notice
- **Delivery failure:** Resend via alternate channel (Slack if email fails, vice versa)

## Scheduling
```
09:00 AM — Signal collection starts
09:05 AM — Context assembly + Claude processing
09:10 AM — Briefing ready for review
09:15 AM — PM reviews and approves
09:20 AM — Briefing shipped to team
```

## Integration Points
- **Trigger:** Cron job or scheduled cloud function
- **Connectors:** OAuth flows for Calendar, Gmail, Slack, Jira, Notion
- **Claude:** API call with system prompt + enriched signals
- **Output:** Email, Slack, or dashboard API
- **Logging:** Track execution time, errors, signal coverage

## Human-in-the-Loop Decision
- **Automated:** Signal collection, enrichment, synthesis, prioritization
- **Human:** Final approval, context addition, decision confirmation
- **Why:** Claude synthesizes noise into signal; humans validate and decide

This respects the principle: *AI handles research and synthesis; humans make commitments.*
