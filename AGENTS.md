# radrootsd - code directives

- this repo is a standalone OSS daemon and must remain cloneable and usable from this repo root
- do not treat the outer workspace as the authoritative runtime or release root for this repo
- during the current integrated development phase, temporary local path dependencies are allowed only to the public `radroots` crate family and approved developer-controlled vendor repos
- do not add temporary local path dependencies from this repo to archived code, `refs/*`, or private platform crates without explicit approval
- read `README.md` and `docs/nix.md` before broad edits
- validate from this repo root with `nix run .#check` and `nix run .#test`
- use the existing coverage commands when coverage-affecting or release-affecting work needs them
- use raw cargo commands only for narrower follow-up work after entering `nix develop`
- toolchain: Rust 1.92, edition 2024
- avoid `unsafe`
