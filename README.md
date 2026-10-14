# n8n Automation Portfolio

Production-grade n8n workflows powered by AI. Built and tested on a low-spec laptop using free tools only (self-hosted n8n, Gemini free tier, Gmail).

## Projects

| Project | What it does | Stack |
|---|---|---|
| **[AI Lead Finder & Qualifier](https://github.com/taha-021/n8n-automation-portfolio/tree/main/lead-finder)** | Finds local businesses via Google Maps, scrapes their websites for emails, scores them with AI (1-10), generates personalized cold outreach, and saves qualified leads to Google Sheets. Deduplicates across runs. | n8n, Apify, Firecrawl, Gemini, Google Sheets |
| **[AI Lead Qualifier](https://github.com/taha-021/n8n-automation-portfolio/tree/main/lead-qualifier)** | Scores leads from a web form 1–10 with AI, logs them, alerts on high-value leads | n8n, Gemini, Discord |
| **[AI Email Triage](https://github.com/taha-021/n8n-automation-portfolio/tree/main/email-automation)** | Reads Gmail over IMAP, classifies as urgent/support/sales/spam, drafts replies | n8n, Gemini, IMAP/SMTP |
| **[Clinic Appointment Agent](https://github.com/taha-021/n8n-automation-portfolio/tree/main/Clinic%20Appointment%20Agent)** | Booking, reminders, reschedule/confirm replies, human handoff | n8n, Gemini, IMAP/SMTP |

## Reliability

Every workflow includes:

- Retries on AI calls (4 attempts)
- Error workflow that logs failures to a table and alerts via Discord
- Guard steps to prevent email loops

## Stack

n8n · Google Gemini API · OpenAI · Apify · Firecrawl · IMAP/SMTP · Discord Webhooks · Google Sheets · HTML Email · JSON · Data Tables

## Contact

- LinkedIn: [linkedin.com/in/tahanadeem07](https://linkedin.com/in/tahanadeem07)
- Fiverr: [fiverr.com/tahanadeem07](https://fiverr.com/tahanadeem07)
- Email: [tahanadeem934@gmail.com](mailto:tahanadeem934@gmail.com)
