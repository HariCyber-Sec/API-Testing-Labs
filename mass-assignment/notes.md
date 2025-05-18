 # Lab: Exploiting a Mass Assignment Vulnerability

📍 **Platform:** PortSwigger Web Security Academy  
📅 **Date Completed:** March 1, 2025  
🎯 **Objective:** Identify and exploit a mass assignment vulnerability to perform unauthorized product purchases.  
✅ **Status:** Successfully completed

---

## 🧠 Overview

This lab demonstrates a common web application vulnerability known as **mass assignment**. Demonstrates how improper handling of object-level permissions in APIs can be abused. Specifically, we target a hidden chosen_discount field in the backend API request — not exposed by the frontend — and inject it to trick the server into giving us a 100% discount.

---

## 🔍 Detailed Methodology

### 🔐 1. Logged into the Application

- Accessed the provided lab instance on PortSwigger.
- Used the default test credentials:
  Username: wiener
  Password: peter
  Logged in as a normal user
  
### 🛒 2. Navigated to Product Purchase Page

- Selected the product: **Lightweight l33t Leather Jacket**.
- Initiated a normal purchase attempt through the frontend by adding the product to cart
- Tried to place an order
- Clicked "Place order" in the basket.
- Got a message saying insufficient credit to buy the product..

### 🎯 3. Inspected the HTTP requests using Burp Suite

- In Proxy > HTTP history, found:
- A GET /api/checkout request
- A POST /api/checkout request
- The GET response showed a field called chosen_discount (it wasn't there in the POST body).

 
### 🔍 4.  Sent the POST request to Repeater and modified it

- Added this to the body:
- {
  "chosen_discount": {
    "percentage": 0
  },
  "chosen_products": [
    {
      "product_id": "1",
      "quantity": 1
    }
  ]
}
- Sent the request — no error, which meant the server accepted the field.

### 📦 5. Tested further to confirm server behavior

- Changed percentage to "x" and resent — got an error.

- This confirmed the server was processing the discount value.

### ✅ 6. Confirmed Exploit & Lab Completion
- Updated the discount to 100:
- {
  "chosen_discount": {
    "percentage": 100
  },
  "chosen_products": [
    {
      "product_id": "1",
      "quantity": 1
    }
  ]
}
- Sent it — 💥 Order went through successfully with 100% discount!

### 🛠️ Tools & Technologies Used

Burp Suite — for intercepting and modifying HTTP requests.

JSON crafting – to inject hidden parameters manually.

Logic testing – to confirm parameter acceptance and behavior.

### 📸 Evidence

Add screenshot proof at: ![Exploit Lab Screenshot](./screenshots/mass-assignment-exploit.jpg)

**Images of steps done**

1.![Exploit Lab Screenshot](https://github.com/HariCyber-Sec/API-Testing-Labs/blob/main/mass-assignment/screenshots/1.jpg)
2.![Exploit Lab Screenshot](https://github.com/HariCyber-Sec/API-Testing-Labs/blob/main/mass-assignment/screenshots/2.jpg)
3.![Exploit Lab Screenshot](https://github.com/HariCyber-Sec/API-Testing-Labs/blob/main/mass-assignment/screenshots/3.jpg)
4.![Exploit Lab Screenshot](https://github.com/HariCyber-Sec/API-Testing-Labs/blob/main/mass-assignment/screenshots/4.jpg)
5.![Exploit Lab Screenshot](https://github.com/HariCyber-Sec/API-Testing-Labs/blob/main/mass-assignment/screenshots/5.jpg)
6.![Exploit Lab Screenshot](https://github.com/HariCyber-Sec/API-Testing-Labs/blob/main/mass-assignment/screenshots/6.jpg)
7.![Exploit Lab Screenshot](https://github.com/HariCyber-Sec/API-Testing-Labs/blob/main/mass-assignment/screenshots/7.jpg)
8.![Exploit Lab Screenshot](https://github.com/HariCyber-Sec/API-Testing-Labs/blob/main/mass-assignment/screenshots/8.jpg)
9.![Exploit Lab Screenshot](https://github.com/HariCyber-Sec/API-Testing-Labs/blob/main/mass-assignment/screenshots/9.jpg)
10.![Exploit Lab Screenshot](https://github.com/HariCyber-Sec/API-Testing-Labs/blob/main/mass-assignment/screenshots/10.jpg)

### 💡 Takeaways

Mass assignment vulnerabilities happen when APIs blindly accept and bind user input to internal objects. This can accidentally expose hidden fields like isAdmin, discount, or userId things a normal user shouldn’t be able to change.
To prevent this, APIs should strictly validate and whitelist only safe fields.Also, returning full JSON objects in responses can unintentionally reveal sensitive fields, making it easier for attackers to discover what they can exploit.
 
 
 

