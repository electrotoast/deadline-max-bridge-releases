# Deadline Max Bridge Releases

Release-only downloads for Deadline Max Bridge packages.

This repository is intentionally small: use the **Releases** page for installer
packages and checksums. The source project and build files are not published in
this repository.

## Current Release

- Installer: `DeadlineMaxBridge-3dsMax2027-Setup.exe`
- Manual package: `DeadlineMaxBridge-3dsMax2027.zip`
- Target: AWS Thinkbox Deadline 10.x repositories with Autodesk 3ds Max 2027
- Installer SHA-256: `66CA758B345504F56B383981132199246D2E1037E6400BB03F867F3B035B7501`
- Zip SHA-256: `54FF8188BF047B921E8250CEF82BFF89ECEB097159A9524335580C3C1DED7C5B`

Download the latest release from:

https://github.com/electrotoast/deadline-max-bridge-releases/releases/latest

## What Is Included

The package installs a private 3ds Max 2027 lane for Deadline:

- `lightning64Max2027.dlx`
- private Deadline Worker plugin files
- private 3ds Max 2027 submitter files
- PowerShell install, validation, smoke-scene, and uninstall tools
- package documentation

The package contains runtime installer scripts required for Deadline and
3ds Max integration. It does not include the C++ bridge source project or the
private build system.

## Install

### Guided Installer

Download and run:

```text
DeadlineMaxBridge-3dsMax2027-Setup.exe
```

Choose the Deadline repository root and whether to install the 3ds Max 2027
Deadline menu for the current Windows user. If repository writes require
elevation, right-click the setup executable and choose **Run as administrator**.

### Manual Zip Install

Extract the release archive, open PowerShell in the extracted folder, and run:

```powershell
.\tools\check-deadline.ps1 -RequireRepositoryPlugin
.\tools\install.ps1 -RepositoryRoot C:\DeadlineRepository10
```

To install the 3ds Max 2027 Deadline menu for the current Windows user:

```powershell
.\tools\install.ps1 -RepositoryRoot C:\DeadlineRepository10 -InstallCurrentUserSubmitter
```

If the Deadline repository path is already configured on the machine, the
installer can usually resolve it without `-RepositoryRoot`.

## Verify

Before installing, verify the download:

```powershell
Get-FileHash .\DeadlineMaxBridge-3dsMax2027-Setup.exe -Algorithm SHA256
Get-FileHash .\DeadlineMaxBridge-3dsMax2027.zip -Algorithm SHA256
```

The hashes should match the SHA-256 values listed above and in the release
notes.

After installation:

1. Restart 3ds Max 2027.
2. Confirm the top menu bar contains `Deadline`.
3. Open `Deadline > Submit Max To Deadline`.
4. Submit a one-frame test using a camera selected in the scene.

## Uninstall

From the extracted package folder:

```powershell
.\tools\uninstall.ps1 -RepositoryRoot C:\DeadlineRepository10
```

To also remove the private current-user 3ds Max menu files:

```powershell
.\tools\uninstall.ps1 -RepositoryRoot C:\DeadlineRepository10 -RemoveCurrentUserSubmitter
```

## Notes

- This is a release/distribution repository, not an open-source source tree.
- GitHub's automatic `Source code (zip)` and `Source code (tar.gz)` downloads
  are README-only repository snapshots. Use the installer or manual package
  assets for installation.
- The installer backs up replaced repository files before overwriting them.
- The default install does not edit stock Deadline `3dsmax`, `3dsCmd`, or
  submitter files.
- Earlier 3ds Max versions continue to use the existing Deadline submitter and
  Worker plugin.
- This project is not affiliated with, endorsed by, or sponsored by Amazon Web
  Services, AWS Thinkbox, or Autodesk.
