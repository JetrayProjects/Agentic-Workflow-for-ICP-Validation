# Automated ICP Validation Workflow

This n8n workflow automates the full **B2B Ideal Customer Profile (ICP)
validation process** -- from extracting companies from an event agenda
to scoring their fit against a vendor profile and storing results in
Google Sheets.

It is designed for **sales, GTM, and growth teams** who want to quickly
identify high-fit prospects at scale using AI-powered research.

------------------------------------------------------------------------

## Overview

The workflow performs the following high-level steps:

1.  Extracts company names from a PDF agenda.
2.  Finds each company's official website.
3.  Scrapes and analyzes both:
    -   The vendor's website (e.g. Ascendo).
    -   Each prospect's website.
4.  Builds structured profiles for both sides.
5.  Evaluates ICP fit using a scoring engine.
6.  Writes results directly to Google Sheets.

End result: a live, continuously updatable **prospect qualification
system**.

------------------------------------------------------------------------

## Workflow Architecture

### 1. Company Extraction

-   Downloads a PDF file from Google Drive.
-   Extracts raw text.
-   Uses Gemini to extract only company names from a specific audience
    section.
-   Parses the output into a clean JSON array.

### 2. Company Website Discovery

-   Uses GPT web search to find the main website for each company.
-   Converts the results into `{ company, url }` pairs.
-   Iterates through companies in batches.

### 3. Vendor Profiling

-   Maps the vendor website using Firecrawl.
-   Filters the most relevant pages using Gemini.
-   Scrapes content from selected URLs.
-   Builds a structured vendor ICP profile (JSON schema).

### 4. Prospect Profiling

-   Maps each prospect's website.
-   Filters relevant pages.
-   Scrapes and summarizes content.
-   Generates a factual company profile for each prospect.

### 5. ICP Validation

-   Combines vendor and prospect profiles.
-   Scores each prospect using:
    -   Must-have signals
    -   Nice-to-have signals
    -   Disqualifiers
    -   Missing information penalties\
-   Produces:
    -   Fit score (0--100)
    -   Fit label (Strong / Possible / Not a Fit)
    -   Confidence level
    -   Key reasoning bullets

### 6. Google Sheets Output

-   Appends or updates one row per company.
-   Keeps a live, structured ICP evaluation table.

------------------------------------------------------------------------

## Output Schema (Google Sheet)

Each row contains:

-   Company Name
-   Industry
-   Sub-Industries
-   Headquarters
-   Regions Served
-   Offerings
-   Primary Customer Types
-   Employee Range
-   ICP Fit Score
-   ICP Fit Label
-   Confidence Level
-   Top Fit Reasons
-   Matched Must-Have Signals
-   Matched Nice-To-Have Signals
-   Disqualifier Signals
-   Missing Information
-   Company Description

------------------------------------------------------------------------

## Tech Stack

-   **n8n** -- Orchestration
-   **Google Drive** -- PDF ingestion
-   **Firecrawl** -- Web mapping + scraping
-   **Gemini (2.5 Flash)** -- Text extraction + profiling
-   **OpenAI (GPT-4.1 / GPT-5)** -- Web search + ICP scoring
-   **Google Sheets** -- Final data store

------------------------------------------------------------------------

## Key Design Principles

-   Facts-only analysis
-   Structured JSON everywhere
-   No marketing fluff
-   Sales-usable outputs
-   Fully automated, no manual research

------------------------------------------------------------------------

## Typical Use Cases

-   Event attendee qualification
-   Account-based marketing (ABM)
-   Conference prospecting
-   Partner evaluation
-   Sales territory planning

------------------------------------------------------------------------

## How to Use

1.  Upload an agenda PDF to Google Drive.
2.  Set the file URL in the workflow.
3.  Set the vendor website URL.
4.  Run the workflow.
5.  Open the connected Google Sheet.

Within minutes, you get a ranked list of **who is actually worth talking
to**.

------------------------------------------------------------------------

## Extending the Workflow

Easy extensions:

-   Add LinkedIn enrichment
-   Add CRM sync (HubSpot / Salesforce)
-   Trigger emails for Strong Fit leads
-   Add industry-specific scoring rules
-   Add revenue estimation agent

------------------------------------------------------------------------

## Why This Is Powerful

This workflow replaces:

-   30+ hours of manual research
-   10+ browser tabs per company
-   Subjective sales opinions

With:

-   Objective AI analysis
-   Reproducible scoring
-   Scalable automation

It turns **lead qualification into an algorithm**.
