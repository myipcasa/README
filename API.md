# 🌐 MyIP.casa API Documentation

[![Service Status](https://img.shields.io/badge/Service-Healthy-success)](https://myip.casa/api/pro/health)
[![License](https://img.shields.io/badge/License-Proprietary-orange)](#)
[![Privacy](https://img.shields.io/badge/Privacy-No--Logs-blue)](#privacy--ethics)
[![IP API](https://img.shields.io/badge/IP-GeoJSON-blue.svg?logo=leaflet)](https://myip.casa/api/ip)
[![Free](https://img.shields.io/badge/Free-100req/h-green.svg)](https://myip.casa/subscribe)
[![JSON](https://img.shields.io/badge/Format-JSON-lightgrey.svg)](https://myip.casa/api/ip)


Welcome to the **MyIP.casa API**. This documentation provides technical specifications for integrating our high-speed IP intelligence, threat detection, and geo-location services.
MyIP.casa delivers fast, accurate IP data for apps, bots, and security tools. Free & Pro IP Geolocation API: Detect public IP, city/ASN details, VPN/proxy, fraud risk. No auth for basics, unlimited scale for pros.

Public Endpoints (No auth, 100 req/day/IP):

    GET /api/ip - Returns requester's public IP as JSON {"ip": "1.2.3.4"} or text.

    GET /api/ping - API status {"status": "ok"}.

Pro Endpoints (X-API-Key required):

    GET /api/pro/health - Service health check.

    GET /api/pro/details - Full geo: city, lat/lon, ASN, ISP, UA parsing, risk score.

    GET /api/pro/security - VPN/Tor/proxy detection, threat analysis.

    POST /api/pro/bulk - Analyze 50+ IPs at once.

    GET /api/pro/usage - Quota tracking.

Perfect for logging, fraud prevention, analytics. 99.9% uptime, IPv6 support. Upgrade via https://myip.casa/subscribe.

Main Use Cases

    Real-time user geolocation in web/apps.

    Fraud detection & bot blocking.

    Network monitoring & compliance.

    Serverless integrations (no backend needed).

keywords: ip api, geolocation api, json api, ai agent tool, vpn detection, tor detection, security

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
* **Description:** Returns the public IP address of the requester.
* **Response:** `{"ip": "1.2.3.4"}`

```bash
curl https://myip.casa/api/ip?format=text
```
* **Description:** Returns the public IP address of the requester in text format.
* **Response:** `1.2.3.4`

```bash
curl https://myip.casa/api/ip/ping
```
* **Description:** Returns the status of public API.
* **Response:** `{"status":"ok"}`

---

## 💎 Pro Endpoints
*Requires `X-API-Key`. Optimized for high-concurrency and security use cases.*

### 1. Service Health
`GET https://myip.casa/api/pro/health`
* **Description:** Checks API availability.
* **Response:** `{"service": "api_pro", "status": "healthy"}`

### 2. Full Geo-Location
`GET /api/pro/details`
* **Description:** Provides deep network intelligence including city, country, ASN, and ISP details.


```json
{
  "ip": "198.51.100.23",
  "location": {
    "city": "Toronto",
    "region": "Ontario",
    "country": "CA",
    "country_name": "Canada",
    "latitude": 43.6532,
    "longitude": -79.3832,
    "timezone": "America/Toronto",
    "currency": "CAD"
  },
  "network": {
    "asn": 6789,
    "asn_org": "ExampleNet Services",
    "usage_type": "Residential"
  },
  "security": {
    "is_bot": false,
    "risk_level": "Low",
    "risk_score": 0
  },
  "user_agent": {
    "browser": "curl",
    "os": "Other",
    "is_mobile": false
  },
  "plan": "pro",
  "quota_remaining": 49994,
  "status": "success"
}
```

### 3. Security Analysis & VPN Detection
`GET /api/pro/security`
* **Description:** Specifically designed for fraud prevention. Detects if an IP belongs to a VPN, Tor Exit Node, or Proxy.
* **Sample Response:**
```json
{
  "ip": "203.0.113.45",
  "network": {
    "asn_org": "Example Broadband Ltd",
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
  "remaining_usage": 49993,
  "status": "success"
}
```

### 4. Bulk Lookup (Mass Analysis)
`POST /api/pro/bulk`

- **Description:** Analyze up to 50 IP addresses in a single request to save RTT and resources.
- **Payload:**
```json
{
  "ips": ["8.8.8.8", "1.1.1.1"]

}
```

### 5. Quota Monitoring
`GET /api/pro/usage`
- **Description:** Returns current plan details, daily limits, and remaining credits.

---

## 🛠 Integration Examples

### curl
```bash
curl -H "X-API-Key: YOUR_API_KEY" https://myip.casa/api/pro/ip
```

```bash
curl -H "X-API-Key: YOUR_API_KEY" https://myip.casa/api/pro/security
```

```bash
curl -H "X-API-Key: YOUR_API_KEY" https://myip.casa/api/pro/vpn
```

```bash
curl -H "X-API-Key: YOUR_API_KEY" https://myip.casa/api/pro/details
```

```bash
curl -H "X-API-Key: YOUR_API_KEY" https://myip.casa/api/pro/health
```

### Python

import requests
```python
url = "https://myip.casa/api/pro/details"
headers = {"X-API-Key": "YOUR_API_KEY"}

response = requests.get(url, headers=headers)
print(response.json())
```

### Node.js (Fetch)
JavaScript
```JavaScript
const response = await fetch('https://myip.casa/api/pro/security', {
    headers: { 'X-API-Key': 'YOUR_API_KEY' }
});
const data = await response.json();
console.log(data);
```

## 🔑 Authentication
All Pro endpoints require a valid API Key passed in the HTTP headers.

* **Header Name:** `X-API-Key`
* **Acquisition:** Get your key at [myip.casa](https://myip.casa/subscribe)

---

## Privacy & Ethics
No-Log Policy: We do not store, log, or track the IP addresses submitted for processing.

Data Minimization: No email addresses or personal identifiers are stored within our API service databases.

Compliance: Our service is built with privacy-first principles, ensuring no footprint is left behind.


## 📬 Support & Suggestions
For technical support, bug reports, or feature suggestions, please use the Contact section on our official website: [https://myip.casa](https://myip.casa/contact)


## 🚀 AI Agents & Bots

Perfect for **LLM agents, crawlers, monitoring**
