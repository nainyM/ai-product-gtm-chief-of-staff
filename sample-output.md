# GTM Chief of Staff — Sample Output

## Example Morning Briefing

```
GTM CHIEF OF STAFF — Morning Briefing
Date: October 1, 2026
Time: 09:10 AM PST
Status: Ready for Review

═══════════════════════════════════════════════════════════════

🎯 TOP 3 PRIORITIES TODAY

1. MOBILE APP LAUNCH DELAY — Stakeholder decision needed
   Source: Email (CEO), Slack, Jira
   Why it matters: Mobile launch was scheduled for Oct 7. Delay impacts Q4 revenue target ($2.5M at risk). CEO needs decision by EOD on revised timeline.
   What's needed: Schedule brief with CEO + Engineering to agree on new launch date (Oct 14 or Oct 21)
   Timeline: Decision deadline TODAY (5 PM)
   Owner: You (approval), Engineering lead (estimation)
   
2. CHECKOUT FLOW QA TESTING — Blocker with cascading impact
   Source: Jira (PROD-1234), Slack thread, Engineering standup notes
   Why it matters: QA testing is blocked waiting for architecture review. This blocks the November release. Testing was supposed to start yesterday.
   What's needed: Schedule 30-min architecture review with QA and engineering to unblock checkout flow testing
   Timeline: Needs to happen today to stay on track
   Owner: Engineering lead, QA lead
   
3. DATABASE MIGRATION ARCHITECTURE REVIEW — Engineering blocker
   Source: Slack (#engineering), Jira (INFRA-567)
   Why it matters: Database migration to PostgreSQL 15 is blocked on architecture review. This impacts our ability to scale for Black Friday traffic. Without this, we can't commit to hosting vendors.
   What's needed: Schedule architecture review session (1 hour) with backend team and database team
   Timeline: Decision needed by tomorrow to stay on 2-week migration schedule
   Owner: Backend engineering lead

═══════════════════════════════════════════════════════════════

⚠️ BLOCKERS (4 items preventing progress)

1. QA Testing Blocked on Architecture Review
   What's blocked: Checkout flow testing (PROD-1234) — blocks November release timeline
   Root cause: Architecture review scheduled but not completed. QA waiting for sign-off.
   Impact: QA team idle, testing schedule slipping 1 day per day of delay
   Owner: Engineering lead (can unblock)
   Timeline: Critical — needs resolution today
   
2. Database Migration on Hold
   What's blocked: PostgreSQL 15 migration (INFRA-567) — blocks Black Friday scaling
   Root cause: Architecture review pending. Unknown whether current approach can handle 10x traffic
   Impact: Can't commit to hosting infrastructure, vendor negotiations stalled
   Owner: Backend lead (can unblock)
   Timeline: High — needs decision by tomorrow to stay on schedule
   
3. Product Documentation Outdated
   What's blocked: Release notes and product docs for Oct launch — blocks marketing handoff
   Root cause: Feature scope still changing. Docs team waiting for final spec
   Impact: Marketing can't create launch content, launch communication might be late
   Owner: Product team (spec finalization)
   Timeline: Medium — due by Oct 3 to give marketing 4 days
   
4. Contracts Pending Legal Review
   What's blocked: Enterprise customer deal ($250K ARR) — impacts Oct revenue
   Root cause: Legal team slower than expected, 1 week behind schedule
   Impact: Sales can't close deal, customer won't commit without contract
   Owner: Legal team (can unblock)
   Timeline: High — customer needs to sign by Oct 5

═══════════════════════════════════════════════════════════════

🔴 DECISIONS REQUIRING ATTENTION

1. Mobile Launch Timeline
   Question: Do we delay mobile launch to Oct 14 or Oct 21? (Can't launch Oct 7)
   Context: Current mobile app has critical animation bug discovered yesterday. Engineering estimates:
     - Oct 14 launch: Fix bug + 1 week testing (tight but possible)
     - Oct 21 launch: Full regression testing + polish
   Options:
     A) Push to Oct 14 (risky, tight timeline, but limits revenue impact)
     B) Push to Oct 21 (safe, but delays revenue by 2 weeks, impacts Q4 targets)
     C) Launch with known bug, but flag it as "known issue" in release notes (lowest risk for schedule, highest risk for customer satisfaction)
   Decision deadline: TODAY (5 PM) — Engineering needs to start planning immediately after decision
   Owner: You (final call), with input from Engineering + Product
   
2. QA Architecture Review Timing
   Question: Can we do architecture review TODAY or does it need to wait until tomorrow?
   Context: QA team blocked, testing was supposed to start yesterday. Architecture team has slots at:
     - Today 2-3 PM (tight, but possible)
     - Tomorrow 10-11 AM (more prep time)
   Options:
     A) Today 2-3 PM: Quick decision, keeps schedule on track
     B) Tomorrow 10-11 AM: Better prepared review, but costs 1 day of testing
   Decision deadline: By 12 PM today (need to confirm slot with architecture team)
   Owner: Engineering lead
   
3. Database Migration Go/No-Go
   Question: Do we proceed with PostgreSQL 15 migration on current schedule?
   Context: Architecture review pending. If architecture is fundamentally flawed, migration needs to restart from scratch (4-week delay). Risk: Can't handle Black Friday 10x traffic.
   Options:
     A) Go: Proceed with current architecture, accept some risk
     B) Hold: Wait for more thorough review (2-week delay, but lower risk)
   Decision deadline: Tomorrow end-of-day (after architecture review)
   Owner: Backend lead + CTO

═══════════════════════════════════════════════════════════════

📅 TODAY'S MEETINGS

9:30 AM — Product Roadmap Sync (1 hour)
Attendees: You, Engineering lead, Design lead, Customer Success lead
Agenda:
  - Q4 prioritization (40 min)
  - Customer feature requests backlog (15 min)
  - Release timeline review (5 min)
Pre-read: Q4 roadmap doc (updated yesterday)

11:00 AM — Engineering Standup (30 min)
Attendees: Engineering team
Agenda: Daily standup, blockers review
Note: Architecture review discussion likely to come up here

2:00 PM — One-on-one with Engineering Lead (30 min)
Agenda: [Your regular 1:1 topics]
Note: Good time to discuss mobile launch decision, architecture review timing

4:00 PM — Sales Sync (30 min)
Attendees: You, Sales lead, Customer Success
Agenda: Deal status, customer escalations
Note: Expect conversation about enterprise contract delay

═══════════════════════════════════════════════════════════════

📊 METRICS TO WATCH

Mobile App Launch Readiness: 65% complete ↓ (was 75% yesterday)
  - Impact: Animation bug discovery caused regression
  - Action: Needs decision on delay timeline

Database Migration Progress: 20% complete → (stable)
  - Status: On hold pending architecture review
  - Action: Waiting for unblock decision

October Release: 85% complete ↑ (was 80% yesterday)
  - Status: On track except for documentation
  - Action: Needs spec finalization for marketing

Q4 Revenue Forecast: $8.2M → $7.5M ↓ (mobile delay impact)
  - Impact: $700K at risk due to mobile launch delay
  - Action: Decision needed today to confirm new forecast

Customer Health Score: 7.4/10 (stable)
  - Escalations this week: 2 (enterprise contracts, feature requests)
  - Action: Monitor contract delays

═══════════════════════════════════════════════════════════════

🔄 FOLLOW-UPS FROM YESTERDAY'S BRIEFING

✅ Design review for checkout flow — COMPLETED
   Status: Design team completed review, approved for QA
   
⏳ Legal review of enterprise contract — IN PROGRESS (1 day delayed)
   Status: Legal team expects review by end of day tomorrow
   Action needed: Follow up if not received by 5 PM tomorrow
   
❌ Product spec finalization for October release — DELAYED
   Status: Was supposed to be done yesterday, still pending
   Action needed: Schedule 30-min alignment with product team today
   
✅ Engineering resource planning for Q4 — COMPLETED
   Status: Engineering lead confirmed resource allocation
   
⏳ Customer feedback synthesis (from voice-of-customer automation) — PENDING
   Status: Waiting for VoC agent to complete analysis
   Note: This will feed into Monday's roadmap prioritization

═══════════════════════════════════════════════════════════════

🎯 RECOMMENDED ACTIONS FOR TODAY

1. [By 10:30 AM] Confirm 2 PM architecture review slot with engineering team
2. [By 12:00 PM] Schedule decision meeting on mobile launch (you + Engineering lead + CEO)
3. [By 1:00 PM] Send message to Legal team: check on contract review status
4. [By 2:00 PM] Attend architecture review (observe and unblock if needed)
5. [By 5:00 PM] Make decision on mobile launch timeline, communicate to team

═══════════════════════════════════════════════════════════════

Questions? This briefing was generated by Claude at 09:10 AM.
Ready to review and approve? [Approve] [Edit] [Regenerate]
```

---

## Key Features of This Sample

**What's shown:**
- **Priorities** ranked by business impact (not just urgency)
- **Blockers** with clear root causes and who can unblock
- **Decisions** with context, options, and deadlines
- **Meetings** with prep notes
- **Metrics** with trend indicators
- **Follow-ups** from yesterday (shows continuity)
- **Action items** you can immediately execute

**What makes this useful:**
- Specific details (names, numbers, deadlines) vs. generic summaries
- Reasoning visible so you can disagree if needed
- Clear owner for each action item
- Timeline clarity (what needs decision today vs. this week)
- Connected to business outcomes ($700K revenue risk, customer escalations)

**Tone:**
- Professional but direct
- Shows urgency where warranted
- Acknowledges complexity (options for major decisions)
- Respects your judgment (doesn't prescribe the decision)
