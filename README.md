# n8n Automation Portfolio

Production-grade n8n workflows powered by AI. Built and tested on a low-spec laptop using free tools only (self-hosted n8n, Gemini free tier, Gmail).

## Projects

| Project | What it does | Stack |
|---|---|---|
| [AI Lead Qualifier](./ai-lead-qualifier) | Scores leads from a web form 1–10 with AI, logs them, alerts on high-value leads | n8n, Gemini, Discord |
| [AI Email Triage](./ai-email-triage) | Reads Gmail over IMAP, classifies as urgent/support/sales/spam, drafts replies | n8n, Gemini, IMAP/SMTP |
| [Clinic Appointment Agent](./clinic-appointment-agent) | Booking, reminders, reschedule/confirm replies, human handoff | n8n, Gemini, IMAP/SMTP |

## Reliability

Every workflow includes:
- Retries on AI calls (4 attempts)
- Error workflow that logs failures to a table and alerts via Discord
- Guard steps to prevent email loops

## Stack

n8n · Google Gemini API · OpenAI · IMAP/SMTP · Discord Webhooks · HTML Email · JSON · Data Tables

## Contact

- LinkedIn: [linkedin.com/in/tahanadeem07](https://linkedin.com/in/tahanadeem07)
- Fiverr: [fiverr.com/tahanadeem07](https://fiverr.com/tahanadeem07)
- Email: tahanadeem934@gmail.com
