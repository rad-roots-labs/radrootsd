<div align="center">

# radrootsd

_a Radroots daemon for NIP-46 signing and JSON-RPC transport_

<p align="center"><a href="https://opensource.org/license/agpl-v3"><img src="https://img.shields.io/badge/license-AGPLv3-blue.svg"></a></p>

</div>

## Overview

radrootsd is a Nostr NIP-46 signing daemon that exposes JSON-RPC and relay-backed transport for Radroots clients.

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
