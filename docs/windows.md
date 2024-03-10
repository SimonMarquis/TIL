---
title: 🪟 Windows
---

### Dev Drive setup

```cmd
:: https://docs.gradle.org/current/userguide/build_environment.html#sec:gradle_environment_variables
SETX GRADLE_USER_HOME E:\.gradle

:: https://maven.apache.org/configure.html
SETX MAVEN_OPTS "-Dmaven.repo.local=E:\.m2\repository"

:: https://developer.android.com/tools/variables
SETX ANDROID_HOME E:\Android
SETX ANDROID_SDK_ROOT E:\Android
SETX ANDROID_USER_HOME E:\.android
```

[🔗](https://learn.microsoft.com/en-us/windows/dev-drive/)

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

### Stop WmmemWSL process

```bash
wsl --shutdown
```

### UEFI BIOS

```bat
shutdown /r /fw /f /t 0
```

### URL file

```ini title="email.url"
[InternetShortcut]
URL=mailto:test@example.org
```

```ini title="example.url"
[InternetShortcut]
URL=https://example.org
```
