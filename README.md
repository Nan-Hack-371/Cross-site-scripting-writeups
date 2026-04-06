# Reflected XSS with WAF Bypass (PortSwigger Lab)

## 🧠 Overview
This lab demonstrates a **Reflected Cross-Site Scripting (XSS)** vulnerability where a **Web Application Firewall (WAF)** blocks most common XSS payloads.

### 🎯 Objective
Bypass the WAF and execute the `print()` function **without any user interaction**.

---

## 🔍 Initial Testing

Tried a basic XSS payload:

```html
<img src=1 onerror=print()>
