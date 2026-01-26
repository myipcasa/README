# myIP.casa

myIP.casa is a free, browser-based toolkit that provides practical network, security, and connectivity diagnostics.  
It helps users understand how their internet connection behaves and identify common networking, DNS, and SSL/TLS issues.

All tools run directly in the browser, with no installation, no registration, and no client software required.

## What myIP.casa Is Used For

myIP.casa is designed to answer common questions such as:
- What is my current public IP address?
- Has my IP address changed while using a VPN?
- Are specific ports open or blocked?
- Who owns an IP address or domain (WHOIS / ICANN lookup)?
- Is my VPN leaking DNS requests?
- How does my traffic route across the internet?
- Is my connection stable and responsive?
- Is an SSL/TLS certificate secure and correctly configured?
- Are DNS records fully propagated worldwide?
- How do I calculate IPv4 and IPv6 subnets?
- How can I quickly convert currencies, including cryptocurrencies?

The platform is suitable for both technical and non-technical users who need fast and reliable diagnostics.

## Available Tools

### Public IP Address & IP Change Detection
Displays the current public IP address and IP version (IPv4 or IPv6).  
It can also alert users when their IP address changes, which is especially useful for VPN users who want to verify tunnel stability or detect unexpected IP leaks.

### Port Checker
Tests whether specific TCP ports are open, closed, or filtered from the internet.  
This tool is useful for developers, system administrators, and anyone troubleshooting firewall, NAT, or server connectivity issues.

### WHOIS / ICANN Lookup
Queries official WHOIS and ICANN databases to retrieve registration and ownership information for IP addresses and domain names, including registrar details, allocation ranges, and ASN information.

### DNS Leak Test
Detects which DNS resolvers are being used and identifies potential DNS leaks.  
This helps verify whether DNS requests are properly routed through a VPN or secure network configuration.

### Traceroute
Shows the network path and latency between the user and a destination host.  
It helps identify routing issues, network congestion, and problematic hops along the route.

### Latency Test
Measures round-trip time and connection responsiveness.  
This is useful for diagnosing instability, packet delays, and general connection quality.

### SSL/TLS Checker
Analyzes HTTPS configurations and evaluates SSL/TLS compatibility across different devices and clients.  
It inspects certificate chains, key exchange mechanisms, supported protocols, cipher suites, and overall security posture.

### SSL Certificate Decoder
Decodes SSL/TLS certificates by either scanning a live website or manually pasting a certificate.  
It displays certificate fields, validity periods, issuer information, and cryptographic parameters in a readable format.

### DNS Propagation Checker
Checks how DNS records propagate across multiple resolvers worldwide.  
This helps confirm whether DNS changes have fully propagated and are visible from different locations.

### Speed Test
Provides a basic internet speed test to measure download speed, upload speed, and latency.  
It is intended as a lightweight complement to more advanced benchmarking tools.

### Subnet Calculator
Calculates IPv4 and IPv6 subnets, network ranges, broadcast addresses, and usable IP ranges.  
This tool is useful for network planning, education, and subnet design.

### Currency & Crypto Exchange Rate Converter
Converts more than 44 fiat currencies and includes support for cryptocurrencies such as Bitcoin and other major digital assets.  
It provides quick and practical exchange rate comparisons.

## Why Browser-Based Network Tools Matter

Browser-based diagnostics offer several advantages:
- No installation or system permissions required
- Cross-platform compatibility (desktop and mobile)
- Works in restricted or locked-down environments
- Easy to access and reproduce results
- Fast and lightweight

These tools are not meant to replace advanced command-line utilities, but to provide quick insight and visibility into common network and security issues.

## Typical Use Cases

- VPN verification and privacy checks
- Network troubleshooting and diagnostics
- Server and firewall configuration testing
- SSL/TLS validation and certificate inspection
- DNS debugging and propagation verification
- Educational and learning purposes
- Quick checks when CLI tools are unavailable

## Privacy and Data Handling

myIP.casa does not require user accounts or registration.  
The tools are designed to minimize data collection and only process information necessary to perform the requested checks.

## 🌐 Public IP API

MyIP.casa provides a free, fast and privacy-friendly API to retrieve your public IP address.

### Endpoint

GET https://myip.casa/api/ip

### Response

```json
{
  "ip": "2012:32c5:303:125::1f04"
}

```

### OpenAPI

The OpenAPI specification is available at:
https://myip.casa/api/openapi.yaml

Rate limit
60 requests per minute per IP
No authentication required

Use cases :
Public IP detection
Network diagnostics
CI/CD pipelines
AI agents & automation

## Project Website

https://myip.casa

## Feedback and Contributions

Feedback, suggestions, and improvement ideas are welcome.  
The project focuses on clarity, accuracy, and usefulness rather than complexity.
