# Security

- **Local only.** The server listens on `127.0.0.1` and requires a per-session
  token that is held only in the browser tab's memory. It must not be exposed
  through a proxy or tunnel.
- **Secrets.** Plaid client credentials and access tokens are kept only in
  macOS Keychain and are never logged, printed or committed.
- **Least privilege.** Access is read-only, limited to the Transactions and
  Investments products, and each new connection requires an explicit approval
  from the owner. There are no money-movement or trading capabilities.
- **Isolated Link page.** Plaid Link runs on a separate one-time local page with
  its own content security policy, so it never loads alongside financial
  reports.
- **Integrity.** Syncs save atomically, version every record, and keep
  questionable records out of totals instead of guessing.
- **At rest.** Data is protected by the operating system's full-disk encryption.
  Backups are expected to be stored on encrypted media.

To report a concern, open an issue in this repository. Do not include account
data in the issue.
