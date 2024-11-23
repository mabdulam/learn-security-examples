# Tampering

This example demonstrates tampering through script injection.

## Steps to reproduce

1. Install all dependencies

    `npm install`

2. Start the **insecure.ts** server

    `npx ts-node insecure.ts`

3. In the browser, type a potentially malicious script in the name field of the form

    ```
        <script> document.body.innerHTML = "<a href='https://google.com'> Gotcha </a>"</script>
    ```

4. Do you see the potentially malicious hyperlink being injected into the form?

## For you to do

Answer the following:

1. Briefly explain the potential vulnerabilities in **insecure.ts**
    The code directly uses user input in the session without sanitization, making it vulnerable to XSS attacks. For instance, injecting scripts into the name field can execute malicious JavaScript in the context of the application.

2. Briefly explain how a malicious attacker can exploit them.
    An attacker could inject a malicious script via the input fields. When the application renders the input, the script would execute, allowing the attacker to steal data, perform unauthorized actions, or modify the page.

3. Briefly explain why **secure.ts** does not have the same vulnerabilties?
    secure.ts sanitizes user inputs using an escapeHTML function, removing potentially malicious characters. This ensures that any HTML or JavaScript content is escaped before being processed, effectively mitigating XSS risks.