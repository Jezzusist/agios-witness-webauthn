# AGIOS witness WebAuthn page

This is a static page, served by GitHub Pages at `https://jezzusist.github.io/agios-witness-webauthn/`. It supports the human-witness credential discussion in Locus-Agentic-Solutions/AGIOS_Imldris_DevCloud#572.

- **RP ID:** `jezzusist.github.io`
- **Origin:** `https://jezzusist.github.io`

## What the page does

It calls the browser's WebAuthn API, with no server and no storage:

1. **Registration.** `navigator.credentials.create` requests a platform authenticator (Windows Hello). It sets `userVerification: "required"` and `attestation: "direct"`, and accepts ES256 or RS256 keys.
2. **Assertion.** `navigator.credentials.get` signs a verifier-supplied, single-use challenge, again with `userVerification: "required"`.

Each step prints the raw outputs (base64url): the credential ID, the attestation object, the client data JSON, the authenticator data, the signature, and the public key. An independent verifier can then check the challenge, origin, RP ID hash, signature, and the signed UP/UV flags.

## What it is not

- It holds no private key and no PIN.
- It records no identity, and it performs no approval.
- Control of this origin sits with the `Jezzusist` GitHub account.
- The verifier must not trust the page's own status messages. It must check the returned bytes.
