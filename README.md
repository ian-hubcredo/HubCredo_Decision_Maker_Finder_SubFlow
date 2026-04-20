# HubCredo People Finder

## Overview

This is a **sub-workflow called by the HubCredo Outreach AI Reasoning workflow** to find decision-makers at qualified companies. It reads company data from the scored sheet, filters for companies marked as automation agencies with "PROCEED" recommendation, searches Apollo for founders and C-suite executives, uses AI to rank contacts by hierarchy, enriches them in bulk, verifies emails through Reoon, and saves qualified leads to a Google Sheet.

## How It Works

```
Triggered by Parent Workflow -> Filter Qualified Companies -> Apollo People Search -> AI Rank by Hierarchy -> Bulk Enrich -> Email Verify -> Save to Sheet
```

### Workflow Diagram

```mermaid
flowchart TD
    A["Workflow Trigger\nFrom AI Reasoning workflow"] --> B["Filter\nAgency + PROCEED"]
    B --> C["Google Sheets\nGet company details"]
    C --> D["Apollo People Search\nFounders + C-Suite"]
    D --> E{"Results Found?"}
    E -- "Yes" --> F["Extract Contacts"]
    E -- "No" --> G["Fallback Search\nBy domain"]
    G --> H["AI Agent - GPT-5.2\nRank by hierarchy"]
    F --> I["Limit 3 per Domain"]
    I --> J["Batch Enrich via Apollo"]
    J --> K["Reoon Email Verify"]
    K --> L["Google Sheets\nSave leads"]

    style A fill:#1B3A4B,color:#fff
    style D fill:#2C5F7C,color:#fff
    style H fill:#3D5A80,color:#fff
    style J fill:#2C5F7C,color:#fff
    style K fill:#4A6D7C,color:#fff
    style L fill:#274C36,color:#fff
```

## Integrations

- **Apollo.io** - People search and bulk enrichment
- **OpenAI (GPT-5.2)** - Contact hierarchy ranking
- **Google Gemini** - Fallback AI for structured output
- **Reoon** - Bulk email verification
- **Google Sheets** - Lead output

## Setup

1. Import `Hubcredo_People_finder.json` into your n8n instance.
2. Update credentials for Apollo, OpenAI, Google Gemini, Reoon, and Google Sheets.
3. This workflow is designed to be called by the HubCredo Outreach AI Reasoning workflow.
