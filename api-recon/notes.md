# Lab: Exploiting an API Endpoint Using Documentation
📍 **Platform:** PortSwigger Web Security Academy  
📅 **Date Completed:** March 1, 2025  
🎯 **Objective:** Leverage publicly exposed API documentation to discover sensitive endpoints and perform unauthorized operations (in this case user deletion).  
✅ **Status:** Successfully completed

---

## 🧠 Overview

This lab illustrates a common API security misconfiguration — **exposing internal or sensitive API operations through publicly available documentation**, such as Swagger or Postman collections.

By discovering accessible API specifications, we identified undocumented functionality and used it to perform an unauthorized `DELETE` operation on another user account.

---

## 🔍 Detailed Methodology

1. **Logged into the Application**

Accessed the lab web application.
Logged in using the provided default credentials:
Username: wiener
Password: peter

---
2.**Captured the Email Update API Request**

Navigated to **My Account > Email Update** section.
Updated the email address to trigger an API request.
Captured the following request in Burp Suite:
PATCH /api/user/wiener
Sent the request to **Burp Repeater** for further manipulation.

---
3.**Discovered the API Documentation**

Modified the request path in Repeater to probe for accessible endpoints:
- Tried `/api/user` → response was a generic error.
- Tried `/api` → returned an HTML page.
Opened the response in browser.
Swagger UI was exposed, revealing full API documentation.

---
4.**Executed DELETE Request from API Docs**

In the Swagger interface, located the `DELETE /api/user/{username}` endpoint.
Entered `carlos` as the target username.
Sent the request directly from the Swagger UI.
Response confirmed that user `carlos` was deleted successfully.

---
5.**Result**

On successful deletion of `carlos`, the lab environment confirmed completion.

---

## 🛠️ Tools & Technologies

- **Burp Suite** – for intercepting and modifying HTTP requests  
- **Browser Dev Tools** – for initial recon and interface inspection  
- **Swagger/OpenAPI Viewer** – to analyze the exposed documentation  

---

## 📸 Evidence

![Exploit Lab Screenshot](./screenshots/exploit-api-docs.png)

**Images of steps done**

1.![Exploit Lab Screenshot](https://github.com/HariCyber-Sec/API-Testing-Labs/blob/main/api-recon/screenshots/1.jpg)
2.![Exploit Lab Screenshot](https://github.com/HariCyber-Sec/API-Testing-Labs/blob/main/api-recon/screenshots/2.jpg)
3.![Exploit Lab Screenshot](https://github.com/HariCyber-Sec/API-Testing-Labs/blob/main/api-recon/screenshots/3.jpg)
4.![Exploit Lab Screenshot](https://github.com/HariCyber-Sec/API-Testing-Labs/blob/main/api-recon/screenshots/4.jpg)
5.![Exploit Lab Screenshot](https://github.com/HariCyber-Sec/API-Testing-Labs/blob/main/api-recon/screenshots/5.jpg)
6.![Exploit Lab Screenshot](https://github.com/HariCyber-Sec/API-Testing-Labs/blob/main/api-recon/screenshots/6.jpg)
7.![Exploit Lab Screenshot](https://github.com/HariCyber-Sec/API-Testing-Labs/blob/main/api-recon/screenshots/7.jpg)
8.![Exploit Lab Screenshot](https://github.com/HariCyber-Sec/API-Testing-Labs/blob/main/api-recon/screenshots/8.jpg)
9.![Exploit Lab Screenshot](https://github.com/HariCyber-Sec/API-Testing-Labs/blob/main/api-recon/screenshots/9.jpg)

---

## 💡Takeaways

- API documentation like Swagger or OpenAPI should never be left exposed in a live environment. It can give attackers a map of your backend.
- Always make sure sensitive actions (like DELETE) are protected with strong authentication and role-based access control — just being logged 
  in shouldn't be enough.
- Developer tools are great for testing, but if not secured properly, they can accidentally expose critical endpoints and create serious vulnerabilities.
