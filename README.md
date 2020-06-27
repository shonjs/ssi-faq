This is a compilation of FAQs with answers, resources etc from various Hyperledger chats, READMEs, queries/blockers that I faced during development. I have kept the answers from contributors in chat (minor edits for typos, later update or for better comprehension)

## Indy

**Where is private and public key stored? in wallet? not on ledger?**

* All that you create or receive go in your wallet. Public DIDs that you create also go in the ledger. DIDs you receive from others may be on a ledger or not. DIDs from VC issuers will be on a ledger (public) and your agent may or may not store them.

**What exactly is stored in Wallets?**

* Indy wallets store: DIDs, the private keys associated with DIDs you create, other ledger transactions that you create (schema, credential definitions, revocation registries, revocation entries).

***"No data is sent to the Blockchain. Ever. It is only used for DIDs, schema/credential metadata and revocation information."* - (@swcurran Rocketchat)  What do u mean by metadata?**

* The "metadata" are the objects needed to prove and verify claims from credentials. That means in Indy -- schema, credentials definitions, RevRegs and RevEntries).

**Can you please explain the credential verification flow, issuer-verifer-holder?**

- Issuer creates DID, schema (or reuses an existing one), Credential Definition (public keys per claim, pointer to Issuers DID, pointer to Schema)
- Issuer optionally creates a Revocation Registries (if creds will be revocable) which has a pointer to the CredDef.
- Issuer offers a credential to the Holder; Holder requests the credential, providing a blinded link secret; Issuer issues credential to the Holder.
- the credential references the CredDef (points to schema and Issuer DID), is signed by the Issuer DID private key, each claim is signed using the keys in the - CredDef, the Holder gets a credential ID (for revocation)
- Verifier sends a proof request to the Holder with the list of claims they want proven. Claims have restrictions about the credentials they can come from (e.g. what schema, what Cred Def, what issuers, etc.)
- Prover finds credentials that meet the criteria in the cred def and constructs a proof.
- They prove they have the link secret that proves the credentials were issued to them.
- The DID and signature on each claims prove they were issued by the issuer
- The signing of each claim using the CredDef keys prove they were not tampered with.
- If revocable, the Prover creates a "Proof of non-revocation" to show the claims are from credentials that are not revoked.
- Verifier gets the Cred Def from the ledger, the schema from the ledger, the Issuer DID from the ledger and uses those to verify the proofs from the Prover.

**Without having information about credentials (it isn't stored on ledger, only store in holder wallet), how will verifier confirms (verify) that these credentials are same as they were issued by issuer? I mean what if holder received credentials, changes later, how will verifer/issuer know that?**

* https://github.com/hyperledger/indy-hipe/tree/master/text/0011-cred-revocation
