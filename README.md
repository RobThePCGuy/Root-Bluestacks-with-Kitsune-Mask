# Root BlueStacks 5+ Rooting Guide (2026 Edition) with Kitsune Mask

[![GitHub Repo Stars](https://img.shields.io/github/stars/RobThePCGuy/Root-Bluestacks-with-Kitsune-Mask?style=social)](https://github.com/RobThePCGuy/Root-Bluestacks-with-Kitsune-Mask)
[![YouTube Video Views](https://img.shields.io/youtube/views/eRXeasi6GQQ?style=social)](https://youtu.be/eRXeasi6GQQ)
[![Last Updated](https://img.shields.io/github/last-commit/RobThePCGuy/Root-Bluestacks-with-Kitsune-Mask)](https://github.com/RobThePCGuy/Root-Bluestacks-with-Kitsune-Mask/commits/master)

Root your **BlueStacks 5+** or **MSI App Player** emulator so apps that require root work. This guide covers both the easy way (a one-click tool) and the fully manual way (Notepad only).

> [!IMPORTANT]
> **The "latest version can't be rooted" advice is out of date.** BlueStacks 5.22 added a disk-integrity check that shuts modified instances down with *"Android system doesn't meet security requirements."* You no longer have to downgrade to get around it — **[BlueStacks Root GUI](https://github.com/RobThePCGuy/BlueStacks-Root-GUI) patches that check out and roots the current build.** Confirmed working on **5.22.232.1002 / Android 13** — the current latest official BlueStacks build as of July 2026. The manual downgrade method below still works and needs no external tool, but it is no longer the *only* option.

---

## Pick Your Path

| You want… | Use | Needs the app? | BlueStacks version |
|---|---|---|---|
| **The easiest route, on any current version** | [Method A: BlueStacks Root GUI](#method-a-bluestacks-root-gui-recommended) | Yes (free, portable, open-source) | Any, including the latest 5.22.x |
| **No external tools, Notepad only** | [Method B: Manual downgrade](#method-b-manual-notepad-only-no-app) | No | **5.22.130.1019** (last build without the integrity check) |
| **Magisk-managed root: modules, Zygisk, hiding** | [Magisk Modules & Hiding](#magisk-modules--hiding-advanced) | Either, then extra steps | Any |

> [!WARNING]
> **Whichever path you pick, read [Stop Auto-Updates](#stop-auto-updates-do-this) first.** A background BlueStacks updater will quietly upgrade your install and undo everything — this is the single most common reason people's root "randomly stops working."

---

## Method A: BlueStacks Root GUI (Recommended)

A free, portable, open-source app that toggles root and read/write with buttons and works on the **latest** BlueStacks — no downgrade, no Notepad.

1. Download the latest `.exe` from **[BlueStacks-Root-GUI Releases](https://github.com/RobThePCGuy/BlueStacks-Root-GUI/releases)**.
2. Right-click it → **Run as administrator**.
3. Follow its README for the two-click flow (Patch Engine → Toggle Root). It auto-detects your instances and shows whether the engine is already patched.

That's the whole thing for app-level root. For Magisk modules/hiding on top, see [Magisk Modules & Hiding](#magisk-modules--hiding-advanced).

**Full app docs:** [BlueStacks-Root-GUI](https://github.com/RobThePCGuy/BlueStacks-Root-GUI).

---

## Method B: Manual (Notepad only, no app)

This roots by editing two config files and installing Kitsune Mask into `/system` — no external tools, just your PC, Notepad, and the Kitsune Mask APK.

> [!IMPORTANT]
> **The manual method requires BlueStacks `5.22.130.1019` or older.** Per [@AndnixSH](https://github.com/RobThePCGuy/Root-Bluestacks-with-Kitsune-Mask/issues/11), **5.22.130.1019 is the last build without the disk-integrity check**, so a modified `/system` boots normally. On `5.22.130.1020`+ the check refuses to boot a modified system — those builds *can* still be rooted, but only by patching the check out first, which is what the [app](#method-a-bluestacks-root-gui-recommended) does for you (or the [advanced hand-patch](#advanced-rooting-the-latest-by-hand-no-app)).

> [!NOTE]
> **Why install into `/system`?** Kitsune Mask (a Magisk Delta fork) is normally a *systemless* root tool that lives in the boot ramdisk. Emulators like BlueStacks have no traditional boot image, so it must be installed directly to the read-only `/system` partition. The Notepad edits below temporarily make that partition writable so the install can happen.

### Prerequisites

- **Administrator rights** — you'll edit files under `C:\ProgramData`.
- **Kitsune Mask APK** — download the pinned, hash-verified copy from **[this repo's Releases](https://github.com/RobThePCGuy/Root-Bluestacks-with-Kitsune-Mask/releases/tag/magisk-delta-kitsune-27.001)**. It's the exact `27.001` build confirmed working on BlueStacks this guide was written against, with a published **SHA-256** so you can verify you got the untampered file. (The original Kitsune repo is abandoned and third-party mirrors 404 or wrap the download in ads — this avoids both.) Kitsune Mask is a GPL-3.0 fork of Magisk Delta ([upstream: HuskyDG](https://github.com/HuskyDG/magisk-files)).
- **BlueStacks 5.22.130.1019** (or older) or MSI App Player — a fresh install gives the most consistent results.

### Instance naming

This guide uses master-instance names; adapt to yours:

```
Tiramisu64 = Android 13    Rvc64 = Android 11    Pie64 = Android 9
```

<details>
<summary><h3>Detailed Steps</h3></summary>

#### Step 1 — Prepare

1. **Uninstall any existing BlueStacks** with the official **[BlueStacks cleaner](https://support.bluestacks.com/hc/en-us/articles/360057724751-How-to-uninstall-BlueStacks-5-BlueStacks-X-and-BlueStacks-Services-completely-from-your-PC)**.
2. **Install [BlueStacks 5.22.130.1019](https://ak-build.bluestacks.com/public/app-player/windows/nxt/5.22.130.1019/03f0020b47ac3b5affd5d7ea53661c44/FullInstaller/x64/BlueStacksFullInstaller_5.22.130.1019_amd64_native.exe)** (or MSI App Player). Immediately do [Stop Auto-Updates](#stop-auto-updates-do-this) so it can't upgrade itself out from under you.

#### Step 2 — Enable root in `bluestacks.conf`

1. Open **`C:\ProgramData\BlueStacks_nxt\bluestacks.conf`** (MSI: `BlueStacks_msi5`) in Notepad **as administrator**.
2. Set these two lines (add them if missing), replacing `Rvc64` with your instance:
   - `bst.feature.rooting="1"`
   - `bst.instance.Rvc64.enable_root_access="1"`
3. Save.

#### Step 3 — Enable R/W on the instance disks

1. Go to **`C:\ProgramData\BlueStacks_nxt\Engine\Rvc64`**.
2. In **`Android.bstk.in`** *and* the instance's **`Rvc64.bstk`**, change `fastboot.vdi` and `Root.vhd` from `type="Readonly"` to `type="Normal"`:
   ```diff
   -   <HardDisk ... location="fastboot.vdi" format="VDI" type="Readonly" />
   -   <HardDisk ... location="Root.vhd"     format="VHD" type="Readonly"/>
   +   <HardDisk ... location="fastboot.vdi" format="VDI" type="Normal" />
   +   <HardDisk ... location="Root.vhd"     format="VHD" type="Normal"/>
   ```
3. Save both files.

#### Step 4 — Install Kitsune Mask to `/system`

1. Launch the instance from the Multi-Instance Manager and install the Kitsune Mask APK (drag-and-drop the APK onto the window).
2. Open Kitsune Mask → **Install** → **Next** → **Direct Install to /system**. *(If that option is missing, fully close and reopen the app inside the emulator.)*
3. Let it finish, then **close BlueStacks completely.**

#### Step 5 — Revert the root flags (this is required)

1. Reopen **`bluestacks.conf`** and set **both** back to `0`:
   - `bst.instance.Rvc64.enable_root_access="0"`
   - `bst.feature.rooting="0"`
2. **Leave the R/W (`type="Normal"`) changes from Step 3 as-is.**
3. Save. Launch the instance — Kitsune Mask is installed and root works.

> [!IMPORTANT]
> **Why revert the flags?** BlueStacks' *own* built-in `su` and Kitsune's `su` can't both be active — if both are, Magisk reports **"a `su` binary not from Magisk has been detected"** (Abnormal State) and modules won't run. Turning `enable_root_access` back to `0` removes BlueStacks' `su` so Kitsune's is the only one. (In the [app](#method-a-bluestacks-root-gui-recommended), "Toggle Root OFF" does the same thing.)

</details>

---

## Stop Auto-Updates (do this)

BlueStacks will silently update itself and undo your root — re-locking the integrity check (patched installs) or upgrading you off `5.22.130.1019` (manual installs). Kill both update paths in an **Administrator** terminal:

```powershell
sc.exe stop BstHdUpdaterSvc
sc.exe config BstHdUpdaterSvc start= disabled
schtasks /Change /TN "BlueStacksHelper_nxt" /DISABLE
```

> [!WARNING]
> **Disable both, and don't panic if the service is missing.** On some builds `BstHdUpdaterSvc` isn't installed — the `sc.exe` lines will say *"service does not exist,"* which is fine. The scheduled task **`BlueStacksHelper_nxt`** is the vector that's always present and can update independently, so it's the important one. Setting `bst.auto_update="0"` in `bluestacks.conf` does **not** work — it is silently ignored.

---

## Magisk Modules & Hiding (Advanced)

Getting *app root* is the easy part. Getting a full **Magisk/Kitsune stack** — Zygisk, Play Integrity Fix, LSPosed, DenyList hiding — is much harder on an emulator, and a lot of standard advice fails on BlueStacks. Here's what actually works, learned the hard way on **5.22.232.1002 / Android 13**.

> [!WARNING]
> **Set expectations:** **STRONG** Play Integrity is unreachable on *any* emulator (it needs a hardware-backed key BlueStacks doesn't have). **BASIC**/**DEVICE** can pass with a well-tuned Play Integrity Fix. General root-hiding (DenyList) works; hardware attestation does not.

### 1. Zygisk: use ReZygisk, not Zygisk Next

BlueStacks installs Magisk in **System Mode** (no boot ramdisk), and its custom kernel blocks the usual Zygisk injection.

- **Zygisk Next fails here** — its daemon starts but the kernel denies every injection (`permission denied … NewInitProcess`), so `libzygisk` never loads into zygote and no Zygisk module works.
- **[ReZygisk](https://github.com/PerformanC/ReZygisk) works** — its **ptrace-based** injector gets past the kernel block. Verified: `libzygisk.so` maps into both zygotes, `zygisk-ptrace64` runs, no denials.
- **Magisk's built-in Zygisk** stays **off** (ReZygisk replaces it).

**Install ReZygisk, reboot, done.** It's the base everything else sits on.

### 2. "Module suspended because Zygisk is not enabled" — ignore it

With ReZygisk, Magisk's app shows *"Zygisk: No"* and labels modules (like Play Integrity Fix) **"suspended because Zygisk is not enabled."** This is a **known cosmetic bug, not a real failure** — the modules still load and run via ReZygisk. It happens because Magisk's *own* Zygisk flag is off while ReZygisk does the real work. Confirmed by the ReZygisk maintainers ([ReZygisk #45](https://github.com/PerformanC/ReZygisk/issues/45)).

> [!WARNING]
> Do **not** "fix" the label by enabling Magisk's built-in Zygisk — that can conflict with ReZygisk and bootloop the instance. Verify functionality with a checker app, not the label.

### 3. LSPosed: install it, then close and reopen the instance

LSPosed runs fine on top of ReZygisk — verified **Activated** (1.9.2, Zygisk) on 5.22.232.1002 / Android 13. After installing any module, **fully close the instance and reopen it** to activate it. The first boot after adding LSPosed is a little slower while Android recompiles (`dex2oat`), so give it a minute.

### 4. Play Integrity Fix: loading ≠ passing

If BASIC still fails after PIF is installed:
- **Force-stop and clear data on Google Play Services**, then re-check — GMS caches its real identity and must re-read the spoof.
- PIF's bundled device fingerprint may be **stale/banned** (Google bans them constantly) — grab a fresh `pif.json`.
- PIF ships ARM libs; on x86 BlueStacks whether it injects into GMS depends on ARM translation. Verify with a **Play Integrity checker** app, not by reading props.

### Recommended order

**ReZygisk → close & reopen → verify Zygisk injects → Play Integrity Fix → close & reopen → LSPosed → close & reopen.** Back up / clone the instance once you have a known-good stack.

### Installing modules from your PC — the "Invalid Uri" trap

Picking a module zip through BlueStacks' **Windows Picker** fails with **`Copying zip to temp directory / Invalid Uri`** — Magisk can't open a Windows-side file reference. Instead, get the zip into **Android's own storage** first (drag-drop it onto the window → it lands in Android's Downloads, or push it with adb), then pick it from internal storage. Or skip the picker entirely and install over adb:

```powershell
adb connect 127.0.0.1:<port>        # BlueStacks ADB port (Settings - Advanced); it changes per reboot
adb push module.zip /data/local/tmp/
adb shell su -c 'magisk --install-module /data/local/tmp/module.zip'
```

---

## Advanced: rooting the latest by hand (no app)

You *can* root a current (`5.22.130.1020`+) build without the app, but it means binary-patching the integrity check out of `HD-Player.exe` yourself — the exact thing [BlueStacks Root GUI](https://github.com/RobThePCGuy/BlueStacks-Root-GUI) automates.

The patch: inside `HD-Player.exe`, the function `_isDiskVerificationRequired()` is forced to return 0 (`xor eax,eax; ret`, bytes `31 C0 C3`), which disables the *"illegally tampered"* shutdown. The catch is **locating** it — it's found by a byte-signature near the `unlock_player.bin` string, and the file offset differs per build, so there's no single universal offset to hand you. The reference implementation (signatures, exact bytes, and the `HD-MultiInstanceManager.exe` reset patch) is open source in **[integrity_patch.py](https://github.com/RobThePCGuy/BlueStacks-Root-GUI/blob/master/integrity_patch.py)** and **[root_persistence.py](https://github.com/RobThePCGuy/BlueStacks-Root-GUI/blob/master/root_persistence.py)**.

> [!NOTE]
> For all but the most determined hex-editors, the app is the practical way to do this on the latest build — it finds the signature across builds, backs up the original, and is reversible. This section exists for transparency, not because hand-patching is recommended.

---

<details>
<summary><h2>Troubleshooting</h2></summary>

### "Android system doesn't meet security" / instance shuts down

BlueStacks 5.22 (Oct 2025) added a disk-integrity check that rejects a modified `/system` on boot. **Two fixes:**
- **Root the current build** with [BlueStacks Root GUI](https://github.com/RobThePCGuy/BlueStacks-Root-GUI) (patches the check out), **or**
- **Use the [manual downgrade](#method-b-manual-notepad-only-no-app)** to `5.22.130.1019` (the last build without the check), then [Stop Auto-Updates](#stop-auto-updates-do-this).

### "A `su` binary not from Magisk has been detected" (Abnormal State)

BlueStacks' own `su` is competing with Magisk's. Remove BlueStacks' `su`: turn root **off** (app: Toggle Root OFF; manual: set `enable_root_access` and `bst.feature.rooting` back to `0`), keep R/W on, reboot. Magisk becomes the only `su`.

### Kitsune install fails / "Direct Install to /system" missing

Almost always the Step 3 R/W edit didn't take, or BlueStacks wasn't fully closed when you edited. Confirm `fastboot.vdi` and `Root.vhd` are `type="Normal"` in **both** `.bstk.in` and `.bstk`. Also try fully closing and reopening the Kitsune app inside the emulator.

### Modules show "suspended because Zygisk is not enabled"

Cosmetic with ReZygisk — see [Magisk Modules & Hiding](#magisk-modules--hiding-advanced). The modules still work.

### Module flash fails with "Invalid Uri"

You picked the zip via the Windows Picker. Get it into Android storage first, or install over adb — see the [Invalid Uri trap](#installing-modules-from-your-pc--the-invalid-uri-trap).

### Instance hangs before the home screen

A module is stalling boot. Remove/disable the offending module, or fall back to a clean instance.

### "Permission denied" saving `bluestacks.conf`

Open Notepad **as administrator** before opening the file.

</details>

<details>
<summary><h2>Version Compatibility</h2></summary>

| BlueStacks Version | Rootable? | How |
|---|---|---|
| 5.20.x – 5.21.x | Yes | Classic flags; no integrity check |
| ≤ 5.22.130.1019 | Yes | Manual (Notepad) **or** app — last build with **no** integrity check |
| 5.22.130.1020+ (incl. latest 5.22.232.x) | Yes | **[App](#method-a-bluestacks-root-gui-recommended)** patches the integrity check out (or [hand-patch](#advanced-rooting-the-latest-by-hand-no-app)) |

Per [@AndnixSH](https://github.com/RobThePCGuy/Root-Bluestacks-with-Kitsune-Mask/issues/11): *"5.22.130.1019 is the last working version without disk integrity check."* Everything above it needs the check patched — which the app does. See [Issue #11](https://github.com/RobThePCGuy/Root-Bluestacks-with-Kitsune-Mask/issues/11) for the full history.

</details>

<details>
<summary><h2>FAQ</h2></summary>

**Q: Do I have to downgrade to root now?**
**A:** No. That advice is outdated. [BlueStacks Root GUI](https://github.com/RobThePCGuy/BlueStacks-Root-GUI) roots the latest build. Downgrading to `5.22.130.1019` is only needed for the fully-manual, no-app method.

**Q: My root stopped working after a while — why?**
**A:** BlueStacks auto-updated and undid it. Do [Stop Auto-Updates](#stop-auto-updates-do-this). On a patched install you can also just re-run the engine patch.

**Q: I can't find `C:\ProgramData`.**
**A:** It's hidden. In File Explorer → **View** → check **Hidden items**.

**Q: Which Kitsune Mask build?**
**A:** The pinned `27.001` copy from **[Releases](https://github.com/RobThePCGuy/Root-Bluestacks-with-Kitsune-Mask/releases/tag/magisk-delta-kitsune-27.001)** (SHA-256 published so you can verify it). Older builds like `26.4` also work. If you hit *"a `su` binary not from Magisk,"* that is **not** caused by the build — it's BlueStacks' own competing `su`; see the [Abnormal State fix](#a-su-binary-not-from-magisk-has-been-detected-abnormal-state).

**Q: Can I undo the root?**
**A:** Yes. App: Toggle Root off. Manual: set the two `bluestacks.conf` values back to `0` and uninstall the Kitsune Mask app.

**Q: Is SELinux enforcing after rooting?**
**A:** No — it's **Disabled** on the BlueStacks 5 guest by default, and neither method changes that (they only edit `bluestacks.conf` and flip disk flags). Verify in a terminal/`adb shell`:
```
getenforce            # expect: Disabled
getprop ro.boot.selinux
```
Confirmed on 5.22.x Android 9/11/13 (all `Disabled`), but it can vary — check your own. If you need SELinux **Enforcing** (some anti-cheat), that requires an extra `magiskpolicy` step beyond this guide.

</details>

---

**If this guide helped, a star on the repo helps others find it.** · [GitHub Repository](https://github.com/RobThePCGuy/Root-Bluestacks-with-Kitsune-Mask)
