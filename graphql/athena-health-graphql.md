# Athenahealth GraphQL Schema

## Overview

This conceptual GraphQL schema models the athenahealth athenaOne REST API and FHIR R4 API surface. The athenaOne platform is a cloud-based EHR, revenue cycle management, and practice management system serving ambulatory practices, hospitals, and health systems across the United States.

- REST API base: `https://api.platform.athenahealth.com/v1/{practiceid}`
- FHIR R4 base: `https://api.platform.athenahealth.com/fhir/r4`
- Developer docs: https://docs.athenahealth.com/api/
- Authentication: OAuth 2.0 `client_credentials`; SMART on FHIR for FHIR endpoints

## Schema File

[athena-health-schema.graphql](athena-health-schema.graphql)

## Type Summary

The schema defines **68 named types** organized across the following domains:

### Practice & Provider (5 types)
| Type | Description |
|------|-------------|
| `Practice` | Top-level practice entity with departments, providers, and schedules |
| `PracticeDetails` | Extended practice attributes: NPI, EHR certification, FHIR URL |
| `Department` | Practice sub-unit with address, phone, place of service |
| `Provider` | Clinician with NPI, specialty, departments, and schedule |
| `ProviderDetails` | Licenses, DEA, Medicare/Medicaid IDs, board certifications |

### Patient (6 types)
| Type | Description |
|------|-------------|
| `Patient` | Core patient record with demographics, contacts, and clinical collections |
| `PatientDetails` | SSN, marital status, race, ethnicity, emergency contact, guarantor |
| `PatientDemographics` | USCDI-aligned demographics: race, ethnicity, language, gender identity |
| `PatientInsurance` | Coverage record linking patient to payer/plan with eligibility data |
| `PatientProvider` | Patient-to-provider relationship: primary care, specialty assignment |
| `Guarantor` | Financial guarantor for the patient account |

### Appointment (5 types)
| Type | Description |
|------|-------------|
| `Appointment` | Scheduled visit with status, datetime, provider, and department |
| `AppointmentDetails` | Reason for visit, referral, authorization, copay |
| `AppointmentType` | Template for visit duration, patient-facing flag, description |
| `AppointmentNotes` | Scheduling notes displayed on provider schedule |
| `OpenAppointmentSlot` | Available slot returned by open-scheduling search |

### Encounter (2 types)
| Type | Description |
|------|-------------|
| `Encounter` | Clinical visit record linking patient, provider, diagnoses, and chart |
| `EncounterDetails` | HPI, ROS, physical exam, assessment, plan, discharge instructions |

### Clinical — Diagnosis, Problem, Allergy (3 types)
| Type | Description |
|------|-------------|
| `Diagnosis` | ICD-10/SNOMED coded diagnosis attached to encounter |
| `Problem` | Active or resolved problem on the patient's problem list |
| `Allergy` | Allergen with reaction list, severity, SNOMED/RxNorm coding |

### Medications (3 types)
| Type | Description |
|------|-------------|
| `Prescription` | Electronic prescription with sig, quantity, refills, pharmacy |
| `MedicationOrder` | Clinical order for a medication with linked diagnoses |
| `PharmacyDetails` | NCPDP pharmacy record with address, NPI, type |

### Vitals (2 types)
| Type | Description |
|------|-------------|
| `VitalSet` | Timestamped collection of vital signs for a patient/encounter |
| `VitalDetails` | Individual vital measurement with type, value, unit, interpretation |

### Lab Orders & Results (5 types)
| Type | Description |
|------|-------------|
| `Lab` | Laboratory facility with NPI, address, contact |
| `LabOrder` | Clinical order for laboratory testing |
| `LabResult` | Result report returned by the lab |
| `LabAnalyte` | Individual analyte value with reference range and abnormal flag |
| `LabObservation` | LOINC-coded observation within a result |

### Documents & Charts (5 types)
| Type | Description |
|------|-------------|
| `Document` | Scanned or electronic document attached to the patient record |
| `DocumentDetails` | Subject, note, attachment type, size, MIME type |
| `DocumentType` | Document category and patient-facing classification |
| `Chart` | Longitudinal patient chart aggregating all clinical domains |
| `ChartDetails` | Summary metrics: last visit, active problems, care gaps |

### Clinical Summaries (4 types)
| Type | Description |
|------|-------------|
| `HealthSummary` | Patient-level aggregate: problems, medications, allergies, vitals, labs |
| `ClinicalSummary` | Encounter-level after-visit summary with patient instructions |
| `CCDA` | C-CDA document XML with section list, author, and custodian |
| `FHIR` | FHIR R4 resource wrapper with profile, meta, and raw JSON |

