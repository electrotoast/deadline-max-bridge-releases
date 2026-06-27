# Deadline Max Bridge Releases

Release-only downloads for Deadline Max Bridge packages.

This repository is intentionally small: use the **Releases** page for installer
packages and checksums. The source project and build files are not published in
this repository.

## Current Release

- Package: `DeadlineMaxBridge-3dsMax2027.zip`
- Target: AWS Thinkbox Deadline 10.x repositories with Autodesk 3ds Max 2027
- SHA-256: `07BE2330374F31BC21FD8E2BD9F809BE7CEF78FC5E9233F82B8C5D4796054047`

Download the latest package from:

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
Get-FileHash .\DeadlineMaxBridge-3dsMax2027.zip -Algorithm SHA256
```

The hash should match the SHA-256 listed above and in the release notes.

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
- The installer backs up replaced repository files before overwriting them.
- The default install does not edit stock Deadline `3dsmax`, `3dsCmd`, or
  submitter files.
- Earlier 3ds Max versions continue to use the existing Deadline submitter and
  Worker plugin.
- This project is not affiliated with, endorsed by, or sponsored by Amazon Web
  Services, AWS Thinkbox, or Autodesk.
