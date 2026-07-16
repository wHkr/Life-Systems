# Software Trust Verification Workflow

## Overview

When Windows blocks an application, the warning message does not always mean the software is dangerous.

Modern Windows security systems evaluate applications using multiple trust signals:

- Application reputation
- Digital signatures
- Publisher identity
- File integrity
- Download source

A blocked application should be investigated before making a decision.

The goal of this workflow is to determine:

1. Where did the software originate?
2. Is the source legitimate?
3. Was the file modified after release?
4. Can Windows verify the publisher?
5. Is the software appropriate to trust?

---

# Trust Verification Model

Software trust should be evaluated in layers.

```text
                SOFTWARE TRUST MODEL

                     SOURCE
                        |
                        v
          Is this the official project?
                        |
                        v
                PACKAGE MANAGER
                        |
                        v
        Did it download the expected file?
                        |
                        v
                     HASH
                        |
                        v
       Does the file match the published release?
                        |
                        v
              DIGITAL SIGNATURE
                        |
                        v
        Can Windows verify the publisher?
                        |
                        v
              FINAL TRUST DECISION
```

!!! note
    No single check proves software is safe. Trust is created by combining multiple pieces of evidence.

---

# Step 1 — Verify the Software Source

## Purpose

The first question should always be:

> Where did this software come from?

Preferred sources:

- Official developer website
- Official GitHub repository
- Trusted package manager

---

## Example: Scoop Package Information

Command:

```powershell
scoop info orcaslicer
```

Example output:

```text
Name        : orcaslicer
Source      : extras
Website     : https://github.com/OrcaSlicer/OrcaSlicer
License     : AGPL-3.0-or-later
```

---

## What This Verifies

This confirms:

| Check | Result |
|---|---|
| Package source | Trusted Scoop repository |
| Project website | Official GitHub |
| Software identity | Matches expected application |

The goal is to avoid downloading software from unknown mirrors or unofficial websites.

---

# Step 2 — Inspect the Package Manifest

Package managers maintain manifests that describe:

- Version
- Download location
- Architecture
- Expected hash

Command:

```powershell
scoop cat orcaslicer
```

Example:

```json
{
    "version": "2.4.2",
    "url": "https://github.com/OrcaSlicer/OrcaSlicer/releases/download/v2.4.2/OrcaSlicer_Windows_V2.4.2_x64_portable.zip",
    "hash": "feba3009dfb9d268779cca5758a1a5bc3b7d0722bf8fa48d5c57340de975d6be"
}
```

---

## What We Are Checking

The manifest should point to:

✅ Official download location
✅ Expected release version
✅ Known cryptographic hash

---

# Step 3 — Verify the File Hash

## What Is a Hash?

A hash is a mathematical fingerprint of a file.

If the file changes by even one character, the hash changes.

Example:

```text
Original File

        |
        v

SHA256 Algorithm

        |
        v

Digital Fingerprint
```

---

## Command

```powershell
Get-FileHash "file.zip" -Algorithm SHA256
```

Example:

```powershell
Get-FileHash "$env:USERPROFILE\scoop\cache\orcaslicer#2.4.2#d6f271e.zip" -Algorithm SHA256
```

Expected:

```text
FEBA3009DFB9D268779CCA5758A1A5BC3B7D0722BF8FA48D5C57340DE975D6BE
```

Actual:

```text
FEBA3009DFB9D268779CCA5758A1A5BC3B7D0722BF8FA48D5C57340DE975D6BE
```

---

## Result Interpretation

| Result | Meaning |
|---|---|
| Hash matches | File is identical to expected release |
| Hash differs | File may be corrupted or modified |

!!! tip
    Matching hashes verify integrity. They do not prove the developer is trustworthy.

---

# Step 4 — Check Digital Signatures

Windows uses Authenticode signatures to verify publishers.

Command:

```powershell
Get-AuthenticodeSignature "application.exe" | Format-List *
```

Example:

```powershell
Get-AuthenticodeSignature "C:\Users\aaron\scoop\apps\orcaslicer\current\orca-slicer.exe" | Format-List *
```

---

# Signature Results

## Signed Application

Example:

```text
Status : Valid
SignerCertificate : Microsoft Corporation
```

Meaning:

- Publisher identity verified
- Windows can confirm who created the application

---

## Unsigned Application

Example:

```text
Status : NotSigned
SignatureType : None
SignerCertificate :
```

Meaning:

- No digital signature exists
- Windows cannot verify publisher identity

!!! warning
    An unsigned application is not automatically malicious. Many open-source projects distribute unsigned Windows binaries.

---

# Case Study — OrcaSlicer

## Investigation Results

| Category | Result |
|---|---|
| Source | Official OrcaSlicer GitHub |
| Package Manager | Scoop Extras |
| Hash Verification | Passed |
| Digital Signature | Not Signed |

---

## Final Diagnosis

The application was legitimate.

Windows blocked the application because:

```text
The executable did not contain a publisher signature.
```

The file itself was verified through:

- Official source
- Package manifest
- SHA256 hash

---

# Useful Command Reference

## Package Information

```powershell
scoop info application
```

---

## View Package Manifest

```powershell
scoop cat application
```

---

## Verify Hash

```powershell
Get-FileHash file -Algorithm SHA256
```

---

## Check Signature

```powershell
Get-AuthenticodeSignature file.exe
```

---

# Troubleshooting Philosophy

A security warning is a starting point, not a conclusion.

Investigate:

1. **Source**
   - Where did it come from?

2. **Package**
   - Did the package manager retrieve the expected file?

3. **Hash**
   - Is the file unchanged?

4. **Signature**
   - Can Windows verify the publisher?

5. **Decision**
   - Is this normal behavior for this type of software?

Evidence creates trust.