# Sales GTM & AI PM Workflow Automations

A complete system of three interconnected Claude Cowork automations designed to help GTM and Product leaders synthesize scattered information into unified briefings, make faster decisions, and reduce context-switching from 10-15 hours per week to near-zero busywork.

**Each automation follows:** Signal → Context → Synthesis → Review → Ship

---

## The Three Automations at a Glance

| Automation | What It Does | When | Time Saved |
|-----------|-------------|------|-----------|
| **GTM Chief of Staff** | Daily briefing from Calendar, Gmail, Slack, Jira, Notion | Daily 9 AM | 30-45 min/day |
| **Voice of Customer Intelligence** | Customer feedback synthesis from CRM, support, calls, interviews | Weekly Fri 4 PM | 2-3 hrs/week |
| **Release Readiness Copilot** | Launch risk assessment across engineering, GTM, deployment | 2 weeks before launch, daily | 50+ hrs/launch |

---

## System Architecture

```
SIGNAL COLLECTION → CONTEXT ASSEMBLY → CLAUDE SYNTHESIS → HUMAN REVIEW → SHIP
    (Connectors)      (Enrichment)      (Prioritization)    (Approval)    (Distribution)
```

**The Human-in-the-Loop Principle:**
- ✅ **Automated:** Data collection, synthesis, pattern recognition, scope filtering
- ✅ **Human:** Validation, judgment, decisions, commitments
- ✅ **Result:** AI handles information overload; you make the calls

---

## How It Works: Complete Flow

### 1️⃣ Automation Runs (On Your Schedule)
- Pulls fresh data from all connectors (Calendar, Gmail, Slack, Jira, Notion, CRM, etc.)
- Only pulls NEW data since last run (timestamp-based filtering)
- Takes 2-5 minutes depending on data volume

### 2️⃣ Claude Synthesizes
- Reads all signals in context
- Identifies patterns and themes
- Ranks by business impact (not just urgency)
- Flags blockers with cascading effects
- Produces structured draft (5-10 minutes)

### 3️⃣ Draft Arrives for Approval
- **GTM Chief:** Slack DM (5 AM, before you wake)
- **VoC Intelligence:** Email (Friday 4 PM)
- **Release Readiness:** Slack DM (daily, 9 AM)

### 4️⃣ You Approve (2 seconds)
- React with ✅ emoji, or
- Reply with notes for edits, or
- React 🔄 to regenerate with new data

### 5️⃣ Auto-Publishes to All Channels
**GTM Chief of Staff:**
- Slack #gtm-daily (pinned)
- Email team distribution list

**VoC Intelligence:**
- Slack #product-insights (threaded)
- Product Strategy doc (new section)
- Email to product + marketing

**Release Readiness:**
- Slack #launch-war-room (pinned status)
- Email to engineering + GTM + leadership
- War room doc (daily checkpoint)

---

## Complete File Structure

