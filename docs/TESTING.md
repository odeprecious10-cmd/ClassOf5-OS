# Testing

Every release runs the full automated suite before it reaches staging.

## The suite

| | |
|---|---|
| Suites | 66 |
| Checks | About 2,300 |
| Tools | Python, Playwright (headless Chromium), PHP built-in server, SQLite, a local mail catcher, stand-ins for the Stripe, Lessonspace and AI APIs |
| Run | One script resets a disposable copy of the site and database before each suite, so suites never depend on each other |

## What is covered

- **API behaviour:** every role allowed and refused the right actions; wrong passwords; refusals that must not count as failed logins.
- **Payments:** Stripe webhooks (paid, failed, cancelled, refunded), several children in one payment, billing held until the first lesson.
- **Time zones:** three timetables, the November 2026 clock changes, classes after midnight in a tutor's own time, the same tutor booked twice.
- **Privacy:** proof that children's and parents' names never appear in what is sent to the AI; contact details stripped from notes.
- **Real browsers** at phone and desktop widths: sign-up, portals, admin pages, no sideways scrolling, no script errors.
- **Whole-site crawl:** every page as a visitor, the owner and each manager, checking for script errors, failed requests, broken links, managers never landing in the owner's admin, and the right wording for each role.
- **Data safety:** backups include every table, migrations upgrade older databases, offboarding archives before removing.

## User acceptance testing

A written week-long test plan for the staging site covers each role (owner, both managers, a tutor, a parent) step by step, including scenarios such as "reset the package calculator to zero" and "a tutor is absent: arrange cover, then a make-up class".
