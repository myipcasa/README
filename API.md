# 🌐 MyIP.casa API Documentation

[![Service Status](https://img.shields.io/badge/Service-Healthy-success)](https://myip.casa/api/pro/health)
[![License](https://img.shields.io/badge/License-Proprietary-orange)](#)
[![Privacy](https://img.shields.io/badge/Privacy-No--Logs-blue)](#privacy--ethics)

Welcome to the **MyIP.casa API**. This documentation provides technical specifications for integrating our high-speed IP intelligence, threat detection, and geo-location services.

---

## 🔑 Authentication
All Pro endpoints require a valid API Key passed in the HTTP headers.

* **Header Name:** `X-API-Key`
* **Acquisition:** Get your key at [myip.casa](https://myip.casa/subscribe)

---

## 🚀 Public Endpoints
*No authentication required. Rate-limited to 100 requests per day per IP.*

### 1. Get Client IP
`GET https://myip.casa/api/ip`
* **Description:** Returns the public IP address of the requester.
* **Response:** `{"ip": "1.2.3.4"}`

### 2. Service Health
`GET https://myip.casa/api/pro/health`
* **Description:** Checks API availability.
* **Response:** `{"service": "api_pro", "status": "healthy"}`

---

## 💎 Pro Endpoints
*Requires `X-API-Key`. Optimized for high-concurrency and security use cases.*

### 1. Full Geo-Location
`GET /api/pro/details`
* **Description:** Provides deep network intelligence including city, country, ASN, and ISP details.

### 2. Security Analysis & VPN Detection
`GET /api/pro/security`
* **Description:** Specifically designed for fraud prevention. Detects if an IP belongs to a VPN, Tor Exit Node, or Proxy.
* **Sample Response:**
```json
{
  "ip": "1.2.3.4",
  "security": {
    "is_tor": false,
    "is_vpn": true,
    "is_proxy": false,
    "is_datacenter": true,
    "risk_score": 0,
    "risk_level": "Low"
  }
}
```

### 3. Bulk Lookup (Mass Analysis)
`POST /api/pro/bulk`

- **Description:** Analyze up to 50 IP addresses in a single request to save RTT and resources.
- **Payload:**
```json
{
  "ips": ["8.8.8.8", "1.1.1.1"]

}
```

### 4. Quota Monitoring
`GET /api/pro/usage`
- **Description:** Returns current plan details, daily limits, and remaining credits.

---

## 🛠 Integration Examples

### curl
```json
curl -H "X-API-Key: YOUR_API_KEY" https://myip.casa/api/pro/ip
```

```json
curl -H "X-API-Key: YOUR_API_KEY" https://myip.casa/api/pro/security
```

```json
curl -H "X-API-Key: YOUR_API_KEY" https://myip.casa/api/pro/vpn
```

```json
curl -H "X-API-Key: YOUR_API_KEY" https://myip.casa/api/pro/details
```

```json
curl -H "X-API-Key: YOUR_API_KEY" https://myip.casa/api/pro/health
```

### Python

import requests
```json
url = "https://myip.casa/api/pro/details"
headers = {"X-API-Key": "YOUR_API_KEY"}

response = requests.get(url, headers=headers)
print(response.json())
```

### Node.js (Fetch)
JavaScript
```json
const response = await fetch('https://myip.casa/api/pro/security', {
    headers: { 'X-API-Key': 'YOUR_API_KEY' }
});
const data = await response.json();
console.log(data);
```

## Privacy & Ethics
No-Log Policy: We do not store, log, or track the IP addresses submitted for processing.

Data Minimization: No email addresses or personal identifiers are stored within our API service databases.

Compliance: Our service is built with privacy-first principles, ensuring no footprint is left behind.


## 📬 Support & Suggestions
For technical support, bug reports, or feature suggestions, please use the Contact section on our official website: https://myip.casa



