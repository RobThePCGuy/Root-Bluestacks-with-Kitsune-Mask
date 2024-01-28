# Installing Kitsune Mask (aka Magisk Delta) on Bluestacks 5

![pic](https://github.com/ZeroOneZero/Root-Bluestacks-with-Kitsune-Mask/assets/10876982/0d6d0f83-3710-428a-b054-dfe3f73e9b79)

> [!IMPORTANT]
> Tested on BlueStacks App Player ```5.20.10.1003``` (Android 11)

> [!NOTE]
> Download the offical installer from [BlueStacks website](https://www.bluestacks.com/).

> If you want the offline image of Android 11 bundled with the installer, run this command in Windows Terminal or PowerShell; otherwise, simply run the installer:

```.\"BlueStacksInstaller*.exe" --defaultImageName Rvc64 --imageToLaunch Rvc64```

> [!WARNING]
> In BlueStacks, Magisk installation fails because the root partition is mounted as read-only. However, modifying values in certain files allows Magisk to install itself to the /system partition without external tools.

## Summary of Steps:

1. Edit BlueStacks Config: Open bluestacks.conf and enable rooting and root access for your Android instance.

2. Modify Instance Files: In the BlueStacks Engine folder, change specific settings in the instance files from "ReadOnly" to "Normal" for both the system and fastboot files. Apply these changes for both master and any cloned instances.

3. Install Kitsune Mask to /system and revert all changes in the bluestacks.conf

## Requirements:
- [Kitsune Mask](https://github.com/HuskyDG/magisk-files/blob/main/README.md) (aka Magisk Delta)

### Step 1: Modify BlueStacks Configuration

1. Open ```C:\ProgramData\BlueStacks_nxt\bluestacks.conf```

2. Change the following settings:
	- ```bst.feature.rooting="0"``` to ```bst.feature.rooting="1"```
	- ```bst.instance.Rvc64.enable_root_access="0"``` to ```bst.instance.Rvc64.enable_root_access="1"```

> [!WARNING]
> If you have created additional instances (clones), ensure to change both the master and cloned instances to ```enable_root_access="1"```.

- **Master Instances:**
	- ```Rvc64``` = Android 11
	- ```Pie64``` = Android 9
	- ```Nougat64``` = Android Nougat
  
- **Cloned Instances:**
	- ```Rvc64_1``` = First Clone of Android 11
	- ```Pie64_1``` = First Clone of Android 9
	- ```Nougat64_1``` = First Clone of Nougat

### Step 2: Modify Instance Files

1. Navigate to ```C:\ProgramData\BlueStacks_nxt\Engine```. Open the folder corresponding to the Master Instance you modified in **bluestacks.conf**. For example, for the **Rvc64** instance, open ```C:\ProgramData\BlueStacks_nxt\Engine\Rvc64```.

2. Within this folder, locate and modify the following files:
	- ```Android.bstk.in```
	- ```Rvc64.bstk```

2. In each file make the following changes:
	- Change ```location="Root.vhd" format="VHD" type="ReadOnly"/>``` to ```location="Root.vhd" format="VHD" type="Normal"/>```
	- Change ```location="fastboot.vdi" format="VHD" type="ReadOnly"/>``` to ```location="fastboot.vdi" format="VHD" type="Normal"/>```

4. Return to ```C:\ProgramData\BlueStacks_nxt\Engine``` and enter the directory corresponding to any cloned instances you modified in **bluestacks.conf**. For example, the first clone of **Rvc64** is ```C:\ProgramData\BlueStacks_nxt\Engine\Rvc64_1```.

5. Find and modify the file that matches the instance name (e.g., ```Rvc64_1.bstk```), applying the same changes as above:
	- Change ```location="Root.vhd" format="VHD" type="ReadOnly"/>``` to ```location="Root.vhd" format="VHD" type="Normal"/>```
	- Change ```location="fastboot.vdi" format="VHD" type="ReadOnly"/>``` to ```location="fastboot.vdi" format="VHD" type="Normal"/>```

6. Save all the changes.

### Step 3: Install Kitsune Mask

1. Launch the instance and install Kitsune Mask.

2. In Kitsune Mask, select the **Install** option under the Magisk field. Use the **Direct Install into system partition** option (not just "Direct Install"). If this option is not visible, close and reopen the Kitsune Mask app.

3. After installation, close the emulator.

4. Revert all changes in the **bluestacks.conf** file.
