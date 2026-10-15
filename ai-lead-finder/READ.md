# AI Lead Finder

Finds local businesses on Google Maps, audits their websites, scores them with AI, and writes personalized cold outreach — automatically.

## The Problem

Finding qualified local business leads means hours of manual work: searching Google Maps, clicking each website, hunting for emails, guessing who's worth contacting. Most lead lists are unqualified, outdated, or full of duplicates.

## The Solution

Enter a niche and a city. 60 seconds later, you have a spreadsheet of qualified leads, each scored 1–10 with a personalized cold email ready to send.

## How It Works

1. User submits a **niche** (e.g., "barbershops") and **location** (e.g., "Manchester") via form.
2. Apify scrapes Google Maps for matching businesses.
3. System checks Google Sheet and skips businesses already contacted.
4. Firecrawl scrapes each website for page content.
5. Regex extracts emails from the scraped content.
6. Gemini scores each lead 1–10 based on digital presence signals.
7. Hot leads (score 7+) get a personalized cold email written by Gemini.
8. Everything saves to Google Sheets.

## Deduplication

Two layers:
- **Sheet-level:** Reads existing Google Sheet first, filters out businesses already saved.
- **In-batch:** Normalizes URLs (strips `https://`, `www.`, trailing slashes) to catch duplicates within the same run.

Run the same search repeatedly and only get new leads each time.

## Scoring Logic

| Signal | Points |
|--------|--------|
| No email found on website | +3 |
| Reviews < 50 | +2 |
| Rating < 4.5 | +2 |
| Reviews > 300 | −2 |
| Email found | −1 |

**Score 7+ = Hot lead** → gets outreach draft, saves to sheet.

Why "no email" is a *positive* signal: businesses without easy contact routes need digital help. That's the target customer.

## Node Map

| # | Node | Purpose |
|---|------|---------|
| 1 | On Form Submission | User enters niche + location |
| 2 | Search Google Maps | Apify scrapes up to N businesses |
| 3 | Read Existing Leads | Fetches all rows from Google Sheet |
| 4 | Filter Existing | Removes already-saved + in-batch duplicates |
| 5 | Has Website? | Skips businesses without a site |
| 6 | Scrape Website | Firecrawl scrapes each site (error-tolerant) |
| 7 | Extract Emails | Regex pulls emails + normalizes fields |
| 8 | Score Lead | Gemini scores 1–10 with reason |
| 9 | Parse Score | Splits score + reason into clean fields |
| 10 | Hot Lead? | Filters scores 7+ |
| 11 | Write Outreach | Gemini writes personalized cold email |
| 12 | Save Hot Leads | Appends to Google Sheet |

## Error Handling

- **Scrape failures:** Firecrawl errors don't kill the workflow — failed scrapes route to a No-Op.
- **Empty sheet:** `Read Existing Leads` uses "Always Output Data" so the first run works.
- **Gemini failures:** Retries 4 times with 5-second waits.
- **Workflow crashes:** Logged to Data Table + Discord alert via error workflow.

## Setup

1. Import the workflow JSON into n8n.
2. Create credentials (do NOT hardcode keys):
   - **Apify** → Query Auth credential with `token`
   - **Firecrawl** → Header Auth credential with `Authorization: Bearer fc-...`
   - **Gemini** → API credential
   - **Google Sheets** → OAuth2
3. Create a Google Sheet named `Lead Finder` with headers:
   `Title | Phone | Website | Email | Rating | Reviews | Address | Score | Reason | Outreach`
4. Update the form fields to match your target market.
5. Activate the workflow and submit via Production URL.

## Example Output

| Title | Rating | Reviews | Score | Reason | Outreach |
|---|---|---|---|---|---|
| Barnes Real Estate Group | 5.0 | 27 | 8 | No email found, low review count | "Hey Barnes team, I noticed you're using a link-in-bio page instead of a dedicated website…" |
| Grange London Limited | 4.9 | 149 | 3 | High rating, email listed — established | (skipped) |

## Best Verticals

Works best for **local service businesses with weak digital presence:**
- Barbershops, salons, gyms
- Plumbers, electricians, tree surgeons
- Restaurants, cafes, bars
- Tutors, cleaners, pest control

Less effective for: real estate agencies, hotels, established firms — they already have emails and strong sites.

## Stack

n8n · Apify (Google Maps Scraper) · Firecrawl · Google Gemini · Google Sheets · JavaScript (Code nodes)

## Author

Taha Nadeem — [LinkedIn](https://linkedin.com/in/tahanadeem07) · [Fiverr](https://fiverr.com/tahanadeem07) · [tahanadeem934@gmail.com](mailto:tahanadeem934@gmail.com)
