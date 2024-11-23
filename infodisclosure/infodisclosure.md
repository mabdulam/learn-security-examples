# Tampering

This example demonstrates information disclosure by injecting malicious query objects into a NoSQL database.

## Steps to reproduce

1. Install all dependencies:

    ```bash
    $ npm install
    ```

2. Insert test data in the MongoDB database. Make sure the `mongod` process is running by typing the `mongosh` command in the terminal. If `mongod` is up, you will see a successful connection message. Use the following command to insert test data:

    ```bash
    $ npx ts-node insert-test-users.ts
    ```

   This will create a database in MongoDB called __infodisclosure__. Verify its presence by connecting with `mongosh` and running the command:

    ```bash
    show dbs;
    ```

3. Start the **insecure.ts** server:

    ```bash
    $ npx ts-node insecure.ts
    ```

4. In the browser, pretend to be a hacker and type a malicious request:

    ```http
    http://localhost:3000/userinfo?username[$ne]=
    ```

5. Observe whether user information is displayed despite the malicious request not having a valid username.

## For you to do

1. **Briefly explain the potential vulnerabilities in `insecure.ts`:**

   The server directly uses user-provided input in database queries without validation. This makes it vulnerable to NoSQL injection, allowing attackers to access unauthorized data.

2. **Briefly explain how a malicious attacker can exploit them:**

   An attacker can craft a query, such as `{ username: { $ne: null } }`, to retrieve unauthorized user information.

3. **Briefly explain the defensive techniques used in `secure.ts` to prevent the information disclosure vulnerability:**

   `secure.ts` validates and sanitizes user inputs, rejecting non-string usernames or invalid formats. This ensures that malicious queries are not processed by the database, mitigating the risk of NoSQL injection.
