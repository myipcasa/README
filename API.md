# 🌐 MyIP.casa API Documentation

[![Service Status](https://img.shields.io/badge/Service-Healthy-success)](https://myip.casa/api/pro/health)
[![License](https://img.shields.io/badge/License-Proprietary-orange)](#)
[![Privacy](https://img.shields.io/badge/Privacy-No--Logs-blue)](#privacy--ethics)
[![IP API](https://img.shields.io/badge/IP-GeoJSON-blue.svg?logo=leaflet)](https://myip.casa/api/ip)
[![Free](https://img.shields.io/badge/Free-100req/day-green.svg)](https://myip.casa/subscribe)
[![JSON](https://img.shields.io/badge/Format-JSON-lightgrey.svg)](https://myip.casa/api/ip)

Welcome to the **MyIP.casa API**. This documentation provides technical specifications for integrating our high-speed IP intelligence, threat detection, and geo-location services.

MyIP.casa delivers fast, accurate IP data for apps, bots, and security tools. Free & Pro IP Geolocation API: Detect public IP, city/ASN details, VPN/proxy, fraud risk. No auth for basics, unlimited scale for pros.

**Public Endpoints** (No auth, 100 req/day/IP):
```
GET /api/ip       - Returns requester's public IP as JSON {"ip": "1.2.3.4"} or text.
GET /api/ip/ping  - API status {"status": "ok"}.
```

**Pro Endpoints** (X-API-Key required):
```
GET  /api/pro/ip       - Get public IP (authenticated).
GET  /api/pro/ping     - API status check (authenticated).
GET  /api/pro/health   - Service health check.
GET  /api/pro/details  - Full geo: city, lat/lon, ASN, ISP, UA parsing, risk score.
GET  /api/pro/security - VPN/Tor/proxy detection, threat analysis.
GET  /api/pro/vpn      - VPN & proxy detection with provider category.
POST /api/pro/bulk     - Analyze up to 50 IPs at once.
GET  /api/pro/usage    - Quota tracking.
```

Perfect for logging, fraud prevention, analytics. 99.9% uptime, IPv6 support. Upgrade via https://myip.casa/subscribe.

**Main Use Cases:**
- Real-time user geolocation in web/apps.
- Fraud detection & bot blocking.
- Network monitoring & compliance.
- Serverless integrations (no backend needed).

keywords: ip api, geolocation api, json api, ai agent tool, vpn detection, tor detection, security

---

## Base URLs

| API | URL |
|-----|-----|
| 🔓 Public API | `https://myip.casa/api/` |
| 🔑 Private API | `https://myip.casa/api/pro/` |

---

## 🚀 Public Endpoints

*No authentication required. Rate-limited to 100 requests per day per IP.*

### Get Client IP

`GET https://myip.casa/api/ip`

```bash
curl https://myip.casa/api/ip
# For private usage with higher limits:
# https://myip.casa/subscribe
```

- **Description:** Returns the public IP address of the requester.
- **Response:** `{"ip": "1.2.3.4"}`

```bash
curl https://myip.casa/api/ip?format=text
```

- **Description:** Returns the public IP address in plain text format.
- **Response:** `1.2.3.4`

```bash
curl https://myip.casa/api/ip/ping
```

- **Description:** Returns the status of the public API.
- **Response:** `{"status":"ok"}`

---

## 💎 Pro Endpoints

*Requires `X-API-Key` header. Optimized for high-concurrency and security use cases.*

### Authentication

```
X-API-Key: YOUR_API_KEY
```

> Note: For security reasons, API keys are displayed only once at purchase time.

---

### 1. Get Public IP (Authenticated)

`GET https://myip.casa/api/pro/ip`

```bash
curl -H "X-API-Key: YOUR_KEY" https://myip.casa/api/pro/ip
```

**Response:**
```json
{
  "ip": "203.0.113.25"
}
```

---

### 2. Service Health

`GET https://myip.casa/api/pro/health`

```bash
curl -H "X-API-Key: YOUR_KEY" https://myip.casa/api/pro/health
```

- **Description:** Checks API availability.

**Response:**
```json
{
  "service": "api_pro",
  "status": "healthy"
}
```

---

### 3. Full Geo-Location

`GET https://myip.casa/api/pro/details`

```bash
curl -H "X-API-Key: YOUR_KEY" https://myip.casa/api/pro/details
```

- **Description:** Complete IP profile — geolocation, network, security signals, and user-agent parsing.

**Response:**
```json
{
  "ip": "203.0.113.25",
  "location": {
    "city": "Toronto",
    "country": "CA",
    "country_name": "Canada",
    "currency": "CAD",
    "latitude": 43.7001,
    "longitude": -79.4163,
    "region": "Ontario",
    "timezone": "America/Toronto"
  },
  "network": {
    "asn": 12345,
    "asn_org": "US Broadband Inc.",
    "usage_type": "Residential",
    "hostname": "ptr_record or No PTR record"
  },
  "security": {
    "is_vpn": false,
    "is_proxy": false,
    "is_tor": false,
    "is_datacenter": false,
    "risk_score": 0,
    "risk_level": "Low",
    "is_bot": false,
    "threat_types": []
  },
  "user_agent": {
    "browser": "curl",
    "os": "Other",
    "is_mobile": false
  },
  "plan": "pro",
  "quota_remaining": 49991,
  "status": "success"
}
```

---

### 4. Security Analysis & Threat Detection

`GET https://myip.casa/api/pro/security`

```bash
curl -H "X-API-Key: YOUR_KEY" https://myip.casa/api/pro/security
```

- **Description:** Real-time detection for VPN, Tor, Proxies, and Datacenter IPs. Specifically designed for fraud prevention.

**Response:**
```json
{
  "ip": "203.0.113.25",
  "network": {
    "asn_org": "US Broadband Inc.",
    "connection_type": "residential"
  },
  "security": {
    "is_datacenter": false,
    "is_proxy": false,
    "is_tor": false,
    "is_vpn": false,
    "risk_level": "Low",
    "risk_score": 0,
    "threat_types": []
  },
  "quota_remaining": 49993
}
```

---

### 5. VPN & Proxy Detection

`GET https://myip.casa/api/pro/vpn`

```bash
curl -H "X-API-Key: YOUR_KEY" https://myip.casa/api/pro/vpn
```

- **Description:** Identifies VPN usage, provider category, and residential vs. datacenter classification.

**Response:**
```json
{
  "ip": "203.0.113.25",
  "is_vpn": false,
  "category": "Residential",
  "provider": "Clean/Residential",
  "quota_remaining": 49992
}
```

---

### 6. Bulk Lookup (Mass Analysis)

`POST https://myip.casa/api/pro/bulk`

- **Description:** Analyze up to 50 IP addresses in a single request to save RTT and resources. IPs not found return an error entry.

**Payload:**
```json
{
  "ips": ["8.8.8.8", "1.1.1.1", "203.0.113.25"]
}
```
```bash
curl -X POST https://myip.casa/api/pro/bulk \
  -H "Content-Type: application/json" \
  -H "X-API-Key: YOUR_KEY" \
  -d '{"ips":["8.8.8.8","1.1.1.1","203.0.113.25"]}'
```

**Response:**
```json
{
  "results": [
    {
      "ip": "8.8.8.8",
      "country": "US",
      "city": "Unknown",
      "asn_org": "Google LLC",
      "usage_type": "Data Center/Hosting",
      "is_vpn": true
    },
    {
      "ip": "1.1.1.1",
      "country": "Unknown",
      "city": "Unknown",
      "asn_org": "Cloudflare, Inc.",
      "usage_type": "Data Center/Hosting",
      "is_vpn": true
    },
    {
      "ip": "203.0.113.25",
      "status": "error",
      "message": "Not found"
    }
  ],
  "count": 3,
  "quota_remaining": 49965
}
---

### 7. Quota Monitoring

`GET https://myip.casa/api/pro/usage`

```bash
curl -H "X-API-Key: YOUR_KEY" https://myip.casa/api/pro/usage
```

- **Description:** Returns current plan details, daily limits, and remaining credits.

**Response:**
```json
{
  "api_key_id": 1,
  "plan": "pro",
  "quota_daily": 50000,
  "used_today": 9
}
```

---

## 🛠 Integration Examples

### curl

```bash
curl -H "X-API-Key: YOUR_API_KEY" https://myip.casa/api/pro/ip
curl -H "X-API-Key: YOUR_API_KEY" https://myip.casa/api/pro/security
curl -H "X-API-Key: YOUR_API_KEY" https://myip.casa/api/pro/vpn
curl -H "X-API-Key: YOUR_API_KEY" https://myip.casa/api/pro/details
curl -H "X-API-Key: YOUR_API_KEY" https://myip.casa/api/pro/health
```

### Python

```python
import requests

url = "https://myip.casa/api/pro/details"
headers = {"X-API-Key": "YOUR_API_KEY"}

response = requests.get(url, headers=headers)
print(response.json())
```

### Node.js (Fetch)

```javascript
const response = await fetch('https://myip.casa/api/pro/security', {
  headers: { 'X-API-Key': 'YOUR_API_KEY' }
});
const data = await response.json();
console.log(data);
```

---

## ⚠️ Error Handling

The API uses standard HTTP status codes and returns a structured JSON object for all errors.

```json
{
  "status": "error",
  "code": 401,
  "message": "Invalid API key"
}
```

| Code | Description |
|------|-------------|
| 400  | Bad Request (missing parameters) |
| 401  | Unauthorized (missing key) |
| 403  | Forbidden (invalid or inactive key) |
| 429  | Too Many Requests (quota exceeded) |

---

## 📊 Rate Limits

| Plan | Limit | Notes |
|------|-------|-------|
| 🔓 Public API | 100 req/day/IP | No authentication required. Returns HTTP 429 when exceeded. Basic IP detection only. |
| 🔑 Private API | Daily quota based on subscription | Real-time tracking via `quota_remaining`. Quota resets at 00:00 UTC daily. |

---

## 🔑 Authentication

All Pro endpoints require a valid API Key passed in the HTTP headers.

- **Header Name:** `X-API-Key`
- **Acquisition:** Get your key at [myip.casa/subscribe](https://myip.casa/subscribe)

---

## Privacy & Ethics

**No-Log Policy:** We do not store, log, or track the IP addresses submitted for processing.

**Data Minimization:** No email addresses or personal identifiers are stored within our API service databases.

**Compliance:** Our service is built with privacy-first principles, ensuring no footprint is left behind.

---

## 📬 Support & Suggestions

For technical support, bug reports, or feature suggestions, please use the Contact section on our official website: [https://myip.casa/contact](https://myip.casa/contact)

---

## 🤖 AI Agents & Bots

Perfect for **LLM agents, crawlers, and monitoring tools**.

---

*© 2026 MyIP.casa · Free IP & Network Analysis Tools*
