# Stage234: Real-Key Signing (Ed25519 + GPG)

This stage introduces real cryptographic signing keys on top of the existing
external signature verification framework (Stage233).

## Overview

Stage233 established a verifiable external signature structure.

Stage234 upgrades this by introducing:

- Ed25519 persistent signing keys
- GPG identity-based signatures
- Detached signature verification

This makes the system verifiable in real-world environments.

## What This Enables

- Tamper resistance at publication level
- Independent verification by third parties
- Meaningful GitHub distribution
- Researcher-grade auditability

## Signing Layers

### Ed25519

- Deterministic signing
- Fast verification
- Repository-level identity

Artifacts:

- `keys/public/stage234_ed25519_public.pem`
- `out/signatures/stage234_release_manifest.ed25519.sig.json`

### GPG

- Identity-based signing
- Compatible with GitHub / standard tooling
- Human-verifiable identity binding

Artifacts:

- `gpg_pubkeys/stage234_maintainer_public.asc`
- `out/signatures/stage234_release_manifest.json.asc`

## How to Run

```bash
./tools/run_stage234_real_keys.sh
Verification
Ed25519
python3 tools/verify_stage234_ed25519.py \
  --payload out/signatures/stage234_release_manifest.json \
  --signature out/signatures/stage234_release_manifest.ed25519.sig.json \
  --public-key keys/public/stage234_ed25519_public.pem
GPG
bash tools/verify_stage234_gpg_detached.sh \
  out/signatures/stage234_release_manifest.json \
  out/signatures/stage234_release_manifest.json.asc \
  gpg_pubkeys/stage234_maintainer_public.asc
Important Notes
Private keys are never committed
All verification is reproducible
No trust is assumed beyond published keys
Stage Progression
Stage233 → External signature verification structure
Stage234 → Real cryptographic identity and signing
Security Model

The system binds:

Claim
↓
Evidence
↓
Manifest
↓
Signature
↓
Verification

This creates a reproducible and auditable security pipeline.

License

MIT License

© 2025 Motohiro Suzuki