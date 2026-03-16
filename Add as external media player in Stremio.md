# 📺 Add Energy Media Player (EMP) as an External Player in Stremio  
Supports **Stremio v4 (server.js method)** and **Stremio v5 (M3U playlist method)**

This guide explains how to integrate **Energy Media Player** or **Energy Media Player for Windows** with both Stremio versions.  
Stremio v4 uses **direct external player definitions** in `server.js`, while Stremio v5 uses **M3U playlists only**.

---

# 🧰 Prerequisites

- **Energy Media Player** or **Energy Media Player for Windows** version **≥ 1.0.281**
- Windows 10 or Windows 11

---

# 🟦 Stremio v5 — External Player via M3U Playlists (Recommended)

Stremio v5 **no longer supports editing `server.js`**.  
External players now work **exclusively through M3U playlist export**.

Stremio generates an `.m3u` file → Windows opens it → EMP plays it.

---

## 1️⃣ Configure Stremio v5 to Use M3U External Player Mode

1. Open **Stremio v5**.  
2. Go to **Settings**.  
3. Scroll to **Player → Advanced**.  
4. Set **Play in external player** to **M3U playlist**.

This is the *only* external player mode in v5.
---

## 2️⃣ Play Videos in EMP from Stremio v5

1. Start any video in Stremio.  
2. Stremio will notify for stream opened in external player and download a `m3u` playlist
3. Open the m3u playlist with EMP → EMP launches → playback begins.
---

## 3️⃣ Localhost Streaming Notes

If Stremio streams via local HTTP, EMP must be allowed to access `localhost`.

Follow the existing EMP guides:
- Enable localhost streaming (EMP)
- Enable localhost streaming (EMP for Windows)

If connections drop:
- Disable  
  **Settings → General → Limit network connections response to 20s**

---

# 🟩 Stremio v4 — External Player via `server.js` (Legacy Method)

Stremio v4 allows direct external player definitions inside `server.js`.  
This section preserves the original workflow for users still on v4.

---

## 1️⃣ Create a Shortcut to EMP’s Execution Alias

Create a `.lnk` shortcut pointing to:

- **Energy Media Player**
  ```
  %LOCALAPPDATA%\Microsoft\WindowsApps\EnergyPlayer.exe
  ```

- **Energy Media Player for Windows**
  ```
  %LOCALAPPDATA%\Microsoft\WindowsApps\EnergyPlayerForWindows.exe
  ```

Name the shortcut with a `.exe` suffix, e.g. `EnergyPlayer.exe`.

---

## 2️⃣ Locate the Stremio Installation Directory

1. Open Start Menu → type **Stremio**.  
2. Right‑click → **Open file location**.  
3. If it opens a shortcut, right‑click again → **Open file location**.  
4. You should now see `server.js`.

---

### 3️⃣ Open the `server.js` Configuration File

- Find the file:  
  ```text
  server.js
  ```
- Open it using a code editor like **VS Code**, **Notepad++**, or **Notepad**

---

## 4️⃣ Add EMP Configuration

#### 🔍 Search for:
```js
mpcBe:
```

#### 🔧 Within about 10 lines, locate:
```js
};
devices.groups.external
```

#### 🧩 Just **before** that section, add:

```js
,emp: {
    title: "EMP",
    args: [ "" ],
    subArg: "--subs-path=",
    timeArg: "",
    playArg: "--path=",
    darwin: { path: [] },
    linux: { path: [] },
    win32: {
        path: ['"<folder>\\<shortcutName>.lnk"']
    }
},
```

Replace:
- `<folder>` → full path to the folder containing your shortcut (with `\\` for path separators)
- `<shortcutName>` → the shortcut filename (including `.exe`)

✅ Example:
```js
path: ['"C:\\Tools\\Shortcuts\\EnergyPlayer.exe.lnk"']
```

#### 🧠 Surrounding code should resemble:

```js
mpcBe: {
    title: "MPC-BE",
    args: [ "" ],
    subArg: "/sub ",
    timeArg: "start ",
    playArg: "",
    darwin: { path: [] },
    linux: { path: [] },
    win32: {
        path: [
            '"C:\\Program Files (x86)\\MPC-BE x64\\mpc-be4.exe"',
            '"C:\\Program Files\\MPC-BE x64\\mpc-be64.exe"'
        ]
    }
},
emp: {
    title: "EMP",
    args: [ "" ],
    subArg: "--subs-path=",
    timeArg: "",
    playArg: "--path=",
    darwin: { path: [] },
    linux: { path: [] },
    win32: {
        path: ['"C:\\Tools\\Shortcuts\\EnergyPlayer.exe.lnk"']
    }
},
};
devices.groups.external = [], Object.keys(players).forEach(function(el) {
```

---

### 5️⃣ Launch EMP via Stremio

- Open **Stremio**
- Start any video or stream
- Check for the **"Play in EMP"** option
- Click it to test playback in Energy Media Player

---

## 6️⃣ Troubleshooting (v4)

If playback fails:
- Ensure localhost loopback is enabled  
- Disable the 20‑second network limit in EMP if streams drop

---