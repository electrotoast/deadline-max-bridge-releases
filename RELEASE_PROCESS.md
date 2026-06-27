# Release Process

This repository is release-only. Do not publish source or private build files
here.

## Quick Update Checklist

1. Rebuild the private package zip.
2. Build the setup executable from the package zip.
3. Smoke-test the setup executable with `/silent /RepositoryRoot` against a
   disposable fake repository.
4. Compute SHA-256 hashes for the setup executable and zip.
5. Update `README.md` with the current asset names and hashes.
6. Create a new GitHub Release with both assets:
   - `DeadlineMaxBridge-3dsMax2027-Setup.exe`
   - `DeadlineMaxBridge-3dsMax2027.zip`
7. Confirm `/releases/latest` points to the new release.
8. Confirm GitHub's automatic source archives contain only public release
   repository files.

## Release Notes Template

```text
Deadline Max Bridge for Autodesk 3ds Max 2027 on AWS Thinkbox Deadline 10.x.

Important download note:
- Download `DeadlineMaxBridge-3dsMax2027-Setup.exe` for the guided Windows installer.
- Download `DeadlineMaxBridge-3dsMax2027.zip` for manual or scripted installation.
- GitHub's automatic `Source code (zip)` and `Source code (tar.gz)` links are release repository snapshots. They are not installer packages and do not contain the private source project.

Assets:
- `DeadlineMaxBridge-3dsMax2027-Setup.exe`
- `DeadlineMaxBridge-3dsMax2027.zip`

SHA-256:
- `DeadlineMaxBridge-3dsMax2027-Setup.exe`: `<hash>`
- `DeadlineMaxBridge-3dsMax2027.zip`: `<hash>`

Validation:
- The setup executable was smoke-tested with `/silent /RepositoryRoot` against a fake repository and installed the expected bridge files plus install manifest.
```
