# Threat model

## What this project does and where untrusted input enters
A personal-finance app (monorepo: Node/TypeScript server, web UI, and shared libraries).
Untrusted input: bank statement imports (CSV/OFX/MT940/...), user-entered transaction data,
API tokens, and uploaded files. Statement parsers are the main untrusted-input surface.

## Components that matter most / least
- most: the bank-statement import/parsing code and the HTTP API layer.
- less: the UI, documentation.

## How to exercise it
Feed crafted statement files (each supported format) through the import path; exercise the API
with malformed requests.

## How you rate severity
- RCE or auth bypass: critical. SQL injection in import queries: high.
- path traversal in file handling: high.
- DoS via a crafted statement: medium.

## Anything to leave alone
- The mobile/desktop wrappers are thin; focus on the shared server code.
