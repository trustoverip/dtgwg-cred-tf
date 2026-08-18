# Decentralized Trust Graph Working Group - Credentials Task Force

This is the working repo for the DTG Credentials Task Force.

## Specification

The normative DTG Core Credentials specification has moved to
[trustoverip/dtgwg-cred-spec](https://github.com/trustoverip/dtgwg-cred-spec).
It defines the DTG Core Credentials: six W3C Verifiable Credential types
that create and annotate a Decentralized Trust Graph, along with the
associated verifiable data structure.

## Issues and Proposals

Issues and proposals specific to the spec itself (credential types, the
verifiable data structure, normative text) should now be directed to the
[dtgwg-cred-spec issue tracker](https://github.com/trustoverip/dtgwg-cred-spec/issues).

## Discussions

General discussions about DTG credentials (i.e., not specific to the spec
text) remain active here in the
[discussions section](https://github.com/trustoverip/dtgwg-cred-tf/discussions)
of this repo.

## Contributing

All commits to this repo must be signed off under the
[Developer Certificate of Origin](https://developercertificate.org/). Add a
`Signed-off-by` trailer to each commit by using the `-s` flag:

```
git commit -s -m "Your commit message"
```

This appends a line matching your git `user.name` and `user.email`:

```
Signed-off-by: Your Name <your.email@example.com>
```

Pull requests with unsigned commits will not be merged. To fix an existing
commit, amend it with `git commit --amend -s` (or, for multiple commits,
`git rebase --signoff <base>`) and force push the branch.

## Supporting Materials

This repo retains supporting/reference material that did not move with the
spec:

- [Use Cases and Applications](./use_cases.md) — illustrative applications of
  the credential types (identity, social capital, governance, etc.)
- [Witnessed Verifiable Relationship Credential Exchange](./witnessed_vrc_flow.md) —
  the witness protocol, kept here as a reference

## External Materials

- the [First Person Project Whitepaper](https://www.firstperson.network/white-paper) for more general information
- the [VTC Bootstrapping Process](https://docs.google.com/document/d/10XphBSyJNrF90AtdEyiwFu2eof-LEKjOvqPQ1wri5Cs/edit?tab=t.0) for information on bootstrapping new VTCs
- the [DTG Glossary](https://docs.google.com/document/d/1gqFqUAYy_huBbn6YakPBScotO15PA0nLq1_9uJkr6bY/edit?tab=t.0#heading=h.mazxiry8x5s3) for definitions of terms
- the [Standard Verifiable Relationship Credential Exchange](https://docs.google.com/document/d/1QrjQfCB9V6l5sx5CBSjKDRf-dCBHzkVQRjr-GQrbyWw/edit?tab=t.0#bookmark=id.kddyxwdo2qf4) flow
