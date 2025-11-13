# Device Diagnostics

Run comprehensive diagnostics on the connected Android device and save results for analysis.

## Task

Collect detailed diagnostic information about device health, performance, and configuration.

### Diagnostic Categories

1. **Device Information**:
   - Read `manifest/device.json` for baseline info
   - Verify current device matches manifest
   - Check for any hardware/software changes

2. **Battery Health**:
   - Battery level: `adb shell dumpsys battery | grep level`
   - Battery health: `adb shell dumpsys battery | grep health`
   - Battery temperature: `adb shell dumpsys battery | grep temperature`
   - Battery voltage: `adb shell dumpsys battery | grep voltage`
   - Battery technology: `adb shell dumpsys battery | grep technology`
   - Charging status: `adb shell dumpsys battery | grep status`
   - Power source: `adb shell dumpsys battery | grep 'AC powered\|USB powered'`

3. **Memory Status**:
   - Total memory: `adb shell cat /proc/meminfo | grep MemTotal`
   - Available memory: `adb shell cat /proc/meminfo | grep MemAvailable`
   - Free memory: `adb shell cat /proc/meminfo | grep MemFree`
   - Cached memory: `adb shell cat /proc/meminfo | grep ^Cached`
   - Swap status: `adb shell cat /proc/meminfo | grep Swap`
   - Memory pressure: `adb shell dumpsys meminfo | head -20`

4. **Storage Status**:
   - Internal storage: `adb shell df /data`
   - SD card (if present): `adb shell df /sdcard`
   - System partition: `adb shell df /system`
   - Cache partition: `adb shell df /cache`
   - Large directories: `adb shell du -sh /data/data/* 2>/dev/null | sort -h | tail -20`

5. **CPU Information**:
   - CPU info: `adb shell cat /proc/cpuinfo`
   - Current CPU frequency: `adb shell cat /sys/devices/system/cpu/cpu*/cpufreq/scaling_cur_freq 2>/dev/null`
   - CPU governor: `adb shell cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_governor 2>/dev/null`
   - Load average: `adb shell cat /proc/loadavg`

6. **Network Status**:
   - Network interfaces: `adb shell ip addr show`
   - Wi-Fi status: `adb shell dumpsys wifi | grep "Wi-Fi is"`
   - Mobile data: `adb shell dumpsys telephony.registry | grep mDataConnectionState`
   - DNS servers: `adb shell getprop | grep dns`

7. **Running Processes**:
   - Top processes by memory: `adb shell ps -A -o pid,vsz,rss,cmd | sort -k2 -n | tail -20`
   - Process count: `adb shell ps -A | wc -l`
   - Root processes: `adb shell ps -A | grep root | wc -l`

8. **System Services**:
   - Running services: `adb shell dumpsys activity services | grep "ServiceRecord{" | wc -l`
   - List critical services status
   - Check for crashed services

9. **Display Information**:
   - Screen resolution: `adb shell wm size`
   - Screen density: `adb shell wm density`
   - Display brightness: `adb shell settings get system screen_brightness`
   - Screen timeout: `adb shell settings get system screen_off_timeout`

10. **System Uptime & Performance**:
    - Uptime: `adb shell uptime`
    - Boot time: `adb shell getprop ro.boottime.*`
    - System load: `adb shell top -n 1 | head -10`

11. **Package Statistics**:
    - Total packages: `adb shell pm list packages | wc -l`
    - System packages: `adb shell pm list packages -s | wc -l`
    - User packages: `adb shell pm list packages -3 | wc -l`
    - Disabled packages: `adb shell pm list packages -d | wc -l`

12. **Security Status**:
    - SELinux status: `adb shell getenforce`
    - Encryption status: `adb shell getprop ro.crypto.state`
    - Security patch level: `adb shell getprop ro.build.version.security_patch`
    - Lock screen security: `adb shell dumpsys trust | grep "lockscreen"`

### Output

1. **Save Diagnostic Report**:
   - Create comprehensive report in: `forensics/diagnostics-{timestamp}.txt`
   - Include all collected information organized by category
   - Add interpretations and warnings for concerning values

2. **Save Separate Logs**:
   - `forensics/battery-status-{timestamp}.txt` - Battery details
   - `forensics/memory-dump-{timestamp}.txt` - Memory information
   - `forensics/process-list-{timestamp}.txt` - Running processes

3. **Create Summary**:
   - Present key findings to user
   - Highlight any concerns (low storage, high memory usage, battery issues)
   - Compare with previous diagnostics if available
   - Provide recommendations for issues found

### Health Indicators

Flag these conditions:
- Battery health not "good"
- Storage < 10% free
- Memory usage > 90%
- Excessive number of running processes
- High CPU temperature (if accessible)
- SELinux disabled
- Outdated security patch (> 6 months old)

### Format

Use clear formatting with sections, subsections, and key-value pairs:

```
======================================
ANDROID DEVICE DIAGNOSTICS
======================================
Generated: {timestamp}
Device: {manufacturer} {model}
Android: {version}

======================================
BATTERY HEALTH
======================================
Level: 85%
Health: Good
Temperature: 28.5°C
Status: Charging
Technology: Li-ion

[Continue for each category...]

======================================
HEALTH WARNINGS
======================================
⚠️ Low storage: Only 8% free on /data
⚠️ High memory usage: 92% of RAM in use

======================================
RECOMMENDATIONS
======================================
1. Clear app cache to free storage
2. Close unnecessary background apps
3. Consider package cleanup
```

## Notes

- Diagnostics are saved with timestamps for historical comparison
- All output goes to `forensics/` directory
- Some commands may fail on certain devices/Android versions
- Report any command failures but continue with remaining diagnostics
- User can run this periodically to track device health over time
