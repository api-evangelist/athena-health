# athenahealth (athena-health)

athenahealth is a cloud-based electronic health record (EHR), revenue cycle management, and practice management platform serving ambulatory practices, hospitals, and health systems across the United States. The athenaOne platform spans patient engagement, scheduling, clinical documentation, ordering, e-prescribing, population health, and billing/claims. The athenahealth API surface exposes both a proprietary REST API and a Cures Act-certified FHIR R4 server with US Core / USCDI conformance, FHIR Subscriptions for event-driven webhooks, FHIR Bulk Data ($export) for population-scale data sharing, and CDS Hooks for embedded clinical decision support. The company is privately held by Veritas Capital and Hellman & Friedman following the 2022 take-private acquisition.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/athena-health/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/athena-health/refs/heads/main/apis.yml)

## Scope

- **Access:** 3rd-Party

## Tags

- EHR
- Electronic Health Records
- Healthcare
- HL7
- FHIR
- Interoperability
- Practice Management
- Revenue Cycle Management
- USCDI
- Cures Act
- SMART on FHIR
- CDS Hooks
- Cloud EHR

## APIs

### athenahealth athenaOne REST API

The athenaOne proprietary REST API exposes the complete provider, patient, and biller workflow surface of athenahealth's cloud-based EHR and practice management platform. Resources include Patients, Appointments, Encounters, Claims, Documents, Charts, Providers, Departments, Insurance, Orders, and Billing. Authenticated via OAuth 2.0 client_credentials at the athenahealth Developer Portal; scoped per practice via the practiceid path parameter.

