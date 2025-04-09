# 🚀 Trigger Datadog Synthetic Test via API (Postman + cURL)

This guide explains how to trigger a [Datadog Synthetic Monitoring test](https://docs.datadoghq.com/synthetics/) using the Datadog API via **Postman** and **cURL**. Useful for testing, automation, or integration into CI/CD pipelines.

---

## 🔐 Prerequisites

Before you begin, make sure you have:

1. **Datadog API Key** and **Application Key**  
   → Available at: `Datadog → Integrations → APIs`

2. **Synthetic Test Public ID**  
   → Found in the URL when viewing a test: `https://app.datadoghq.com/synthetics/details/<public_id>`


3. **Correct Datadog API base URL**, depending on your region:

| Region | Base URL |
|--------|----------|
| US     | `https://api.datadoghq.com` |
| US3    | `https://api.us3.datadoghq.com` |
| EU     | `https://api.datadoghq.eu` |
| Gov    | `https://api.ddog-gov.com` |

---

## 📬 Trigger a Test Using Postman

### 🔧 Setup

- **Method:** `POST`
- **URL:**  `https://<your-datadog-site>/api/v1/synthetics/tests/trigger`

Replace `<your-datadog-site>` with the appropriate domain (`api.us3.datadoghq.com`, etc.)

### 🧾 Headers

| Key                 | Value                  |
|---------------------|------------------------|
| `DD-API-KEY`        | Your Datadog API Key   |
| `DD-APPLICATION-KEY`| Your Application Key   |
| `Content-Type`      | `application/json`     |

### 📤 Body (raw → JSON)

```json
{
"tests": [
  {
    "public_id": "your-public-id"
  }
]
}
```

## 💻 Trigger a Test Using cURL

```
curl -X POST "https://<your-datadog-site>/api/v1/synthetics/tests/trigger" \
  -H "DD-API-KEY: <YOUR_DATADOG_API_KEY>" \
  -H "DD-APPLICATION-KEY: <YOUR_DATADOG_APP_KEY>" \
  -H "Content-Type: application/json" \
  -d '{
    "tests": [
      {
        "public_id": "your-public-id"
      }
    ]
  }'
```

## ✅ Expected Response

A successful request will return a response containing a `batch_id` and `result_id`, like:
```
{
  "batch_id": "abc123",
  "results": [
    {
      "public_id": "your-public-id",
      "result_id": "result-id-123"
    }
  ]
}
```
