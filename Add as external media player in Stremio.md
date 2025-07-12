# 📺 Add Energy Media Player (EMP) as an External Player in Stremio

Easily modify Stremio’s configuration to enable playback with Energy Media Player or Energy Media Player for Windows.

---

## 🧰 Prerequisites

Ensure your version of **Energy Media Player** or **Energy Media Player for Windows** is **≥ 1.0.281**.

---

## ⚙️ Step-by-Step Setup

### 1️⃣ Create a Shortcut to EMP’s Execution Alias

Choose a folder where the shortcut will live, allowing Stremio to launch EMP correctly.

- Right-click inside the target folder → choose **New > Shortcut**
- Use one of the following paths:

  - **For Energy Media Player:**
    ```text
    %LOCALAPPDATA%\Microsoft\WindowsApps\EnergyPlayer.exe
    ```

  - **For Energy Media Player for Windows:**
    ```text
    %LOCALAPPDATA%\Microsoft\WindowsApps\EnergyPlayerForWindows.exe
    ```

- Name the shortcut **with a `.exe` suffix**, e.g., `EnergyPlayer.exe`
- Click **Finish**

---

### 2️⃣ Locate the Stremio Installation Directory

- Open the **Start Menu**
- Type `Stremio`
- **Right-click** the app → choose **Open file location**
- If this opens a shortcut, **right-click** it again → select **Open file location** once more
- You are now in the folder containing `server.js`

---

### 3️⃣ Open the `server.js` Configuration File

- Find the file:  
  ```text
  server.js
  ```
- Open it using a code editor like **VS Code**, **Notepad++**, or **Notepad**

---

### 4️⃣ Add EMP Configuration

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

### 6️⃣ Troubleshooting Playback Issues

If the media doesn’t play:
- Ensure **localhost loopback** is enabled

📎 Helpful guides:
- [Enable local streaming for Energy Media Player](https://github.com/IDimitrovDev/Energy-Media-Player/blob/master/Enable%20localhost%20streaming%20-%20Energy%20Media%20Player.md)
- [Enable local streaming for Energy Media Player for Windows](https://github.com/IDimitrovDev/Energy-Media-Player/blob/master/Enable%20localhost%20streaming%20-%20Energy%20Media%20Player%20for%20Windows.md)

💡 If connections drop often, confirm that this setting is **disabled** in EMP:  
`Settings > General > Limit network connections response to 20s`

---