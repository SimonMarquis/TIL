---
title: 🐘 Gradle
---

### Cleanup caches and build directories

```bash
# Gradle cache
rm -rf ~/.gradle/caches

# Gradle build dirs
find . -type d -name "build" -prune -exec echo '{}' \; -exec rm -r '{}' \;
```

### Declaring a repository filter

!!! quote
    Gradle exposes an API to declare what a repository may or may not contain.

    By default, repositories include everything and exclude nothing:  

    - If you declare an include, then it excludes everything but what is included.
    - If you declare an exclude, then it includes everything but what is excluded.
    - If you declare both includes and excludes, then it includes only what is explicitly included and not excluded.

See [RepositoryContentDescriptor](https://docs.gradle.org/current/javadoc/org/gradle/api/artifacts/repositories/RepositoryContentDescriptor.html) for all available methods.

```kotlin
repositories {
    maven {
        url = uri("https://repo.mycompany.com/maven2")
        content {
            // this repository *only* contains artifacts with group "my.company"
            includeGroup("my.company")
        }
    }
    mavenCentral {
        content {
            // this repository contains everything BUT artifacts with group starting with "my.company"
            excludeGroupByRegex("my\\.company.*")
        }
    }
}
```

!!! warning
    Filters declared using the repository-level content filter are not exclusive. This means that declaring that a repository includes an artifact doesn’t mean that the other repositories can’t have it either: you must declare what every repository contains in extension.

[🔗](https://docs.gradle.org/current/userguide/declaring_repositories.html#sec:declaring-repository-filter)

### Declaring content exclusively found in one repository

```kotlin
repositories {
    // This repository will _not_ be searched for artifacts in my.company despite being declared first
    mavenCentral()
    exclusiveContent {
        forRepository {
            maven {
                url = uri("https://repo.mycompany.com/maven2")
            }
        }
        filter {
            // this repository *only* contains artifacts with group "my.company"
            includeGroup("my.company")
        }
    }
}
```

[🔗](https://docs.gradle.org/current/userguide/declaring_repositories.html#declaring_content_exclusively_found_in_one_repository)

### Gradle tasks

```
Build Setup tasks
-----------------
init - Initializes a new Gradle build.
wrapper - Generates Gradle wrapper files.

Help tasks
----------
javaToolchains - Displays the detected java toolchains.
projects - Displays the sub-projects of root project.
properties - Displays the properties of root project.
```

### List project properties

```bash
gradlew properties

# To get a specific property
gradlew -q properties --console=plain | grep "^<my-property>:" | awk '{printf $2}'

# Or on newer versions
gradlew -q properties --property=<my-property>
```

### Override build type attribute

```kotlin
implementation(project(":lib")) {
    attributes {
        attribute(BuildTypeAttr.ATTRIBUTE, objects.named<BuildTypeAttr>(DEBUG))
    }
}
```

### Project properties

You can add properties directly to your Project object via the `-P` command line option.
Gradle can also set project properties when it sees specially-named system properties or environment variables.

- Setting a project property via a system property:
  ```properties
  org.gradle.project.foo=bar
  ```

- Setting a project property via an environment variable:
  ```properties
  ORG_GRADLE_PROJECT_foo=bar
  ```

[🔗](https://docs.gradle.org/current/userguide/build_environment.html#sec:project_properties)

### Reproducible builds

```kotlin
/* build.gradle.kts */
tasks.withType<AbstractArchiveTask>().configureEach {
    isPreserveFileTimestamps = false
    isReproducibleFileOrder = true
}
```

[🔗](https://docs.gradle.org/current/userguide/working_with_files.html#sec:reproducible_archives)

### System properties

Using the `-D` command-line option, you can pass a system property to the JVM which runs Gradle.  
You can also set system properties in `gradle.properties` files with the prefix `systemProp.`.

```properties
# gradle.properties
systemProp.gradle.user.home=/gradle
```
!!! info
    command-line options take precedence over system properties.

[🔗](https://docs.gradle.org/current/userguide/build_environment.html#sec:gradle_system_properties)

### Upgrading the Gradle Wrapper

```bash
# Update the version in gradle/wrapper/gradle-wrapper.properties
./gradlew wrapper --gradle-version x.y.z --distribution-type bin
# Update the in gradle-wrapper.jar
./gradlew wrapper
# Validate the version
./gradlew --version
```

[🔗](https://docs.gradle.org/current/userguide/gradle_wrapper.html#sec:upgrading_wrapper)

### Version Catalog extensions and delegates

Extension to access `VersionCatalog`:

```kotlin
fun Project.versionCatalog(name: String = "libs"): VersionCatalog =
    project.extensions.getByType<VersionCatalogsExtension>().named(name)
```

Extensions to fetch versions, libraries, plugins and bundles from a `VersionCatalog` as delegates:

```kotlin
fun VersionCatalog.versions(): ReadOnlyProperty<Any?, VersionConstraint> = ReadOnlyProperty { _, property ->
    findVersion(property.name).orElseThrow {
        IllegalStateException("Version alias named ${property.name} doesn't exist in catalog named $name")
    }
}

fun VersionCatalog.libraries(): ReadOnlyProperty<Any?, Provider<MinimalExternalModuleDependency>> = ReadOnlyProperty { _, property ->
    findLibrary(property.name).orElseThrow {
        IllegalStateException("Library alias named ${property.name} doesn't exist in catalog named $name")
    }
}

fun VersionCatalog.plugins(): ReadOnlyProperty<Any?, Provider<PluginDependency>> = ReadOnlyProperty { _, property ->
    findPlugin(property.name).orElseThrow {
        IllegalStateException("Plugin alias named ${property.name} doesn't exist in catalog named $name")
    }
}

fun VersionCatalog.bundles(): ReadOnlyProperty<Any?, Provider<ExternalModuleDependencyBundle>> = ReadOnlyProperty { _, property ->
    findBundle(property.name).orElseThrow {
        IllegalStateException("Bundle alias named ${property.name} doesn't exist in catalog named $name")
    }
}
```

This can then be used like this in a custom `Plugin`:

```toml
# gradle/libs.versions.toml
[versions]
kotlin = "1.7.10"

[plugins]
org-jetbrains-kotlin-android = { id = "org.jetbrains.kotlin.android", version.ref = "kotlin" }

[bundles]
example = ["lib1", "lib2"]

[libraries]
example1 = "com.example:lib1:#"
example2 = "com.example:lib2:#"
kotlinxCoroutinesCore = { group = "org.jetbrains.kotlinx", name = "kotlinx-coroutines-core", version = "1.6.4" }
```

```kotlin
class MyCatalog(catalog: VersionCatalog): VersionCatalog by catalog {
    val kotlin by versions() // "1.7.10"
    val `org-jetbrains-kotlin-android` by plugins() // "org.jetbrains.kotlin.android:1.7.10"
    val example by bundles() // ["com.example:lib1:#", "com.example:lib2:#"]
    val kotlinxCoroutinesCore by library() // "org.jetbrains.kotlinx:kotlinx-coroutines-core:1.6.4"
}

class MyPlugin : Plugin<Project> {
    override fun apply(target: Project) {
        val catalog = MyCatalog(target.versionCatalog())
        dependencies {
            add("implementation", catalog.kotlinxCoroutinesCore)
        }
    }
}
```

### Version declaration semantics

- An exact version: e.g. `1.3`, `1.3.0-beta3`, `1.0-20150201.131010-1`
- A Maven-style version range: e.g. `[1.0,)`, `[1.1, 2.0)`, `(1.2, 1.5]`
- A prefix version range: e.g. `1.+`, `1.3.+`
- A latest-status version: e.g. `latest.integration`, `latest.release`
- A Maven `SNAPSHOT` version identifier: e.g. `1.0-SNAPSHOT`, `1.4.9-beta1-SNAPSHOT`

Shorthand notation for strict dependencies

```kotlin
dependencies {
    // short-hand notation with !!
    implementation("org.slf4j:slf4j-api:1.7.15!!")
    // is equivalent to
    implementation("org.slf4j:slf4j-api") {
        version {
           strictly("1.7.15")
        }
    }
```

[🔗](https://docs.gradle.org/current/userguide/single_versions.html)

### Welcome message

!!! quote
    Controls whether Gradle should print a welcome message. If set to `never` then the welcome message will be suppressed. If set to `once` then the message is printed once for each new version of Gradle. Default is `once`.

```properties
# gradle.properties
org.gradle.welcome=never
```