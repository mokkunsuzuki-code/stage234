（# Stage235: GitHub Verified Commit (GPG Identity Binding)

This stage binds local GPG signing keys to a GitHub account,
enabling "Verified" commit status on GitHub.

## Overview

Stage234 introduced real cryptographic signing using:

- Ed25519 keys (repository-level identity)
- GPG keys (identity-based signing)

Stage235 extends this by:

- Linking GPG public key to GitHub account
- Enabling GitHub-side signature verification
- Making commit authorship visibly verifiable

## What This Enables

- GitHub "Verified" badge on commits
- Stronger authorship authenticity
- Public auditability of commit origin
- Alignment with real-world developer identity

## Verification Flow

Local commit (signed with private key)
↓
GitHub receives commit
↓
GitHub matches public key
↓
**Verified badge displayed**

## Requirements

- GPG key pair (created locally)
- Public key registered on GitHub
- Git configured to use signing key
- Verified email address on GitHub

## Setup (Local)

### 1. Check GPG key

```bash
gpg --list-secret-keys --keyid-format=long
2. Set signing key
git config --global user.signingkey <KEY_ID>
git config --global commit.gpgsign true
3. Ensure GPG agent works
export GPG_TTY=$(tty)
Export Public Key
gpg --armor --export <KEY_ID> > gpg_pubkeys/stage235_github_public.asc

👉 このファイルを GitHub に登録

GitHub:
Settings → SSH and GPG keys → New GPG key

Test Signed Commit
git commit -S -m "Stage235: signed commit"
git push
Expected Result

GitHub上で👇

👉 Verified 表示

Important Notes
Verified = GitHubが署名を検証した状態
完全な身元保証ではないが、強い本人性証明
秘密鍵は絶対に公開しない
Stage Progression

Stage234 → Cryptographic signing (Ed25519 + GPG)
Stage235 → GitHub identity verification (Verified commits)

Security Model Extension

The system now binds:

Claim
↓
Evidence
↓
Manifest
↓
Signature
↓
GitHub Identity Verification

This connects cryptographic proof with platform-level identity.

License

MIT License

© 2025 Motohiro Suzuki）
