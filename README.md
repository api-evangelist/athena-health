# athenahealth

athenahealth is a cloud-based electronic health record (EHR), revenue cycle management, and practice management platform serving ambulatory practices, hospitals, and health systems across the United States. The athenaOne platform spans patient engagement, scheduling, clinical documentation, ordering, e-prescribing, population health, and billing/claims. The company is privately held by Veritas Capital and Hellman & Friedman following the 2022 take-private acquisition.

This catalog entry captures athenahealth's developer surface — both the proprietary athenaOne REST API and the Cures Act-certified HL7 FHIR R4 server, plus the event, bulk, and clinical-decision-support APIs layered around them.

## APIs

| API | What it does |
|---|---|
| **athenaOne REST API** | Proprietary REST surface for the full provider, patient, scheduling, clinical, and biller workflow — Patients, Appointments, Encounters, Claims, Documents, Charts, Providers, Departments. |
| **FHIR R4 API** | ONC Cures Act-certified HL7 FHIR R4 server serving US Core / USCDI profiles. Patient, Encounter, Observation, Condition, MedicationRequest, AllergyIntolerance, DocumentReference, DiagnosticReport, Immunization, CarePlan, and more. |
| **FHIR Subscriptions API** | Near real-time event notifications via the athenahealth Event Subscription Platform, conforming to the FHIR R5 Backport STU 1.0.0 implementation guide. rest-hook channel, id-only payload. |
| **FHIR Bulk Data Access API** | Group-level `$export` ($export) operation per the FHIR Bulk Data Access (Flat FHIR) Export Implementation Guide. NDJSON output for population-scale data sharing and EHI export. |
| **CDS Hooks API** | Embedded clinical decision support at patient-view, order-select, order-sign, and appointment-book hook points inside the athenaOne provider experience. |

## Authentication

- OAuth 2.0 with `authorization_code` (SMART App Launch) and `client_credentials` (SMART Backend Services).
- Token endpoint: `https://api.platform.athenahealth.com/oauth2/v1/token`
- Authorization endpoint: `https://api.platform.athenahealth.com/oauth2/v1/authorize`
- Register applications and obtain credentials in the [athenahealth Developer Portal](https://mydata.athenahealth.com/access-the-apis).

## Environments

| Environment | Base URL |
|---|---|
| Preview FHIR R4 | `https://api.preview.platform.athenahealth.com/fhir/r4` |
| Production FHIR R4 | `https://api.platform.athenahealth.com/fhir/r4` |
| Preview athenaOne REST | `https://api.preview.platform.athenahealth.com/v1/{practiceid}` |
| Production athenaOne REST | `https://api.platform.athenahealth.com/v1/{practiceid}` |

## Artifacts

- [`apis.yml`](apis.yml) — APIs.json inventory of athenahealth's API surface.
- [`openapi/`](openapi) — OpenAPI 3.0 contracts for athenaOne REST, FHIR R4, FHIR Subscriptions, Bulk Data, and CDS Hooks.
- [`asyncapi/`](asyncapi) — AsyncAPI 3.0 contract for FHIR Subscriptions webhook delivery.
- [`capabilities/`](capabilities) — Naftiko capability definitions for Patients, Appointments, Encounters, Claims, Documents, Providers, FHIR resources, Subscriptions, Bulk Export, and CDS Hooks.
- [`json-schema/`](json-schema) — JSON Schemas for Patient, Appointment, and FHIR Patient.
- [`json-ld/`](json-ld) — JSON-LD context aligning athenahealth identifiers with `schema.org` and `hl7.org/fhir`.
- [`examples/`](examples) — Worked request/response examples.
- [`rules/`](rules) — Spectral ruleset enforcing athenahealth API conventions.
- [`vocabulary/`](vocabulary) — Operational and capability vocabulary.
- [`plans/`](plans) — Commercial plans (athenaOne contract, MDP partnership, Cures Act free access).
- [`rate-limits/`](rate-limits) — Throttling policies for REST, FHIR, Subscriptions, and Bulk Data.
- [`finops/`](finops) — FinOps surface aligned to the FOCUS data spec.

## Standards and Certification

- HL7 FHIR R4
- US Core / USCDI v3
- 21st Century Cures Act Information Blocking compliance
- ONC Health IT Certification
- SMART App Launch 2.0, SMART Backend Services
- CDS Hooks 1.0
- FHIR Subscriptions R5 Backport STU 1.0.0

## Open Source

- [`athenahealth/mdp`](https://github.com/athenahealth/mdp) — More Disruption Please API samples (Java).
- [`athenahealth/apiserver-athenaFlex`](https://github.com/athenahealth/apiserver-athenaFlex) — athenaPractice/athenaFlow FHIR API server samples.
- [`athenahealth/aone-fhir-subscriptions`](https://github.com/athenahealth/aone-fhir-subscriptions) — Sample webhook subscriber for the athenaOne FHIR Subscriptions framework.
- [`athenahealth/vscode-cql-extension`](https://github.com/athenahealth/vscode-cql-extension) — Clinical Quality Language syntax highlighting for VS Code.

## References

- [athenahealth homepage](https://www.athenahealth.com/)
- [APIs at athenahealth](https://docs.athenahealth.com/api/)
- [athenahealth Developer Portal](https://mydata.athenahealth.com/access-the-apis)
- [athenahealth Marketplace](https://www.athenahealth.com/solutions/marketplace)
- [Athena Core FHIR Implementation Guide](https://fhir.athena.io/athenacoreext/index.html)
