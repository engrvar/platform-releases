# Platform releases

Installers, update packages and checksums for Platform. This repository holds no source; it is the update source that installed Platforms read, and it is public so that reading it needs no token.

## Each release

| Asset | What it is |
| --- | --- |
| `Platform-Setup-<version>.exe` | The Windows installer. Run it as administrator for a first install or an in-place upgrade. |
| `platform-<version>.zip` | The update package an installed Platform downloads and applies from Administration > Deployment, or installs offline through the same page. |
| `platform-<version>.zip.sha256` | The package's SHA-256; the installed Platform verifies the download against it before applying. |

The release notes name the source commit the build came from.

## How an installed Platform uses this

Every install ships with this repository as its update source (`Updates:GitHubRepository`). The service checks for a newer release 90 seconds after it starts and every 6 hours, tells administrators when one exists, and Administration > Deployment installs it: download, verify, prepare, restart. The newest non-draft release that carries `platform-<version>.zip` is the update; pre-releases are offered only when an install asks for them.

## Publishing

From the source repository: `scripts\release.ps1 -Version X` builds the assets, `scripts\publish-release.ps1 -Version X` creates the release here.
