<img width="1360" height="960" alt="02_LeadRoute_diagram" src="https://github.com/user-attachments/assets/3b9a43ea-e01f-4040-82c4-9a5c4b51b211" />
[leadroute.json](https://github.com/user-attachments/files/32848274/leadroute.json)
# LeadRoute — Multi-Source Real Estate Lead Management Automation

A lead capture and routing system for a real estate business. It collects leads from several channels, removes duplicates, gives each lead an ID, assigns it to the right agent by city, notifies everyone involved, and follows up if the agent hasn't acted.

**Built with:** n8n · Webhooks (Facebook, website, WhatsApp) · Google Sheets · Gmail · JavaScript · Scheduled sync

---

## The Problem
Real estate leads arrive from Facebook ads, website forms and WhatsApp. When they're handled manually, leads get duplicated, go to the wrong agent, or sit untouched, and a slow response often means a lost client.

## What It Does
1. **Multi-source intake:** Separate webhooks for Facebook lead ads, the website form and WhatsApp, plus a manual trigger for testing.
2. **Normalize:** Data from every source is mapped into one consistent format.
3. **Deduplicate:** A decision engine checks for existing leads, and duplicates are logged separately instead of being re-processed.
4. **Lead ID:** New leads get a sequential ID from a lead counter.
5. **Agent assignment:** The right agent is looked up by city from an agents sheet.
6. **Record and notify:** The lead is added to the master sheet, the assigned agent gets an email, and the customer receives a confirmation email with their lead ID.
7. **Route by city:** Leads are copied to city sheets for Delhi, Mumbai, Bangalore and Kolkata.
8. **Follow-up:** After a wait, the workflow checks whether the agent has acted and sends a reminder if not.
9. **Scheduled sync:** A scheduled run reads the city sheets and updates the master sheet, so status changes made by city teams flow back to one place.

## Architecture
![Workflow diagram](diagram.png)

## Key Design Decisions
- **One pipeline for all channels:** normalizing early means dedup, ID generation and routing only had to be built once.
- **Duplicates are logged, not dropped:** the team can still see repeat enquiries, which often signal a warm lead.
- **Two-way sync:** city teams work in their own sheets, and the master sheet stays current automatically.

## Files
- `leadroute.json` — n8n workflow export (credentials, webhook paths and sheet IDs replaced with placeholders)
- `diagram.png` — architecture diagram

## Setup
1. Import `leadroute.json` into n8n.
2. Connect Google Sheets and Gmail credentials.
3. Replace `YOUR_GOOGLE_SHEET_ID` with your master, agents and city sheet IDs.
4. Point your Facebook, website and WhatsApp sources at the workflow's webhook URLs.

---
Built by **Pranita Priya**, n8n & AI Automation Builder
