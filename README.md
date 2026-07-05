#AI Client Acquisition & Onboarding System

> A fully automated CRM system built with Make.com — No frontend, no manual work. All workflows triggered via Postman.

![Make.com](https://img.shields.io/badge/Make.com-Automation-6B2FA0?style=for-the-badge)
![Airtable](https://img.shields.io/badge/Airtable-Database-18BFFF?style=for-the-badge)
![Groq AI](https://img.shields.io/badge/Groq-AI%20Model-F55036?style=for-the-badge)
![Gmail](https://img.shields.io/badge/Gmail-Email-EA4335?style=for-the-badge)
![Google Drive](https://img.shields.io/badge/Google%20Drive-Storage-34A853?style=for-the-badge)
![Postman](https://img.shields.io/badge/Postman-Testing-FF6C37?style=for-the-badge)

---

##Developer
**Murad Khan**  
Flutter Developer | Automation Engineer  
📧 muradkhankakar33@gmail.com  
🔗 [LinkedIn](https://linkedin.com/in/murad-k-b9428029)

---

##Project Overview

This system manages a complete client lifecycle — from initial inquiry through negotiation, scheduling, follow-ups, and weekly reporting — using **4 automated workflows** in Make.com.

**Key Features:**
- ✅ No frontend required — all requests via Postman
- ✅ AI-powered lead analysis & reply classification (Groq AI)
- ✅ Auto Google Drive folder creation per client
- ✅ Airtable as live CRM database
- ✅ Automated follow-up emails with Cold Lead logic
- ✅ Google Calendar meeting scheduling
- ✅ Weekly AI-generated management report

---

##Tech Stack

| Tool | Purpose |
|------|---------|
| Make.com | Main automation platform |
| Airtable | CRM database (Leads table) |
| Groq AI (llama-3.3-70b) | AI analysis, classification, summaries |
| Gmail | Proposals, follow-ups, reports |
| Google Drive | Auto-create client folders |
| Google Calendar | Schedule meetings |
| Postman | API testing (no frontend) |

---

##Airtable Structure

**Base:** AI CRM System  
**Table:** Leads

| Field | Type |
|-------|------|
| Name | Text |
| Email | Email |
| Company | Text |
| Project Details | Long Text |
| Budget | Number |
| Status | Single Select |
| Last Email Sent | Date |
| Follow-up Count | Number |
| Drive Folder Link | URL |
| Meeting Date | Date |
| Created At | Date |

**Statuses:** `New Lead` → `Proposal Sent` → `Negotiation` → `Follow Up 1/2` → `Call Scheduled` → `Won` / `Lost` / `Cold Lead`

---

## ⚙️ Workflows

### Workflow 1 — New Lead Intake
**Trigger:** Webhook (Postman POST request)

```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "company": "ABC Inc",
  "project": "Need AI chatbot for customer support",
  "budget": "3000"
}
```

**Flow:**
`Webhooks` → `Groq AI (analyze project)` → `Google Drive (create folder)` → `Airtable (save record)` → `Gmail (send proposal)`

---

### Workflow 2 — Client Reply Handler
**Trigger:** Webhook (Postman POST request)

```json
{
  "client_id": "rec_xxxxx",
  "message": "Looks good but pricing is high"
}
```

**AI Classification:**
| Reply Type | Action | Status |
|-----------|--------|--------|
| Negotiating | Update record | Negotiation |
| Ready To Proceed | Create Calendar meeting + email | Call Scheduled |
| Rejected | Update record | Lost |
| Interested | No action | Proposal Sent |

**Flow:**
`Webhooks` → `Groq AI (classify)` → `Router (4 branches)` → `Airtable (update)`

---

### Workflow 3 — Automated Follow-Up System
**Trigger:** Scheduled (Daily at 09:00 AM)

**Logic:**
- Search Airtable for: `Proposal Sent` or `Negotiation`
- If Last Email Sent > 3 days ago → send follow-up email
- Increment Follow-up Count
- If Follow-up Count > 3 → mark as `Cold Lead`

**Flow:**
`Airtable (search)` → `Iterator` → `HTTP/Groq` → `Gmail (send)` → `Airtable (update)`

---

### Workflow 4 — Weekly Management Report
**Trigger:** Scheduled (Every Monday)

**Report includes:**
- Total Leads
- Won Deals
- Lost Deals
- Negotiations
- Calls Scheduled
- Pending Responses

**Flow:**
`Airtable (fetch all)` → `Tools (calculate counts)` → `Groq AI (generate summary)` → `Gmail (send report)`

---

##Testing

All workflows tested via **Postman** — no frontend used.

| Test | Method | Result |
|------|--------|--------|
| WK1 New Lead | POST to WK1 webhook | 200 OK — Lead created, email sent |
| WK2 Client Reply | POST to WK2 webhook | 200 OK — Status updated |
| WK3 Follow-Up | Manual Run | Email sent, count incremented |
| WK4 Weekly Report | Manual Run | AI report email received |

---

##Learning Outcomes

- **Webhooks** — Receive & process HTTP POST requests
- **APIs & Postman** — Simulate real-world calls without frontend
- **Airtable CRM** — Live state database management
- **AI Integration** — Groq AI for analysis & classification
- **State Management** — Lead lifecycle across multiple workflows
- **Scheduling** — Daily & weekly automated triggers
- **Multi-Workflow Architecture** — 4 workflows as one system

---

##Documentation

Full project documentation PDF is included in this repository.

---

> Built with ❤️ by **Murad Khan** |  1 July 2026
