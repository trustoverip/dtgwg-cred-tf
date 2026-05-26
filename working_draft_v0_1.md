{{INSTRUCTIONS ABOUT THE USE OF THIS TEMPLATE: All editorial instructions are enclosed in {{double curly braces}} and MUST be either removed from or replaced in the specification document. All other text MUST be included in the specification document. NOTE: As of 2026, ToIP specifications are required to use [Spec-Up-T](https://trustoverip.github.io/spec-up-t-website/). It will automatically generate a table of contents for the entire specification document.}}

# Decentralized Trust Graph Credentials - Core Specification

_Version:_ 0.1
_Document Status:_ Working Draft
_DOI:_ {{see [this wiki page](https://lf-toip.atlassian.net/wiki/spaces/HOME/pages/767787009/ToIP+Approved+Deliverable+Process#Persistent-DOI-Link) for instructions about how to add a DOI}}

_Editors:_ {{MUST list the full names, optional OrcID and official LF affiliations of each editor.}}

- {{Editor 1, Org A}}
- {{Editor 2, Org B}}

_Contributors:_ {{MUST list the full names and official LF affiliations of each substantial contributor — all other acknowledgements go in the Acknowledgements Appendix at the end.}}

- {{Contributor 1, Org C}}
- {{Contributor 2, Org A}}

**Abstract**

{{REQUIRED. MUST be a concise summary of the specification written so someone without domain-specific knowledge can quickly understand what it covers.}}

**Intellectual Property Rights**

This specification is provided under the [Joint Development Foundation](https://jointdevelopment.org) (JDF) charter for [Trust Over IP](https://trustoverip.org) (ToIP) and is subject to the intellectual property rights policy of the **Decentralized Trust Graph Working Group**:

{{modify the following bullets to reflect the IPR terms of the Working Group}}
_Copyright:_ [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/)
_Patent:_ W3C Mode (based on the [W3C Patent Policy](https://www.w3.org/Consortium/Patent-Policy-20040205/))
_Source Code:_ [Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0)

THESE MATERIALS ARE PROVIDED “AS IS.” The parties expressly disclaim any warranties (express, implied, or otherwise), including implied warranties of merchantability, non-infringement, fitness for a particular purpose, or title, related to the materials. The entire risk as to implementing or otherwise using the materials is assumed by the implementer and user. IN NO EVENT WILL THE PARTIES BE LIABLE TO ANY OTHER PARTY FOR LOST PROFITS OR ANY FORM OF INDIRECT, SPECIAL, INCIDENTAL, OR CONSEQUENTIAL DAMAGES OF ANY CHARACTER FROM ANY CAUSES OF ACTION OF ANY KIND WITH RESPECT TO THIS DELIVERABLE OR ITS GOVERNING AGREEMENT, WHETHER BASED ON BREACH OF CONTRACT, TORT (INCLUDING NEGLIGENCE), OR OTHERWISE, AND WHETHER OR NOT THE OTHER MEMBER HAS BEEN ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

## Introduction

{{REQUIRED. This is the first numbered section and SHALL be written so a layperson can quickly get an overview of the purpose and structure of the specification.}}

## Requirements Language

The key words “MUST”, “MUST NOT”, “REQUIRED”, “SHALL”, “SHALL NOT”, “SHOULD”, “SHOULD NOT”, “RECOMMENDED”, “MAY”, and “OPTIONAL” in this document are to be interpreted as described in [IETF RFC 2119](https://datatracker.ietf.org/doc/html/rfc2119).

## Terminology

{{This section SHOULD include the most important terms required for a reader to understand the specification. These terms SHOULD be managed using the Spec-Up-T glossary features. This glossary MAY include terms that are in the referenced glossaries above if those terms are essential to understanding the specification—in that case those terms SHOULD use the Spec-Up-T transclusion (tref) feature. Alternatively, in the judgement of the editors, this section MAY be either: a) replaced, or b) supplemented with a separate glossary included as an Appendix.}}

Any hyperlinked term not included in this section is referenced from one of the following glossaries:

- [ToIP Main Glossary](https://glossary.trustoverip.org)
- [ToIP General IT Glossary](https://trustoverip.github.io/ctwg-general-glossary)
- {{any other external glossary included in Spec-Up-T xrefs}}

## {{First Level Section Name}}

{{Every top-level section MUST include exactly one of the following two sentences immediately after the section header:
This section is normative.
This section is informative.
The first sentence MUST be used if the section contains any normative requirements expressed using RFC keywords. The second sentence MUST be used if the section does NOT contain any normative requirements (and therefore MUST NOT contain any RFC keywords). As a general best practice, all normative sections SHOULD be grouped together.}}

{{Each new section or subsection SHOULD begin with at least a sentence or paragraph introducing the purpose of that section.}}

### {{Second Level Section Name}}

{{Each new section or subsection SHOULD always begin with at least a sentence or paragraph introducing the purpose of that section.}}

#### {{Third Level Section Name}}

{{Each new section or subsection SHOULD always begin with at least a sentence or paragraph introducing the purpose of that section.}}

{{A bit about the [[ref: VTC]] for your info... (just showing an example glossary reference here in the text)}}

{{When nesting sections it is RECOMMENDED to go no more than three levels deep. Use as many sections as is necessary to cover all the requirements of the specification, but keep the text and diagrams as concise as possible. [See this IETF guidance](https://www.ietf.org/archive/id/draft-flanagan-7322bis-07.html#name-body-of-the-memo).}}

## Security Considerations

{{REQUIRED for all ToIP specifications. This section SHOULD be formatted as either a numbered list or numbered subsections. [See this IETF guidance](https://www.ietf.org/archive/id/draft-flanagan-7322bis-07.html#name-security-considerations-sec) and also the Security Considerations sections in [DID Core](https://www.w3.org/TR/did-1.0/#security-considerations) and [W3C VC](https://www.w3.org/TR/vc-data-model/#security-considerations).}}

## Privacy Considerations

{{REQUIRED for all ToIP specifications. This section SHOULD be formatted as either a numbered list or numbered subsections. [See this IETF guidance](https://datatracker.ietf.org/doc/html/rfc6973) and also the Privacy Considerations sections in [DID Core](https://www.w3.org/TR/did-1.0/#privacy-considerations) and [W3C VC](https://www.w3.org/TR/vc-data-model/#privacy-considerations).}}

## Governance Considerations

{{RECOMMENDED for most ToIP specifications. This section SHOULD be formatted as either a numbered list or numbered subsections. This section SHOULD include any relevant references to the [ToIP governance metamodel](https://trustoverip.org/wp-content/uploads/ToIP-Governance-Metamodel-Specification-V1.0-2021-12-21.pdf). [See also this IETF guidance](https://www.ietf.org/archive/id/draft-attoumani-ietf-inclusion-00.html).}}

## Internationalization Considerations

{{RECOMMENDED for most ToIP specifications. This section SHOULD be formatted as either a numbered list or numbered subsections. [See this IETF guidance](https://www.ietf.org/archive/id/draft-flanagan-7322bis-07.html#name-internationalization-consid).}}

## Accessibility Considerations

{{RECOMMENDED for most ToIP specifications. This section SHOULD be formatted as either a numbered list or numbered subsections. [See this IETF guidance](https://datatracker.ietf.org/doc/html/rfc6973) and also the Accessibility Considerations section in [W3C VC](https://www.w3.org/TR/vc-data-model/#accessibility-considerations).}}

## Conformance

{{REQUIRED. This section should state what normative requirements (expressed using “MUST” or “SHALL” keywords) apply to which conformance targets. See the [Guidelines to Writing Conformance Clauses](https://docs.oasis-open.org/templates/TCHandbook/ConformanceGuidelines.html) from OASIS Open.}}

### Conformance Targets

### Conformance Tests

## References

{{Required. See the [IETF guidance](https://www.ietf.org/archive/id/draft-flanagan-7322bis-07.html#name-references-section) on how to add normative references and informative references.}}

### Normative References

### Informative References

## Appendices

### Appendix A: {{Name}}

### Appendix B: {{Name}}

### Appendix C: Acknowledgements

{{The final appendix should contain any additional acknowledgements}}

Copyright © 2026 Trust Over IP (ToIP) Contributors
This work is licensed under a Creative Commons Attribution 4.0 International License.
