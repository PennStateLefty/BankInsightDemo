# BankInsight

A **personal, single-household, local-first** finance tool. It runs on one
person's own Mac and analyzes that person's own accounts. It is not a hosted
service, has no other users, and offers no accounts to the public.

The application source is kept in a private repository. This public repository
describes the project, how it uses financial data, and its security posture.

## What it does

- Imports historical bank, card and brokerage statements (CSV) after a
  row-by-row preview and confirmation.
- Optionally syncs the owner's own accounts **read-only** through
  [Plaid](https://plaid.com):
  - **Transactions** for checking, savings and credit cards.
  - **Investments** for holdings, securities, investment activity and
    broker-reported tax lots.
- Classifies spending and income, links transfers between accounts, and keeps
  the original institution categories next to the local ones.
- Answers planning questions from that local ledger, such as monthly cash flow,
  net worth on a common date, and car-affordability scenarios with every
  assumption stated.

It does **not** move money, make payments, place trades, give investment advice,
or prepare taxes. Only the Plaid Transactions and Investments products are used.
Auth, Identity, Transfer and payment products are not requested.

## How it works

| Layer | Choice |
| --- | --- |
| Backend | Python, FastAPI, bound to `127.0.0.1` only |
| Storage | SQLite on the owner's encrypted disk |
| Frontend | React and TypeScript, served by the local backend |
| Secrets | macOS Keychain; never written to the database, logs or files |
| Bank connection | Plaid Link, opened from a separate one-time local page |

Sync follows a fixed sequence:

1. The owner approves each institution before connecting it.
2. The owner signs in only on the institution's own page through Plaid Link.
   The app never sees or stores bank usernames, passwords or MFA codes.
3. The app fetches every page of updates first, then saves them in a single
   database transaction together with the sync cursor. A failed or interrupted
   sync leaves the previous data unchanged.
4. Each record is stored with its provider ID, version history and removal
   markers, so replaying a sync never creates duplicates.
5. Synced rows that overlap earlier manual imports are held for the owner to
   review, so they are never counted twice.
6. Disconnecting revokes access at Plaid and removes the stored token.

## Status

This is a personal project under active development. It is not offered to
anyone else, and there is no sign-up.

See [PRIVACY.md](PRIVACY.md) and [SECURITY.md](SECURITY.md).
