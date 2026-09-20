# MediFlow GitHub upload guide

Upload the extracted project files, not only the ZIP or Word document. The document explains the project; the files in `dist/` run it.

## Repository details

- Suggested repository name: Mediflow
- Description: Hospital resource and queue simulator with urgency-aware dispatch, patient intake, dynamic wait estimates, manual WhatsApp notifications and security demonstrations.
- Visibility: choose Public only if competition rules permit and the files contain no secrets or real patient data.

## Exact destinations

| File | Repository destination |
| --- | --- |
| README.md | Root of Mediflow |
| dist/index.html | dist/index.html |
| dist/engine.js | dist/engine.js |
| dist/upgrade.js | dist/upgrade.js |
| dist/upgrade.css | dist/upgrade.css |
| dist/registration.js | dist/registration.js |
| engine.test.cjs and ui-smoke.test.cjs | Root of Mediflow |
| GITHUB_SETUP.md | docs/GITHUB_SETUP.md |
| Downloaded Word guide, optional | docs/MediFlow_GitHub_Guide.docx |

Keep all five web files together in `dist/`. Do not paste JavaScript into the README. The ZIP intentionally excludes site-hosting metadata and Git credentials.

## Upload through GitHub

1. Download and extract MediFlow_GitHub_Source.zip on your computer.
2. Open your Mediflow repository. If it does not exist, create it first.
3. Select Add file then Upload files. In an empty repository, use the uploading an existing file link if shown.
4. Drag the extracted files and folders into the upload area, preserving `dist/` and `docs/`. Do not upload the enclosing ZIP as the only file.
5. Review file paths and existing-file differences. Keep unrelated work. Use a new branch and pull request if the repository already has code or protects its main branch.
6. Enter a meaningful commit message, such as Add patient registration and manual WhatsApp flow, and commit or propose the changes.
7. Open dist/index.html in the repository to confirm it exists. The GitHub file viewer displays source; uploading files alone does not publish a running website.

Official instructions: https://docs.github.com/en/repositories/working-with-files/managing-files/adding-a-file-to-a-repository

## Run and test

Use a local static web server with its document root set to `dist/`. No npm dependencies are needed for this version. With Node installed, run `node engine.test.cjs` and `node ui-smoke.test.cjs` from the repository root. The second test uses a mock DOM, not browser visual testing.

For a static hosting service, choose `dist` as the publish directory. This guide does not configure GitHub Pages or change your domain. The existing hosted MediFlow link is separate from your GitHub repository.

## New registration workflow

For patient self-registration, choose Patient in the demonstration role selector, then Enter demo. Patient Registration opens automatically and the Demo Mode badge remains visible. Register to receive a token; its status appears below the form. Patient mode does not expose staff dispatch controls. To demonstrate the hospital workflow, use Change demonstration role and select an authorized staff role. All patient-role entries share a single local demo persona, not separate authenticated accounts.

Enter as Administrator or Reception. Open Registration, enter fictional identity and health details, use your own test phone number with country code, and choose notification consent separately. Submit to issue a token. Triage staff then reassess urgency with a reason in Triage Queue. No health answer automatically determines urgency.

In Token Desk, select that token and choose Review WhatsApp message. Check the displayed full recipient number and generic message, confirm consent, then choose Open WhatsApp. Press Send within WhatsApp. MediFlow cannot confirm sending or delivery. No symptoms, weight, allergies or clinical details are placed in the message.

## Security limits and next steps

Intake is stored only in the current tab, never in browser local storage or a medical database. Reload/reset clears it; Delete intake details removes the individual contact and history while retaining an anonymous simulation token. Locking hides dialogs but does not encrypt memory. Roles and checks remain client-side demonstrations.

Do not upload patient records, contact lists, API keys, passwords, .env files or account tokens to GitHub. Before real hospital use, implement server authentication/MFA, authorization, transactional allocation, encrypted storage, retention controls, external audits and clinical/privacy review. Automatic messaging additionally needs a server-side approved messaging provider; never embed provider secrets in these JavaScript files.
