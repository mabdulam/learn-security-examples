# Privilege Escalation

The example demonstrates a privilege escalation vulnerability and how to exploit it.

## Steps to reproduce

1. Install all dependencies:

    ```bash
    $ npm install
    ```

2. Start the **insecure.ts** server:

    ```bash
    $ npx ts-node insecure.ts
    ```

3. In the browser, send a GET request:

    ```http
    http://localhost:3000/send-form
    ```

4. Try different `UserIds` and see which one grants authorized access to change the role of that user.

## For you to do

1. **Briefly explain the potential vulnerabilities in `insecure.ts`:**

   The server relies on client-provided data for user identification and role validation. This allows attackers to escalate privileges by manipulating `userId` or directly modifying the role.

2. **Briefly explain how a malicious attacker can exploit them:**

   Attackers can impersonate an administrator by sending a crafted `userId` and changing roles without proper authorization checks.

3. **Briefly explain the defensive techniques used in `secure.ts` to prevent the privilege escalation vulnerability:**

   `secure.ts` uses session-based authentication to validate the user's identity and role on the server side. Only authenticated admin users are allowed to update roles, ensuring proper access control and preventing privilege escalation.
