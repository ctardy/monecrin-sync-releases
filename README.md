<p align="center">
  <img src="logo.png" alt="Mon Écrin" width="128">
</p>

<h1 align="center">Mon Écrin — Desktop Releases</h1>

<p align="center">
  Signed installer releases for the <b>Mon Écrin</b> desktop client.<br>
  <a href="https://monecrin.com">monecrin.com</a>
</p>

<p align="center">
  <a href="../../releases/latest"><img src="https://img.shields.io/github/v/release/ctardy/monecrin-sync-releases?label=latest%20release" alt="Latest release"></a>
  <a href="../../releases"><img src="https://img.shields.io/github/downloads/ctardy/monecrin-sync-releases/total" alt="Downloads"></a>
  <img src="https://img.shields.io/badge/platform-Windows-0078D6" alt="Platform: Windows">
  <img src="https://img.shields.io/badge/macOS-planned-lightgrey" alt="macOS: planned">
  <img src="https://img.shields.io/badge/license-Proprietary-lightgrey" alt="License: Proprietary">
</p>

---

## What is Mon Écrin?

**Mon Écrin** is a sovereign, French-hosted cloud storage service for your photos, videos and
documents — encrypted at rest and in transit, with automatic backup from every device. Think of it
as a privacy-first alternative to the usual cloud photo services, with your data hosted exclusively
in France (OVH, Gravelines/Paris).

Mon Écrin is available on:

- **Android** — automatic camera-roll backup, on-device AI (face/scene recognition, nothing sent to
  a server)
- **Web** — browse and manage your vault at [monecrin.com](https://monecrin.com)
- **Desktop** (this release channel) — a two-way sync client for Windows (and soon macOS), backing up
  and restoring folders between your computer and your vault, similar to Dropbox or Google Drive

Learn more, see pricing, or create an account at **[monecrin.com](https://monecrin.com)**.

## About this repository

This repository **mirrors signed release artifacts only** — it contains **no source code**. The
desktop client is closed-source, developed in a separate private repository. This repo exists purely
as a public, auditable distribution channel: the in-app auto-updater and manual downloads both read
from here, and the verification steps below let anyone confirm that a downloaded installer is exactly
what was published, without having to trust this hosting channel itself.

## Download

Grab the latest installer from **[Releases](../../releases/latest)**:

| File | Description |
|---|---|
| `monecrin-sync-setup-<version>.exe` | Windows installer (per-user, no admin rights required) |
| `SHA256SUMS.txt` | SHA-256 checksum of the installer |
| `SHA256SUMS.txt.sig` | Ed25519 signature of `SHA256SUMS.txt` (raw, 64 bytes) |

The installer itself is also Authenticode-signed (Azure Trusted Signing, publisher **UIT Guard**), so
Windows SmartScreen should show a verified publisher rather than an "unknown publisher" warning.

## Verifying a download

Two independent signatures protect every release:

1. **Authenticode** (Windows SmartScreen trust) — verified automatically by Windows at install time.
2. **Ed25519** over `SHA256SUMS.txt` — this is what the app itself checks before ever accepting an
   automatic update. A release cannot be forged or downgraded by anyone who doesn't hold the offline
   private key, including us, if this GitHub account were ever compromised: the app's embedded public
   key is the actual root of trust, not this repository's authenticity.

To verify manually on Windows (PowerShell):

```powershell
# Check the installer's hash matches the one listed in SHA256SUMS.txt
CertUtil -hashfile monecrin-sync-setup-<version>.exe SHA256
```

The Ed25519 signature over `SHA256SUMS.txt` is what the desktop app itself verifies before installing
any update — the source code and public key live in the private source repository, so this is not
something a third party can independently re-verify from this repo alone today. What matters for
security is that *the app* enforces it on every update, fail-closed, regardless of what this
repository serves.

Anti-downgrade is built in: the version that matters is the one embedded in the **signed** file name
inside `SHA256SUMS.txt`, not any external metadata — an attacker with write access to this repo alone
cannot make installed clients silently roll back to an older, vulnerable version.

## Auto-update

The desktop app checks this repository's releases automatically and installs updates silently once
verified, following the two checks above (fail-closed: if either check fails, the update is rejected
and the app keeps running its current version).

## Platforms

- **Windows** — available today.
- **macOS** — planned, not yet released.

## Support

For account, billing or general product support, visit **[monecrin.com](https://monecrin.com)**.

## Security

Found a vulnerability in a released binary or in the update chain? Please report it responsibly via
[monecrin.com](https://monecrin.com) rather than opening a public issue.

## License

Mon Écrin desktop is proprietary software, © UIT Guard. This repository distributes compiled,
signed binaries only; no license to the source code is granted.
