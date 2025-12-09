# Decentralized Trust Graph Credentials

**NOTE**: This is early draft for comment and revision (v0.2) of these specifications.

See the [First Person Project Whitepaper](https://www.firstperson.network/white-paper) for more information.

## Credential Types

Seven related credential types are described here: [Decentralized Trust Graph Credentials](./dtg.md).

1.  **Community Credential** (VCC): Establishes membership in a community defined by a Community DID (C-DID).
2.  **Personhood Credential** (PHC): A specialized VCC issued by a C-DID listed in a trust registry (PHC-DID) to establish verified personhood.
3.  **Relationship Credential** (VRC): Establishes a directional relationship edge between two entities within the same community context.
4.  **Persona Credential** (VPC): Enables an entity to share a specific persona/context without creating a new DTG edge.
5.  **Endorsement Credential** (VEC): Endorses another entity for skills or accomplishments.
6.  **Witness Credential** (VWC): Attests to the establishment of a Relationship Credential from the perspective of a Witness DID (W-DID).
7.  **Relationship Card** (R-Card): A human-readable identity presentation (JCard) akin to a business card.



## Credential Exchange Flows

- [Standard Verifiable Relationship Credential Exchange](https://docs.google.com/document/d/1RtS86BqyVn3i3mXm48VhC-SRaYvW2W_MvR4w6x9KQWY/edit?tab=t.0#heading=h.siks62ntn9c5)
- [Witnessed Verifiable Relationship Credential Exchange](./witnessed_vrc_flow.md)
