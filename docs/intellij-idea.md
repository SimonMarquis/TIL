---
title: 📦 IntelliJ IDEA
---

### Code formatting as a weak warning
 
`File` → `Settings` → `Editor` → `Inspections` → `File is not formatted according to project settings`

[🔗](https://twitter.com/kotlin/status/1067825173196414976)

### Find and replace with regex capturing groups

- Search: `#!html <h2>(?<title>.*?)</h2>`
- Replace: `#!html <h1>${title}</h1>`

[🔗](https://www.jetbrains.com/help/idea/tutorial-finding-and-replacing-text-using-regular-expressions.html#capture_groups_and_backreference)

### KSP generated code

- JVM
  ```kotlin
  kotlin {
      sourceSets.main {
          kotlin.srcDir("build/generated/ksp/main/kotlin")
      }
      sourceSets.test {
          kotlin.srcDir("build/generated/ksp/test/kotlin")
      }
  }
  ```
- Android
  ```kotlin
  androidComponents.beforeVariants {
      kotlin.sourceSets.register(it.name) {
          kotlin.srcDir(file("$buildDir/generated/ksp/${it.name}/kotlin"))
      }
  }
  ```

[🔗](https://kotlinlang.org/docs/ksp-quickstart.html#make-ide-aware-of-generated-code)

### Linkify file path

```kotlin
import java.nio.file.Path

println(path.toUri())
```
<div class="result" markdown>
```
file:///C:/Foo/bar.txt
```
</div>

### Plugins

- [ADB Idea](https://plugins.jetbrains.com/plugin/7380-adb-idea)
- [Atom Material Icons](https://plugins.jetbrains.com/plugin/10044-atom-material-icons)
- [File Expander](https://plugins.jetbrains.com/plugin/11940-file-expander)
- [XWin Keymap](https://plugins.jetbrains.com/plugin/13094-xwin-keymap)

### Project icon

```gitignore
!.idea/icon.png
!.idea/icon_dark.png
```

### Required plugins

++ctrl+alt+s++ → `Build, Execution, Deployment` → `Required Plugins`.

```xml title=".idea/externalDependencies.xml"
<?xml version="1.0" encoding="UTF-8"?>
<project version="4">
  <component name="ExternalDependencies">
    <plugin id="org.editorconfig.editorconfigjetbrains" />
  </component>
</project>
```

[🔗](https://www.jetbrains.com/help/idea/managing-plugins.html#required-plugins) [🔗](https://www.jetbrains.com/help/idea/settings-required-plugins.html)

### Shortcuts

| Shortcut         | Description         |
|------------------|---------------------|
| ++ctrl+shift+p++ | Type of expression  |
| ++ctrl+shift+i++ | Quick definition    |
