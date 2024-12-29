Here’s a refined version of the notes with clear sections, code blocks, and hyperlinks for better readability:

---

# Notes on Privilege Escalation

## Vertical Privilege Escalation

### Accessing Sensitive Functionality
- Websites may host sensitive functionality at URLs like:
  ```
  https://insecure-website.com/admin
  ```
- This URL might be accessible to non-administrative users. Sometimes, such URLs are disclosed in the `robots.txt` file:
  ```
  https://insecure-website.com/robots.txt
  ```
- Even if the URL is not disclosed, use a **wordlist** to brute-force its location.

### Checking for Client-Side Admin Variables
- Review client-side scripts for admin-related variables. For example:
  ```javascript
  <script>
      var isAdmin = false;
      if (isAdmin) {
          ...
          var adminPanelTag = document.createElement('a');
          adminPanelTag.setAttribute('href', 'https://insecure-website.com/administrator-panel-yb556');
          adminPanelTag.innerText = 'Admin panel';
          ...
      }
  </script>
  ```

---

## Identifying Admin Parameters
1. **Using Burp Proxy:**
   - Search for request parameters that set `Admin` as `True`.
   - Check for `POST` requests with responses that include a `roleID`. 
     - **Action:** Use these `roleID` values to attempt role elevation to "Admin."

2. **Bypassing Multi-Step Processes:**
   - For administrative actions requiring multiple steps:
     1. Capture each request in the process.
     2. Modify the session cookie to match your current user.
     3. Replay requests to skip steps and directly submit final-stage actions.
   - **Example:** Updating user details might involve:
     - Loading a form.
     - Submitting changes.
     - Reviewing and confirming changes.
   - An attacker can skip to the last step with appropriate parameters.

---

## Horizontal Privilege Escalation

### Predictable User IDs
- If the application uses predictable User IDs:
  1. Locate GUIDs or IDs in the application.
  2. Use these IDs to access restricted areas, such as admin panels or other users’ data.
  3. Example:
     - Check the **source code** or **server responses** for references to such IDs.

### Checking for Data Leakage
1. Use **Burp Proxy** to modify the `id` parameter in the URL to another user’s ID.
2. Inspect server responses for leaked data.

---

### Additional Notes
- For access controls relying on the `Referer` header:
  - Forge the `Referer` header to simulate legitimate requests to administrative sub-pages.
  - Example:
    - Access `/admin/deleteUser` by setting the `Referer` to `/admin`.

---

### Summary
- Always inspect client-side scripts, request parameters, and HTTP headers.
- Use tools like Burp Suite to manipulate requests and test access controls.
- Watch for multi-step processes and predictable data structures that can be exploited.

--- 

This structure provides a clear, well-organized reference for studying privilege escalation techniques. Hyperlinks and code blocks are formatted to differentiate between actions, observations, and example code.