### Scheduling (2 types)
| Type | Description |
|------|-------------|
| `Schedule` | Provider/department schedule template |
| `Availability` | Real-time slot availability for a provider/department/date |

### Insurance & Billing (8 types)
| Type | Description |
|------|-------------|
| `InsurancePayer` | Insurance company with claim address and EDI payer ID |
| `InsurancePlan` | Specific plan under a payer |
| `Claim` | Professional billing claim with charges, payments, and diagnoses |
| `ClaimDetails` | Rendering/billing/referring provider, place of service, auth numbers |
| `Charge` | Individual CPT/HCPCS line on a claim |
| `ChargeDetail` | Revenue code, NDC, dental fields per charge line |
| `Payment` | Payment posting: check, EFT, or patient payment |
| `PaymentDetails` | EOB reference, adjustment codes, write-off details |

### EOB (2 types)
| Type | Description |
|------|-------------|
| `EOB` | Explanation of Benefits from payer with check and claim totals |
| `EOBLine` | Line-level EOB adjudication with CARC/RARC codes |

### Messaging & Portal (5 types)
| Type | Description |
|------|-------------|
| `Message` | Internal practice message |
| `PatientMessage` | Secure message exchanged with the patient via the portal |
| `MessageDetails` | Thread ID, category, tags |
| `Portal` | Patient portal account with access and notification preferences |
| `PortalDetails` | Feature flags: schedule, Rx request, bill pay, record download |

### Auth & Webhooks (3 types)
| Type | Description |
|------|-------------|
| `APIKey` | OAuth client credential key with scopes and environment |
| `Token` | OAuth 2.0 access token including SMART launch context |
| `Webhook` | FHIR Subscription rest-hook endpoint with event filter |

### Supporting Types
`Address`, `StateLicense`, `EmergencyContact`, `Immunization`, `PageInfo`, `PatientConnection`, `PatientEdge`, `AppointmentConnection`, `AppointmentEdge`, `EncounterConnection`, `EncounterEdge`, `ClaimConnection`, `ClaimEdge`

## Authentication

All queries and mutations require an `Authorization: Bearer <access_token>` header. Tokens are obtained via:

- **athenaOne REST API**: OAuth 2.0 `client_credentials` flow at the athenahealth authorization server
- **FHIR R4 API**: SMART on FHIR authorization (`launch`, `patient/*.read`, `user/*.write` scopes)

The `practiceid` path parameter scopes all athenaOne REST operations. FHIR requests use the same token but target `https://api.platform.athenahealth.com/fhir/r4`.

## Key Enumerations

- `AppointmentStatus` — `OPEN | BOOKED | CHECKED_IN | CHECKED_OUT | CANCELLED | RESCHEDULED | NO_SHOW | FUTURE | CHARGE_ENTERED`
- `ClaimStatus` — `OPEN | SUBMITTED | ACCEPTED | REJECTED | PAID | DENIED | VOIDED | CLOSED`
- `LabResultStatus` — `FINAL | PRELIMINARY | CORRECTED | CANCELLED | PENDING`
- `DocumentStatus` — `OPEN | CLOSED | DELETED | ERROR`
- `MessageStatus` — `OPEN | CLOSED | DRAFT | SENT`
- `WebhookStatus` — `ACTIVE | INACTIVE | ERROR`
- `Gender` — `MALE | FEMALE | OTHER | UNKNOWN`
- `FHIRResourceType` — Patient, Encounter, Observation, Condition, MedicationRequest, AllergyIntolerance, DocumentReference, DiagnosticReport, CarePlan, Goal, Immunization, Procedure

## References

- [athenaOne API Documentation](https://docs.athenahealth.com/api/docs/athenaone-apis)
- [FHIR R4 API Documentation](https://docs.athenahealth.com/api/docs/fhir-apis)
- [FHIR R4 API Reference](https://mydata.athenahealth.com/fhirapidoc/r4)
- [Athena Core FHIR Implementation Guide](https://fhir.athena.io/athenacoreext/index.html)
- [athenaOne FHIR Subscriptions](https://github.com/athenahealth/aone-fhir-subscriptions)
- [Developer Portal](https://mydata.athenahealth.com/access-the-apis)
- [Sandbox Environment](https://docs.athenahealth.com/api/sandbox)
