<div align="center">

# radrootsd

_a Radroots bridge and write-plane daemon with optional NIP-46 JSON-RPC control_

<p align="center"><a href="https://opensource.org/license/agpl-v3"><img src="https://img.shields.io/badge/license-AGPLv3-blue.svg"></a></p>

</div>

## Overview

radrootsd is the Radroots bridge and write-plane daemon. It exposes authenticated JSON-RPC ingress for canonical Radroots event publishing, including listing publication and listing-backed order requests, and it can optionally expose public `nip46.*` JSON-RPC control when that surface is explicitly enabled. Relay-backed NIP-46 listener behavior remains available for Nostr-native flows.

## Local identity

`identity.json` is local-only secret material and is intentionally not tracked.
Use `identity.example.json` as the template for your local identity file.

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
