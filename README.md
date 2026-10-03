\# Enterprise Web Application Firewall (WAF) Deployment \& Threat Mitigation

\## Overview

This project demonstrates the setup, hardening, and threat detection capabilities of an open-source \*\*ModSecurity WAF\*\* integrated with the \*\*OWASP Core Rule Set (CRS)\*\* on an \*\*Nginx\*\* web server hosted on Ubuntu Server.

The WAF was validated against common OWASP Top 10 web attack vectors initiated from \*\*Kali Linux\*\*.

\## Network \& Infrastructure Architecture

\* \*\*Target Server:\*\* Ubuntu Server (`10.0.2.15`) running Nginx \& ModSecurity.

\* \*\*Attacker System:\*\* Kali Linux (`10.0.2.4`) issuing crafted HTTP payloads.

\* \*\*Firewall Engine:\*\* ModSecurity v3 / OWASP CRS in Active Enforcement (`SecRuleEngine On`).

\## Test Results \& Attack Verification

| Vulnerability / Attack Type | Payload Executed | WAF Action | HTTP Response | OWASP Rule ID |

| :--- | :--- | :--- | :--- | :--- |

| \*\*Legitimate Traffic\*\* | `/index.html?query=tea` | Allowed | `200 OK` | N/A |

| \*\*SQL Injection (SQLi)\*\* | `?query=' OR '1'='1` | Blocked | `403 Forbidden` | `942100` |

| \*\*Cross-Site Scripting (XSS)\*\* | `?query=<script>alert(1)</script>` | Blocked | `403 Forbidden` | `941110` |

| \*\*Path Traversal\*\* | `?page=../../../../etc/passwd` | Blocked | `403 Forbidden` | `930110` |

\## Technical Implementation Steps

1\. \*\*Engine Enforcement:\*\* Transitioned ModSecurity from `DetectionOnly` to `SecRuleEngine On` mode in `/etc/modsecurity/modsecurity.conf`.

2\. \*\*Rule Integration:\*\* Installed and configured the \*\*OWASP Core Rule Set (CRS)\*\* (`crs-setup.conf`).

3\. \*\*Attacker Simulation:\*\* Used `curl` CLI on Kali Linux to generate malformed HTTP requests containing payload strings.

4\. \*\*Log Security Analysis:\*\* Inspected and extracted event signatures from `/var/log/apache2/modsec\_audit.log`.

\## Security Takeaways

\* \*\*Pre-Execution Filtering:\*\* ModSecurity inspects HTTP headers, GET parameters, and POST request bodies before they reach application logic, neutralizing SQL and script injection threats.

\* \*\*Rule Tuning Balance:\*\* Enterprise deployments require adjusting rule thresholds to block malicious payloads while whitelisting legitimate user activity to eliminate false positives.
