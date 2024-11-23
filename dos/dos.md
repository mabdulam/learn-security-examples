# Denial-of-Service (DoS)

This example demonstrates DoS vulnerabilities and how they can be exploited.

## Steps to reproduce

1. Install all dependencies

    `$ npm install`

2. Ignore if you have already done this once. Insert test data in the MongoDB database. Make sure the `mongod` is up and running by typing the `mongosh` command in the terminal. If the `mongod` process is up, you will see that the connection was successful. Command to insert test data:

    `$ npx ts-node insert-test-users.ts`

   This will create a database in MongoDB called __infodisclosure__. Verify its presence by connecting with `mongosh` and running the command `show dbs;`.

3. Start the **insecure.ts** server

    `$ npx ts-node insecure.ts`

4. In the browser, pretend to be a hacker and type a malicious request:

    ```
    http://localhost:3000/userinfo?id[$ne]=
    ```

5. Do you see the server crashing?

## For you to do

1. **Briefly explain the potential vulnerabilities in `insecure.ts` that can lead to a DoS attack.**

   The endpoint allows unlimited and unsanitized queries, making it prone to NoSQL injection-based resource exhaustion or malformed requests crashing the server.

2. **Briefly explain how a malicious attacker can exploit them.**

   Attackers can repeatedly send malformed or computationally expensive queries, overloading the database or crashing the application.

3. **Briefly explain the defensive techniques used in `secure.ts` to prevent the DoS vulnerability.**

   `secure.ts` implements rate limiting using `express-rate-limit`, which restricts the number of requests per IP within a time window. Additionally, input validation ensures malformed queries are rejected.
