# ADB Device Setup

Conduct initial device probe and setup for Android device management.

## Task

You will perform the following steps:

1. **Check ADB Connection**:
   - Run `adb devices` to verify a device is connected
   - If no device is connected, prompt user to connect device and enable USB debugging
   - If multiple devices are connected, ask user which device to configure

2. **Collect Device Information**:
   - Device manufacturer: `adb shell getprop ro.product.manufacturer`
   - Device model (marketing name): `adb shell getprop ro.product.model`
   - Device model (precise PN): `adb shell getprop ro.product.name`
   - Android version: `adb shell getprop ro.build.version.release`
   - SDK level: `adb shell getprop ro.build.version.sdk`
   - Serial number: `adb get-serialno`
   - Build ID: `adb shell getprop ro.build.id`
   - Build fingerprint: `adb shell getprop ro.build.fingerprint`
   - Bootloader version: `adb shell getprop ro.bootloader`
   - CPU ABI: `adb shell getprop ro.product.cpu.abi`
   - Screen density: `adb shell wm density`
   - Screen resolution: `adb shell wm size`
   - Total memory: `adb shell cat /proc/meminfo | grep MemTotal`
   - Storage info: `adb shell df /data`

3. **Check Bootloader Status**:
   - Try to determine bootloader lock status (may require device-specific commands)
   - Common check: `adb shell getprop ro.boot.verifiedbootstate`
   - Note: Some devices may require `adb reboot bootloader` then `fastboot oem device-info` (don't reboot without user permission)

4. **Check Root Status**:
   - Check if device is rooted: `adb shell su -c "echo rooted" 2>/dev/null || echo "not rooted"`

5. **Create manifest/device.json**:
   - Create a JSON file at `manifest/device.json` with all collected information
   - Structure should include:
     - manufacturer
     - model (marketing name)
     - model_pn (precise part number)
     - serial_number
     - android_version
     - sdk_level
     - build_id
     - build_fingerprint
     - bootloader_version
     - bootloader_locked (true/false/unknown)
     - cpu_abi
     - screen_density
     - screen_resolution
     - total_memory
     - storage_info
     - root_status (rooted/not_rooted)
     - probe_date (ISO 8601 timestamp)

6. **Export Initial Package List**:
   - Export all installed packages: `adb shell pm list packages -f`
   - Save to `packages/initial-packages-YYYY-MM-DD.txt` with current date
   - Also create a user packages list: `adb shell pm list packages -3 -f`
   - Save to `packages/user-packages-YYYY-MM-DD.txt`

7. **Update CLAUDE.md**:
   - Update the device name placeholder in CLAUDE.md with actual device info
   - Replace `{Replace with device}` with: `{manufacturer} {model} ({model_pn})`

## Output

Provide a summary of the device configuration and confirm all files have been created successfully.
