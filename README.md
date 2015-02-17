# trentauth

Trentauth is a mechanism for mutual authentication (of domains, emails and phone numbers) and sharing secrets over a secure second channel (trusted third-party). It's main goal is to prevent man-in-the-middle attacks over an insecure channel.

## Protocol Flows

### Verify integrity and authencity of data published by a non-HTTPS domain

Scenario: Alice's domain doesn't have HTTPS and Bob needs to verify that the data he (or an app on his behalf) sees on Alice's domain was published by her (aka the domain owner). Note that Trentauth server is HTTPS only.

1. Alice asks a trentauth server to verify her domain.
2. The trentauth server does a whois for the domain to retrieve the registrant email address and sends verification email.
3. Alice clicks on the verification link in her email that takes her to the trentauth server and gets a secret in return.
4. Alice can now publish her trentauth server (rel=trentauth) and adds trentauth related data-* attributes to elements (including an hmac created using the secret received in step 3).
5. If Bob also trusts Alice's trentauth server he can send a verification request to the trentauth server with Alice's domain name, data published on Alice's site to be authenticated (e.g., link rels) and data-* attributes associated with the data (including the hmac)
6. The trentauth server will then comapre the hmac received from Bob to the one it will generate using the shared serect it had given for Alice's domain (in step 3) and let Bob know if the data is authentic.

### Sharing secrets

...
