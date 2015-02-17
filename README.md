# trentauth

Trentauth is a mechanism for mutual authentication (of domains, emails and phone numbers) and sharing secrets over a secure second channel (trusted third-party). It's main goal is to prevent man-in-the-middle attacks over an insecure channel.

## Protocol Flows

### Verify integrity and authencity of data published by a non-HTTPS domain

Scenario: Alice's domain doesn't have HTTPS and Bob needs to verify that the data he (or an app on his behalf) sees on Alice's domain was published by her (aka the domain owner). Note that Trentauth server is HTTPS only.

* Alice asks a trentauth server to verify her domain.
* The trentauth server does a whois for the domain to retrieve the registrant email address and sends verification email.
* Alice clicks on the verification link in her email that takes her to the trentauth server and gets a secret in return.
* Alice can now publish her trentauth server (rel=trentauth) and adds trentauth related data-* attributes to elements (including an hmac created using the secret received in the previous step).
* If Bob also trusts Alice's trentserver he can send a verification request to the trentauth server with Alice's domain name, data published on Alice's site to be authenticated (e.g., link rels) and data-* attributes associated with the data (including the hmac).

### Sharing secrets

...
