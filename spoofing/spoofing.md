# Spoofing

This example demonstrates spoofind through two ways -- Stealing cookies programmatically and cross site request forgery (CSRF).

## Steps to reproduce the vulnerability

1. Install dependencies

    `$ npx install`

2. Start the **insecure.ts** server

    `npx ts-node insecure.ts`

3. Start the malicious server **mal.ts**

    `npx ts-node mal.ts`

4. Open __http://localhost:8000__ in a browser, type a name and Submit.

5. Open the __Application__ tab in the Browser's inspect pane. Find the __Cookies__ under __Storage__. You should see a __connect.sid__ cookie being set.

6. Open the HTML file __mal-steal-cookie.html__ file in the same browser (different tab). Open inspect and view the console.

7. Click the link in the HTML file. Do you see the cookie being stolen in the console?

8. Open the HTML file __mal-csrf.html__ file in the same browser (different tab). What do you see if the user has not logged out of **insecure.ts**? What do you see if the user has logged out? 


## For you to answer

1. Briefly explain the spoofing vulnerability in **insecure.ts**.
    The server is vulnerable to session hijacking and CSRF attacks. It sets cookies with the httpOnly flag disabled, making them accessible to client-side scripts, which can steal sensitive session data. Additionally, it does not implement protections like SameSite or CSRF tokens to validate the origin of requests.

2. Briefly explain different ways in which vulnerability can be exploited.
    Session Hijacking: An attacker can steal session cookies using XSS or social engineering and impersonate the user.
    CSRF: An attacker can trick a user into submitting a forged request to perform unauthorized actions, exploiting the lack of origin validation.

3. Briefly explain why **secure.ts** does not have the spoofing vulnerability in **insecure.ts**.
    secure.ts sets cookies with the httpOnly and SameSite flags enabled, preventing access to cookies via scripts and mitigating CSRF risks. Additionally, it improves session management, making it harder to hijack sessions.