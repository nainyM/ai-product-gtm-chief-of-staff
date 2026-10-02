# GTM Chief of Staff

## Problem
Product and GTM leaders wake up to scattered updates across multiple channels:
- Calendar notifications about meetings
- Emails from stakeholders
- Slack messages and mentions
- Jira tickets and blockers
- Notion docs and updates

This fragmentation creates information overload and makes it hard to identify what actually needs attention today.

## Goal
Deliver a unified morning briefing that surfaces:
- **Priorities** — What should the leader focus on today?
- **Blockers** — What's preventing progress?
- **Decisions Requiring Attention** — What needs a call or decision today?

## Signal
- Calendar: Upcoming meetings, participants, agendas
- Gmail: New emails from key stakeholders, urgent flags
- Slack: Mentions, thread updates, status changes
- Jira: Open tickets, overdue issues, status changes
- Notion: Document updates, action items

## Context Sources
1. **Calendar API** — Events, attendees, descriptions
2. **Gmail API** — Subject lines, sender, priority flags
3. **Slack API** — Messages, mentions, thread context
4. **Jira API** — Issues, status, assignees, due dates
5. **Notion API** — Database updates, page changes

## Filters / Rules
- **High Priority:** Emails marked urgent, Slack mentions with keywords (blocker, urgent, decision needed)
- **Meetings:** Today's meetings with 3+ attendees or external participants
- **Overdue Items:** Jira tickets past due date
- **Recent Changes:** Notion docs updated in last 24 hours

## Claude Workflow
1. **Signal Collection** — Gather updates from all sources
2. **Context Assembly** — Combine signals with historical context
3. **Draft Synthesis** — Claude synthesizes into structured briefing
4. **Prioritization** — Claude ranks by urgency and impact
5. **Blocker Identification** — Claude flags blockers and dependencies
6. **Decision Flagging** — Claude identifies what needs human decision
7. **Draft Review** — Human reviews and edits
8. **Ship** — Deliver briefing via email or dashboard

## Output
A structured morning briefing (7–10 AM delivery) containing:

```
GTM CHIEF OF STAFF — Morning Briefing
Date: [Today]

🎯 TOP 3 PRIORITIES
1. [Priority 1] — Why it matters
2. [Priority 2] — Why it matters
3. [Priority 3] — Why it matters

⚠️ BLOCKERS
- [Blocker 1] — Blocking [what]
- [Blocker 2] — Blocking [what]

🔴 DECISIONS REQUIRING ATTENTION
- [Decision 1] — Decision needed by [time]
- [Decision 2] — Decision needed by [time]

📅 MEETINGS TODAY
- [Time] [Meeting] (with [key people])

📊 METRICS TO WATCH
- [Metric 1]: [Status]
- [Metric 2]: [Status]
```

## Human Review
The PM/GTM leader reviews the briefing and:
- Confirms priorities align with strategy
- Validates blocker assessment
- Approves decision list
- Edits or adds context

## Ship
- Email briefing to self + relevant stakeholders (optional)
- Update team on priorities and blockers
- Schedule decision meetings
- Archive briefing for later reference

## Fallback
If any connector fails:
- Use cached data from previous day
- Send text-only summary email
- Log missing data source for manual follow-up

## Evaluation Metrics
- **Time Saved:** How many minutes of context-gathering does this save daily?
- **Decision Speed:** How much faster are decisions made with centralized briefing?
- **Blocker Resolution:** How many blockers are resolved within 24 hours of being flagged?
- **Accuracy:** Does the briefing capture all truly urgent items? (false negative rate)
- **Adoption:** Does the PM actually use the briefing daily?
