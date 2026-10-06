# Privacy

BankInsight is used by one person, its owner, for that person's own financial
accounts. There are no other end users.

## Data collected

The app collects only:
- Financial data the owner authorizes through Plaid Link: account type, mask,
  balances, transactions, holdings, securities, investment activity and tax lots.
- Statements the owner imports manually.

The app never collects institution usernames, passwords, MFA codes or session
cookies. Authentication happens only on the institution's own page.

## Where data lives

- All data stays on the owner's computer, in a local SQLite database on an
  encrypted disk.
- Plaid access tokens are stored in macOS Keychain.
- There is no BankInsight server, cloud database or analytics service.
- Data is not sold, shared, or used for advertising or model training.
- Any optional AI assistant runs locally on the same machine.

## Data from Plaid

- Only the fields needed for analysis are kept. Plaid responses are reduced to
  an allowlist of fields before storage. Location details and the full HTTP
  traffic are not retained.
- Data is used only to produce the owner's own reports.

## Retention and deletion

The owner can disconnect an institution at any time. Disconnecting revokes the
Plaid Item and removes its token from Keychain. Locally stored history can be
deleted by removing the local database and its backups.

Plaid's own handling of data is described in the
[Plaid End User Privacy Policy](https://plaid.com/legal/#end-user-privacy-policy).
