 # Lab: Exploiting a Mass Assignment Vulnerability

📍 **Platform:** PortSwigger Web Security Academy  
📅 **Date Completed:** March 1, 2025  
🎯 **Objective:** Identify and exploit a mass assignment vulnerability to perform unauthorized product purchases.  
✅ **Status:** Successfully completed

---

## 🧠 Overview

This lab demonstrates a common web application vulnerability known as **mass assignment**, where the server improperly trusts user-supplied JSON input. By manipulating JSON parameters, an attacker can assign values to sensitive or hidden fields that should not be user-controllable. The goal of this lab was to exploit this behavior to purchase a premium product without the required authorization.

---

## 🔍 Detailed Methodology

### 🔐 1. Logged into the Application

- Accessed the provided lab instance on PortSwigger.
- Used the default test credentials:
  Username: wiener
  Password: peter
  
### 🛒 2. Navigated to Product Purchase Page

- Selected the product: **Lightweight l33t Leather Jacket**.
- Initiated a normal purchase attempt through the frontend by adding the product to cart.

### 🎯 3. Captured the Request in Burp Suite

- Initiated a normal purchase attempt through the frontend by adding the product to cart.
- Intercepted Checkout Request

-Used Burp Suite to intercept the checkout request.
The request was captured as:

POST /api/checkout HTTP/1.1
Content-Type: application/json

 
### 🔍 4. Attempted Basic Injection

 -Tried injecting a discount value directly.
 -Received an error response indicating improper request body.

### 📦 5. Analyzed Full JSON Structure

-Switched Burp Suite to display full JSON object using the Content-Type Converter extension.
-Reused the entire structure from the initial API response and added the discount parameter manually.
-This request succeeded and a discount was applied.

### ✅ 6. Confirmed Exploit & Lab Completion

-After the modified checkout request, returned to the cart summary.
-Verified that the discount had been applied without any authorization.
-Lab marked as Solved.

### 🛠️ Tools & Technologies Used

Burp Suite — for intercepting and modifying HTTP requests.

Content-Type Converter — for auto-converting requests into JSON.

Browser Dev Tools — to inspect and verify request/response payloads.

📸 Evidence

Add screenshot proof at:api-recon/screenshots/mass-assignment-exploit.png

### 💡 Key Takeaways

Mass assignment can expose hidden parameters like isAdmin, discount, or userId.

APIs should strictly validate and whitelist allowed fields.

Returning full JSON responses can leak exploitable structure.
 
 
 