```
ai-product-gtm-chief-of-staff/  (GitHub repo root)

│   ├── README.md   (This file — portfolio overview)
│   ├── 01-gtm-chief-of-staff-cowork-prompt.md   (Ready to paste into Cowork)
│   ├── 02-voc-product-intelligence-cowork-prompt.md
│   └── 03-release-readiness-copilot-cowork-prompt.md

---

## Getting Started (5 Steps)

### Step 1: Set Up Connectors
- Go to Claude Desktop → Cowork → Settings → Connectors
- Connect: Google Calendar, Gmail, Slack, Jira, Notion
- This is one-time setup

### Step 2: Copy a Cowork Prompt
- Choose one automation (recommend GTM Chief of Staff first)
- Copy the entire `XX-automation-name-cowork-prompt.md` file
- Example: `01-gtm-chief-of-staff-cowork-prompt.md`

### Step 3: Paste into Cowork
1. Open Claude Desktop
2. Click **Cowork** tab → **New Task**
3. Paste the markdown
4. Edit the customization sections (takes 3 minutes)
5. Click **Run** to test

### Step 4: Review the Output
- Does the briefing/synthesis look right?
- Are the priorities accurate?
- Is the delivery channel correct?
- Make any tweaks needed

### Step 5: Schedule It
Once satisfied, schedule with one command:

```
/schedule "gtm-chief-of-staff" "daily at 9 AM"
```

Or:

```
/schedule "voc-intelligence" "every Friday at 4 PM"
```

---

## Each Automation Explained

### 🎯 GTM Chief of Staff

**Solves:** Information overload, scattered updates across tools

**Pulls from:**
- Google Calendar (today's meetings + next 7 days)
- Gmail (starred/important emails from last 24h)
- Slack (mentions + keywords: blocker, urgent, decision)
- Jira (open tickets assigned to you, approaching deadlines)
- Notion (recently updated docs from last 24h)

**Outputs:**
- 🎯 Top 3 Priorities (ranked by business impact)
- ⚠️ Blockers (with root cause, owner, timeline)
- 🔴 Decisions Requiring Attention (with deadline)
- 📅 Today's Meetings (with context)
- 📊 Metrics to Watch

**Approval workflow:**
- Arrives: Slack DM (status: "Ready for Review ✋")
- You do: React ✅
- Publishes: #gtm-daily + email team

**Cadence:** Daily at 9 AM

---

### 👥 Voice of Customer Intelligence

**Solves:** Customer feedback fragmentation, missed patterns

**Pulls from:**
- HubSpot (customer notes from last 7 days)
- Zendesk (support tickets with feature request/bug tags)
- Granola (customer call transcripts from last 7 days)
- Notion (interview database, recently updated)
- Slack (#customer-feedback channel, last 7 days)

**Outputs:**
- 🎯 Top Themes (customer mentions, segment, evidence)
- 📊 Pain Points (what's broken, frequency, impact)
- 🔍 Surprising Insights (unexpected use cases)
- 💡 Unmet Needs (ranked by priority, competitive context)
- 👥 By Customer Segment (enterprise vs. mid-market vs. startup)

**Approval workflow:**
- Arrives: Email (subject: "VoC Synthesis [READY FOR REVIEW]")
- You do: Reply "approved"
- Publishes: #product-insights + Product Strategy doc + email team

**Cadence:** Every Friday at 4 PM

---

### 🚀 Release Readiness Copilot

**Solves:** Launch coordination chaos, hidden dependencies, surprises

**Pulls from:**
- Jira (Q4 Release project, open/blocked/in-progress tickets)
- GitHub (PRs merged, code review status, test results)
- Slack (#engineering-standup, #gtm-release, #customer-comms)
- Notion (spec docs, release notes status, GTM checklist)
- Google Drive (marketing materials status)
- Jenkins/GitHub Actions (staging deploy status, test results)

**Outputs:**
- 🎯 Readiness Summary (GREEN/YELLOW/RED + % complete)
- ⚠️ Top Blockers (with owner, impact, timeline, workaround)
- 🔗 Dependencies Checklist (what's waiting on what)
- 📊 GTM Readiness (5 dimensions: marketing, sales, CS, support, leadership)
- ✅ Launch Checklist (all go/no-go criteria)
- 💡 Recommended Actions (what to do in next 24h)

**Approval workflow:**
- Arrives: Slack DM (status indicator: 🟢 GREEN / 🟨 YELLOW / 🔴 RED)
- You do: React ✅ (or 🚨 if RED to alert leadership)
- Publishes: #launch-war-room + email leadership + war room doc

**Cadence:** Daily from 2 weeks before launch until launch

---

## How Scope Filtering Works (New Data Detection)

**Problem:** Without this, Claude would re-process the same data every run.

**Solution:** Each automation specifies a scope filter. Examples:

**GTM Chief of Staff:**
- "Pull signals from last 24 hours only"
- Claude remembers last run timestamp (9 AM yesterday)
- Today's run (9 AM) pulls only data from yesterday 9 AM → today 9 AM

**VoC Intelligence:**
- "Pull feedback from last 7 days only"
- Last Friday's run (4 PM) is marked
- This Friday's run (4 PM) pulls only feedback from last Friday 4 PM → this Friday 4 PM
- Prevents duplicate themes from being re-synthesized

**Result:** Week 2 and beyond, you only see NEW insights, not repeated ones.

---

## Key Features

✅ **Human Review is Non-Negotiable**
- Claude drafts, you approve
- No automation happens without your 2-second approval
- You can edit before publishing

✅ **Scope Filtering (NEW DATA ONLY)**
- Each automation only pulls data newer than the last run
- Avoids duplicate insights
- Timestamps tracked automatically

✅ **Edit & Regenerate**
- Reply with notes: "Move #2 to #1. Add context on X."
- Claude regenerates and resubmits
- Approve updated version

✅ **Fallback Behavior**
- If a connector fails, uses cached data
- Notes which sources are stale
- Never crashes due to missing data

✅ **Multi-Channel Publishing**
- Single approval → 3+ channels simultaneously
- Slack, email, docs all updated
- Customizable per automation

---

## Approval Workflows at a Glance

| Automation | Arrives | Approval | Publishes To |
|-----------|---------|----------|-------------|
| **GTM Chief** | Slack DM | React ✅ | #gtm-daily, email |
| **VoC Intel** | Email | Reply "approved" | #product-insights, doc |
| **Release Ready** | Slack DM | React ✅ or 🚨 | #launch-war-room, email |

**See [APPROVAL_WORKFLOWS.md](../APPROVAL_WORKFLOWS.md) for detailed workflow diagrams and examples.**

---

## Additional Resources

- **[APPROVAL_WORKFLOWS.md](../APPROVAL_WORKFLOWS.md)** — Complete approval process for each automation with examples
- **[LINKEDIN_POST.md](../LINKEDIN_POST.md)** — LinkedIn post template + 45-60 min video script outline

---

## Implementation Timeline

**Week 1:** Set up GTM Chief of Staff
- Connect connectors
- Customize prompt
- Test and approve
- Schedule for daily 9 AM

**Week 2-3:** Add VoC Intelligence
- Reuse connector setup
- Customize VoC prompt
- Integrate with GTM briefing
- Schedule for Friday 4 PM

**Week 4+:** Add Release Readiness
- Use when approaching a launch
- Runs daily for 2 weeks pre-launch
- Integrates signals from both automations above

---

## Why This Works

1. **Reusable Architecture** — All three use the same Signal → Synthesis → Review → Ship pattern
2. **Compound Effect** — Each automation feeds insights to the others
3. **Human Judgment** — AI synthesizes; you decide. You never blindly ship.
4. **Time Math** — 15 min setup per automation. Saves 10-15 hrs/week. Payoff: 40x ROI.
5. **Scope Filtering** — Knows what's new; never repeats insights from previous runs.

---

## Next Steps

1. **Read the cowork-prompt.md files** — Choose the automation that addresses your #1 pain
2. **Set up connectors** — One-time setup in Claude Cowork
3. **Customize & run** — Paste prompt, edit 3 sections, click Run
4. **Approve & schedule** — React ✅, then `/schedule "automation-name" "cadence"`
5. **Share feedback** — This is a template; customize for your stack

---

## Questions?

Each `XX-automation-name-cowork-prompt.md` file includes:
- Complete step-by-step instructions
- Specific scope filters (what data to pull)
- Approval workflow (how you approve)
- Example outputs
- Fallback behavior

**Start with GTM Chief of Staff.** It's the fastest to set up and delivers immediate value.

**For detailed approval workflows, see [APPROVAL_WORKFLOWS.md](../APPROVAL_WORKFLOWS.md)**

---

**Built with Claude Cowork. Ready to run. Customizable for any GTM stack.**
