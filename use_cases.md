# Use Cases and Applications

## 1. Identity & Sybil Resistance

*Confirming uniqueness and humanity without doxxing.*

| Fact to Prove | Credentials Used | Method (ZKP vs Reveal) | Use Case |
| :--- | :--- | :--- | :--- |
| **"I am a verified human."** | **PHC** | **ZKP** | Logging into a social platform that bans bots without revealing your name or government ID. |
| **"I am a unique member of this community."** | **VCC** + **PHC** | **ZKP** | "One-person-one-vote" governance systems where you prove you have the right to vote exactly once, without revealing which member you are. |
| **"I am a citizen of Country X."** | **PHC** (from Gov Issuer) | **Reveal** or **ZKP** | KYC/AML compliance where the C-DID is a national registry. |
| **"I have been a member since [Year]."** | **VCC** | **ZKP** (Range Proof) | Airdrops or loyalty rewards reserved for long-term community members (proving `validFrom` < 2022). |

## 2. Social Capital & Trust (Web of Trust)

*Quantifying reputation through graph topology.*

| Fact to Prove | Credentials Used | Method (ZKP vs Reveal) | Use Case |
| :--- | :--- | :--- | :--- |
| **"I have > 50 connections in this community."** | **VCC** + **50x VRCs** | **ZKP** (Count) | Gating access to a "VIP Lounge" based on community popularity rather than wealth. |
| **"I am connected to [Influencer]."** | **VCC** + **VRC** (from Influencer) | **Reveal** | Establishing immediate credibility by showing a direct link to a community leader. |
| **"My relationship is notarized."** | **VRC** + **VWC** | **Reveal** | Proving a relationship exists (e.g., employment) that was witnessed by a third party (e.g., HR or Auditor). |
| **"I am trusted by people you trust."** | **VCC** + **VRC** (Chain) | **Reveal** | The "LinkedIn" model: showing 2nd-degree connections to establish a warm introduction path. |

## 3. Competence & Reputation

*Proving skills based on peer or expert validation.*

| Fact to Prove | Credentials Used | Method (ZKP vs Reveal) | Use Case |
| :--- | :--- | :--- | :--- |
| **"I am a rated Expert in Rust."** | **VCC** + **VEC** | **Reveal** | Hiring/Recruiting. Proving a specific skill endorsement from a known entity within a developer community. |
| **"I have 5 distinct endorsements for Integrity."** | **5x VECs** (from diff issuers) | **ZKP** (Aggregation) | Reputation scoring. Proving you are a "high integrity" user to lower collateral requirements for a loan, without revealing who vouched for you. |
| **"I was endorsed by a Verified Human."** | **VEC** + **Issuer's PHC** | **ZKP** (Nested) | Filtering out bot-farm endorsements. "My rating is real because the people who rated me are proven humans." |

## 4. Contextual Identity & Persona Management

*Managing how you are perceived across different edges.*

| Fact to Prove | Credentials Used | Method (ZKP vs Reveal) | Use Case |
| :--- | :--- | :--- | :--- |
| **"I am also [Famous Persona]."** | **VPC** | **Reveal** (P2P) | **The Banksy Maneuver.** You are at a coffee shop (as Alice). You send a VPC to your friend proving you also control the "Banksy" DID, without linking Alice to Banksy on the public graph. |
| **"This allows me to message you."** | **R-Card** | **Reveal** | Spam filtering. Proving you have verified contact details (Email/JCard) associated with a valid relationship edge, allowing you to bypass a spam filter. |
| **"I am the same person from Context A."** | **VCC (Community A)** + **VCC (Community B)** | **ZKP** (Linkage) | Cross-app reputation. Proving that the owner of the "Chess Club" profile is the same entity as the "DeFi Trader" profile without merging the identities publicly. |

## 5. Advanced Composite Proofs

*Complex logic combining multiple types.*

- **The "Sybil-Resistant Graph" Proof:**
  - *Credentials:* **VRC** (Relationship) + **Issuer's PHC** (Personhood).
  - *Claim:* "I have relationships with 10 *verified humans*."
  - *Why:* This prevents users from spinning up 100 fake nodes to endorse themselves.

- **The "Qualified Witness" Proof:**
  - *Credentials:* **VWC** (Witness) + **Witness's VEC** (Endorsement).
  - *Claim:* "This contract/relationship was witnessed by someone explicitly endorsed as a 'Notary' or 'Auditor'."

- **The "Community Bridge" Proof:**
  - *Credentials:* **VCC** (from Community A) + **VCC** (from Community B).
  - *Claim:* "I act as a bridge node between the Engineering Team and the Sales Team."
  - *Why:* Useful for organizational analysis to identify key communication hubs.
  