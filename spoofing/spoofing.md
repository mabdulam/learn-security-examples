# Spoofing

This example demonstrates spoofing through two methods: stealing cookies programmatically and cross-site request forgery (CSRF).

## Steps to reproduce the vulnerability

1. Install dependencies:

    ```bash
    $ npm install
    ```

2. Start the **insecure.ts** server:

    ```bash
    $ npx ts-node insecure.ts
    ```

3. Start the malicious server **mal.ts**:

    ```bash
    $ npx ts-node mal.ts
    ```

4. Open [http://localhost:8000](http://localhost:8000) in a browser, type a name, and click **Submit**.

5. Open the **Application** tab in the browser's inspect pane. Find the **Cookies** section under **Storage**. You should see a `connect.sid` cookie being set.

6. Open the HTML file **mal-steal-cookie.html** in the same browser (different tab). Open the inspect console.

7. Click the link in the HTML file. Do you see the cookie being stolen in the console?

8. Open the HTML file **mal-csrf.html** in the same browser (different tab). Observe:
    - What happens if the user has not logged out of **insecure.ts**?
    - What happens if the user has logged out?

## For you to answer

1. **Briefly explain the spoofing vulnerability in `insecure.ts`:**

   The server is vulnerable to session hijacking and CSRF attacks. It sets cookies with the `httpOnly` flag disabled, making them accessible to client-side scripts, which can steal sensitive session data. Additionally, it does not implement protections like `SameSite` or CSRF tokens to validate the origin of requests.

2. **Briefly explain different ways in which the vulnerability can be exploited:**

   - **Session Hijacking:** An attacker can steal session cookies using XSS or social engineering and impersonate the user.
   - **CSRF:** An attacker can trick a user into submitting a forged request to perform unauthorized actions, exploiting the lack of origin validation.

3. **Briefly explain why `secure.ts` does not have the spoofing vulnerability in `insecure.ts`:**

   `secure.ts` sets cookies with the `httpOnly` and `SameSite` flags enabled, preventing access to cookies via scripts and mitigating CSRF risks. Additionally, it improves session management, making it harder to hijack sessions.
