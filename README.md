# Vulnerability Assessment Report — AltoroMutual (demo.testfire.net)

> **Internship:** Future Interns Cyber Security Internship 2026 — Task 1
> **Prepared by:** Anshul
> **Date:** 14 March 2026
> **Status:** Final
> **Classification:** Confidential — For Educational Use Only

---

## 1. Target Overview

| Attribute | Value |
|-----------|-------|
| Application Name | AltoroMutual |
| Target URL | https://demo.testfire.net |
| Host / IP Address | 65.61.137.117 |
| Application Type | AltoroJ — Intentionally Vulnerable Banking Application |
| Developed By | HCL Technologies Ltd. |
| Technology Stack | Java (JSP), Apache Tomcat (Apache-Coyote/1.1), ISO-8859-1 |

AltoroMutual is a purpose-built, intentionally insecure web application developed to support cybersecurity training, skills development, and security tool evaluation. The objective of this assessment is to systematically identify and document security weaknesses present within the application, conducted under strictly controlled, ethical, and non-exploitative conditions.

---

## 2. Scope of Assessment

### 2.1 In-Scope Activities (Passive Analysis Only)

The assessment was confined exclusively to publicly accessible endpoints, employing passive analysis techniques throughout.

| Endpoint | Description |
|----------|-------------|
| Homepage | Primary landing page of the application |
| `/login.jsp` | User authentication interface |
| `/feedback.jsp` | Customer feedback submission form |
| `/search.jsp` | Application search functionality |
| `/status_check.jsp` | Server status monitoring page |
| `/swagger/index.html` | API documentation interface (Swagger UI) |
| `/cgi.exe` | CGI handler endpoint |
| `/admin/clients.xls` | Sensitive file identified via automated spider crawl (234 URLs) |

### 2.2 Out-of-Scope Activities

The following activities were explicitly excluded from the scope of this engagement:

- Authentication bypass attempts or credential-based attacks
- Active exploitation of identified vulnerabilities (e.g., SQL Injection execution)
- Access to authenticated dashboards or restricted application areas
- Denial-of-Service (DoS) testing of any kind
- Assessment of third-party services (e.g., external Swagger integrations)

> ⚠️ **Compliance Note:** All testing activities adhered strictly to passive, non-intrusive methodologies. No exploitation attempts were made, and no disruption to the application or its services was performed at any stage.

---

## 3. Methodology and Tools

| Tool / Technique | Purpose |
|------------------|---------|
| OWASP ZAP 2.17.0 (Checkmarx) | Passive vulnerability scanning (11 alerts); spider crawl across 234 URLs |
| PTK | HTTP header and response analysis (16 findings, 10 unique) |
| Nmap 7.98 | Network scanning and service enumeration |
| Browser Developer Tools (Chrome) | HTTP header inspection, cookie attribute analysis, and DOM review |
| Wappalyzer | Technology stack fingerprinting and identification |
| Shodan | External reconnaissance and host intelligence gathering |
| Manual Review | Source code inspection, parameter analysis, and contextual validation |

---

## 4. Findings Summary

### 4.1 Severity Distribution

| Severity Level | Count |
|----------------|-------|
| 🔴 High | 4 |
| 🟠 Medium | 4 |
| 🟡 Low | 4 |
| ℹ️ Informational | 3 |
| **Total** | **15** |

---

### 4.2 High-Risk Vulnerabilities

> Require immediate remediation in a production context.

| ID | Vulnerability |
|----|---------------|
| V-01 | Reflected Cross-Site Scripting (XSS) |
| V-02 | SQL Injection (Potential) |
| V-03 | Absence of Anti-CSRF Tokens |
| V-04 | Exposure of Sensitive File (`/admin/clients.xls`) |

---

### 4.3 Medium-Risk Vulnerabilities

> Security misconfigurations that may contribute to a broader attack surface.

| ID | Vulnerability |
|----|---------------|
| V-05 | Missing Content Security Policy (CSP) Header |
| V-06 | Missing Anti-Clickjacking Protection (X-Frame-Options) |
| V-07 | Absence of Subresource Integrity (SRI) Checks |
| V-08 | Server Banner Information Disclosure |

---

### 4.4 Low-Risk Vulnerabilities

> Lower-severity issues that may pose incremental risk when combined with other findings.

| ID | Vulnerability |
|----|---------------|
| V-09 | Session Cookie Missing SameSite Attribute |
| V-10 | Inclusion of Cross-Domain JavaScript Resources |
| V-11 | Missing X-Content-Type-Options Header |
| V-12 | Missing Referrer-Policy Header |

---

### 4.5 Informational Findings

> Contextual observations relevant to the overall security posture.

| ID | Observation |
|----|-------------|
| V-13 | Publicly Accessible Swagger UI Without Authentication Controls |
| V-14 | Application Information Disclosure via Embedded HTML Comments |
| V-15 | Session Token Identified Within Application Responses |

---

## 5. Conclusion

This assessment identified a range of security misconfigurations and potential vulnerabilities spanning multiple severity classifications. Although AltoroMutual is an intentionally insecure application deployed for training purposes, the findings documented herein are representative of security risks commonly encountered in real-world production environments.

**Principal areas of concern include:**

- Insufficient input validation, exposing the application to injection-based attack vectors (XSS, SQL Injection)
- Absence of critical HTTP security headers, weakening the application's defensive posture
- Exposure of sensitive resources to unauthenticated users
- Inadequate session management and request integrity protection mechanisms

---

## 6. Recommendations

| # | Recommendation |
|---|----------------|
| 1 | Implement comprehensive input validation and contextual output encoding across all user-supplied data entry points |
| 2 | Enforce secure coding standards and conduct regular code reviews to reduce injection-based risks |
| 3 | Introduce and enforce CSRF protection tokens across all state-modifying requests |
| 4 | Restrict access to sensitive files and administrative directories via server-side access controls |
| 5 | Configure essential HTTP security headers: CSP, HSTS, X-Frame-Options, X-Content-Type-Options, Referrer-Policy |
| 6 | Apply `SameSite`, `Secure`, and `HttpOnly` attributes to all session cookies |
| 7 | Disable or restrict access to developer-facing interfaces (e.g., Swagger UI) in non-development environments |

---

*End of Report — Prepared by Anshul | Future Interns Cyber Security Internship 2026*
