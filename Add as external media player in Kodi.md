# 📺 Add Energy Media Player (EMP) as an External Player in Kodi

This guide explains how to configure **Kodi** to use **Energy Media Player (EMP)** or **Energy Media Player for Windows** as an **external video player**.

---

## 🧰 Prerequisites

- **Energy Media Player** or **Energy Media Player for Windows**
- **Minimum version:** `v1.0.281` or newer
- **Kodi** installed on Windows

---

## ⚙️ Step‑by‑Step Setup

---

## 1️⃣ Locate the Real EMP Executable Path

Kodi requires a **real file path** to the executable.

1. Press **Win + R**
2. Enter:
```
%LOCALAPPDATA%\Microsoft\WindowsApps\
```
3. Press **Enter**

You should see one (or both) of the following files:
- Energy Media Player
```
EnergyPlayer.exe
```
- Energy Media Player for Windows
```
EnergyPlayerWin.exe
```
---

## 2️⃣ Locate Kodi’s `userdata` Directory

Kodi stores its `userdata` folder in different locations depending on how it was installed.

### 🟦 Standard (Installer) Version of Kodi
If you installed Kodi from the official website or via a normal installer, the userdata directory is located at:

```
%APPDATA%\Kodi\userdata
```

Paste this into the **Start Menu** or **File Explorer** address bar and press Enter.

---

### 🟩 Microsoft Store Version of Kodi
The Microsoft Store version sandboxes the app, so the userdata directory is stored under **LocalState** instead of AppData/Roaming.

Use this path:

```
%LOCALAPPDATA%\Packages\XBMCFoundation.Kodi_4n2hpmxwrvr6p\LocalState\userdata
```

Paste it into the **Start Menu** or **File Explorer** to open the folder.


## 3️⃣ Create `playercorefactory.xml`

Inside the `userdata` folder, create a file named:

```
playercorefactory.xml
````

Paste the following **default configuration**.

### ▶ Energy Media Player
```xml
<?xml version="1.0" encoding="UTF-8"?>
<playercorefactory>
  <players>
    <player name="EMP" type="ExternalPlayer" audio="true" video="true">
      <filename>{path to exe}\EnergyPlayer.exe</filename>
      <args>--path "{1}"</args>
      <hidexbmc>false</hidexbmc>
      <hideconsole>false</hideconsole>
      <warpcursor>none</warpcursor>
    </player>

  </players>
     <rules action="prepend">
    <rule video="true" player="EMP"/>
  </rules>
</playercorefactory>
````

### ▶ Energy Media Player for Windows

```xml
<?xml version="1.0" encoding="UTF-8"?>
<playercorefactory>
  <players>
    <player name="EMP" type="ExternalPlayer" audio="true" video="true">
      <filename>{path to exe}\EnergyPlayerWin.exe</filename>
      <args>--path "{1}"</args>
      <hidexbmc>false</hidexbmc>
      <hideconsole>false</hideconsole>
      <warpcursor>none</warpcursor>
    </player>

  </players>
     <rules action="prepend">
    <rule video="true" player="EMP"/>
  </rules>
</playercorefactory>
```

Replace the `{path to exe}` with the real path for `%LOCALAPPDATA%\Microsoft\WindowsApps\`

🔗 Advanced configuration reference:  
<https://kodi.wiki/view/External_players>

✅ With this configuration, **all video playback** in Kodi will open in EMP.

***

## 4️⃣ Playback of Local & Network Media Files

Kodi passes **file paths** directly to EMP.  
Due to **Windows file access restrictions**, EMP must be explicitly allowed to access those locations.

### ✅ Required action

Add folders (or entire drives) containing your media to **EMP’s File Manager**.

*   Files outside added locations **will not play***   
*   This restriction **does apply to local and network mounted drives**
*   This restriction **does not apply to removable drives**

### 📸 Visual guides

**Add a media folder**  
![alt text](https://raw.githubusercontent.com/IDimitrovDev/Energy-Media-Player/refs/heads/master/Assets/add-media-folder.png)

**Add a drive or folder from the folder picker**  
![alt text](https://raw.githubusercontent.com/IDimitrovDev/Energy-Media-Player/refs/heads/master/Assets/network-drive.png)

**You will see the drive or folder in the file manager which means that file in it can now be accessed**  
![alt text](https://raw.githubusercontent.com/IDimitrovDev/Energy-Media-Player/refs/heads/master/Assets/drive.png)

***

## 5️⃣ (Optional) Enable Full‑Screen Playback in EMP

EMP does **not** support switching to full screen via command‑line arguments at this moment.  
Enable full‑screen behavior directly in the player settings.

**Expanded Full Screen Mode**  
![alt text](https://raw.githubusercontent.com/IDimitrovDev/Energy-Media-Player/refs/heads/master/Assets/expanded-full-screen-mode.png)

***

## 6️⃣ Launch EMP via Kodi

1.  Open **Kodi**
2.  Start any **video or stream**
3.  Playback will open automatically in **Energy Media Player**

