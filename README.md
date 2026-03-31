<div align="center">

# radrootsd

_a Radroots bridge and write-plane daemon with optional NIP-46 JSON-RPC control_

<p align="center"><a href="https://opensource.org/license/agpl-v3"><img src="https://img.shields.io/badge/license-AGPLv3-blue.svg"></a></p>

</div>

## Overview

radrootsd is the Radroots bridge and write-plane daemon. It exposes authenticated JSON-RPC ingress for canonical Radroots event publishing, including listing publication and listing-backed order requests, and it can optionally expose public `nip46.*` JSON-RPC control when that surface is explicitly enabled. Relay-backed NIP-46 listener behavior remains available for Nostr-native flows.

Bridge jobs and idempotency records persist at `config.bridge.state_path`. Bridge publish methods default to the embedded service identity signer, but they can also target an already-connected outbound NIP-46 session by passing `signer_session_id`.

## Bridge Job Lifecycle

Bridge write commands expose one durable lifecycle:

- `accepted`: the request has been reserved and is still in-flight in the current process. This state is non-terminal.
- `published`: terminal success. The event was signed and the configured delivery policy was satisfied.
- `failed`: terminal failure. This includes post-reservation contract/signing failures, relay publish failures, and restart recovery of interrupted accepted jobs.

Bridge APIs now expose a stable lifecycle view:

- `terminal`: whether the job is terminal
- `recovered_after_restart`: whether a failed job was terminalized during startup recovery because the previous process died before completion

`bridge.status` reports retained job counts by lifecycle state, including `recovered_failed_jobs`. It also reports bridge signer capability truthfully:

- `signer_mode`: `selectable_per_request`
- `default_signer_mode`: `embedded_service_identity`
- `supported_signer_modes`: `["embedded_service_identity", "nip46_session"]`
- `available_nip46_signer_sessions`: current count of outbound remote-signer sessions the bridge could target immediately

`bridge.job.status` and bridge publish responses return the same stable job view, so clients do not need to infer lifecycle semantics from raw store internals.

Accepted jobs are not resumable across restart. If radrootsd restarts before publish completion, startup recovery converts those jobs into terminal `failed` records with the summary `bridge publish did not complete before process restart`.

## Local identity

`identity.json` is local-only secret material and is intentionally not tracked.
Use `identity.example.json` as the template for your local identity file.

## Validation

This repository uses Nix as the canonical local validation surface:

```bash
nix run .#fmt
nix run .#check
nix run .#test
```

Enter the repo shell when you need narrower ad hoc cargo commands:

```bash
nix develop
```

## Coverage

Coverage policy and thresholds are defined in:
- `contract/coverage/POLICY.md`
- `contract/coverage/thresholds.toml`
- `contract/coverage/include.txt`

Run a coverage report:
```bash
make coverage-report
```

Run the strict gate:
```bash
make coverage-gate
```

## License

This code is released under a copyleft open-source license.
