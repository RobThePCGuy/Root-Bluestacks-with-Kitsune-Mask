# Root BlueStacks 5+ Rooting Guide (2025 Edition) with Kitsune Mask
[![GitHub Repo Stars](https://img.shields.io/github/stars/RobThePCGuy/Root-Bluestacks-with-Kitsune-Mask?style=social)](https://github.com/RobThePCGuy/Root-Bluestacks-with-Kitsune-Mask)
[![YouTube Video Views](https://img.shields.io/youtube/views/eRXeasi6GQQ?style=social)](https://youtu.be/eRXeasi6GQQ)
[![Last Updated](https://img.shields.io/github/last-commit/RobThePCGuy/Root-Bluestacks-with-Kitsune-Mask)](https://github.com/RobThePCGuy/Root-Bluestacks-with-Kitsune-Mask/commits/main)

> [!IMPORTANT]
> **Getting "Android system doesn't meet security" popup?** Check out [Troubleshooting](https://github.com/RobThePCGuy/Root-Bluestacks-with-Kitsune-Mask#getting-android-system-doesnt-meet-security-popup).

**Root your BlueStacks 5+ or MSI App Player emulator effortlessly using Kitsune Mask.** This guide provides a streamlined, text-based approach to granting root access to your instances, allowing you to run applications that require root privileges. No external tools are necessary, just your PC, Notepad, and Kitsune Mask.

[![Watch the Tutorial on YouTube](https://github.com/user-attachments/assets/d73e49bf-68fb-4b51-99eb-2b442d1be7cc)](https://youtu.be/eRXeasi6GQQ)

> [!NOTE]
> **BlueStacks Root GUI (Recommended Method)**
>
> My Python-based portable application allows you to toggle root access and enable read/write (R/W) permissions for your BlueStacks and MSI App Player instances with simple button clicks. It automatically detects all instances and has been **recently updated to fix critical bugs and improve reliability.**
>
> For an easier experience, check it out at **[BlueStacks-Root-GUI](https://github.com/RobThePCGuy/BlueStacks-Root-GUI)**.

> [!IMPORTANT]
> **Tested Versions:**
>
> This guide is verified to work on **BlueStacks App Player `5.22.0.1102`** and **MSI App Player `5.10.0.1085`**, supporting Android 9, 11, and 13. This tutorial assumes you are using a master instance like **Rvc64** (Android 11).

> [!WARNING]
> **Understanding Kitsune Mask and BlueStacks Partitions:**
>
> Kitsune Mask is a systemless root tool. However, BlueStacks partitions are initially read-only, which prevents a direct installation. This guide uses a simple configuration file edit (via Notepad) to temporarily enable read/write permissions, allowing Kitsune Mask to be installed on the system partition.

## Prerequisites

Before you begin, ensure you have the following:

- **Administrator Rights:** You need administrative access to modify system files in `C:\ProgramData`.
- **Kitsune Mask APK:** Download the latest APK from the [KitsuneMagisk repository](https://github.com/1q23lyc45/KitsuneMagisk/releases).
- **Fresh BlueStacks/MSI Installation (Recommended):** For the most consistent results, start with a clean installation.

## Expected Outcome

Upon successful completion of this guide, your BlueStacks or MSI App Player instance will be fully rooted with Kitsune Mask.

## Summary of Steps

Here's a quick overview of the rooting process. See the "Detailed Steps" section below for a comprehensive walkthrough:

- [x] **Step 1: Prepare:** Cleanly install BlueStacks or MSI App Player.
- [x] **Step 2: Modify Configuration:** Edit `bluestacks.conf` to enable root access features.
- [x] **Step 3: Enable R/W:** Adjust settings in instance files to allow read/write access to system partitions.
- [x] **Step 4: Install Kitsune Mask:** Install Kitsune Mask directly to the `/system` partition and revert configuration changes.

---

<details>
<summary><h2>Detailed Steps</h2></summary>

**Instance Naming Convention:**

This tutorial uses the following naming conventions for master instances:

```
Master Instances:
  - Tiramisu64  = Android 13 (beta)
  - Rvc64       = Android 11
  - Pie64       = Android 9
```

*Adapt the instance names according to your setup.*

### Step 1: Prepare

1. **Fully Uninstall Previous Versions:**
   - Use the official tool to completely **[uninstall all previous BlueStacks installations](https://support.bluestacks.com/hc/en-us/articles/360057724751-How-to-uninstall-BlueStacks-5-BlueStacks-X-and-BlueStacks-Services-completely-from-your-PC)**.

2. **Install the Latest Version:**
   - Download from the official website: **[BlueStacks](https://www.bluestacks.com/)** or **[MSI App Player](https://www.msi.com/Landing/appplayer)**.

### Step 2: Modify BlueStacks Config

1. **Locate the Main Configuration File:**
   - For **BlueStacks 5**, navigate to **`C:\ProgramData\BlueStacks_nxt`**.
   - For **MSI App Player**, navigate to **`C:\ProgramData\BlueStacks_msi5`**.

2. **Edit with Notepad:**
   - Open **`bluestacks.conf`** using a text editor with administrator rights.

3. **Modify Configuration Values:**
   - Find and change the following two lines. If they don't exist, add them.
   - Change **`bst.feature.rooting="0"`** to **`bst.feature.rooting="1"`**.
   - Change **`bst.instance.Rvc64.enable_root_access="0"`** to **`bst.instance.Rvc64.enable_root_access="1"`**.

   > **Note:** Replace `Rvc64` with your target instance name (e.g., `Pie64`, `Tiramisu64`, or a custom name like `Rvc64_1`).

4. **Save Changes:**
   - Save the modified **`bluestacks.conf`** file.

### Step 3: Enable R/W

1. **Navigate to the Instance Folder:**
   - For **BlueStacks 5**: **`C:\ProgramData\BlueStacks_nxt\Engine\Rvc64`**
   - For **MSI App Player**: **`C:\ProgramData\BlueStacks_msi5\Engine\Rvc64`**

   > **Note:** Replace `Rvc64` with your target instance folder name. Cloned instances may have names like `Rvc64_1`.

2. **Modify the `.bstk.in` file:**
   - Open **`Android.bstk.in`** with a text editor. This file is always in the master instance folder.
   - For the **`location="fastboot.vdi"`** and **`location="Root.vhd"`** entries, change the attribute from **`type="Readonly"`** to **`type="Normal"`**.
   - **Example:**
     ```diff
     -         <HardDisk uuid="{...}" location="fastboot.vdi" format="VDI" type="Readonly" />
     -         <HardDisk uuid="{...}" location="Root.vhd" format="VHD" type="Readonly"/>
     +         <HardDisk uuid="{...}" location="fastboot.vdi" format="VDI" type="Normal" />
     +         <HardDisk uuid="{...}" location="Root.vhd" format="VHD" type="Normal"/>
     ```
   - Save the file.

3. **Modify the `.bstk` file:**
   - Open **`Rvc64.bstk`** (or your instance's `.bstk` file) with a text editor.
   - Repeat the same change: set `fastboot.vdi` and `Root.vhd` to **`type="Normal"`**.
   - Save the file.

### Step 4: Install Kitsune Mask

1. Download the **[Kitsune Mask](https://github.com/1q23lyc45/KitsuneMagisk/releases)** APK file.

2. Launch the target instance from the BlueStacks/MSI Multi-Instance Manager and install the APK.

3. Open the Kitsune Mask application.

4. **Root using Kitsune Mask:**
   - In the app, select the **Install** option.
   - Tap **Next**.
   - Select the **Direct Install to /system** option.

   > **Note:** If this option is missing, completely close and reopen the Kitsune Mask app inside the emulator. This usually resolves the issue.

5. Let the installation complete, then **close the BlueStacks emulator completely**.

6. **Revert Configuration Changes:**
   - Open **`bluestacks.conf`** again (from Step 2).
   - Change **`bst.instance.Rvc64.enable_root_access="1"`** back to **`"0"`**.
   - **Crucially**, also ensure **`bst.feature.rooting="1"`** is changed back to **`"0"`**.
   - Save the file. You must leave the R/W changes from Step 3 as `type="Normal"`.

7. **Done!** Launch the instance. Kitsune Mask should be installed, and root access will work.

</details>

<details>
<summary><h2>Troubleshooting</h2></summary>

### Getting "Android system doesn't meet security" popup?

**You're not alone!** This started happening with BlueStacks version 5.22 (released October 2025).

#### What's Happening?

When you enable root access OR read/write permissions in BlueStacks 5.22+:
- Shows security warning: *"Android system doesn't meet security and will be shutdown"*

**Root Cause:** Google replaced SafetyNet with Play Integrity API in January 2025. BlueStacks 5.22 now actively checks for modifications and blocks startup.

#### How to Fix It

<details>
<summary><b>Downgrade to BlueStacks 5.21</b></summary>

1. **Backup Your Data**
   - Export any important app data/saves from BlueStacks

2. **Completely Uninstall BlueStacks**
   - Download [BSTCleaner](https://support.bluestacks.com/hc/en-us/articles/360057724751) from official BlueStacks support
   - Run it to completely remove all BlueStacks files

3. **Install BlueStacks 5.21**
   - Download from [Uptodown Archive](https://bluestacks-app-player.en.uptodown.com/windows/versions)
   - Look for version **5.21.x.xxxx** (January 2025)
   - Install normally

4. **Apply This Rooting Guide**
   - Follow the normal steps in this README
   - Everything should work as documented!

Use [BlueStacks-Root-GUI](https://github.com/RobThePCGuy/BlueStacks-Root-GUI) to quickly toggle root between instances.

</details>

#### Version Compatibility

| BlueStacks Version | Root Working? | Notes |
|-------------------|---------------|-------|
| 5.20.x | Yes | Fully compatible |
| 5.21.x | Yes | Last confirmed working version |
| 5.22.0.1102+ | No | Play Integrity enforcement (Oct 2025) |

**Tracking:** See [Issue #11](https://github.com/RobThePCGuy/Root-Bluestacks-with-Kitsune-Mask/issues/11) for community updates and potential workarounds.

---

### Kitsune Mask Installation Issues

- **Problem:** Kitsune Mask fails to install, or the "Direct Install to /system" option is missing.
- **Solution:** This almost always means the R/W changes in Step 3 were not done correctly, or BlueStacks was not fully closed before making the changes. Double-check that `fastboot.vdi` and `Root.vhd` are set to `type="Normal"` in both the `.bstk.in` and `.bstk` files.

### "Permission Denied" when saving files

- **Problem:** You cannot save `bluestacks.conf` or other files.
- **Solution:** You must open your text editor (like Notepad) **as an administrator**. Right-click the editor's icon and select "Run as administrator" before opening the file.

</details>

<details>
<summary><h2>FAQ - Frequently Asked Questions</h2></summary>

**Q: I can't find the `C:\ProgramData` folder!**

**A:** This folder is hidden by default in Windows. In File Explorer, go to the **View** tab and check the box for **Hidden items**.

**Q: This all seems terribly difficult; isn't there a better way?**

**A:** Yes! The manual steps are here for transparency, but for a much easier process, use my **[BlueStacks-Root-GUI](https://github.com/RobThePCGuy/BlueStacks-Root-GUI)** tool. It handles all the configuration file editing with simple buttons.

**Q: Can I reverse this rooting process?**

**A:** Yes. In the GUI, simply toggle Root off. Manually, change the values in `bluestacks.conf` back to `"0"` and uninstall the Kitsune Mask app from the instance.

</details>

---

**If this guide has helped you, please consider leaving a star on the repository!** It helps others discover this guide and motivates further improvements.

[GitHub Repository](https://github.com/RobThePCGuy/Root-Bluestacks-with-Kitsune-Mask)
