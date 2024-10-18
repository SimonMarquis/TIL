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

### Environment variables paths

| Variable | Path |
|----------|------|
| `#!batch %AllUsersProfile%` | `C:\ProgramData` |
| `#!batch %AppData%` | `C:\Users\{username}\AppData\Roaming` |
| `#!batch %CommonProgramFiles%` | `C:\Program Files\Common Files` |
| `#!batch %CommonProgramFiles(x86)%` | `C:\Program Files (x86)\Common Files` |
| `#!batch %comSpec%` | `C:\Windows\System32\cmd.exe` |
| `#!batch %HomeDrive%` | `C:` |
| `#!batch %HomeDrive%` | `C:` |
| `#!batch %HomePath%` | `C:\Users\{username}` |
| `#!batch %LocalAppData%` | `C:\Users\{username}\AppData\Local` |
| `#!batch %ProgramData%` | `C:\ProgramData` |
| `#!batch %ProgramFiles%` | `C:\Program Files` |
| `#!batch %ProgramFiles(x86)%` | `C:\Program Files (x86)` |
| `#!batch %Public%` | `C:\Users\Public` |
| `#!batch %SystemDrive%` | `C:` |
| `#!batch %SystemRoot%` | `C:\Windows` |
| `#!batch %Temp%` | `C:\Users\{username}\AppData\Local\Temp` |
| `#!batch %Tmp%` | `C:\Users\{username}\AppData\Local\Temp` |
| `#!batch %UserProfile%` | `C:\Users\{username}` |
| `#!batch %WinDir%` | `C:\Windows` |

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

### Startup programs

`#!batch %AppData%\Microsoft\Windows\Start Menu\Programs\Startup`

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
