### 1. Update & Version APIs

Lunar for Roblox uses two primary endpoints: a backend API (`api.lunarrobloxprod.com`) that handles client telemetry and version gating, and an unauthenticated Cloudflare R2 bucket (`appupdates.lunarrobloxprod.com`) that hosts the actual build manifests and binaries.

#### A. Direct Bucket Manifests (No Auth Required)
These endpoints can be fetched with standard HTTP GET requests (no special headers needed):

| Platform / Channel | Manifest URL | Description |
| :--- | :--- | :--- |
| **Windows (Latest)** | [`https://appupdates.lunarrobloxprod.com/latest.yml`](https://appupdates.lunarrobloxprod.com/latest.yml) | Returns current Windows release, sha512, and download URLs |
| **macOS (Latest)** | [`https://appupdates.lunarrobloxprod.com/latest-mac.yml`](https://appupdates.lunarrobloxprod.com/latest-mac.yml) | Returns current macOS DMG and arm64 ZIP manifests |
| **Windows (Beta)** | [`https://appupdates.lunarrobloxprod.com/beta.yml`](https://appupdates.lunarrobloxprod.com/beta.yml) | Windows Beta channel manifest |
| **macOS (Beta)** | [`https://appupdates.lunarrobloxprod.com/beta-mac.yml`](https://appupdates.lunarrobloxprod.com/beta-mac.yml) | macOS Beta channel manifest |
| **Windows (Alpha)** | [`https://appupdates.lunarrobloxprod.com/alpha.yml`](https://appupdates.lunarrobloxprod.com/alpha.yml) | Windows Alpha channel manifest |
| **macOS (Alpha)** | [`https://appupdates.lunarrobloxprod.com/alpha-mac.yml`](https://appupdates.lunarrobloxprod.com/alpha-mac.yml) | macOS Alpha channel manifest |

---

#### B. Launcher Updater API (Backend Authenticated)
If you want to query the backend launcher service directly (as the desktop app does):

- **Base URL:** `https://api.lunarrobloxprod.com/v1/updater`
- **Endpoints:**
  - `GET /v1/updater/latest.yml?installation_id=<UUID>&version=<SEMVER>` (Windows)
  - `GET /v1/updater/latest-mac.yml?installation_id=<UUID>&version=<SEMVER>` (macOS)
- **Required Headers:**
  - `x-installation-id`: Any valid UUIDv4 string (e.g. `9da34852-297f-4510-9d9b-636b236541a1`)
  - `x-version`: Current client version (e.g. `0.1.0` or `1.0.16`)
  - `User-Agent`: Any standard browser user-agent (to bypass Cloudflare WAF bot filters)

**Example cURL:**
```bash
curl -H "x-installation-id: 00000000-0000-0000-0000-000000000000" \
     -H "x-version: 1.0.0" \
     -H "User-Agent: Mozilla/5.0" \
     "https://api.lunarrobloxprod.com/v1/updater/latest.yml?installation_id=00000000-0000-0000-0000-000000000000&version=1.0.0"
```

---

### 2. Public Versions on Distribution Bucket

The bucket currently stores the three most recent production builds: **`1.0.16`**, **`1.0.15`**, and **`1.0.14`**.

---

#### Version 1.0.16 *(Current Latest — Nov 3, 2026)*

##### Windows
* **Installer (Setup Executable):**  
  [lunar-for-roblox-1.0.16-setup.exe](https://appupdates.lunarrobloxprod.com/lunar-for-roblox-1.0.16-setup.exe) *(1.14 MB / 1,195,832 bytes)*
* **Full Application Package (NSIS 7z Archive):**  
  [lunar-for-roblox-1.0.16-x64.nsis.7z](https://appupdates.lunarrobloxprod.com/lunar-for-roblox-1.0.16-x64.nsis.7z) *(121.27 MB / 127,164,340 bytes)*

##### macOS
* **Disk Image (Universal DMG for Intel & Apple Silicon):**  
  [lunar-for-roblox-1.0.16.dmg](https://appupdates.lunarrobloxprod.com/lunar-for-roblox-1.0.16.dmg) *(147.60 MB / 154,764,819 bytes)*  
  *(Blockmap: [lunar-for-roblox-1.0.16.dmg.blockmap](https://appupdates.lunarrobloxprod.com/lunar-for-roblox-1.0.16.dmg.blockmap))*
* **Apple Silicon ZIP Archive:**  
  [lunar-for-roblox-1.0.16-arm64-mac.zip](https://appupdates.lunarrobloxprod.com/lunar-for-roblox-1.0.16-arm64-mac.zip) *(140.37 MB / 147,185,523 bytes)*  
  *(Blockmap: [lunar-for-roblox-1.0.16-arm64-mac.zip.blockmap](https://appupdates.lunarrobloxprod.com/lunar-for-roblox-1.0.16-arm64-mac.zip.blockmap))*

---

#### Version 1.0.15

##### Windows
* **Installer (Setup Executable):**  
  [lunar-for-roblox-1.0.15-setup.exe](https://appupdates.lunarrobloxprod.com/lunar-for-roblox-1.0.15-setup.exe) *(1.14 MB / 1,195,832 bytes)*
* **Full Application Package (NSIS 7z Archive):**  
  [lunar-for-roblox-1.0.15-x64.nsis.7z](https://appupdates.lunarrobloxprod.com/lunar-for-roblox-1.0.15-x64.nsis.7z) *(121.38 MB / 127,271,072 bytes)*

##### macOS
* **Disk Image (Universal DMG for Intel & Apple Silicon):**  
  [lunar-for-roblox-1.0.15.dmg](https://appupdates.lunarrobloxprod.com/lunar-for-roblox-1.0.15.dmg) *(147.62 MB / 154,795,159 bytes)*  
  *(Blockmap: [lunar-for-roblox-1.0.15.dmg.blockmap](https://appupdates.lunarrobloxprod.com/lunar-for-roblox-1.0.15.dmg.blockmap))*
* **Apple Silicon ZIP Archive:**  
  [lunar-for-roblox-1.0.15-arm64-mac.zip](https://appupdates.lunarrobloxprod.com/lunar-for-roblox-1.0.15-arm64-mac.zip) *(140.40 MB / 147,220,347 bytes)*  
  *(Blockmap: [lunar-for-roblox-1.0.15-arm64-mac.zip.blockmap](https://appupdates.lunarrobloxprod.com/lunar-for-roblox-1.0.15-arm64-mac.zip.blockmap))*

---

#### Version 1.0.14

##### Windows
* **Installer (Setup Executable):**  
  [lunar-for-roblox-1.0.14-setup.exe](https://appupdates.lunarrobloxprod.com/lunar-for-roblox-1.0.14-setup.exe) *(1.14 MB / 1,195,832 bytes)*
* **Full Application Package (NSIS 7z Archive):**  
  [lunar-for-roblox-1.0.14-x64.nsis.7z](https://appupdates.lunarrobloxprod.com/lunar-for-roblox-1.0.14-x64.nsis.7z) *(121.26 MB / 127,155,511 bytes)*

##### macOS
* **Disk Image (Universal DMG for Intel & Apple Silicon):**  
  [lunar-for-roblox-1.0.14.dmg](https://appupdates.lunarrobloxprod.com/lunar-for-roblox-1.0.14.dmg) *(147.52 MB / 154,686,910 bytes)*  
  *(Blockmap: [lunar-for-roblox-1.0.14.dmg.blockmap](https://appupdates.lunarrobloxprod.com/lunar-for-roblox-1.0.14.dmg.blockmap))*
* **Apple Silicon ZIP Archive:**  
  [lunar-for-roblox-1.0.14-arm64-mac.zip](https://appupdates.lunarrobloxprod.com/lunar-for-roblox-1.0.14-arm64-mac.zip) *(140.32 MB / 147,133,586 bytes)*  
  *(Blockmap: [lunar-for-roblox-1.0.14-arm64-mac.zip.blockmap](https://appupdates.lunarrobloxprod.com/lunar-for-roblox-1.0.14-arm64-mac.zip.blockmap))*
