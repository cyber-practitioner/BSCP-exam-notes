Here's the text converted into properly structured notes with clear sections and code formatting:

---

# Notes on Access Control Bypass and Exploitation

## Access Control Rule Example

An application might configure an access control rule as follows:
```
DENY: POST, /admin/deleteUser, managers
```
This rule denies access to the `POST` method on the URL `/admin/deleteUser` for users in the `managers` group. However, flaws in the implementation might allow bypassing these restrictions.

---

### Bypassing Restrictions via Request Headers
If the application relies on strict front-end controls for URL-based restrictions but allows the URL to be overridden via request headers, you can bypass access controls with a request like:
```
POST / HTTP/1.1
X-Original-URL: /admin/delete
```
This request accesses the `/admin/delete` page despite the configured restriction.

---

### Changing the Request Method
- Try **changing the request method** to `GET` or another method.
- Some applications may fail to properly enforce restrictions on alternative methods, allowing unauthorized access.

---

## Exploiting Multi-Step Processes

For multi-step processes that involve privilege changes:
1. Use **Burp Suite** to capture the requests for each step.
2. Modify the **session cookie** to reflect your current user.
3. Replay the requests to skip steps and directly execute actions.
4. Inspect the responses for unauthorized outcomes.

### Example: Administrative Function to Update User Details
Steps typically include:
1. **Load the form** containing details for a specific user.
2. **Submit the changes.**
3. **Review and confirm** the changes.

**Attack:**  
An attacker can skip steps 1 and 2 by directly submitting the request for step 3 with the required parameters, thereby bypassing proper controls.

---

## Referer Header Exploitation

### Concept
Some websites base access controls on the `Referer` header in the HTTP request. For example:
- The main administrative page (`/admin`) enforces robust access control.
- Sub-pages (e.g., `/admin/deleteUser`) only check if the `Referer` header contains the main `/admin` URL.

### Attack
The `Referer` header can be fully controlled by an attacker:
1. Forge direct requests to sensitive sub-pages.
2. Add the required `Referer` header to the request.
3. Bypass access controls and gain unauthorized access.

---

### Summary
- **Headers:** Test for `X-Original-URL` and `Referer` header manipulation.
- **Methods:** Change HTTP request methods (`POST`, `GET`, etc.) to bypass restrictions.
- **Multi-Step Processes:** Capture, modify, and replay intermediate requests to skip enforced steps.
- **Tools:** Use Burp Suite for parameter analysis, request modification, and response inspection.

--- 

This structure provides clarity, highlighting methods, examples, and actionable steps for testing access control vulnerabilities.