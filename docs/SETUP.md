# Setup Guide

## 1. Import the workflow

Import `workflow.json` into your n8n instance. The workflow is inactive by default so you can configure it safely before activation.

## 2. Connect credentials

Create and select your own credentials in n8n for:

- Groq API
- Airtable Personal Access Token
- WooCommerce API
- Gmail OAuth2
- PDFShift API key

The GitHub workflow contains **no reusable credentials or secret keys**.

## 3. Configure Airtable

The workflow uses three logical data areas. You may keep them in separate bases, as represented by the placeholders, or adapt the nodes to your own Airtable design.

### Products table

Required fields:

| Field | Suggested type | Purpose |
|---|---|---|
| SKU | Single line text | Unique product identifier |
| Name | Single line text | Product name |
| Price | Number / Currency | Product price |
| Stock | Number | Available inventory |
| WooID | Number | WooCommerce product ID |
| BatchID | Single line text | Optional batch reference |

Replace:

- `YOUR_AIRTABLE_PRODUCTS_BASE_ID`
- `YOUR_AIRTABLE_PRODUCTS_TABLE_ID`

### Orders table

Required fields:

| Field | Suggested type | Purpose |
|---|---|---|
| OrderID | Autonumber or unique ID | Order reference |
| CustomerName | Single line text | Customer name |
| ProductSKU | Single line text | Product SKU |
| Quantity | Number | Quantity ordered |
| TotalAmount | Currency / Number | Calculated order total |

Replace:

- `YOUR_AIRTABLE_ORDERS_BASE_ID`
- `YOUR_AIRTABLE_ORDERS_TABLE_ID`

### Customers table

Required fields:

| Field | Suggested type | Purpose |
|---|---|---|
| Name | Single line text | Customer name |
| Email | Email | Invoice recipient |
| Phone | Phone / text | Optional contact number |

Replace:

- `YOUR_AIRTABLE_CUSTOMERS_BASE_ID`
- `YOUR_AIRTABLE_CUSTOMERS_TABLE_ID`

## 4. Configure WooCommerce

Create WooCommerce REST API credentials for a test/demo store and select them on each WooCommerce node. Use a staging store while testing product creation and stock updates.

## 5. Configure PDF generation

In the **HTML to PDF** node, replace:

```text
YOUR_PDFSHIFT_API_KEY
```

with your own secure configuration. For production use, prefer an n8n credential or environment-based approach rather than storing the key directly in an exported workflow.

## 6. Configure Gmail

Connect your Gmail OAuth2 credential to the **Send Email** node. Use a test recipient during development.

## 7. Test the workflow

Test one branch at a time:

### Product test

```text
Add 25 black shirts with SKU SHIRT-001 at price 29.99
```

Verify Airtable and WooCommerce.

### Order test

```text
Create an order for Demo Customer for 2 units of SHIRT-001
```

Verify order creation, total calculation, and stock reduction.

### Invoice test

```text
Send the latest invoice to Demo Customer
```

Verify order lookup, customer lookup, PDF generation, and email delivery.

## 8. Production checklist

Before production use, add validation, authentication on the webhook, error handling/retries, idempotency or duplicate prevention, logging, and human review for sensitive operations.
