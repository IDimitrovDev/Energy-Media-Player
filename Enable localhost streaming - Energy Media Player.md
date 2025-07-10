# 🌐 Why Can't Energy Media Player Connect to Localhost?

By default, Windows blocks apps installed from the Microsoft Store (like Energy Media Player) from accessing your own computer through the network — even if you're trying to stream from something running on the same machine (like `127.0.0.1` or `localhost`).

This restriction is called **loopback isolation**. It's designed to protect your system from apps that might try to access sensitive local data or services.

However, if you're using a trusted app like Energy Media Player, you can safely allow it to access local network streams.

---

## ✅ What Happens When You Enable It?

Once you allow loopback access:
- Energy Media Player will be able to stream from local servers (like Plex, Jellyfin, Stremio or custom web apps running on your PC).
- This setting stays enabled until you manually turn it off.

---
## 🛠 Enable local streaming using Command Prompt

1. Open the **Start menu**, type `cmd`, right-click **Command Prompt**, and choose **Run as administrator**.
2. Copy and paste this command to **enable** local streaming:

   ```cmd
   CheckNetIsolation LoopbackExempt -a -n="6615IvanDimitrov89.EnergyPlayer_1gdjqnh0agk8c"
   ```
3. To **disable local** streaming later, use:

    ```cmd
    CheckNetIsolation LoopbackExempt -d -n="6615IvanDimitrov89.EnergyPlayer_1gdjqnh0agk8c"
    ```

## 🛠 Enable Using a Shortcut

You can create a desktop shortcuts to quickly enable/disable local streaming for **Energy Media Player** without opening the command prompt manually.

### 🔧 Steps to Create the Shortcut

1. **Right-click** in any folder or on your desktop and choose **New > Shortcut**.
2. In the dialog that appears, paste the following command:

   ```cmd
   cmd.exe /k "CheckNetIsolation LoopbackExempt -a -n=""6615IvanDimitrov89.EnergyPlayer_1gdjqnh0agk8c"""
   ```

3. Click **Next**, and give your shortcut a name, such as:  
   `Enable Local Streaming in Energy Media Player`
4. Click **Finish**.
5. Right click and run as administrator.

---

### 🧯 Create a Shortcut to Disable Local Streaming

To remove the permission later, follow the same steps, but use this command instead:

```cmd
cmd.exe /k "CheckNetIsolation LoopbackExempt -d -n=""6615IvanDimitrov89.EnergyPlayer_1gdjqnh0agk8c"""
```

You can name this shortcut something like:  
`Disable Local Streaming in Energy Media Player`

---
