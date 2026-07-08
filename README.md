# AI Lead Generation & Enrichment System

A Make.com automation that captures inbound leads and automatically enriches them with company, role, and social profile data — built by [Sohag Gain](https://bd.linkedin.com/in/sohaggain), Founder & CEO of [AI Smart Galaxy](https://www.aismartgalaxy.com), an AI automation agency helping businesses adopt AI-driven workflows.

This project was built to remove manual lead research from AI Smart Galaxy's own sales process, and demonstrates a two-path AI enrichment pipeline: structured CRM-based enrichment (Apollo) running in parallel with unstructured web-scraped enrichment (Apify + AI summarization).

## What It Does

1. **Google Forms (Watch Responses)** — captures new inbound leads submitted through the AI Smart Galaxy Lead Generation Form (First Name, Last Name, Email).
2. **Google Sheets (Add a Row)** — logs the raw lead immediately to a central tracking sheet.
3. **Apollo (Create a Contact)** — pushes the lead into Apollo.io as a CRM contact using their submitted email.
4. **Router** — splits the flow into two parallel enrichment paths:

   **Path 1 — Structured Enrichment**
   - **Text Parser (Match Pattern)** — extracts structured fields from the lead data.
   - **HTTP (Make a Request)** — calls an external enrichment endpoint.
   - **OpenAI (Generate a Completion)** — synthesizes the retrieved data into a clean enrichment summary.
   - **Tools (Set Variable)** — stores the result for downstream use.

   **Path 2 — Social/Web Enrichment**
   - **Apify (Run an Actor)** — runs a LinkedIn profile scraping actor against the lead's public profile.
   - **Apify (Get Dataset Items)** — retrieves the scraped profile data (work history, education, verified contact info).
   - **Tools (Get Variable)** — pulls in prior context for the AI step.
   - **OpenAI (Generate a Completion)** — writes a natural-language enrichment summary (e.g. "X is the [role] at [company], with a background in...").
   - **Google Sheets (Update a Row)** — writes the final enriched profile — company, website, LinkedIn URL, and AI-generated summary — back to the tracking sheet.

## Tracking Sheet Structure

`First Name | Last Name | Email | Website | Company | Data Enrichment | LinkedIn Profile`

The "Data Enrichment" column holds the AI-generated summary, giving the sales team an instant, readable snapshot of who the lead is without manual research.

## Tech Stack

| Component | Tool |
|---|---|
| Orchestration | [Make.com](https://make.com) |
| Lead capture | Google Forms |
| CRM sync | [Apollo.io](https://apollo.io) |
| Profile scraping | [Apify](https://apify.com) (LinkedIn scraper) |
| AI summarization | OpenAI (GPT) |
| Lead tracking | Google Sheets |
| Flow branching | Make.com Router |

## Setup

1. Import the Make.com blueprint into a new scenario.
2. Reconnect your own accounts for:
   - Google Forms / Google Sheets
   - Apollo.io
   - Apify
   - OpenAI API
3. Replace the Google Form ID with your own lead capture form (First Name, Last Name, Email fields).
4. Point the Google Sheets modules at your own tracking spreadsheet, matching the column structure above.
5. Configure the Apify actor with your LinkedIn scraping input parameters.
6. Adjust the OpenAI prompts in each path to match your desired enrichment summary style.
7. Turn on the scenario and set your preferred polling interval.

## Why This Matters

Manually researching every inbound lead — checking their company, role, LinkedIn, and background — doesn't scale past a handful of leads a day. This system automates that research in two complementary ways: structured CRM enrichment via Apollo for firmographic data, and AI-summarized web enrichment via Apify + OpenAI for a natural-language snapshot a sales rep can read in five seconds instead of five minutes of digging.

## About AI Smart Galaxy

AI Smart Galaxy is an AI automation agency founded by Sohag Gain, specializing in AI Agents, workflow automation (n8n, Make.com, Zapier, GoHighLevel), and business process automation for agencies, SaaS companies, e-commerce, real estate, coaches, and service businesses.

🌐 [aismartgalaxy.com](https://www.aismartgalaxy.com) | [Services](https://aismartgalaxy.com/services-ai-automation) | [LinkedIn](https://bd.linkedin.com/in/sohaggain)

## Author

**Sohag Gain**
Founder & CEO, AI Smart Galaxy — AI Automation, AI Agents & Business Workflow Consulting
