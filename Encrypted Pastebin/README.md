
📌 Challenge Description

We are told about a secure pastebin service that encrypts user data using 128-bit AES. The key is supposedly never stored on the server, making it “impossible” for hackers to retrieve sensitive data.

Our task is to find the flag.

🔍 Step 1 – Intercept the Request

Using Burp Suite, we send a message via the pastebin application.
When intercepting the request, we notice a suspicious parameter that looks like a long base64-like encoded string:

pxgC6E!we0olYLSISbWHchuoX4yjnz!WfATMzK2yfiZ3clIXMKSO8hbWfs0nzhhmC5ZFxpr!KroyV9!ywkDpWPUR-vMow5Rk7zNnRUlQueK2tn7fLdJudpw6BHNt60BSkayIyUldHMl79S43mEJANBWDi1WA0mObKaCns9pqAMDGk2nX5f044FDuitG7rr4kq456Z4!7UjFl1LOYR2c13A~~


This “encrypted” blob is sent along with our request.

🔍 Step 2 – Hypothesis

Since the application claims AES encryption, but we as users control the entire encrypted blob being sent, there may be no real validation or decryption happening server-side.

In other words:

The server might just accept whatever string we send.

If that’s the case, altering the string could reveal something unintended, like the flag.

🔍 Step 3 – Testing Input Tampering

We simply modify the long string in the request (e.g., removing/replacing some characters, or appending test strings) and resend it.

After altering the parameter and sending it back to the server, instead of rejecting it, the server responds with the flag!

🎯 Step 4 – Retrieve the Flag

The response reveals the hidden flag:

^FLAG^5ed665e93f7d6c29b071f7005200ba6d6e1ef74b3303eea93c5393ada5e2a918$FLAG$
