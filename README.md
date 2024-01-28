# Installing Kitsune Mask (aka Magisk Delta) on Bluestacks 5

![pic](https://github.com/ZeroOneZero/Root-Bluestacks-with-Kitsune-Mask/assets/10876982/0d6d0f83-3710-428a-b054-dfe3f73e9b79)

> [!IMPORTANT]
> Tested on BlueStacks App Player ```5.20.10.1003``` (Android 11)

> [!WARNING]
> In BlueStacks, Magisk installation fails because the root partition is mounted as read-only. However, modifying values in certain files allows Magisk to install itself to the /system partition without external tools.

## Summary of Steps:

1. Open **bluestacks.conf** and enable rooting and root access for your Android instance.

2. In the BlueStacks Engine folder, modify settings in two files for the Master instance, changing "ReadOnly" to "Normal" for both the **fastboot.vdi** and **Root.vhd**. 

3. Direct install of Kitsune Mask into **/system**. Then revert all changes in **bluestacks.conf**.

## Requirements:
- [Kitsune Mask](https://github.com/HuskyDG/magisk-files/blob/main/README.md) (aka Magisk Delta)

> A [fresh install](https://www.bluestacks.com/) of BlueStacks is recommended for consistency. Any alterations can affect the steps below.

---

### Step 1: Modify BlueStacks Configuration

1. Open the configuration file at ```C:\ProgramData\BlueStacks_nxt\bluestacks.conf```.

2. In this file, modify the following settings by changing their values from **"0"** to **"1"**:
   - ```bst.feature.rooting="0"``` to ```bst.feature.rooting="1"```

   - ```bst.instance.Rvc64.enable_root_access="0"``` to ```bst.instance.Rvc64.enable_root_access="1"```

### Step 2: Modify Instance Files

1. Navigate to ```C:\ProgramData\BlueStacks_nxt\Engine```.

2. Open the folder for the Master instance using the below info for reference:

```
Master Instances:
  - Rvc64 = Android 11
  - Pie64 = Android 9
  - Nougat64 = Android Nougat
```

> [!NOTE]
> Since this guide is about Android 11, the folder below is correct:
 
```C:\ProgramData\BlueStacks_nxt\Engine\Rvc64```

3. Open the following two files and change the data as shown:
	- ```C:\ProgramData\BlueStacks_nxt\Engine\Rvc64\Android.bstk.in```
		- For ```"fastboot.vdi"```, change the type from ```"Readonly"``` to ```"Normal"```.

	- ```C:\ProgramData\BlueStacks_nxt\Engine\Rvc64\Rvc64.bstk```
 		- For ```"Root.vhd"```, change the type from ```"Readonly"``` to ```"Normal"```.

4. Save all the changes.

### Step 3: Install Kitsune Mask

1. Launch the instance and install Kitsune Mask.

2. In Kitsune Mask, select the Install option under the Magisk field.

3. Use the Direct Install into system partition option (not just "Direct Install").

> [!WARNING]
> If this option is not visible, close and reopen the Kitsune Mask app.

4. After installation, close the emulator.

5. Undo all the edits in **bluestacks.conf** (change the 1's back to 0's).

---
