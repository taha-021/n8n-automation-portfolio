Clinic Appointment Agent

An appointment system built with n8n and Gemini AI. Patients book online, get confirmations and reminders, and reschedule by replying to an email. The front desk is alerted only when a human is needed.

Portfolio demo with dummy data.

Features
Online booking form that rejects past dates
Taken slot? Shows the free times for that day
Instant confirmation email and a reminder the day before
AI reads patient replies: confirm, reschedule (checks availability, moves the booking, emails the patient), or question/unclear (alerts the front desk)
Every error is logged and sent to Discord
Workflows
Workflow	Trigger
Clinic - Booking	n8n Form
Clinic - Reminders	Schedule (hourly)
Clinic - Replies	IMAP email
Clinic - Error Handler	Error Trigger

JSON files are in workflows/, screenshots in screenshots/.

Stack

n8n · Google Gemini · SMTP/IMAP · Discord. Easy to swap for Slack, Teams, Sheets, Airtable, WhatsApp, or OpenAI.

Setup
Create two n8n Data Tables: appointments and error_logs.
Import the four JSON files and add your credentials.
Set Error Handler as the error workflow on the other three.
Replace YOUR_PRODUCTION_FORM_URL and the sender email, then activate.
Limitations

Runs on localhost, so it only works while my laptop and n8n are running. Dummy data only. I can build a production-ready version for you, hosted and running 24/7.

Contact

Feel free to ask for the full demo video.

LinkedIn : https://www.linkedin.com/in/tahanadeem07
