# PEN&PAD terminology-driven input
SNOMED CT decides the options; outputs for openEHR and FHIR

Made by Gunnar Nordqvist · [GitHub](https://github.com/gunnarnordqvist) · [LinkedIn](https://www.linkedin.com/in/gunnarnordqvist) · [books.geon.se](https://books.geon.se)  
**Live demo:** https://gunnarnordqvist.github.io/Hack/ · **Source:** https://github.com/gunnarnordqvist/Hack/tree/main/penpad-snomed

## Idea
The terminology decides, the model only suggests. The user types or dictates free text, or points at a body map. Candidate findings come from SNOMED CT ECL sets on a FHIR terminology server (HL7 Nordics `tx-nordics.fhir.org`), and the app asks only for the details a finding allows, for example side only when the body site is lateralizable. No code is ever invented by a model.

## What it does
- **Free text, Swedish or English.** Side, duration, severity, character, onset and progress are read from the text; the rest is matched to a finding.
- **Body map with close-ups** in the spirit of the original demo: front and back figure, hand, leg, back, and a cross-section of the head and neck (nose, mouth, teeth, tongue, throat, larynx; drawn for this project). The side you click becomes the patient's side.
- **Aspect of a site**, the body's counterpart of a tooth surface: anterior, posterior, medial, lateral, proximal, distal (SNOMED CT qualifier values).
- **Several findings, e.g. after a fall.** A list of findings, marked on the body. One sentence such as "ont i armen, handen och huvudet" / "pain in the left arm and right leg" becomes one proposal per body part, each with its own body part, side and values; every proposal must have its finding site inside its own body part (checked on the server), and nothing is added without a click.
- **Outputs from one selection or from the whole list:** a sentence (clinician or patient wording), a SNOMED CT expression, an openEHR COMPOSITION (following the mapping in the clinergy-extractor) and a FHIR Condition (a Bundle for a list). What a target cannot hold is listed as unmapped, not invented.

## Notes
- Runs in the browser; the public site holds no SNOMED CT content. Search words typed by a visitor go to the terminology server; a guard blocks text that looks like identity numbers, phone numbers or e-mail addresses.
- The body figure is from an MIT-licensed package (the origin of the original artwork could not be verified, see THIRD_PARTY_NOTICES.md); the head cross-section is our own drawing.
- Prototype for made-up examples only: never enter real patient data. 61 unit tests and 59 browser checks pass; an English audit finds no Swedish text. Honest status of the quality gates is in `docs/build-record.yaml` in the source.
- Limits: small self-written evaluation set (14 phrases), the guard is heuristic, body-part word lists are our own and unreviewed, a few ready-made SNOMED findings show an odd first site, no dental chart.