- **Human URL:** [https://docs.athenahealth.com/api/docs/athenaone-apis](https://docs.athenahealth.com/api/docs/athenaone-apis)
- **Base URL:** `https://api.platform.athenahealth.com/v1/{practiceid}`

#### Tags

- EHR
- Healthcare
- Practice Management
- Patients
- Appointments
- Encounters
- Claims
- Documents
- Providers

#### Properties

- [Documentation](https://docs.athenahealth.com/api/docs/athenaone-apis)
- [Documentation](https://docs.athenahealth.com/api/api-ref/patient)
- [Documentation](https://docs.athenahealth.com/api/api-ref/appointment)
- [Documentation](https://docs.athenahealth.com/api/docs/encounter)
- [OpenAPI](openapi/athenahealth-athenaone-rest-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/athenahealth-athenaone-rest-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/athenahealth-athenaone-rest-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [JSON Schema](json-schema/athenahealth-patient-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/athenahealth-appointment-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON-LD](json-ld/athena-health-context.jsonld) — [JSON-LD](https://www.w3.org/TR/json-ld11/)

### athenahealth FHIR R4 API

The athenahealth FHIR R4 server is certified to the ONC Cures Act Final Rule and serves US Core and USCDI profiles. Preview base URL https://api.preview.platform.athenahealth.com/fhir/r4 and production base URL https://api.platform.athenahealth.com/fhir/r4. Supports Patient, Encounter, Observation, Condition, MedicationRequest, AllergyIntolerance, DocumentReference, DiagnosticReport, CarePlan, Goal, Immunization, and other US Core profiles. Authenticated via SMART on FHIR with the same OAuth 2.0 authorization server as the proprietary athenaOne API.

- **Human URL:** [https://docs.athenahealth.com/api/docs/fhir-apis](https://docs.athenahealth.com/api/docs/fhir-apis)
- **Base URL:** `https://api.platform.athenahealth.com/fhir/r4`

#### Tags

- EHR
- FHIR
- Healthcare
- HL7
- USCDI
- US Core
- Interoperability

#### Properties

- [Documentation](https://docs.athenahealth.com/api/docs/fhir-apis)
- [Documentation](https://docs.athenahealth.com/api/guides/base-fhir-urls)
- [Documentation](https://mydata.athenahealth.com/fhirapidoc/r4)
- [Documentation](https://fhir.athena.io/athenacoreext/index.html)
- [OpenAPI](openapi/athenahealth-fhir-r4-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/athenahealth-fhir-r4-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/athenahealth-fhir-r4-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [JSON Schema](json-schema/athenahealth-fhir-patient-schema.json) — [JSON Schema](https://json-schema.org/specification)

### athenahealth FHIR Subscriptions API

The athenahealth Event Subscription Platform delivers near real-time healthcare-domain event notifications via FHIR Subscriptions. Conforms to FHIR Subscriptions R5 Backport STU 1.0.0 implementation guide. Currently supports the rest-hook channel and id-only payload type. Webhook endpoints must respond with 2xx within a 2 second timeout. Use this API to react to creates and updates on Patients, Appointments, Encounters, Observations, Conditions, and other clinical resources without polling.

- **Human URL:** [https://github.com/athenahealth/aone-fhir-subscriptions](https://github.com/athenahealth/aone-fhir-subscriptions)
- **Base URL:** `https://api.platform.athenahealth.com/fhir/r4`

#### Tags

- EHR
- Events
- FHIR
- Healthcare
- Subscriptions
- Webhooks

#### Properties

- [Documentation](https://github.com/athenahealth/aone-fhir-subscriptions)
- [OpenAPI](openapi/athenahealth-fhir-subscriptions-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/athenahealth-fhir-subscriptions-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/athenahealth-fhir-subscriptions-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [AsyncAPI](asyncapi/athenahealth-fhir-subscriptions-asyncapi.yml) — [AsyncAPI Specification](https://www.asyncapi.com/docs/reference/specification/latest)

### athenahealth FHIR Bulk Data Access API

FHIR Bulk Data Access ($export) for athenahealth — Group-level export operation that returns NDJSON files containing FHIR resources for all patients in a specified Group. Implements the FHIR Bulk Data Access (Flat FHIR) Export Implementation Guide and the FHIR Asynchronous Request Pattern. Required for 21st Century Cures Act compliance and is used for population-health analytics and EHI export workflows.

- **Human URL:** [https://docs.athenahealth.com/api/resources/227-release-added-fhir-bulk-data-access-capability-support-21st-century-cures](https://docs.athenahealth.com/api/resources/227-release-added-fhir-bulk-data-access-capability-support-21st-century-cures)
- **Base URL:** `https://api.platform.athenahealth.com/fhir/r4`

#### Tags

- Bulk Data
- EHR
- FHIR
- Healthcare
- Interoperability
- USCDI

#### Properties

- [Documentation](https://docs.athenahealth.com/api/resources/227-release-added-fhir-bulk-data-access-capability-support-21st-century-cures)
- [Documentation](https://docs.mydata.athenahealth.com/fhir-r4/ehiexport.html)
- [OpenAPI](openapi/athenahealth-fhir-bulk-data-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/athenahealth-fhir-bulk-data-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/athenahealth-fhir-bulk-data-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### athenahealth CDS Hooks API

CDS Hooks integration for athenaOne — invoke remote clinical decision support services at well-defined points in the EHR workflow (patient-view, order-select, order-sign, appointment-book). Returns Cards (suggestion, action, link) and optional SMART App Launch links to display real-time guidance inside the athenaOne provider experience.

- **Human URL:** [https://docs.athenahealth.com/downloads/athenaone-cds-hooks-integration-guide](https://docs.athenahealth.com/downloads/athenaone-cds-hooks-integration-guide)

#### Tags

- CDS Hooks
- Clinical Decision Support
- EHR
- FHIR
- Healthcare

#### Properties

- [Documentation](https://docs.athenahealth.com/downloads/athenaone-cds-hooks-integration-guide)
- [OpenAPI](openapi/athenahealth-cds-hooks-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/athenahealth-cds-hooks-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/athenahealth-cds-hooks-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [LinkedIn](https://www.linkedin.com/company/athenahealth)
- [Portal](https://www.athenahealth.com/)
- [Documentation](https://docs.athenahealth.com/api/)
- [Documentation](https://docs.athenahealth.com/api/guides/overview)
- [Portal](https://mydata.athenahealth.com/access-the-apis)
- [Sandbox](https://docs.athenahealth.com/api/sandbox)
- [Documentation](https://docs.athenahealth.com/api/guides/athenaone-environments)
- [Documentation](https://docs.athenahealth.com/api/guides/base-fhir-urls)
- [Documentation](https://docs.athenahealth.com/api/guides/onboarding-overview)
- [Support](https://docs.athenahealth.com/api/support)
- [Marketplace](https://www.athenahealth.com/solutions/marketplace)
- [Blog](https://www.athenahealth.com/knowledge-hub)
- [Source](https://github.com/athenahealth)
- [Documentation](https://fhir.athena.io/athenacoreext/index.html)
- [Documentation](https://mydata.athenahealth.com/fhirapidoc/r4)
- [Plans](plans/athena-health-plans-pricing.yml)
- [Rate Limits](rate-limits/athena-health-rate-limits.yml)
- [Fin Ops](finops/athena-health-finops.yml)
- [Vocabulary](vocabulary/athena-health-vocabulary.yml)
- [Spectral Rules](rules/athena-health-rules.yml) — [Spectral](https://docs.stoplight.io/docs/spectral)
- [Samples](https://github.com/athenahealth/mdp)
- [Samples](https://github.com/athenahealth/apiserver-athenaFlex)
- [Samples](https://github.com/athenahealth/aone-fhir-subscriptions)
- [Tools](https://github.com/athenahealth/vscode-cql-extension)
- [SDK](https://github.com/eleanorhealth/go-athenahealth)
