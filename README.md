# Deep-OCR API — Postman Collection

Official Postman collection for the [Deep-OCR API](https://deep-ocr.com). Extract structured data from invoices, receipts, contracts, ID documents, and more using AI-powered OCR.

## Download

| File | Description |
|------|-------------|
| [Deep-OCR API.postman_collection.json](./Deep-OCR%20API.postman_collection.json) | Postman Collection (v2.1) |
| [Deep-OCR API.postman_environment.json](./Deep-OCR%20API.postman_environment.json) | Postman Environment |

## Setup

### 1. Import into Postman

1. Open Postman
2. Click **Import** (top left)
3. Drag & drop both files — or select them via the file picker
4. Click **Import**

### 2. Select the Environment

In the top-right corner of Postman, select **Deep-OCR API** from the environment dropdown.

### 3. Set your API key

1. Click the **Eye icon** (environment quick look) next to the dropdown
2. Set the `api_key` variable to your `dpr_...` API key
3. Click **Save**

> Get your API key at [deep-ocr.com](https://deep-ocr.com).

---

## What's Included

### Status
| Request | Description |
|---------|-------------|
| `GET /` | Service information |
| `GET /health` | Health check — use this for uptime monitoring |

### OCR
| Request | `document_type` |
|---------|----------------|
| Process Document (Auto-detect) | *(none — auto-detects)* |
| Process Invoice | `invoice` |
| Process Receipt | `receipt` |
| Process Contract | `contract` |
| Process ID Document | `id_document` |
| Process Delivery Note | `delivery_note` |
| Process Handwriting | `handwriting` |
| Process Bank Statement | `bank_statement` |
| Process Payslip | `payslip` |
| Process Purchase Order | `purchase_order` |
| Process Generic Document | `generic` |

---

## Authentication

All OCR requests require a Bearer token:

```
Authorization: Bearer dpr_your_api_key_here
```

The collection is pre-configured to use the `{{api_key}}` environment variable — just set it once and all requests will be authenticated automatically.

---

## Supported File Types

| Format | Extension |
|--------|-----------|
| PDF | `.pdf` |
| PNG | `.png` |
| JPEG | `.jpg`, `.jpeg` |
| WebP | `.webp` |

**Max file size:** 10 MB

---

## Response Format

```json
{
  "success": true,
  "filename": "hashed_filename",
  "document_type": "invoice",
  "content": {
    // Structured fields depending on document_type
  },
  "metadata": {
    "pages": 1,
    "processing_time_ms": 3100,
    "tokens_input": 12000,
    "tokens_output": 1800,
    "timing": {
      "file_validation_ms": 50,
      "pdf_conversion_ms": 500,
      "image_processing_ms": 200,
      "llm_inference_ms": 2200,
      "auth_ms": 150
    }
  }
}
```

---

## Error Codes

| Code | Meaning |
|------|---------|
| `400` | Invalid file format, missing file, or file too large |
| `401` | Missing or invalid API key |
| `402` | Page quota exhausted — upgrade your plan |
| `403` | API key revoked or not found |
| `413` | File exceeds the 10 MB size limit |
| `429` | Rate limit exceeded (60 requests/minute per API key) |
| `503` | Service temporarily unavailable |

---

## Links

- **Website:** [deep-ocr.com](https://deep-ocr.com)
- **API Reference:** [deep-ocr.com/docs](https://deep-ocr.com/docs)
