# Repudiation

The example demonstrates a vulnerability that can lead to repudiation by malicious users attempting to access the services provided by a server.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Run the server __insecure.ts__.

3. Pretend to be a malicous user and interact with the services by sending requests from the browser.

4. Do you think your actions can be repudiated?

## For you to do

1. Briefly explain the vulnerability.
    The server does not log user actions. This allows malicious users to deny their actions, such as deleting or modifying sensitive data, as there is no traceability.

2. Briefly explain why the vulnerability is addressed in __secure.ts__.
    secure.ts implements request logging to a file, recording each request and its origin. This ensures accountability and provides a mechanism to trace malicious actions.

3. Which design pattern is used in the secure version to address the vulnerability? Briefly explain how it works?
    Logging Middleware: It logs all requests, including their method, endpoint, and IP address. This pattern ensures centralized logging and simplifies tracking user actions for audit and forensic purposes.