# Root BlueStacks 5+ Rooting Guide (2025 Edition) with Kitsune Magisk 🦊

[![GitHub Repo Stars](https://img.shields.io/github/stars/RobThePCGuy/Root-Bluestacks-with-Kitsune-Mask?style=social)](https://github.com/RobThePCGuy/Root-Bluestacks-with-Kitsune-Mask)
[![YouTube Video Views](https://img.shields.io/youtube/views/eRXeasi6GQQ?style=social)](https://youtu.be/eRXeasi6GQQ)
[![Last Updated](https://img.shields.io/github/last-commit/RobThePCGuy/Root-Bluestacks-with-Kitsune-Mask)](https://github.com/RobThePCGuy/Root-Bluestacks-with-Kitsune-Mask/commits/main)

**Root your BlueStacks 5+ emulator effortlessly using Kitsune Magisk (formerly Magisk Delta)!** This guide provides a streamlined approach to granting root access to your BlueStacks instance, allowing you to run powerful root-requiring applications.  No external tools or complex scripts are necessary – just your PC, Notepad, and Magisk!

[![Watch the Tutorial on YouTube](https://github.com/user-attachments/assets/d73e49bf-68fb-4b51-99eb-2b442d1be7cc)](https://youtu.be/eRXeasi6GQQ)

> [!NOTE]
> **All-in-One Solution:**
>
> Root BlueStacks 5+ using just your *PC*, *Magisk* (Kitsune Magisk), and *Notepad*.  **No external tools needed!** For a complete walkthrough, watch the video tutorial above or visit my [YouTube Channel](https://www.youtube.com/@RobThePCGuy).

> [!IMPORTANT]
> **Kitsune Magisk Fork Recommended!**
>
> **January 26, 2025 Update:**  Due to inactivity in the original Kitsune Mask project, users may encounter issues with newer modules.  Thanks to [@DaRandomCube](https://github.com/DaRandomCube)'s observation, we now recommend using the actively maintained fork: [**KitsuneMagisk by 1q23lyc45**](https://github.com/1q23lyc45/KitsuneMagisk).

> [!NOTE]
> **BlueStacks Root GUI - New Project!**
>
> *Simplify* *Steps* **1** and **2** below by using my python based *'Root'*-**GUI**, which allows you to toggle R/W and Root in a simple GUI with no need to edit **ANY** files! Check it out [BlueStacks-Root-GUI](https://github.com/RobThePCGuy/BlueStacks-Root-GUI) and please leave feedback with fixes or issues if found.

> [!IMPORTANT]
> **Tested BlueStacks Version:**
>
> This guide is verified to work on **BlueStacks App Player `5.22.0.1102`**.  While it may work on other versions, this is the tested and recommended version for this tutorial.

> [!WARNING]
> **Understanding Magisk and BlueStacks Partitions:**
>
> Magisk, a systemless root tool, is designed for Android devices. However, BlueStacks partitions are initially read-only, preventing direct Magisk installation. This guide utilizes a simple configuration file edit (using Notepad) to temporarily enable read/write permissions, allowing Magisk (Kitsune Magisk) to be installed on the system partition.  **No external scripts or tools are required for this permission change.**

## 🚀 Prerequisites

Before you begin, ensure you have the following:

*   ✅ **PC with Administrator Rights:** You'll need administrative access to modify system files.
*   🦊 **Kitsune Magisk APK:** Download the latest APK from the [KitsuneMagisk repository](https://github.com/1q23lyc45/KitsuneMagisk/releases) (recommended fork).
*   🔄 **Fresh BlueStacks Installation (Recommended):**  For the most consistent results, it's advised to start with a clean installation of [BlueStacks](https://www.bluestacks.com/).  This minimizes potential conflicts and ensures a smooth process.

## ✨ Expected Outcome

Upon successful completion of this guide, your BlueStacks instance will be fully rooted with Kitsune Magisk, granting you the ability to run applications that require root privileges.

## 📝 Summary of Steps

Here's a quick overview of the rooting process.  See the "Detailed Steps" section below for a comprehensive walkthrough.

- [x] **Step 1: Modify BlueStacks Configuration:** Edit `bluestacks.conf` to enable root access.
- [x] **Step 2: Modify Instance Files:** Adjust settings in instance configuration files to allow read/write access to system partitions.
- [x] **Step 3: Install Kitsune Magisk:** Install Kitsune Magisk directly to the `/system` partition and revert configuration changes.

---

<details>
<summary><h2> 🛠️ Detailed Steps</h2></summary>

**Clean BlueStacks Installation is Key!**
>
> For optimal results, **[uninstall all previous BlueStacks installations](https://support.bluestacks.com/hc/en-us/articles/360057724751-How-to-uninstall-BlueStacks-5-BlueStacks-X-and-BlueStacks-Services-completely-from-your-PC)** and perform a fresh install of the latest version.  This significantly reduces the chance of encountering issues during the rooting process.

**Instance Naming Convention:**
>
> This tutorial uses the following naming conventions for Master Instances:

```
Master Instances:
  - Rvc64 = Android 11
  - Pie64 = Android 9
```

**Adapt instance names according to your BlueStacks setup.**

### Step 1: Modify BlueStacks Configuration

1.  **Locate `bluestacks.conf`:** Navigate to `C:\ProgramData\BlueStacks_nxt\bluestacks.conf`.
2.  **Open with Notepad:** Open the `bluestacks.conf` file using your preferred text editor.
3.  **Modify Configuration Values:**
    *   Change `bst.feature.rooting="0"` to `bst.feature.rooting="1"`
    *   Change `bst.instance.Rvc64.enable_root_access="0"` to `bst.instance.Rvc64.enable_root_access="1"`
        *   **Note:** If you are using a different instance (e.g., Pie64), modify the corresponding `bst.instance.[InstanceName].enable_root_access` line.
4.  **Save Changes:** Save the modified `bluestacks.conf` file.

### Step 2: Modify Instance Files

1.  **Navigate to Instance Folders:** Go to `C:\ProgramData\BlueStacks_nxt\Engine\Rvc64\` (or your instance folder, e.g., `Pie64`).
2.  **Modify `Android.bstk.in` and `Rvc64.bstk`:** Open both `Android.bstk.in` and `Rvc64.bstk` files with Notepad (or your text editor).
3.  **Change Partition Permissions:** In both files, locate the sections for `"fastboot.vdi"` and `"Root.vhd"`.
    *   Change the line containing `"type":"Readonly"` to `"type":"Normal"` for both `"fastboot.vdi"` and `"Root.vhd"`.
    *   **Example (within the file):**
        ```diff
        -       "prop": {
        -               "type": "Readonly"
        -       },
        +       "prop": {
        +               "type": "Normal"
        +       },
        ```
4.  **Save Changes:** Save both `Android.bstk.in` and `Rvc64.bstk` files.

### Step 3: Install Kitsune Magisk

1.  **Launch BlueStacks Instance:** Start the BlueStacks instance you are rooting (e.g., Rvc64).
2.  **Install Kitsune Magisk APK:** Install the downloaded Kitsune Magisk APK within your BlueStacks instance.
3.  **Open Kitsune Magisk App:** Launch the Kitsune Magisk application.
4.  **Install Magisk (Direct Install to System):**
    *   Select the "Install" at the top under the "Magisk" field in the Kitsune Magisk app.
    *   Select the Next link to the right.
    *   **Crucially, select "Direct Install into system partition"** from the installation options. **Do not choose just "Direct Install".**

    **"Direct Install into system partition" Option Missing?**
    >
    > If you do not see the "Direct Install into system partition" option, **completely close and reopen the Kitsune Magisk app.** This usually resolves the issue.
5.  **Complete Installation and Close Emulator:** Allow Kitsune Magisk to complete the installation process. Once finished, **completely close the BlueStacks emulator.**
6.  **Revert `bluestacks.conf` Edits:**
    *   Re-open `C:\ProgramData\BlueStacks_nxt\bluestacks.conf` with Notepad.
    *   **Undo the changes from Step 1:**
        *   Change `bst.feature.rooting="1"` back to `bst.feature.rooting="0"`
        *   Change `bst.instance.Rvc64.enable_root_access="1"` back to `bst.instance.Rvc64.enable_root_access="0"`
    *   Save the modified `bluestacks.conf` file.

</details>

<details>
<summary><h2> Troubleshooting 🐛</h2></summary>

*   **Magisk Installation Issues:**
    *   **Problem:** Kitsune Magisk fails to install or encounters errors.
    *   **Solution:**  Ensure you performed a **fresh install** of BlueStacks as recommended.  If issues persist, thoroughly uninstall BlueStacks and reinstall, strictly following the steps in my [YouTube guide](https://youtu.be/eRXeasi6GQQ).
*   **Kitsune Magisk App Crashing or Not Opening:**
    *   **Problem:** The Kitsune Magisk app crashes upon opening or fails to launch.
    *   **Solution:** Reinstall the Kitsune Magisk APK, ensuring you have downloaded the latest version from the [KitsuneMagisk repository](https://github.com/1q23lyc45/KitsuneMagisk/releases).  Restart your BlueStacks instance after reinstalling.

</details>

<details>
<summary><h2> ❓ FAQ - Frequently Asked Questions</h2></summary>

**Q: I can't find the `bluestacks.conf` or instance configuration files!**

**A:** Files may require an Administrator.
  1. **Administrative Access:** Verify that you are logged in to your PC with an account that has administrative privileges. File access might be restricted without admin rights.
  2. **Correct Directory:** Double-check that you are navigating to the correct directory: `C:\ProgramData\BlueStacks_nxt\`.  Ensure hidden folders are visible in your file explorer settings.

**Q: This all seems terribly difficult, isn't there a better way?**

**A:** Yes, there is!
  1. **[BlueStacks-Root-GUI](https://github.com/RobThePCGuy/BlueStacks-Root-GUI)** allows you to change the config values with simple check boxes. Then all you need to do it follow along with the Magisk install.

**Q: Can I reverse this rooting process?**

**A:** Yes, the rooting process is reversible. To unroot:
  1.  **Revert Configuration Changes:** Undo the edits made to `bluestacks.conf` (change the `1`s back to `0`s).
  2.  **Uninstall Kitsune Magisk:** Uninstall the Kitsune Magisk app from within your BlueStacks instance.

</details>

---

🙏 **If this guide has helped you root your BlueStacks instance, please consider leaving a star on the repository!** ⭐ It helps others discover this guide and motivates further improvements.

[GitHub Repository](https://github.com/RobThePCGuy/Root-Bluestacks-with-Kitsune-Mask)

---
