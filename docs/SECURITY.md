# Security & privacy design

The platform handles card payments (through Stripe) and children's data, so security and privacy were design rules from the first version, not add-ons. This page describes the approach at a high level; implementation details are deliberately not published.

## Access control

- **Separate credentials per role:** site administrator, Tutor manager, Enrolment manager; tutors and families have their own sign-ins (PINs, with one-time reset links that expire).
- **Server-side authorisation:** every API action is checked against a permission table for the caller's role. Hiding a button is only for comfort; the server refuses anything outside the role.
- **Least privilege:** managers never see pay or payment details. Only the owner can approve hours, change prices, touch keys, delete families or restore data.
- **Configuration checks:** manager passwords that are too short, reused, or the same as the owner's are switched off automatically and flagged in the Launch check.
- **Brute-force protection** on every sign-in, idle sign-out for managers, and "type DELETE to confirm" on destructive actions.
- **Audit trail:** every manager change is logged with time, role and what it was about; office notes record who wrote, edited or removed them.

## Secrets

- Keys and passwords live only in server-side config files that are never in a release package and never in version control.
- Payment card data never touches the platform: Stripe Checkout and Stripe's customer portal handle it.
- Webhooks from Stripe and Lessonspace are verified before anything is changed.

## Privacy

- **Children's names never reach the AI.** Names are replaced with codes before any call, emails and phone numbers are stripped, and the AI only writes drafts that a person approves.
- **Contact-detail filter:** phone numbers, emails, social handles and private-lesson offers typed into lesson notes are removed automatically and reported to the office.
- **Tutors** see only first names, homework and notes of the children they teach.
- **Families** see only their own children; each child's tile shows only that child's information.
- **Retention limits** on recordings, homework files and resumes (see [OPERATIONS.md](OPERATIONS.md)).
- Untrusted text from public forms is treated as data, never as instructions, when it is shown to the AI.
- No tracking or advertising cookies.

## Safeguarding features

- Lessons only inside the platform's classroom, with recordings kept for safety.
- A "Report a concern" flow for tutors and office staff that emails the office immediately.
- Social club sessions always with two adults, first names only, and recordings visible to the office only.
