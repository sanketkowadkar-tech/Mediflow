# MediFlow Hospital Operations Simulator

A multi-tab, synthetic-data hospital dispatch simulator. Open `dist/index.html` using a local static web server. No installation or external API keys are required. Run `node engine.test.cjs` for the scheduling tests.

## Views

Overview, Triage Queue, Resources, Token Desk, Turnover, Analytics, Security & Audit, Project Blueprint, Patient Registration.

## Working functionality

- Critical-first urgency/age scoring, explainable allocation and routine reassessment flags
- Atomic doctor/nurse/bed/equipment capacity checks and configurable 15–20% emergency reserve
- Separate minor-care lane; actual routing share depends on eligible cases
- Individual doctor rolling-three histories and parallel-lane ETA projection
- Shared patient/token model, consent, masked synthetic destinations and rate-limited message previews
- Lab → discharge → cleaning → available bed lifecycle
- Matched FIFO comparison from a cloned cohort; no fabricated performance improvement
- Demonstration roles, five-minute idle locking, reason-required overrides and session audit exports
- Session-only demonstration intake with phone, age, optional height/weight and fictional medical history
- New registrations wait for staff reassessment before dispatch
- Manual WhatsApp click-to-chat with recipient confirmation and consent; staff must press Send
- No browser persistence, medical-data server or automatic external messaging

## Important limitations

This is not a clinical system, autonomous triage tool, secure login service or certified medical product. Roles are selectable in-browser, checks are client-side, audit records are mutable, and no SMS is sent. Use fictional health details and your own or an explicitly consenting test recipient's number. Clicking Open WhatsApp shares that number and generic token message with WhatsApp. Send is manual and delivery is unverified. Intake is held in tab memory only, excluded from reports and audits, and removed on reload/reset or individual deletion. Emergency priority cannot create unavailable resources; aging cannot guarantee bounded waiting under sustained overload. ETAs may be lower bounds when resource constraints bind.

## Registration and notification demo

Choose **Patient** in **Choose a demonstration role**, then **Enter demo**. Patient Registration opens immediately with a visible **Demo Mode** badge. Submit the form to receive a token and view its status below. Staff tools and other patients' registration cards are hidden in this view. All patient-role entries in this tab belong to one demonstration persona; this is not authenticated patient isolation.

Use **Change demonstration role** to switch to a staff role for reassessment, dispatch and manual WhatsApp sending. The existing folder layout is unchanged.

Choose Administrator or Reception, then Patient Registration. Complete required demo name, age, international-format phone and reason for visit. Optional fields include measurements, onset, allergies, medicines, conditions and emergency contact. Acknowledge demo-only use; separately select WhatsApp consent. Submit to issue a token. A Triage nurse, Doctor or Administrator must reassess that token with a reason before dispatch. In Token Desk select the token, review WhatsApp, confirm the recipient, open WhatsApp and manually press Send. No automatic messaging provider is connected.

See `docs/GITHUB_SETUP.md` for GitHub upload instructions. Run `node engine.test.cjs` and `node ui-smoke.test.cjs` from the repository root.

The comparator is a controlled snapshot experiment, not a calibrated hospital outcome study. It uses the same input cohort, resources, treatment durations, reserve and automatic turnover in both arms. Current patients are reset to waiting for the experiment. Results are retained until rerun.

## Production roadmap

Managed authentication/MFA; server authorization; transactional PostgreSQL resource locking; FastAPI or equivalent backend; encrypted storage and recovery; external tamper-evident audits; input validation and API abuse protection; approved SMS consent/delivery integration; retention and breach procedures; HL7 FHIR interoperability; legal and clinical validation.

Do not commit secrets, medical records or real phone numbers to GitHub. No HIPAA or DPDP compliance is asserted.
