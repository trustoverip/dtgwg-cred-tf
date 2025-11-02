# Verifiable Relationship Credential (Draft)

## Abstract

This document introduces a new proposed subtype of W3C Verifiable Credentials:
1. **Verifiable Relationship Credential** (VRC): Enables standardized issuance, exchange, and verification of claims about the existence of a relationship between two entities, as recognized by one entity towards the other.

This credential type can be issued by and to individuals, organizations, agents, or any other entities, whether human or machine.

## Status of This Document

This is an early-stage draft for review and discussion. It is not a standard and will be revised based on feedback.

## Terminology

The following terms are used to describe concepts in this specification.

**_Verifiable Relationship Credential (VRC)_**
A subtype of a Verifiable Credential that expresses a verifiable, directional claim about the existence of a relationship between two or more entities.

**_Entity_**
Any individual, organization, or autonomous agent that can be identified by a Decentralized Identifier (DID) or another verifiable identifier.

**_From_**
The entity asserting the relationship. It is the originator of the relationship claim and is typically the issuer of the VRC.

**_To_**
The entity that is the target of the relationship claim. It represents the party toward which the relationship is directed.

**_Persona_**
A privacy-preserving, context-specific identifier that allows an entity to represent itself differently in various contexts without revealing its global identity.

**_Pairwise DID_**
A DID created uniquely for a specific relationship or context to prevent correlation of activities across multiple relationships.

**_Issuer_**
The entity that creates and signs the VRC, asserting the existence of a relationship between itself (or another entity) and one or more targets.

**_Proof_**
A cryptographic mechanism that enables verifiers to validate the authenticity, integrity, and authorship of a Verifiable Relationship Credential.

## Overview & Motivation

These credential types were proposed by the First Person Project as a decentralized and privacy-preserving global infrastructure for social verification.

