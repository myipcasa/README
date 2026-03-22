# 🌐 MyIP.casa API Documentation

[![Service Status](https://img.shields.io/badge/Service-Healthy-success)](https://myip.casa/api/pro/health)
[![License](https://img.shields.io/badge/License-Proprietary-orange)](#)
[![Privacy](https://img.shields.io/badge/Privacy-No--Logs-blue)](#privacy--ethics)
[![IP API](https://img.shields.io/badge/IP-GeoJSON-blue.svg?logo=leaflet)](https://myip.casa/api/ip)
[![Free](https://img.shields.io/badge/Free-100req/day-green.svg)](https://myip.casa/subscribe)
[![JSON](https://img.shields.io/badge/Format-JSON-lightgrey.svg)](https://myip.casa/api/ip)

Welcome to the **MyIP.casa API**. This documentation provides technical specifications for integrating our high-speed IP intelligence, threat detection, and geo-location services.

MyIP.casa delivers fast, accurate IP data for apps, bots, and security tools. Free & Pro IP Geolocation API: Detect public IP, city/ASN details, VPN/proxy, fraud risk. No auth for basics, unlimited scale for pros. IPv4 and IPv6 supported throughout.

**Public Endpoints** (No auth, 100 req/day/IP):
```
GET /api/ip       - Returns requester's public IP as JSON {"ip": "1.2.3.4"} or text.
GET /api/ip/ping  - API status {"status": "ok"}.
```

**Pro Endpoints** (X-API-Key required):
```
GET  /api/pro/ip          - Get public IP (authenticated).
GET  /api/pro/ping        - API status check (authenticated).
GET  /api/pro/health      - Service health check.
GET  /api/pro/details     - Full geo: city, lat/lon, ASN, ISP, UA parsing, risk score, evidence. Accepts optional ?ip=.
GET  /api/pro/security    - VPN/Tor/proxy/datacenter detection, evidence array & reputation. Accepts optional ?ip=.
GET  /api/pro/vpn         - VPN & proxy detection with provider category. Accepts optional ?ip=.
POST /api/pro/bulk        - Analyze up to 50 IPs at once. Accepts optional ?mode=fast.
POST /api/pro/bulk/export - Same as /bulk but returns a CSV file attachment.
GET  /api/pro/usage       - Quota tracking with reset countdown.
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
# Query any IPv4 or IPv6 address using the optional ?ip= parameter:
curl -H "X-API-Key: YOUR_KEY" "https://myip.casa/api/pro/details?ip=203.0.113.25"
```

- **Description:** Complete IP profile — geolocation, network, security signals, and user-agent parsing. Defaults to the caller's IP if `?ip=` is omitted. The `evidence` array provides human-readable reasons explaining the risk score. The `cached` field indicates whether the response was served from cache.

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
    "hostname": "ptr.example.net"
  },
  "security": {
    "is_vpn": false,
    "is_proxy": false,
    "is_tor": false,
    "is_datacenter": false,
    "risk_score": 0,
    "risk_level": "Low",
    "evidence": [],
    "is_bot": false
  },
  "user_agent": {
    "browser": "curl",
    "os": "Other",
    "is_mobile": false
  },
  "plan": "pro",
  "quota_remaining": 49991,
  "status": "success",
  "cached": false
}
```

---

### 4. Security & Reputation

`GET https://myip.casa/api/pro/security`

```bash
curl -H "X-API-Key: YOUR_KEY" https://myip.casa/api/pro/security
# Query any IPv4 or IPv6 address using the optional ?ip= parameter:
curl -H "X-API-Key: YOUR_KEY" "https://myip.casa/api/pro/security?ip=203.0.113.25"
```

- **Description:** Real-time detection for VPN, Tor, proxies, and datacenter IPs. The `evidence` array provides human-readable reasons explaining the risk score. The `reputation` block reports blacklist status and local incident count. Accepts an optional `?ip=` query parameter to analyze any IPv4 or IPv6 address.

**Response:**
```json
{
  "ip": "203.0.113.25",
  "network": {
    "asn_org": "US Broadband Inc.",
    "connection_type": "residential",
    "hostname": "ptr.example.net"
  },
  "security": {
    "is_datacenter": false,
    "is_proxy": false,
    "is_tor": false,
    "is_vpn": false,
    "risk_level": "Low",
    "risk_score": 5,
    "evidence": []
  },
  "reputation": {
    "is_listed": false,
    "local_incidents": 0
  },
  "quota_remaining": 49993
}
```

> **Note on `connection_type`:** Possible values include `residential`, `Data Center/Hosting`, `Tor Exit Node`, `Business/Unknown`, and others depending on the IP classification.

---

### 5. VPN & Proxy Detection

`GET https://myip.casa/api/pro/vpn`

```bash
curl -H "X-API-Key: YOUR_KEY" https://myip.casa/api/pro/vpn
# Query any IPv4 or IPv6 address using the optional ?ip= parameter:
curl -H "X-API-Key: YOUR_KEY" "https://myip.casa/api/pro/vpn?ip=203.0.113.25"
```

- **Description:** Identifies VPN usage, provider category, and residential vs. datacenter classification. Supports both IPv4 and IPv6.

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

- **Description:** Analyze up to 50 IPv4 or IPv6 addresses in a single request. Each result includes country, ASN org, risk scoring, VPN detection, and a human-readable `evidence` array. The response includes a `summary` object with aggregated statistics, a `truncated` flag, and the `mode` used. Use `?mode=fast` for reduced latency (same response schema).

**Payload:**
```json
{
  "ips": ["198.51.100.10", "198.51.100.42", "203.0.113.25"]
}
```
```bash
curl -X POST https://myip.casa/api/pro/bulk \
  -H "Content-Type: application/json" \
  -H "X-API-Key: YOUR_KEY" \
  -d '{"ips":["198.51.100.10","198.51.100.42","203.0.113.25"]}'

# Fast mode (reduced latency, same response schema):
curl -X POST "https://myip.casa/api/pro/bulk?mode=fast" \
  -H "Content-Type: application/json" \
  -H "X-API-Key: YOUR_KEY" \
  -d '{"ips":["198.51.100.10","198.51.100.42","203.0.113.25"]}'
```

**Response:**
```json
{
  "results": [
    {
      "ip": "198.51.100.10",
      "country": "US",
      "city": "Unknown",
      "asn_org": "Example CDN LLC",
      "risk_score": 80,
      "risk_level": "High",
      "is_vpn": true,
      "evidence": ["DataCenter/VPN IP address", "Automated traffic from hosting network"]
    },
    {
      "ip": "198.51.100.42",
      "country": "Unknown",
      "city": "Unknown",
      "asn_org": "Example Hosting Ltd.",
      "risk_score": 80,
      "risk_level": "High",
      "is_vpn": true,
      "evidence": ["DataCenter/VPN IP address", "Automated traffic from hosting network"]
    },
    {
      "ip": "203.0.113.25",
      "status": "error",
      "message": "Not found in database"
    }
  ],
  "summary": {
    "total": 3,
    "high_risk": 2,
    "vpn_detected": 2,
    "low_risk": 0,
    "errors": 1
  },
  "truncated": false,
  "count": 3,
  "mode": "full",
  "quota_remaining": 49974
}
```

---

### 7. Bulk Export (CSV)

`POST https://myip.casa/api/pro/bulk/export`

- **Description:** Same analysis as `/api/pro/bulk` but returns results as a **CSV file attachment** instead of JSON. Useful for offline processing or spreadsheet imports. The `?mode=fast` parameter is also supported.

```bash
curl -X POST https://myip.casa/api/pro/bulk/export \
  -H "Content-Type: application/json" \
  -H "X-API-Key: YOUR_KEY" \
  -d '{"ips":["198.51.100.10","198.51.100.42","203.0.113.25"]}' \
  --output results.csv
```

**Response:** `text/csv` file attachment.

```
ip,country,city,asn_org,risk_score,risk_level,is_vpn,evidence,status,message
198.51.100.10,US,Unknown,Example CDN LLC,80,High,true,"DataCenter/VPN IP address",,
198.51.100.42,Unknown,Unknown,Example Hosting Ltd.,80,High,true,"DataCenter/VPN IP address",,
203.0.113.25,,,,,,,,error,Not found in database
```

---

### 8. Quota Monitoring

`GET https://myip.casa/api/pro/usage`

```bash
curl -H "X-API-Key: YOUR_KEY" https://myip.casa/api/pro/usage
```

- **Description:** Returns current plan details, daily quota limit, requests made today, remaining quota, and the time until the next daily reset (formatted as `HH:MM:SS`).

**Response:**
```json
{
  "plan": "pro",
  "quota_limit": 50000,
  "requests_today": 15,
  "quota_remaining": 49985,
  "reset_in": "13:39:15",
  "status": "active"
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

### Python — Bulk with summary

```python
import requests

r = requests.post(
    "https://myip.casa/api/pro/bulk",
    headers={"Content-Type": "application/json", "X-API-Key": "YOUR_API_KEY"},
    json={"ips": ["198.51.100.10", "198.51.100.42", "203.0.113.25"]}
)
data = r.json()
print(f"High risk: {data['summary']['high_risk']} / {data['summary']['total']}")
print(f"VPNs detected: {data['summary']['vpn_detected']}")
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
