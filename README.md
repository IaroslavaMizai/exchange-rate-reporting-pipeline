# Exchange Rate Monitoring & Reporting Pipeline

Automated exchange rate monitoring and reporting workflow built with n8n.

This project retrieves historical exchange rate data from the National Bank of Ukraine (NBU) Open Data API, stores exchange rate history in Google Sheets, calculates exchange rate statistics, generates AI-powered summaries using OpenAI GPT-4o-mini, and delivers scheduled email reports.

---

## Overview

The workflow automates the complete exchange rate reporting process.

Exchange rate data is retrieved from the National Bank of Ukraine Open Data API, transformed into a standardized structure, stored in Google Sheets, analyzed using JavaScript, summarized using OpenAI GPT-4o-mini, and distributed automatically via email.

The workflow continuously maintains a historical exchange rate dataset and generates periodic analytical reports.

For each monitored currency, the workflow calculates:

- Current exchange rate
- Minimum exchange rate and occurrence date
- Maximum exchange rate and occurrence date

---

## Features

- Scheduled workflow execution
- NBU Open Data API integration
- Historical exchange rate tracking
- Google Sheets storage
- Date normalization
- Duplicate prevention
- Append-or-update storage strategy
- JavaScript analytics
- OpenAI-powered summaries
- Automated email notifications
- End-to-end workflow automation

---

## Workflow

![Workflow](Images/workflow.png)

---

## Workflow Architecture

```text
Schedule Trigger
      │
      ▼
HTTP Request
      │
      ▼
Filter (USD, EUR)
      │
      ▼
Edit Fields
(Generate Record ID + Normalize Date)
      │
      ▼
Google Sheets
(Append or Update)
      │
      ▼
JavaScript Analytics
      │
      ▼
OpenAI Summary Generation
      │
      ▼
Email Formatting
      │
      ▼
Gmail Notification
```

---

## Technologies

- n8n
- JavaScript
- OpenAI GPT-4o-mini
- Google Sheets
- Gmail
- REST API
- HTTP Request

---

## Prerequisites

Before running the workflow, prepare:

- n8n instance
- OpenAI API access
- Google account
- Gmail OAuth2 credentials
- Google Sheets OAuth2 credentials

---

## Setup Instructions

### 1. Create a Google Sheet

Create a spreadsheet for storing exchange rate history.

Suggested structure:

| id | exchange_date | currency | currency_short | rate |
|----|----|----|----|----|

---

### 2. Configure Google Sheets Credentials

Create a Google Sheets OAuth2 credential in n8n and connect it to your spreadsheet.

---

### 3. Configure Gmail Credentials

Create a Gmail OAuth2 credential in n8n.

---

### 4. Configure OpenAI Credentials

Create an OpenAI credential and connect it to the OpenAI node.

---

### 5. Import the Workflow

Import the workflow JSON file into n8n.

---

### 6. Update Configuration

Replace the following placeholders:

- `YOUR_GOOGLE_SHEET_ID`
- `YOUR_GOOGLE_SHEET_URL`
- `your-email@example.com`

Select your own:

- Google Sheets credentials
- Gmail credentials
- OpenAI credentials

---

### 7. Test the Workflow

Verify that:

- Exchange rates are retrieved successfully
- Records are written to Google Sheets
- Existing records are updated correctly
- Statistics are calculated correctly
- OpenAI summary is generated
- Email delivery succeeds

---

### 8. Activate the Workflow

Enable the workflow and configure the desired schedule.

Example:

- Every Monday
- 08:00 AM

---

## Data Source

Exchange rate data is retrieved from the National Bank of Ukraine Open Data API.

Official documentation:

https://bank.gov.ua/ua/open-data/api-dev

Currencies currently monitored:

- USD (US Dollar)
- EUR (Euro)

---

## Historical Data Storage

Historical exchange rate data is stored in Google Sheets.

### Data Model

| Field | Type |
|---------|---------|
| id | String |
| exchange_date | Date |
| currency | String |
| currency_short | String |
| rate | Number |

### Unique Identifier Examples

```text
USD_24.06.2026
EUR_24.06.2026
```

The unique identifier allows the workflow to update existing records and append new records without creating duplicates.

---

## Workflow Steps

### 1. Data Collection

Retrieve exchange rate data from the NBU Open Data API.

### 2. Currency Filtering

Keep only target currencies:

- USD
- EUR

### 3. Record Preparation

Generate unique IDs and normalize date values.

### 4. Historical Data Storage

Store records using the Append-or-Update strategy.

### 5. Statistical Analysis

Calculate:

- Current exchange rate
- Current exchange rate date
- Minimum exchange rate
- Date of minimum exchange rate
- Maximum exchange rate
- Date of maximum exchange rate

### 6. OpenAI Summary Generation

Generate a concise business-style exchange rate report using OpenAI GPT-4o-mini.

### 7. Email Formatting

Append static content and report metadata.

### 8. Email Delivery

Send the final report automatically via Gmail.

---

## Email Example

![Email Example](Images/email_example.png)

---

## Repository Structure

```text
.
├── README.md
├── workflow
│   └── exchange_rate_reporting.json
└── Images
    ├── workflow.png
    └── email_example.png
```

---

## Security Notes

Sensitive information has been removed from this repository.

The workflow does not contain:

- API keys
- OAuth tokens
- OpenAI credentials
- Gmail credentials
- Google account information
- Spreadsheet IDs
- Spreadsheet URLs
- Email addresses
- n8n instance identifiers

To reproduce this project, create your own credentials and storage resources.

---

## Skills Demonstrated

- Workflow Automation
- REST API Integration
- Data Collection
- Historical Data Management
- Data Transformation
- Data Deduplication
- JavaScript Data Processing
- Google Sheets Automation
- OpenAI Integration
- AI-Augmented Reporting
- Automated Reporting
- ETL Pipeline Design
- Workflow Orchestration

---

## Project Outcomes

This project demonstrates how n8n can be used to automate a complete reporting workflow, from data collection to report delivery.

The solution integrates external API data, maintains historical records, performs automated calculations, generates AI-powered summaries, and distributes reports without manual intervention.

By combining workflow automation, data processing, cloud storage, AI-powered reporting, and scheduled email delivery, the project showcases a practical end-to-end automation solution applicable to financial monitoring and business reporting scenarios.

### Key Capabilities Demonstrated

- Building production-style n8n workflows
- Integrating third-party APIs
- Managing historical datasets
- Implementing deduplication strategies
- Processing data with JavaScript
- Using AI for business reporting
- Automating recurring reporting tasks
