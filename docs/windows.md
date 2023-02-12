---
title: 🪟 Windows
---

### Reboot GPU driver

=== "MkDocs"
    ++win+ctrl+shift+b++

=== "GitHub"
    <kbd>Win</kbd> + <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>B</kbd>

### Reset file ownership

```powershell
REM Make local administrators group owner.
takeown /F C:\files /R /A /D Y
REM Reset ACLs to defaults.
icacls C:\files /reset /T /C /L /Q
```

[🔗](https://superuser.com/a/813881/733209)

### UEFI BIOS

```bat
shutdown /r /fw /f /t 0
```
