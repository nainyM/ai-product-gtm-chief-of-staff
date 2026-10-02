# GTM Chief of Staff — Connectors

## Overview
The GTM Chief of Staff collects signals from 5 primary connectors. Each provides structured data that feeds into Claude for synthesis.

---

## 1. Google Calendar

**Purpose:** Identify today's meetings, attendees, and agenda items

**Data Extracted:**
- Event title and description
- Time (start/end)
- Attendee list
- Calendar (personal, team, shared)
- Agenda links/documents

**Integration Method:**
- OAuth 2.0 with Google Calendar API
- Scopes: `calendar.readonly`
- Rate limit: ~1000 calls/hour

**Query:**
```
GET https://www.googleapis.com/calendar/v3/calendars/primary/events
Parameters:
  - timeMin: today 00:00:00
  - timeMax: today 23:59:59
  - maxResults: 50
  - singleEvents: true
```

**Fallback:**
- Retry with cached data from yesterday
- Skip if connection fails

**Sample Output:**
```json
{
  "event_id": "abc123",
  "title": "Product Roadmap Sync",
  "time": "2026-10-01T10:00:00Z",
  "duration_minutes": 60,
  "attendees": ["eng-lead", "design-lead", "customer-success"],
  "description": "Q4 prioritization",
  "location": "Zoom link"
}
```

---

## 2. Gmail

**Purpose:** Flag urgent emails and action items from stakeholders

**Data Extracted:**
- Sender
- Subject line
- Priority flag (marked urgent)
- Labels (e.g., blocked, decision, urgent)
- Timestamp
- Snippet (first 100 chars)

**Integration Method:**
- OAuth 2.0 with Gmail API
- Scopes: `gmail.readonly`
- Rate limit: ~1000 calls/hour

**Query:**
```
GET https://www.googleapis.com/gmail/v1/users/me/messages
Parameters:
  - q: "is:starred OR is:important OR from:[key stakeholders]"
  - maxResults: 20
  - after: [24 hours ago timestamp]
```

**Fallback:**
- Retry with cached data
- Skip if connection fails

**Sample Output:**
```json
{
  "message_id": "def456",
  "from": "ceo@company.com",
  "subject": "Mobile app launch delay",
  "priority": "high",
  "timestamp": "2026-10-01T08:30:00Z",
  "snippet": "We need to discuss the mobile launch timeline..."
}
```

---

## 3. Slack

**Purpose:** Capture team updates, mentions, and thread activity

**Data Extracted:**
- Message text
- User and timestamp
- Thread replies count
- Mentions and reactions
- Channel context
- Keywords (blocker, urgent, blocked, decision)

**Integration Method:**
- OAuth 2.0 with Slack API
- Scopes: `channels:history`, `users:read`, `search:read`
- Rate limit: ~60 calls/minute

**Query:**
```
GET https://slack.com/api/search.messages
Parameters:
  - query: "mentions:@[pm_user] OR (blocker OR blocked OR urgent OR decision OR help)"
  - sort: "timestamp"
  - sort_dir: "desc"
  - count: 20
  - after: [24 hours ago]
```

**Fallback:**
- Retry with cached data
- Skip if connection fails

**Sample Output:**
```json
{
  "message": "Database migration hit a blocker—architecture review needed",
  "user": "eng-team",
  "channel": "#engineering",
  "timestamp": "2026-10-01T08:15:00Z",
  "thread_replies": 5,
  "keywords": ["blocker"]
}
```

---

## 4. Jira

**Purpose:** Identify open tickets, blockers, and overdue items

**Data Extracted:**
- Ticket ID and title
- Status (open, in progress, blocked)
- Assignee
- Due date
- Priority
- Labels
- Blocked by / blocks relationships

**Integration Method:**
- OAuth 2.0 with Jira Cloud API (or API token for self-hosted)
- Scopes: `read:jira-work`
- Rate limit: ~100 calls/minute

**Query:**
```
GET https://api.atlassian.com/ex/jira/[site_id]/rest/api/3/issues/search
Parameters:
  - jql: "assignee=currentUser() AND (status=Open OR status='In Progress' OR status=Blocked)"
  - maxResults: 50
  - fields: ["status", "summary", "duedate", "priority", "labels"]
```

**Fallback:**
- Retry with cached data
- Skip if connection fails

**Sample Output:**
```json
{
  "ticket_id": "PROD-1234",
  "title": "Checkout flow testing",
  "status": "Blocked",
  "assigned_to": "qa-team",
  "due_date": "2026-10-02",
  "priority": "high",
  "blocked_by": "PROD-1233"
}
```

---

## 5. Notion

**Purpose:** Track action items, documents, and status updates

**Data Extracted:**
- Page title
- Status (In Progress, Blocked, Complete)
- Owner
- Due date
- Last modified timestamp
- Content summary

**Integration Method:**
- OAuth 2.0 with Notion API
- Scopes: `read:databases`, `read:pages`
- Rate limit: ~3 requests/second

**Query:**
```
POST https://api.notion.com/v1/databases/[database_id]/query
Body:
  - filter: { "property": "Last Edited", "date": { "last_day": {} } }
  - sorts: [{ "property": "Last Edited", "direction": "descending" }]
```

**Fallback:**
- Retry with cached data
- Skip if connection fails

**Sample Output:**
```json
{
  "page_id": "notion_123",
  "title": "Q4 OKRs",
  "status": "In Progress",
  "owner": "product-team",
  "due_date": "2026-12-31",
  "last_updated": "2026-09-30T16:45:00Z",
  "url": "https://notion.so/..."
}
```

---

## Authentication & Security

**Environment Variables Required:**
```
GOOGLE_CALENDAR_API_KEY=[key]
GOOGLE_GMAIL_API_KEY=[key]
SLACK_BOT_TOKEN=[token]
JIRA_API_TOKEN=[token]
NOTION_API_KEY=[key]
```

**OAuth Refresh:**
- Tokens refreshed every 30 minutes
- Failed refresh triggers fallback to cached data

**Data Privacy:**
- No storage of raw email/Slack content
- Only structured metadata stored
- Cache expires after 24 hours
- Deletion logs maintained

---

## Connector Health Check

**Daily at 8:50 AM (before signal collection):**
1. Test each connector endpoint
2. Verify OAuth tokens are valid
3. Log any connection issues
4. Alert if 2+ connectors are down

**Fallback if any connector down:**
- Use previous day's data for that connector
- Note in briefing: "Calendar data cached from yesterday"

---

## Expansion Options (Future)

- **HubSpot/Salesforce:** Customer signals, deals at risk
- **GitHub:** Engineering blocker tracking
- **Analytics Platform:** Real-time metrics and alerts
- **Product Documentation:** Context on features and decisions
