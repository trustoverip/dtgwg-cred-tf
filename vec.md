# Verifiable Endorsement Credential (Draft)

## Abstract

This document introduces a new proposed subtype of W3C Verifiable Credentials:
1. **Verifiable Endorsement Credential**: Enables standardized issuance, exchange, and verification of claims in which one entity makes specific endorsements about aspects of the relationship with another entity in the context of a specific [Verifiable Relationship Credential](./vrc.md).

This credential type can be issued by and to individuals, organizations, agents, or any other entities, whether human or machine.


## Status of This Document

This is an early-stage draft for review and discussion. It is not a standard and will be revised based on feedback.

## Overview & Motivation

These credential types were proposed by the First Person Project as a decentralized and privacy-preserving global infrastructure for social verification.

Read more about the motivation and vision for this effort in the [First Person Project Whitepaper](https://www.firstperson.network/white-paper).

### Example Use Cases

- Parental approvals and endorsements
- Employment or reference endorsements
- Professional ratings or recommendations
- AI agent trust scoring
- Peer reviews
- Quality or skill endorsements

## Terminology

TBD

## Credential Structure

A **Verifiable Endorsement Credential** extends the standard [Verifiable Credential](https://www.w3.org/TR/vc-data-model) as follows:

```json
{
  "@context": [
    "https://www.w3.org/ns/credentials/v2",
    "https://firstperson.network/credentials/endorsement/v1"
  ],
  "type": [
    "VerifiableCredential",
    "EndorsementCredential"
  ],
  "issuer": "...",
  "issuanceDate": "...",
  "name": "...",
  "description": "...",
  "credentialSubject": {
    "id": "...",
    "relationshipCredential": {
      "id": "...",
      "digest": "..."
    },
    "endorser": {
      "did": "...",
      "name": "...",
      "alsoKnownAs": [],
      "linkageProofs": [ ... ],
      "externalProofs": [ ... ]
    },
    "endorsed": {
      "did": "...",
      "name": "...",
      "alsoKnownAs": []
    },
    "endorsementClaims": [
      {
        "type": "...",
        "claimType": "...",
        "value": "..."
      }
    ]
  },
  "proof": {
    "type": "...",
    "created": "...",
    "proofPurpose": "...",
    "verificationMethod": "...",
    "proofValue": "..."
  }
}
```

**Notes:**
- **Verifiable Endorsement Credential** explicitly references an existing VRC (via the `relationshipCredential.id`, which may be a DID, URI, or VC object identifier).
- The `endorser` is the party making the endorsement about some aspect(s) of the relationship.
- The `endorsed` is typically the recipient or target of the endorsement.
- The `endorsementClaims` object contains the actual claims, comments, or ratings about the relationship—**this is what distinguishes a VEC from a VRC**.
- The endorsement can be as granular or broad as your schema permits (can include scores, booleans, free text, or links to vocabularies).
- Follows the same signature/proof structure for authenticity.

### Definitions

- **@context** (`array[string]`, Required)
  JSON-LD context URIs defining the semantic meaning of terms in the credential.

- **type** (`array[string]`, Required)
  Credential type identifiers. Must include `"VerifiableCredential"` and `"EndorsementCredential"`.

- **issuer** (`string`, Required)
  DID or URI identifying the entity issuing the credential.

- **issuanceDate** (`string`, Required)
  The issuance date of the credential, in ISO 8601 format.

- **name** (`string`, Optional)
  Human-readable name or title for the endorsement credential.

- **description** (`string`, Optional)
  Human-readable description of the endorsement.

- **credentialSubject** (`object`, Required)
  Defines the relationship endorsement.
  - **id** (`string`, Required)
    Unique identifier for this endorsement (can also be the id of the endorsed subject or a new identifier).
  - **relationshipCredential** (`object`, Required):
    An object referencing the Verifiable Relationship Credential (VRC) being endorsed.
    - **id** (`string`, Required): The identifier (DID, URI, or hash) of the external relationship credential.
    - **digest** (`string`, Optional): Optional cryptographic hash of the referenced credential, for integrity confirmation.
    - **digestType** (`string`, Optional): The type of digest used
  - **endorser** (`object`, Required)
    Information about the endorsement-asserting entity:
      - **did** (`string`, Required): DID of the endorser.
      - **name** (`string`, Optional): Human-readable name of the endorser.
      - **alsoKnownAs** (`array[string]`, Optional): Alternative subject-controlled IDs.
      - **linkageProofs** (`array[object]`, Optional): Cryptographic linkage proofs as defined in VRC.
      - **externalProofs** (`array[object]`, Optional): References to externally published linkage proofs as in VRC.
  - **endorsed** (`object`, Required)
    Information about the entity being endorsed:
      - **did** (`string`, Required): DID of the endorsed.
      - **name** (`string`, Optional): Human-readable name of the endorsed.
      - **alsoKnownAs** (`array[string]`, Optional): Alternative subject-controlled IDs.
  - **endorsementClaims** (`array[object]`, Required)
    Array of endorsement statements—formal claims referencing clear vocabularies/ontologies, and/or informal comments.
    - **type** (`string`, Required)
      Classifies the claim; either `"FormalClaim"` (for data using a machine-readable vocabulary or ontology), or `"FreeForm"` (for unstructured comments or references).
    - **claimType** (`string`, Required)
      - For `"FormalClaim"`, this should be a URI or term from a published vocabulary or ontology describing the nature of the claim (examples: `"https://schema.org/roleName"`, or `"https://www.sfia-online.org/en/sfia-8/skills/project-management"`).
      - For `"FreeForm"`, this may be `"comment"` or another plain label.
    - **value** (any, Required)
      - For `"FormalClaim"`, a string, number, boolean, or array representing the value of the claim (e.g., `"excellent"`, `["python", "cryptography"]`, `true`, etc.).
      - For `"FreeForm"`, a text narrative or general endorsement.

- **proof** (`object`, Required)
  Cryptographic proof of credential authenticity:
  - **type** (`string`, Required): The proof cryptographic suite used.
  - **created** (`string`, Required): When the proof was created, ISO 8601 format.
  - **proofPurpose** (`string`, Required): Proof purpose (usually `"assertionMethod"`).
  - **verificationMethod** (`string`, Required): Verification method reference.
  - **proofValue** (`string`, Required): Signature value.

---

## Example: Alice endorses Bob as "excellent teammate" for their coworker relationship

```json
{
  "@context": [
    "https://www.w3.org/ns/credentials/v2",
    "https://firstperson.network/credentials/endorsement/v1"
  ],
  "type": [
    "VerifiableCredential",
    "EndorsementCredential"
  ],
  "issuer": "did:example:alice",
  "issuanceDate": "2024-06-21T12:00:00Z",
  "name": "Endorsement for Bob Jones",
  "description": "Alice's endorsement of Bob for exceptional teamwork and leadership in their coworker relationship.",
  "credentialSubject": {
    "id": "urn:uuid:vec-alice-bob-1234",
    "relationshipCredential": {
      "id": "did:example:aliceCoworkerBob",
      "digest": "32af6a08af965a8c212640e1eda0e577584a96542ebf2c2dc006ee4234c9883a",
      "digestType": "SHA-256"

    },
    "endorser": {
      "did": "did:example:aliceVrcDid",
      "name": "Alice Smith",
      "alsoKnownAs": [
        "did:example:aliceProfessionalDid"
      ]
    },
    "endorsed": {
      "did": "did:example:bobVrcDid",
      "name": "Bob Jones",
      "alsoKnownAs": [
        "did:example:bobProfessionalDid"
      ]
    },
    "endorsementClaims": [
      {
        "type": "FormalClaim",
        "claimType": "https://schema.org/roleName",
        "value": "project manager"
      },
      {
        "type": "FormalClaim",
        "claimType": "https://www.sfia-online.org/en/sfia-8/skills/information-security",
        "value": "advanced"
      },
      {
        "type": "FormalClaim",
        "claimType": "https://www.example.org/vocab/teamwork",
        "value": "exceptional"
      },
      {
        "type": "FreeForm",
        "claimType": "comment",
        "value": "Bob is one of the most reliable team members I have worked with, always positive and proactive."
      }
    ]
  },
  "proof": {
    "type": "Ed25519Signature2020",
    "created": "2024-06-21T12:00:01Z",
    "proofPurpose": "assertionMethod",
    "verificationMethod": "did:example:alice#key-1",
    "proofValue": "zKesw8HyJh3WpHrT70pBy..."
  }
}
```

**Notes:**
- The `relationshipCredential` field points to the VRC; verifiers can use this to check the existence and basis of the relationship before trusting the endorsement.
- `endorsementClaims` can include structured claims (e.g., `"leadership": true`) and/or narrative text.

## Security and Privacy Considerations

TBD - Reference ongoing work from the DTGWG.

## Future Work

TBD

## References

- [W3C Verifiable Credentials Data Model](https://www.w3.org/TR/vc-data-model/)

---