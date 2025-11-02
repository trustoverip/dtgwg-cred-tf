

# Relationship Card Credential Specification (Draft)

## Abstract

The **RelationshipCardCredential** is a subtype of [Verifiable Credential](https://www.w3.org/TR/vc-data-model/) that expresses business card-style information about the issuer  in the context of a specific [Verifiable Relationship Credential](./vrc.md).
- These cards are suitable for any type of relationship between any entity types, human, organizational or machine.
- The data provided MUST conform to [jCard (RFC 7095)](https://datatracker.ietf.org/doc/html/rfc7095), the JSON serialization of vCard ([RFC 6350](https://datatracker.ietf.org/doc/html/rfc6350)).
- Additionally, this credential MUST reference a **RelationshipCredential** VC that explicitly asserts the existence of a specific relationship between the subject and an external entity.


## Status of This Document

This is an early-stage draft for review and discussion. It is not a standard and will be revised based on feedback.

## Overview & Motivation

The **Relationship Card Credential** is a type of Verifiable Credential that acts as a digital business card, or more generally a relationship card, using the standardized jCard format to ensure compatibility with existing contact information systems.

The intent is to support voluntary disclosures of one entity to another in the context of a specific [Verifiable Relationship Credential](./vrc.md).

Unlike traditional or unauthenticated digital cards, this credential is cryptographically signed for authenticity and includes a mandatory reference to an authoritative `RelationshipCredential`. This ensures trust in both the cardholder's identity and their claimed relationship (such as employment or membership), making it ideal for secure, privacy-preserving professional introductions and verifiable contact sharing.

### Example Use Cases

TBD

## Terminology

TBD

## Credential Structure

```json
{
  "@context": [
    "https://www.w3.org/ns/credentials/v2",
    "https://firstperson.network/credentials/rcard/v1"
  ],
  "type": ["VerifiableCredential", "RelationshipCardCredential"],
  "issuer": "...",
  "issuanceDate": "...",
  "credentialSubject": {
    "id": "...",
    "relationshipCredential": {
      "id": "...",
      "digest": "..."
    },
    "jcard": [ ... ]
  },

  "proof": { "...": "VC-compliant proof" }
}
```

**jCard conformance:**
- The payload at `credentialSubject.jcard` MUST be a valid [jCard array](https://datatracker.ietf.org/doc/html/rfc7095) as specified in RFC 7095 Section 2.
- The top-level jCard type MUST be `"vcard"`.


## Definitions

**RelationshipCardCredential**
A Verifiable Credential containing a digital business card as governed by the jCard format ([RFC 7095](https://datatracker.ietf.org/doc/html/rfc7095)), and a reference to a RelationshipCredential.

**relationshipCredential**
A REQUIRED property that identifies an externally held or discoverable Verifiable Credential of type `RelationshipCredential`.

- `id` (REQUIRED): A URI or DID URL pointing to the referenced credential.
- `digest` (OPTIONAL): A digest of the referenced credential, for integrity.
- `digestType` (`string`, Optional): The type of digest used.

**digest**
A digest is a cryptographic hash value of the referenced `RelationshipCredential` VC, encoded in base64url (RFC 4648 §5). Recommended hash algorithm is SHA-256.

**jcard**
A REQUIRED property whose value is a valid jCard array (see RFC 7095). This array MUST conform to the vCard/v4 property and type specifications (see [RFC 6350](https://datatracker.ietf.org/doc/html/rfc6350)). Sample fields include `"fn"` (formatted name), `"org"` (organization), `"email"`, `"tel"`, etc. See example.



---

## Example

```json
{
  "@context": [
    "https://www.w3.org/ns/credentials/v2",
    "https://firstperson.network/credentials/rcard/v1"
  ],
  "type": ["VerifiableCredential", "RelationshipCardCredential"],
  "issuer": "did:example:aliceVrcDid",
  "issuanceDate": "2024-06-01T12:00:00Z",
  "credentialSubject": {
    "id": "did:example:bobVrcDid",
    "relationshipCredential": {
      "id": "did:example:aliceCoworkerBob",
      "digest": "47DEQpj8HBSa-_TImW-5JCeuQeRkm5NMpJWZG3hSuFU"
    },
    "jcard": [
      "vcard",
      [
        ["fn", {}, "text", "Jane Doe"],
        ["org", {}, "text", "Example Corp"],
        ["email", {}, "text", "jane.doe@example.com"],
        ["tel", {"type":["work","voice"]}, "text", "+1-555-555-1234"],
        ["title", {}, "text", "Lead Developer"],
        ["adr", {}, "text", ["", "", "100 Business St", "Metropolis", "CA", "94000", "USA"]]
      ]
    ]
  },
  "proof": {
    "type": "Ed25519Signature2020",
    "created": "2024-06-01T12:00:00Z",
    "verificationMethod": "did:example:alice#keys-1",
    "proofPurpose": "assertionMethod",
    "proofValue": "eyJ...kfw"
  }
}
```

---

## 5. Notes

- The **`jcard`** array structure MUST strictly follow [RFC 7095](https://datatracker.ietf.org/doc/html/rfc7095). Implementers SHOULD validate the property order and semantics per the RFC.
- The `relationshipCredential` object MUST reference a valid credential of type `RelationshipCredential` that asserts or describes the relevant relationship.
- The digest aids in offline validation but is OPTIONAL.
- The top-level VC claims the cardholder's connection to a relationship specified in the reference.



## Security and Privacy Considerations

TBD - See ongoing work of the DTGWG

## Future Work

TBD

## References

- [W3C Verifiable Credentials Data Model](https://www.w3.org/TR/vc-data-model/)
- [RFC 7095: jCard (JSON format for vCard)](https://datatracker.ietf.org/doc/html/rfc7095)
- [RFC 6350: vCard Format Specification](https://datatracker.ietf.org/doc/html/rfc6350)
- [RFC 4648: Base64url encoding](https://datatracker.ietf.org/doc/html/rfc4648)
- [RelationshipCredential](./vrc.md)

