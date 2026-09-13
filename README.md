# AI E-Commerce Operations Automation

A portfolio-ready **AI-powered e-commerce operations workflow** built with **n8n**. The system accepts natural-language requests, classifies the requested operation, extracts structured business data with AI, and routes the request into product, order, or invoice automation.

## What the project solves

E-commerce teams often repeat the same operational tasks manually: updating inventory, creating products, recording orders, reducing stock, finding customer/order data, and generating invoices. This workflow combines AI with automation so those operations can be triggered from a simple request and executed across the connected systems.

## Workflow architecture

```text
Webhook / User Request
        |
        v
AI Automation Manager
        |
        +--> PRODUCT --> Extract product data --> Airtable inventory
        |                                      --> WooCommerce create/update
        |
        +--> ORDER ----> Extract order data ----> Check inventory
        |                                      --> Calculate total
        |                                      --> Airtable order record
        |                                      --> Reduce stock
        |                                      --> WooCommerce stock update
        |
        +--> INVOICE --> Identify customer -----> Find order + product + customer
                                               --> Generate invoice HTML
                                               --> Convert HTML to PDF
                                               --> Send invoice through Gmail
```

## Core features

- Natural-language request classification with an AI agent
- Product creation and inventory updates
- WooCommerce product synchronization
- Order extraction and processing
- Inventory lookup and automatic stock reduction
- Airtable-based products, orders, and customer records
- Automated invoice HTML generation
- PDF invoice conversion
- Gmail invoice delivery
- Webhook-based entry point for external apps or frontends

## Tech stack

- **n8n** — workflow orchestration
- **Groq / LLM** — request classification and structured data extraction
- **WooCommerce** — product and stock operations
- **Airtable** — operational data / lightweight CRM
- **Gmail** — invoice delivery
- **PDFShift** — HTML-to-PDF conversion
- **JavaScript** — data transformation and calculations
- **REST / Webhooks** — workflow entry and external integrations

## Repository structure

```text
AI-Ecommerce-Operations-Automation/
├── workflow.json
├── README.md
├── .gitignore
├── NOTICE.md
└── docs/
    └── SETUP.md
```

## Quick start

1. Import `workflow.json` into n8n.
2. Connect your own Groq, Airtable, WooCommerce, Gmail, and PDFShift credentials.
3. Replace the Airtable placeholder Base IDs and Table IDs.
4. Create the required Airtable fields listed in `docs/SETUP.md`.
5. Configure the WooCommerce store connection.
6. Test the webhook with a demo request before activating the workflow.

> No API keys, credentials, private account IDs, or source-owner data are included in this repository.

## Example requests

```text
Add 25 black shirts with SKU SHIRT-001 at price 29.99
Create an order for Demo Customer for 2 units of SHIRT-001
Send the latest invoice to Demo Customer


