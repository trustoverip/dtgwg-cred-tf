# Witnessed session-based VRC exchange

There are a variety of important use cases of ***witnessed*** Verifiable Relationship Credentials (VRCs), hereafter referred to as WVRCs.

A trusted "fair witness", authorized by an overarching organization or trust community by virtue of possession of an appropriate Verifiable Credentials (VC), can lend legitimacy to VRC exchange processes by witnessing them in real-time. *A trusted witness might be a human, or might be an agent or bot authorized by the organization to perform this function.*

Some use cases include:

*  **Events** (e.g. conferences or classes or meetings) - An on-site human docent or automated bot could witness an in-person VRC exchange, to confirm that **humans**[^1] present in the same space performed the exchange live and on-site (i.e. "proximity" or "attendance" bound credentials)
* **Virtual VRC real-time exchange** - An authorized human or bot witnesses and witnesses a virtual real-time exchange of VRCs by two **humans**.
* **Verifiable virtual "selfies" or "check-ins"** - An authorized human or bot witnesses a virtual "selfie" of one or more people in the same place or virtual session at the same time

## Terminology

**Working definitions**: To **witness** is to observe real-time communications, exchanges and proof presentations in a shared private session or channel, usually within a fixed time-window. In the context of the processed proposed here, a **witness** is an entity (human or agent/bot) explicitly authorized by some trust community to witness some communications and provide verifiable proof of their witness.

## Witnessed VRC Session Flow (Alice, Bob and Witness)

This is an extension of the VRC exchange flow described in the [First Person Project Whitepaper](https://docs.google.com/document/d/1RtS86BqyVn3i3mXm48VhC-SRaYvW2W_MvR4w6x9KQWY/edit?tab=t.0#heading=h.siks62ntn9c5).
1. **Session Creation** - Forming a shared notarization session.
   1. **Session Request:**
      **Alice** (or **Bob**) sends a `session-request` message to **Witness**, asking her to act as witness for a VRC exchange with the other party (specifying both DIDs and the purpose).

   2. **Session Coordination:**
      **Witness** reviews the request, confirms her availability (optionally replying with a `session-response` message), and, if accepted, generates a unique session ID and her own witness nonce.

   3. **Session Invitation:**
      **Witness** sends a `session-invitation` message to both **Alice** and **Bob**. This includes the session ID, her witness nonce, the participant DIDs, the purpose, and (if needed) a link to a real-time communication channel.

   4. **Session Acknowledgement:**
      **Alice** and **Bob** each generate a unique party nonce and reply with a `session-ack` message to **Witness**, referencing the session ID and witness's nonce, and including their own party nonce and acceptance.

   5. **Session Start Announcement:**
      After receiving both acknowledgements, **Witness** sends a `session-start` message to **Alice** and **Bob**. This message includes the session ID and all three nonces (witness, Alice, and Bob), and marks the official session start time. An expiration time can also be optionally specified.

2. **Credential Creation and Signing:**

   1. **Bob**'s agent wallet generates a [VRC](./vrc.md) including the pairwise private DIDs, session info (ID and nonces), datestamp, and any persona DIDs he wishes to connect. **Bob** signs the VRC with his relevant keys and sends the signed VRC to **Alice** and **Witness**.

   2. **Alice**'s agent wallet generates a [VRC](./vrc.md) including the pairwise private DIDs, session info (ID and nonces), datestamp, and any persona DIDs he wishes to connect. **Alice** signs the VRC with her relevant keys and sends the signed VRC to **Bob** and **Witness**.

4. **Witness Endorsement:**

   1. **Witness**, who has observed the process in real time, verifies both signatures and the session information. **Witness** then issues a new [Verifiable Witness Credential](./vwc.md) that is a linkage proof, explicitly attesting that the credentials were signed under her observation during the session. The session may have a "timeout" window set to ensure synchrony. witness may also include proof of her delegated authority and perhaps an event credential (e.g. for a particular conference or class).

5. **Credential Distribution:**

   1. **Witness** sends the completed, witnessed VRC (WVRC) to both **Alice** and **Bob**. The witnessed credential now contains Alice's, Bob's, and witness's signatures, along with full session information and nonces.

6. **Verification:**

   1. **Alice** and **Bob** each verify **Witness**'s witness signature and, if needed, her witness delegation credential from her organization.

**At the end of this flow, Alice and Bob possess a relationship credential, cryptographically signed by both parties and witnessed in real time by witness, with the session context securely bound into the record.**

