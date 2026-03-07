# Threat Intelligence Feed Dashboard

## Problem Statement
Security analysts can often be overwhelmed by the large amounts of threat intelligence data that comes from security blogs, CVE feeds, vulnerability databases, and other sources. Reviewing this manually and being able to accurately prioritize its information takes up a lot of time and can lead to some threats being overlooked. This project is going to automate the collection, summarization, and prioritization of threat intelligence using AI. This will allow analysts to focus on more time-sensitive security threats.

## Architecture

## Components
- **Data Ingestion:** Collects threat intelligence data from sources such as RSS feeds, CVE databases, and security blogs. The data is normalized and stored in Airtable for further processing.
- **AI Processing:** Uses an AI model through Flowise and the Groq API to summarize threat reports and extract indicators of compromise (IOCs).
- **Relevance Scoring:** Evaluates how relevant each threat is to an organization by comparing threat data to the organization’s technology stack and assigning a relevance score.
- **Output Dashboard:** Displays prioritized threat intelligence through an Airtable dashboard where analysts can review summaries, severity levels, and extracted indicators.

## How to Run
1. Configure the n8n workflow to ingest threat intelligence data from RSS feeds and security blogs.
2. Store normalized threat records in Airtable.
3. Run the Flowise AI workflow to summarize threat reports and extract IOCs using the Groq API.
4. Apply the relevance scoring component to prioritize threats.
5. View results in the Airtable dashboard interface.
