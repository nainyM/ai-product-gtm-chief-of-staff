# GTM Chief of Staff — Schedule & Orchestration

## Execution Schedule

### Daily Execution: 9:00 AM (User's Local Timezone)

```
08:50 AM — Pre-flight check (connector health)
09:00 AM — Signal collection starts
09:05 AM — Context assembly + Claude processing
09:10 AM — Briefing ready for review
09:15 AM — User reviews and approves
09:20 AM — Briefing shipped to team (if configured)
```

---

## Detailed Timeline

### 08:50 AM — Pre-flight Health Check (5 minutes)
**What:** Test all connectors before collection
**Timeout:** 2 minutes per connector
**Action:** If connector fails, use cached data
**Log:** Connection status for debugging

**Pseudo-code:**
```
for each connector in [Calendar, Gmail, Slack, Jira, Notion]:
  ping connector endpoint
  if response not received within 2s:
    mark as "degraded"
    log error
  else:
    mark as "healthy"
```

---

### 09:00 AM — Signal Collection (5 minutes)
**What:** Pull raw signals from all sources
**Parallel:** All 5 connectors fetch simultaneously (avoid serial delays)
**Timeout:** 3 minutes total

**Execution:**
```
Tasks (run in parallel):
  1. Calendar: Fetch today's events
  2. Gmail: Fetch emails from last 24h (starred/important)
  3. Slack: Search for mentions + keywords
  4. Jira: Query user's open/blocked tickets
  5. Notion: Query recently updated pages

Aggregation: Combine all signals into single JSON payload
Size limit: 1MB max (fail gracefully if exceeded)
```

**Fallback:**
- If Calendar fails: use cached events from yesterday
- If Gmail fails: skip email signals
- If Slack fails: use cached Slack activity
- If Jira fails: use cached ticket list
- If Notion fails: skip document updates

---

### 09:05 AM — Context Assembly & Claude Processing (5 minutes)
**What:** Enrich signals and send to Claude for synthesis
**Timeout:** 4 minutes

**Execution:**
```
Step 1: Enrich signals (1 minute)
  - Resolve user mentions to names
  - Extract meeting agendas
  - Classify email senders (internal/external/customer)
  - Link Jira tickets to roadmap
  - Extract Notion action items

Step 2: Deduplicate
  - If same issue appears in multiple sources, merge
  - Example: Slack mentions blocker + Jira ticket both about database
  
Step 3: Add context
  - Include previous day's briefing for reference
  - Include user's OKRs/priorities
  - Include team roster

Step 4: Call Claude API
  - Model: Claude 3.5 Opus (or Sonnet for cost optimization)
  - System prompt: See prompt.md
  - Input: Enriched signals + context
  - Max tokens: 2000
  - Temperature: 0.7 (consistent but not robotic)

Step 5: Parse response
  - Extract structured briefing (priorities, blockers, decisions)
  - Validate format
  - Cache for fallback
```

**Fallback:**
- If Claude timeout: use summary from previous day's briefing
- If Claude fails: send text summary of raw signals

---

### 09:10 AM — Briefing Ready for Review
**What:** Briefing is formatted and ready
**Delivery:** Email to user inbox + optional Slack notification
**Format:** HTML email for better formatting

**Email structure:**
```
Subject: GTM Chief of Staff — Morning Briefing [Date]

From: gtm-chief-of-staff@company.com
To: [user_email]

[HTML formatted briefing]

Action link: [Review & Approve] -> [Edit/Approve form]
```

---

### 09:15 AM — User Reviews & Approves
**Duration:** 5-10 minutes (user's discretion)
**Actions Available:**
- ✅ Approve as-is
- ✏️ Edit briefing (add/remove items)
- 🔄 Regenerate (recollect signals and re-process)
- ❌ Dismiss (skip today)

---

### 09:20 AM — Ship Briefing
**What:** Deliver approved briefing to team/channels
**Options:**

**Option 1: Email to team**
```
Send to: [team@company.com]
Subject: GTM Daily Briefing — [Date]
Body: Approved briefing
```

**Option 2: Slack channel**
```
Post to: #gtm-daily
Format: Threaded message with reactions for decisions
```

**Option 3: Dashboard/Wiki**
```
Update: /wiki/gtm-daily
Append today's briefing to running log
```

**Option 4: Calendar event**
```
Create: "GTM Daily Sync" meeting
Description: Include briefing content
Attendees: Auto-add team members
```

**Option 5: Disable (user only, no team distribution)**

---

## Cron/Scheduler Configuration

### Using Cloud Function (Recommended)

**Service:** Google Cloud Scheduler / AWS EventBridge / Azure Logic Apps

```
Name: gtm-chief-of-staff-daily
Schedule: 0 9 * * * (9 AM every day, UTC)
  → Adjust for user's timezone
Timezone: User's local (e.g., America/Los_Angeles)
HTTP Endpoint: https://api.company.com/automations/gtm-chief-of-staff
Authentication: Service account + API key
Retry: 1 retry on failure (120s delay)
```

### Using Node.js/Python (Self-hosted)

```python
# Use APScheduler (Python)
from apscheduler.schedulers.background import BackgroundScheduler

scheduler = BackgroundScheduler()
scheduler.add_job(
  func=gtm_chief_of_staff,
  trigger="cron",
  hour=9,
  minute=0,
  timezone="America/Los_Angeles",
  id="gtm_morning_briefing"
)
scheduler.start()
```

### Using GitHub Actions (Free, but less flexible)

```yaml
name: GTM Chief of Staff
on:
  schedule:
    - cron: '0 9 * * *'

jobs:
  briefing:
    runs-on: ubuntu-latest
    steps:
      - name: Run GTM Chief of Staff
        run: python scripts/gtm_chief_of_staff.py
```

---

## Adjustment Options

**If 9 AM doesn't work:**
- User can change in settings: `BRIEFING_TIME=08:00` or `BRIEFING_TIME=10:00`
- Timezone automatically detected from system settings
- Changes take effect next day

**Weekend/Holiday handling:**
- By default: Runs every day including weekends
- Option to skip weekends: `SKIP_WEEKENDS=true`
- Option to skip holidays: `SKIP_HOLIDAYS=true`

---

## Monitoring & Alerts

**Track daily:**
- Signal collection duration
- Claude processing time
- User approval rate (% of briefings approved)
- Connector health status

**Alert conditions:**
- Collection takes > 5 minutes: investigate
- Claude timeout: fallback triggered
- 3+ connector failures: send alert to user
- User doesn't review briefing by 10 AM: send reminder

---

## Frequency Variations (Future Options)

- **Daily (current):** 9 AM every day
- **Weekday only:** Mon-Fri 9 AM (skip weekends)
- **Twice daily:** 9 AM + 4 PM (post-standup update)
- **Weekly digest:** Every Monday 9 AM (higher-level synthesis)
- **On-demand:** User can manually trigger anytime
