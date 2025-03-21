# Root BlueStacks 5+ Rooting Guide (2025 Edition) with Kitsune Mask 🦊

[![GitHub Repo Stars](https://img.shields.io/github/stars/RobThePCGuy/Root-Bluestacks-with-Kitsune-Mask?style=social)](https://github.com/RobThePCGuy/Root-Bluestacks-with-Kitsune-Mask)
[![YouTube Video Views](https://img.shields.io/youtube/views/eRXeasi6GQQ?style=social)](https://youtu.be/eRXeasi6GQQ)
[![Last Updated](https://img.shields.io/github/last-commit/RobThePCGuy/Root-Bluestacks-with-Kitsune-Mask)](https://github.com/RobThePCGuy/Root-Bluestacks-with-Kitsune-Mask/commits/main)

**Root your BlueStacks 5+ emulator effortlessly using Kitsune Mask (formerly Magisk Delta)!** This guide provides a streamlined approach to granting root access to your BlueStacks instance, allowing you to run applications that require root privileges. No external tools or complex scripts are necessary – just your PC, Notepad, and Kitsune Mask!

[![Watch the Tutorial on YouTube](https://github.com/user-attachments/assets/d73e49bf-68fb-4b51-99eb-2b442d1be7cc)](https://youtu.be/eRXeasi6GQQ)

> [!NOTE]
> **All-in-One Solution:**
>
> Root BlueStacks 5+ using just your *PC*, *Kitsune Mask*, and *Notepad*. **No external tools needed!** For a complete walkthrough, watch the video tutorial above or visit my [YouTube Channel](https://www.youtube.com/@RobThePCGuy).

> [!NOTE]
> **BlueStacks Root GUI**
> My Python based portable application allows you to toggle root access and enable read/write (R/W) permissions for your BlueStacks instances. It automatically detects both master and cloned instances, eliminating the need to manually edit the configuration files I describe below.
>
> Check it out at **[BlueStacks-Root-GUI](https://github.com/RobThePCGuy/BlueStacks-Root-GUI)** and please leave feedback if you encounter any issues.

> [!IMPORTANT]
> **Tested BlueStacks Version:**
>
> This guide is verified to work on **BlueStacks App Player `5.22.0.1102`** and supports Android 9, 11, and 13. This tutorial assumes you are using the master instance named **Rvc64** (Android 11).

> [!WARNING]
> **Understanding Kitsune Mask and BlueStacks Partitions:**
>
> Kitsune Mask is a systemless root tool designed for Android devices. However, BlueStacks partitions are initially read-only, which prevents a direct Kitsune Mask installation. This guide uses a simple configuration file edit (via Notepad) to temporarily enable read/write permissions, allowing Kitsune Mask to be installed on the system partition. **No external scripts or tools are required for this permission change.**

## 🚀 Prerequisites

Before you begin, ensure you have the following:

- ✅ **PC with Administrator Rights:** You need administrative access to modify system files.
- 🦊 **Kitsune Mask APK:** Download the latest APK from the [KitsuneMagisk repository](https://github.com/1q23lyc45/KitsuneMagisk/releases) (recommended fork).
- 🔄 **Fresh BlueStacks Installation (Recommended):** For the most consistent results, start with a clean installation of [BlueStacks](https://www.bluestacks.com/). This minimizes potential conflicts during the rooting process.

## ✨ Expected Outcome

Upon successful completion of this guide, your BlueStacks instance will be fully rooted with Kitsune Mask, granting you the ability to run applications that require root privileges.

## 📝 Summary of Steps

Here's a quick overview of the rooting process. See the "Detailed Steps" section below for a comprehensive walkthrough:

- [x] **Step 1: Modify BlueStacks Configuration:** Edit `bluestacks.conf` to enable root access.
- [x] **Step 2: Modify Instance Files:** Adjust settings in instance configuration files to allow read/write access to system partitions.
- [x] **Step 3: Install Kitsune Mask:** Install Kitsune Mask directly to the `/system` partition and revert configuration changes.

---

<details>
<summary><h2>🛠️ Detailed Steps</h2></summary>

**Instance Naming Convention:**
This tutorial uses the following naming conventions for master instances:

```
Master Instances:
  - Tiramisu64  = Android 13 (beta)
  - Rvc64       = Android 11
  - Pie64       = Android 9
```

*Adapt the instance names according to your BlueStacks setup.*

### Step 1: Prepare:
1. **Fully Uninstall BlueStacks:**
   - Use the official tool to completely **[uninstall all previous BlueStacks installations](https://support.bluestacks.com/hc/en-us/articles/360057724751-How-to-uninstall-BlueStacks-5-BlueStacks-X-and-BlueStacks-Services-completely-from-your-PC)**.
   - Download and install the latest BlueStacks version from the official website: **[BlueStacks](https://www.bluestacks.com/)**.

### Step 2: Modify BlueStacks Config:
1. **Locate the Main Configuration File:**
   Navigate to **`C:\ProgramData\BlueStacks_nxt`**.

2. **Edit with Notepad:**
   Open **`bluestacks.conf`** using your preferred text editor.

3. **Modify Configuration Values:**
   - Change **`bst.feature.rooting="0"`** to **`bst.feature.rooting="1"`**.
   - Change **`bst.instance.Rvc64.enable_root_access="0"`** to **`bst.instance.Rvc64.enable_root_access="1"`**.
> **Note:** If you are using a different instance (e.g., Pie64 or Tiramisu64), modify the [InstanceName] for all the lines similar to this: `bst.instance.[InstanceName].enable_root_access`.

4. **Save Changes:**
   Save the modified **`bluestacks.conf`** file.

### Step 3: Enable R/W:

1. **Navigate to the Master Instance Folder:**
   Go to **`C:\ProgramData\BlueStacks_nxt\Engine\Rvc64`** (or your instance folder, e.g., `Pie64` or `Tiramisu64`).
> **Note:** Cloned instances do not make a copy of the **`Android.bstk.in`** file; it will always be found within the master instance directory.
2. Open **`Android.bstk.in`** with Notepad (or your text editor).
3. **Change Partition Permissions:**
   - For the **`location="fastboot.vdi"`** and **`location="Root.vhd"`** entries, change the attribute from **`type="Readonly"`** to **`type="Normal"`**.
   - **Example:**
     ```diff
     -       location="fastboot.vdi" format="VDI" type="Readonly" />
     -       location="Root.vhd" format="VHD" type="Readonly"/>

     +       location="fastboot.vdi" format="VDI" type="Normal" />
     +       location="Root.vhd" format="VHD" type="Normal"/>
     ```
   - Save the file.

> **Note:** If you are rooting the master instance **`Rvc64`**, then this file will be located in the master instance folder **(`C:\ProgramData\BlueStacks_nxt\Engine\Rvc64`)**.
> **Note:** If you have cloned (or copied) the master instance, the folder and file might be named something like `Rvc64_1`. In this case, replace the instance name in the instructions accordingly.
4. Open **`Rvc64.bstk`** with Notepad (or your text editor).
5. **Change Partition Permissions:**
   - For the **`location="fastboot.vdi"`** and **`location="Root.vhd"`** entries, change the attribute from **`type="Readonly"`** to **`type="Normal"`**.
   - **Example:**
     ```diff
     -       location="fastboot.vdi" format="VDI" type="Readonly" />
     -       location="Root.vhd" format="VHD" type="Readonly"/>

     +       location="fastboot.vdi" format="VDI" type="Normal" />
     +       location="Root.vhd" format="VHD" type="Normal"/>
     ```
   - Save the file.

### Step 4: Install Kitsune Mask

1. Download the **[Kitsune Mask](https://github.com/1q23lyc45/KitsuneMagisk/releases)** apk file.
2. Launch the instance from the Multi-Instance Manager and install the apk.
3. You should see the Kitsune Mask application; click on it to run.
4. Root using **Kitsune Mask**:
   - Once open, look to the top under the Kitsune Mask section and select the **Install** option.
   - At the top right, tap the **Next** link to proceed.
   - Select the **Direct Install to /system** option.

> **Note:** If the **Direct Install to /system** option is missing, do not select **Direct Install**.
>
> Completely close and reopen the Kitsune Mask app. This usually resolves the issue.

5. Click Next and watch the install log for any errors.
6. Allow Kitsune Mask to finish installing, then close the BlueStacks emulator.
7. Open up the Main Configuration File: **`bluestacks.conf`**.
   - Change the value for **`bst.instance.Rvc64.enable_root_access="1"` back to `bst.instance.Rvc64.enable_root_access="0"` (or the corresponding line for your instance, e.g., Pie64 or Tiramisu64).
> **Note:** The file will have automatically changed the value for **`bst.feature.rooting=`** back to **`"0"`**, this is normal and an important part of the process
   - Save the file.

</details>

<details>
<summary><h2>Troubleshooting 🐛</h2></summary>

- **Kitsune Mask Installation Issues:**
  - **Problem:** Kitsune Mask fails to install or encounters errors.
  - **Solution:**
	- **Fully Uninstall BlueStacks:**
	  - Use the official tool to completely **[uninstall all previous BlueStacks installations](https://support.bluestacks.com/hc/en-us/articles/360057724751-How-to-uninstall-BlueStacks-5-BlueStacks-X-and-BlueStacks-Services-completely-from-your-PC)**.
	  - Download and install the latest BlueStacks version from the official website: **[BlueStacks](https://www.bluestacks.com/)**.

- **Kitsune Mask App Crashing or Not Opening:**
  - **Problem:** The Kitsune Mask app crashes or fails to launch.
  - **Solution:** Reinstall the Kitsune Mask APK from the [KitsuneMagisk repository](https://github.com/1q23lyc45/KitsuneMagisk/releases) and restart your BlueStacks instance.

</details>

<details>
<summary><h2>❓ FAQ - Frequently Asked Questions</h2></summary>

**Q: I can't find the `bluestacks.conf` or instance configuration files!**
**A:**
1. **Administrative Access:** Verify that you are logged in with an account that has administrator privileges.
2. **Correct Directory:** Double-check that you are navigating to `C:\ProgramData\BlueStacks_nxt\`. Also, ensure that hidden folders are visible in your file explorer settings.

**Q: This all seems terribly difficult; isn't there a better way?**
**A:** Yes, there is!
- Try using [BlueStacks-Root-GUI](https://github.com/RobThePCGuy/BlueStacks-Root-GUI), which lets you change the configuration values with simple checkboxes. After that, simply follow along with the Kitsune Mask installation.

**Q: Can I reverse this rooting process?**
**A:** Yes, the process is reversible.
1. **Revert Configuration Changes:** Undo the edits made to `bluestacks.conf` (change the `1`s back to `0`s).
2. **Uninstall Kitsune Mask:** Remove the Kitsune Mask app from within your BlueStacks instance.

</details>

---

🙏 **If this guide has helped you root your BlueStacks instance, please consider leaving a star on the repository!** ⭐ It helps others discover this guide and motivates further improvements.

[GitHub Repository](https://github.com/RobThePCGuy/Root-Bluestacks-with-Kitsune-Mask)
