# CIP-8 Schema Definitions #



This folder contains various schema definitions that can be used with CIP-8 Message Signing wth CIP-30 compatible 
wallets to cryptographically authenticate users based on their wallet keys rather than submitting a transaction to
the blockchain.

It is, in my opinion, critical that the message payload for CIP-8 signing should always be human-readable such that the
end user has visibility into the payload that they are signing, and we do not develop a consumer culture of signing for
an unknown payload that may pose security vulnerabilities such as signing a hash for a transaction that drains a user's
wallet.

To this end, we should pass the payload as well-formed JSON such that the implementing wallet may reconstruct and display
the payload in a nicely formatted way to the end user.

An important point here is that the service implementing CIP-8 signing should always use a canonical format for construction
and transmission of the signing payload so that it can be reconstructed properly on both ends (signer and validator) to
ensure that no data tampering has taken place.

## Schemas ##

### [Authentication](authentication.json) ###

Describes a schema format to be used for authenticating a user to a website or service (URI).

#### Field Notes ####

**uri**: This should match against the calling server or originating service. For example, only allow a URI of 
https://buffybot.io if this matches the originating website where the request was made.

**userID**: This should match against the signing key being used for authentication by the wallet. For example, a user
being asked to sign with their staking key; the staking key of the wallet in use must match the userID specified in the
payload.

**expiration**: The signature should be generated and submitted to the server for validation prior to this date-time,
otherwise the nonce value should be considered invalid and should be regenerated.
**Note**: After successful validation the server should return an authentication token that may be used by the client
throughout the duration of the authenticated session.