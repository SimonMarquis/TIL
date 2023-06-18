---
title: 🐘 Gradle
---

### Cleanup caches and build directories

!!! warning "Global cache"

    === ":simple-linux: Linux"

        ```bash
        for d in ~/.gradle/{.tmp,build-scan-data,caches,daemon,jdks,native,wrapper}; do
            test -d "$d" && du --human-readable --summarize "$d" && rm --recursive "$d"
        done
        ```

    === ":material-apple: Apple"

        ```bash
        for d in ~/.gradle/{.tmp,build-scan-data,caches,daemon,jdks,native,wrapper}; do
            test -d "$d" && du -hs "$d" && rm -rf "$d"
        done
        ```

!!! warning "Local cache"

    === ":simple-linux: Linux"

        ```bash
        test -d .gradle && du --human-readable --summarize .gradle && rm --recursive .gradle
        ```

    === ":material-apple: Apple"

        ```bash
        test -d .gradle && du -hs .gradle && rm -rf .gradle
        ```

!!! warning "Build directories"

    === ":simple-linux: Linux"

        ```bash
        find . -type d -name 'build' -prune -exec du --human-readable --summarize '{}' \; -exec rm --recursive '{}' \;
        ```

    === ":material-apple: Apple"

        ```bash
        find . -type d -name 'build' -prune -exec du -hs '{}' \; -exec rm -rf '{}' \;
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

### Download dependencies upfront

This relies on the [dependency verification](https://docs.gradle.org/current/userguide/dependency_verification.html) feature:

```bash
./gradlew assemble lint test connectedAndroidTest --dry-run --write-verification-metadata sha256
```

This will then create `gradle/verification-metadata.dryrun.xml` as a side-effect.

!!! quote

    Because `--dry-run` doesn’t execute tasks, this would be much faster, but it will miss any resolution happening at task execution time.

### Gradle properties are not passed to included builds

When requesting an included build like this:

```kotlin title="settings.gradle.kts"
pluginManagement {
    includeBuild("build-logic")
}
```

**Gradle properties from the default `gradle.properties` are not passed to it.**
Instead you must have a dedicated `build-logic/gradle.properties`, or use a symbolic link.

[🔗](https://github.com/gradle/gradle/issues/2534)

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

## Kotlin extensions

```kotlin
fun Project.isRootProject() = rootProject === this

fun Project.isJava() = isJavaLibrary() || project.pluginManager.hasPlugin("java")
fun Project.isJavaLibrary() = project.pluginManager.hasPlugin("java-library")

fun Project.isKotlin() = isKotlinAndroid() || isKotlinJvm()
fun Project.isKotlinAndroid() = pluginManager.hasPlugin("org.jetbrains.kotlin.android")
fun Project.isKotlinJvm() = pluginManager.hasPlugin("org.jetbrains.kotlin.jvm")

fun Project.isAndroid() = isAndroidApplication() || isAndroidLibrary() || isAndroidTest() || isAndroidDynamicFeature()
fun Project.isAndroidApplication() = plugins.hasPlugin(AppPlugin::class.java)
fun Project.isAndroidLibrary() = plugins.hasPlugin(LibraryPlugin::class.java)
fun Project.isAndroidTest() = plugins.hasPlugin(TestPlugin::class.java)
fun Project.isAndroidDynamicFeature() = plugins.hasPlugin(DynamicFeaturePlugin::class.java)

fun Project.isUsingKapt() = pluginManager.hasPlugin("org.jetbrains.kotlin.kapt")
fun Project.isUsingKsp() = pluginManager.hasPlugin("com.google.devtools.ksp")
fun Project.isUsingLint() = pluginManager.hasPlugin("com.android.internal.lint")


/**
 * Best-effort tries to apply an [action] on a task with matching [name]. If the task doesn't exist
 * at the time this is called, a [TaskContainer.whenTaskAdded] callback is added to match on the
 * name and execute the action when it's added.
 *
 * This approach has caveats, namely that you won't get an immediate failure or indication if you've
 * requested action on a task that may never be added. This is intended to be similar to the
 * behavior of [PluginManager.withPlugin].
 */
fun TaskContainer.withName(name: String, action: Action<Task>) {
    try {
        named(name, action)
    } catch (_: UnknownTaskException) {
        whenTaskAdded {
            if (this@whenTaskAdded.name == name) action(this)
        }
    }
}
```

[🔗](https://github.com/slackhq/slack-gradle-plugin)

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

### Override Version Catalog versions

```kotlin
dependencyResolutionManagement {
    versionCatalogs {
        val prefix = "libs_version_"
        val overrides = providers.systemPropertiesPrefixedBy(prefix)
            .get().mapKeys { (key, _) -> key.removePrefix(prefix) }
        maybeCreate("libs").apply {
            if (overrides.isNotEmpty()) logger.lifecycle("Overriding versions $overrides")
            overrides.forEach { (key, value) -> version(key, value) }
        }
    }
}
```

```bash
gradlew --system-prop "libs_version_=1.2.3" --system-prop "libs_version_=3.2.1"
# or simpler
gradlew -Dlibs_version_foo=1.2.3 -Dlibs_version_bar=3.2.1
```
<div class="result" markdown>
```
Overriding versions {foo=1.2.3, bar=3.2.1}
```
</div>

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

```kotlin title="build.gradle.kts"
tasks.withType<AbstractArchiveTask> {
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

### Test fixtures


!!! note "Producer"

    ```kotlin title="repo/build.gradle.kts"
    plugins {
        kotlin("jvm")
        `java-test-fixtures`
    }

    dependencies {
        // Dependencies of test fixtures (not leaked to consumers)
        testFixturesImplementation("...")
    }
    ```

    ```kotlin title="repo/src/main/kotlin/com/example/Repository.kt"
    fun interface Repository {
        operator fun invoke(id: String): Boolean
    }
    ```

    ```kotlin title="repo/src/testFixtures/kotlin/com/example/FakeRepository.kt"
    class FakeRepository(
        private val block: (id: String) -> Boolean = ::fail
    ): Repository {
        override fun invoke(id: String): Boolean = block(id)
    }
    ```

!!! note "Consumer"

    ```kotlin title="app/build.gradle.kts"
    plugins {
        kotlin("jvm")
    }

    dependencies {
        implementation(project(":repo"))
        testImplementation(testFixtures(project(":repo")))
    }
    ```

    ```kotlin title="app/src/test/kotlin/com/example/Test.kt"
    class Test {

        @Test
        fun test() {
            val repository: Repository = FakeRepository { id: String -> todo() }
            /* ... */
        }

    }
    ```

[🔗](https://docs.gradle.org/current/userguide/java_testing.html#sec:java_test_fixtures)

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
