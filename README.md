# Rooting Bluestacks 5+ with Kitsune Mask (aka Magisk Delta)
## 2025 Edition

> [!NOTE]
> Only a *PC*, *Magisk*, and *Notepad* are required to *root* the latest version of BlueStacks; ***no external tools are needed***.
> These instructions and more can be found on my [YouTube](https://www.youtube.com/@RobThePCGuy) channel, or simply click the picture below to go straight to it.
>
> To bring in the new year, I have been working on a Python application that simplifies the process of the initial config editing. The new repo is located at [BlueStacks-Root-GUI](https://github.com/RobThePCGuy/BlueStacks-Root-GUI).

[![YouTube](https://github.com/RobThePCGuy/Root-Bluestacks-with-Kitsune-Mask/assets/10876982/a9ad2b20-9faa-4c73-850e-cf03ad4d4a71)](https://youtu.be/eRXeasi6GQQ)

> [!IMPORTANT]
> Tested on BlueStacks App Player `5.21.650.1063`

> [!WARNING]
Magisk is a systemless root tool that can be installed on most Android devices, but it cannot be installed in BlueStacks because the partitions are set to read-only by default. To change the permissions, you must edit a text file on your computer. No external scripts or tools are needed. After you have completed the editing, BlueStacks will have read/write permissions, and you will be able to install Magisk on the system partition.

## Prerequisites
- A PC with administrative access.
- [Kitsune Mask](https://github.com/HuskyDG/magisk-files/blob/main/README.md) (Magisk Delta) apk.
- A fresh install of [BlueStacks](https://www.bluestacks.com/) is recommended to ensure consistency in following these steps.

## Expected Outcome
After completing this tutorial, your instance of BlueStacks will be rooted, allowing you to run apps that require root access.

## Summary of Steps
1. **Modify BlueStacks Configuration:** Open `bluestacks.conf` to enable rooting and root access for your Android instance.
2. **Modify Instance Files:** In the BlueStacks Engine folder, adjust settings for the Master instance, changing `"ReadOnly"` to `"Normal"` for both `fastboot.vdi` and `Root.vhd`.
3. **Install Kitsune Mask:** Directly install Kitsune Mask into `/system`, then revert all changes in `bluestacks.conf`.

---

## Detailed Steps
I can't stress this enough: For this to work, you must remove all traces of BlueStacks from your computer and then install the latest version. If you don't, the rooting process won't work. The full steps for installing and rooting are in my YouTube video.

> [!NOTE]
> The following naming convention is used in this tutorial:

```
Master Instances:
  - Rvc64 = Android 11
  - Pie64 = Android 9
```

### Step 1: Modify BlueStacks Configuration
- Modify the following settings in `C:\ProgramData\BlueStacks_nxt\bluestacks.conf`
  - `bst.feature.rooting="0"` to `bst.feature.rooting="1"`
  - `bst.instance.Rvc64.enable_root_access="0"` to `bst.instance.Rvc64.enable_root_access="1"`

### Step 2: Modify Instance Files
- Modify the following settings in `C:\ProgramData\BlueStacks_nxt\Engine\Rvc64\Android.bstk.in` and in `C:\ProgramData\BlueStacks_nxt\Engine\Rvc64\Rvc64.bstk`.
- Change the type for `"fastboot.vdi"` and `"Root.vhd"` from `"Readonly"` to `"Normal"`.
- Save all the changes.

### Step 3: Install Kitsune Mask
- Launch the instance and install the Kitsune Mask apk.
- In Kitsune Mask, select the Install option under the Magisk field.
- Use the Direct Install into system partition option (not just "Direct Install").

> [!WARNING]
> If this option is not visible, close and reopen the Kitsune Mask app.

- After installation, close the emulator.
- Undo all the edits we did above in `C:\ProgramData\BlueStacks_nxt\bluestacks.conf` (change the 1's back to 0's).

## Troubleshooting
- **Magisk not installing:** Uninstall BlueStacks and reinstall following my YouTube guide.
- **Kitsune Mask fails to open:** Reinstall Kitsune Mask and ensure it's the latest version.

## FAQ
**Q: What if I can't find the configuration files mentioned?**

A: Ensure that you have administrative access and that you are looking in the correct directory for your BlueStacks installation.

**Q: Can this rooting process be reversed?**

A: Yes, simply revert the changes made to the configuration files and uninstall Kitsune Mask.

---

If this guide helped, please leave a star on GitHub!

---