Read more about the motivation and vision for this effort in the [First Person Project Whitepaper](https://www.firstperson.network/white-paper).

### Example Use Cases

- Friends or colleagues
- Parent/guardian-child relationships for consent
- Employer-employee relationships
- Organizational affiliations (e.g., board membership)
- User control over an AI agent
- Agent to agent relationships

In various combinations these credentials can also help to provide:
- Proof of personhood
- Age verification
- Content provenance
- ???

## Credential Structure

A **Verifiable Relationship Credential** extends the standard [Verifiable Credential](https://www.w3.org/TR/vc-data-model) as follows:

```json
{
  "@context": [
    "https://www.w3.org/ns/credentials/v2",
    "https://firstperson.network/credentials/relationship/v1"
  ],
  "type": [
    "VerifiableCredential",
    "RelationshipCredential"
  ],
  "issuer": "...",
  "validFrom": "...",
  "name": "...",
  "description": "...",
  "credentialSubject": {
    "id": "...",
    "from": {
      "did": "...",
      "name": "...",
      "alsoKnownAs": [ ... ],
      "linkageProofs": [ ... ],
      "externalProofs": [ ... ],
      "nonce": "..."
    },
    "to": {
      "did": "...",
      "name": "...",
      "alsoKnownAs": [ ... ],
    },
    "relationshipType": "...",
    "startDate": "...",
    "endDate": "...",
    "session": {
      "id": "...",
      "witnessId": "...",
    }
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
- A Verifiable Relationship Credential explicitly does NOT make any endorsement statements about the character, qualities, or aspects of the relationship. That is what [Verifiable Endorsement Credentials](./vec.md) are for. This allows for decoupling and privacy-preserving disclosure when desired.
- A VRC only has one, if any, `relationshipType`. If there are multiple relationshipTypes, issue multiple VRCs.

### Definitions

- **@context** (`array[string]`, Required)
  JSON-LD context URIs defining the semantic meaning of terms in the credential.

- **type** (`array[string]`, Required)
  Credential type identifiers. Must include `"VerifiableCredential"` and `"RelationshipCredential"`.

- **issuer** (`string`, Required)
  DID or URI identifying the entity issuing the credential.

- **validFrom** (`string`, Required)
  The date and time the credential becomes valid, in ISO 8601 format.

- **name** (`string`, Optional)
  Human-readable name or title for the credential.

- **description** (`string`, Optional)
  Human-readable description of the credential or the relationship.

- **credentialSubject** (`object`, Required)
  The relationship assertion between the entities involved.

  - **id** (`string`, Required)
    DID or URI representing the pairwise relationship between the two entities.

  - **from** (`object`, Required)
    Information about the asserting ("from") entity:
    - **did** (`string`, Required)
      DID of the "from" entity — a single-use DID for this relationship.
    - **name** (`string`, Optional)
      Human-readable name of the "from" entity.
    - **alsoKnownAs** (`array[string]`, Optional)
      Array of verifiable, subject-controlled identifiers/personas (such as DIDs or resolvable URIs) for trustworthy correlation across decentralized identity systems.
    - **linkageProofs** (`array[object]`, Optional)
      An array of cryptographic proofs, each generated by signing a canonical message (such as the subject's DID or a credential hash) with the private key of an identifier listed in `alsoKnownAs`. Used to demonstrate that the entity controls the referenced identifier.
      - **type** (`string`, Required)
        The proof or signature type (e.g., `"Ed25519Signature2020"`, `"PGPSignature2020"`).
      - **identifier** (`string`, Required)
        The identifier (from `alsoKnownAs`) for which control is being proven.
      - **created** (`string`, Required)
        The ISO 8601 date and time when the proof was created.
      - **proofValue** (`string`, Required)
        The cryptographic signature value, such as a JWS or PGP armored block, demonstrating control of the identifier.
      - **nonce** (string, Optional)
        A unique nonce that used when coordinating an exchange session

    - **externalProofs** (`array[object]`, Optional)
      An array of references to externally published proofs or verifiable credentials that demonstrate the entity’s control over an identifier in `alsoKnownAs`.
      - **identifier** (`string`, Required)
        The identifier (from `alsoKnownAs`) to which the external proof refers.
      - **proofUrl** (`string`, Required)
        A HTTPS URL, DID URL, or other resolvable URI where the verifiable proof can be found.
      - **type** (`string`, Optional)
        The type or standard of the external proof (e.g., `"VerifiableCredential"`, `"LinkedDataSignature2020"`, `"PGPSignature2020"`).
      - **created** (`string`, Optional)
        The ISO 8601 date and time when the external proof was created.

  - **to** (`object`, Required)
    Information about the target ("to") entity:
    - **did** (`string`, Required)
      DID of the "to" entity — a single-use DID for this relationship.
    - **name** (`string`, Optional)
      Human-readable name of the "to" entity.
    - **alsoKnownAs** (`array[string]`, Optional)
      Array of verifiable, subject-controlled identifiers/personas (such as DIDs or resolvable URIs) for trustworthy correlation across decentralized identity systems.

  - **relationshipType** (`string`, Optional)
    URI or term from a published vocabulary specifying the nature of the relationship.

  - **startDate** (`string`, Optional)
    Start date of the relationship, in ISO 8601 format.

  - **endDate** (`string`, Optional)
    End date of the relationship, if applicable, in ISO 8601 format.

  - **session:** (`object`, Optional)
    Describes the live witnessing session linking the Fair Witness and the participants, if any.
    Contains:
      - **id** (`string`, Required): A unique session identifier (e.g. UUID or URN)
      - **witnessId** (`string`, Optional): The DID of the  session witness of any

- **proof** (`object`, Required)
  Cryptographic proof of credential authenticity.
  - **type** (`string`, Required)
    The proof cryptographic suite used (e.g., `"Ed25519Signature2020"`).
  - **created** (`string`, Required)
    When the proof was created, in ISO 8601 format.
  - **proofPurpose** (`string`, Required)
    The intent of the proof (usually `"assertionMethod"`).
  - **verificationMethod** (`string`, Required)
    URI or DID URL for the public key or verification method used.
  - **proofValue** (`string`, Required)
    The signature value (property name may vary by cryptosuite, e.g., `"jws"`).

**Notes:**
- **Required** fields must always be present for a valid `RelationshipCredential`.
- **Optional** fields are for additional expression, documentation, or usability.

## Example: Alice issues a VRC to Bob, as a previous co-worker

```json
{
  "@context": [
    "https://www.w3.org/ns/credentials/v2",
    "https://firstperson.network/credentials/relationship/v1"
  ],
  "type": [
    "VerifiableCredential",
    "RelationshipCredential"
  ],
  "issuer": "did:example:alice",
  "validFrom": "2024-06-18T10:00:00Z",
  "name": "Bob:Co-worker",
  "description": "This credential attests that Bob was my co-worker from 1/10/2010 through 10/11/2025.",
  "credentialSubject": {
    "id": "did:example:aliceCoworkerBob",
    "from": {
      "did": "did:example:aliceVrcDid",
      "name": "Alice Smith",
      "alsoKnownAs": [
        "did:example:aliceProfessionalDid",
        "openpgp4fpr:ABCD1234EF5678901234567890ABCDEF12345678"
      ],
      "nonce": "9b8cf3ce-7e10-4f90-93c2-013781c9edb3",
      "linkageProofs": [
        {
          "type": "Ed25519Signature2020",
          "identifier": "did:example:aliceProfessionalDid",
          "created": "2024-06-20T08:00:00Z",
          "proofValue": "zHTh34rGk2Wm..."
        },
        {
          "type": "PGPSignature2020",
          "identifier": "openpgp4fpr:ABCD1234EF5678901234567890ABCDEF12345678",
          "created": "2024-06-20T08:01:00Z",
          "proofValue": "-----BEGIN PGP SIGNATURE-----..."
        }
      ]
    },
    "to": {
      "did": "did:example:bobVrcDid",
      "name": "Bob Jones",
      "alsoKnownAs": [
        "did:example:bobProfessionalDid"
      ]
    },
    "relationshipType": "https://schema.org/Coworker",
    "startDate": "2018-09-01",
    "endDate": "2022-06-30",
    "session": {
      "id": "d91e13c0-67a4-4aed-9e48-04e249c83a00",
      "witnessId": "did:example:witness123"
    }
  },
  "proof": {
    "type": "Ed25519Signature2020",
    "created": "2024-06-18T10:01:00Z",
    "proofPurpose": "assertionMethod",
    "verificationMethod": "did:example:university-123#key-1",
    "proofValue": "zKesw8HyJh3WpHrT70pBy..."
  }
}
```

## Security and Privacy Considerations

TBD - Reference ongoing work from the DTGWG.

## Future Work

- Standardization of `relationshipType` vocabularies
- ZKP support for selective disclosure
- TBD

## References

- [W3C Verifiable Credentials Data Model](https://www.w3.org/TR/vc-data-model/)
