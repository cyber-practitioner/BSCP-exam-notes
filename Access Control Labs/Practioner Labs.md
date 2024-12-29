Here's the text formatted into proper Markdown:

```markdown
An application might configure a rule as follows:

```
DENY: POST, /admin/deleteUser, managers
```

This rule denies access to the `POST` method on the URL `/admin/deleteUser` for users in the `managers` group. Various things can go wrong in this situation, leading to access control bypasses.

If a website uses rigorous front-end controls to restrict access based on the URL, but the application allows the URL to be overridden via a request header, then it might be possible to bypass the access controls using a request like the following:

```
POST / HTTP/1.1
X-Original-URL: /admin/delete
```

This accesses the `/admin/delete` page.
```
You canaslo change the REQUQEST METHOD to `GET`, or use a different request METHOD tp bypass restrictions

#### Exploiting Multi-step Processes
If you find a multi-step process to change the privileges of a user (with more than two steps), follow these steps:
1. Capture the request of each step using Burp Suite.
2. Change the session cookie to your current user.
3. Replay the requests and check the responses for any unauthorized actions.

For example, the administrative function to update user details might involve the following steps:
1. Load the form that contains details for a specific user.
2. Submit the changes.
3. Review the changes and confirm.

The website assumes that a user will only reach step 3 if they have completed the first steps, which are properly controlled. An attacker can gain unauthorized access to the function by skipping the first two steps and directly submitting the request for the third step with the required parameters.

#### Referer Header Exploitation
Some websites base access controls on the `Referer` header submitted in the HTTP request. For example:
- An application robustly enforces access control over the main administrative page at `/admin`.
- Sub-pages, such as `/admin/deleteUser`, only inspect the `Referer` header. If the `Referer` header contains the main `/admin` URL, the request is allowed.

In this case, the `Referer` header can be fully controlled by an attacker. This means that they can forge direct requests to sensitive sub-pages by supplying the required `Referer` header and gain unauthorized access.