Here's the text converted into proper Markdown:

Vertical Priv escalation

```markdown
For example, a website might host sensitive functionality at the following URL:

```
https://insecure-website.com/admin
```

This might be accessible by any user, not only administrative users who have a link to the functionality in their user interface. In some cases, the administrative URL might be disclosed in other locations, such as the `robots.txt` file:

```
https://insecure-website.com/robots.txt
```

Even if the URL isn't disclosed anywhere, an attacker may be able to use a wordlist to brute-force the location of the sensitive functionality.

If the URL is obscured, then check for any client-side scripts that would have the variable for admin set as `false`:

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
```

#### Identifying Admin Parameters
- Check for request parameters in the Burp Proxy to find parameters that will set `Admin` as `True`.
- Check for any `POST` request where the response might contain a `roleID` that can be used to change the role of the user to the Admin's role.



---

### Horizontal Privilege Escalation

#### Predictable User IDs
- When there are unpredictable user IDs in the request URL, find GUIDs of the web application. Provide the GUID to the admin to gain access to the admin panel or "Carlos" (test user) accounts.
- Check the source code or responses for such IDs.

#### Data Leakage in Responses
- Use Burp Proxy to change the `id` parameter in the URL to the ID of the target user.
- Inspect the response for any leaked data related to the user being accessed.
