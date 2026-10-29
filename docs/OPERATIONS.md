# Operations

How the platform is released, run and recovered.

## Environments

| | Staging | Production |
|---|---|---|
| Domain | classof5.online | classof5.com |
| Access | Password-protected, "do not index", a visible TEST banner | Public site; admin and portals behind their own sign-ins |
| Data | Test families, tutors and payments; can be reset with "Start fresh" (blocked on production) | Real data |
| Payments | Stripe test mode | Stripe live mode |

## Release process

1. Change is specified (the business rule first, in plain words).
2. Pushed to the private repository; **CI** runs the automated suite on a clean runner.
3. A green build is **deployed to staging automatically**; user-acceptance checks there.
4. **Production by approval**, only for commits whose tests passed, with a backup first and a health check after. Server-only configuration (database, payments, keys, site settings) is never deployed.

More than 100 releases followed this path in October 2026; the milestones are in [CHANGELOG.md](../CHANGELOG.md).

## Built-in operational tooling

- **Launch check:** a green, amber and red page that checks the settings that often go wrong (Stripe mode and keys, prices matching everywhere, scheduled jobs running, term dates, team logins, AI key).
- **Daily summary email:** money in, sign-ups, payment problems, cancellations, families waiting, children waiting for a seat, missing lesson notes, tutors late or missing, system health.
- **Real-time alerts:** one email if a tutor hasn't joined 10 minutes after the start, with the cover options.
- **Team activity:** every change by a manager, by day, with filters; repeated jobs counted; prunable by the owner.

## Monitoring

- **Hourly uptime checks** (GitHub Actions, 7 am to midnight Toronto time): the key pages, a health check for the database, the scheduled jobs and the daily backup, the staging site, and SSL certificate expiry.
- **Privacy-safe health check:** the site answers only yes/no facts (database answering, jobs ran recently, backup made), never names, money or settings.
- **One alert per incident:** a problem opens a tracked issue and emails the office; when the next check passes it closes itself and sends a "back to normal" email. No repeat emails while a problem is open, and a page is only counted as down after three failed tries.
- Built to run on the free GitHub Actions allowance alongside CI and deployments.

## Backups and recovery

- Daily database backup of every table, kept 30 days.
- Automatic backup before any bulk reset, and a one-click download.
- Offboarding a family writes an archive of their records before anything is removed.
- Restore of the enrolment register from a backup (owner only).
- Next step: copy backups off the server to cloud storage (see [CLOUD-ROADMAP.md](CLOUD-ROADMAP.md)).
