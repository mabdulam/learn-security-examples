# Tampering

This example demonstrates tampering through script injection.

## Steps to reproduce

1. Install all dependencies:

    ```bash
    $ npm install
    ```

2. Start the **insecure.ts** server:

    ```bash
    $ npx ts-node insecure.ts
    ```

3. In the browser, type a potentially malicious script into the name field of the form:

    ```html
    <script>document.body.innerHTML = "<a href='https://google.com'> Gotcha </a>"</script>
    ```

4. Do you see the potentially malicious hyperlink being injected into the form?

## For you to do

1. **Briefly explain the potential vulnerabilities in `insecure.ts`:**

   The code directly uses user input in the session without sanitization, making it vulnerable to XSS attacks. For instance, injecting scripts into the name field can execute malicious JavaScript in the context of the application.

2. **Briefly explain how a malicious attacker can exploit them:**

   An attacker could inject a malicious script via the input fields. When the application renders the input, the script would execute, allowing the attacker to steal data, perform unauthorized actions, or modify the page.

3. **Briefly explain why `secure.ts` does not have the same vulnerabilities:**

   `secure.ts` sanitizes user inputs using an `escapeHTML` function, which removes potentially malicious characters. This ensures that any HTML or JavaScript content is escaped before being processed, effectively mitigating XSS risks.
