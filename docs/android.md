---
title: 🤖 Android
---

### AAPT and GZ files

AAPT will silently decompress any `.gz` file from the `assets` directory.  
If you store a (compressed) `/assets/data.json.gz` file, AAPT will only package a (decompressed) `/assets/data.json` file in the resulting apk and aab.

A workaround is to move the file in Java's resources folder `/resources/assets/data.json.gz`.

[🔗](https://cs.android.com/android/platform/superproject/+/master:frameworks/base/tools/aapt/Package.cpp;l=276-279;drc=18f16d6241c6398a034237c2a5343f94d1938f6a)

### AAPT ignore assets from third party libraries

```kotlin
android {
    androidResources {
        ignoreAssetsPatterns += "SomeFont.ttf"
    }
}
```

[🔗](https://developer.android.com/reference/tools/gradle-api/7.4/com/android/build/api/dsl/AndroidResources#ignoreAssetsPatterns())

### ADB with fzf

=== ":simple-linux: Linux"

    ```bash
    adb devices -l 2> /dev/null `: # list devices and ignore daemon messages` |
      tail -n +2 `: # ignore first line` |
      head -n -1 `: # ignore last line` |
      cut -d " " -f1 `: # extract device id` |
      fzf --header '📱 Select one or more devices' --border --reverse --multi \
          --preview-window="right:66%" \
          --preview="adb -s {} shell getprop | grep -E 'ro.build.(description|fingerprint|version.(release|sdk))|ro.product.(cpu.abi|device|locale|manufacturer|model|name)'" |
      xargs --no-run-if-empty --verbose -I % adb -s % `: # run your command of choice`
    ```

=== ":simple-apple: macOS"

    ```bash
    adb devices -l 2> /dev/null `: # list devices and ignore daemon messages` |
      tail -n +2 `: # ignore first line` |
      ghead -n -1 `: # ignore last line` |
      cut -d " " -f1 `: # extract device id` |
      fzf --header '📱 Select one or more devices' --border --reverse --multi \
          --preview-window="right:66%" \
          --preview="adb -s {} shell getprop | grep -E 'ro.build.(description|fingerprint|version.(release|sdk))|ro.product.(cpu.abi|device|locale|manufacturer|model|name)'" |
      xargs -t -I % adb -s % `: # run your command of choice`
    ```

<div class="result" markdown>
```raw
> <search>                     ┌────────────────────────────────────────────────────────┐
  3/3                          │ [ro.build.description]: [sdk_gphone64_x86_64-user 14 U │
  Select one or more devices   │ [ro.build.fingerprint]: [google/sdk_gphone64_x86_64/em │
  18261FDEE000YJ               │ [ro.build.version.release]: [14]                       │
> emulator-5554                │ [ro.build.version.release_or_codename]: [14]           │
  emulator-5556                │ [ro.build.version.release_or_preview_display]: [14]    │
                               │ [ro.build.version.sdk]: [34]                           │
                               │ [ro.product.cpu.abi]: [x86_64]                         │
                               │ [ro.product.cpu.abilist]: [x86_64,arm64-v8a]           │
                               │ [ro.product.cpu.abilist32]: []                         │
                               │ [ro.product.cpu.abilist64]: [x86_64,arm64-v8a]         │
                               │ [ro.product.device]: [emu64xa]                         │
                               │ [ro.product.locale]: [en-US]                           │
                               │ [ro.product.manufacturer]: [Google]                    │
                               │ [ro.product.model]: [sdk_gphone64_x86_64]              │
                               │ [ro.product.name]: [sdk_gphone64_x86_64]               │
                               └────────────────────────────────────────────────────────┘
```
</div>

!!! tip "This can also be used as an alias, for example `adbz`"

    === ":simple-linux: Linux"

        ```bash title="~/.bashrc"
        function adbz() {
          adb devices -l 2> /dev/null `: # list devices and ignore daemon messages` |
            tail -n +2 `: # ignore first line` |
            head -n -1 `: # ignore last line` |
            cut -d " " -f1 `: # extract device id` |
            fzf --header '📱 Select one or more devices' --border --reverse --multi \
                --preview-window="right:66%" \
                --preview="adb -s {} shell getprop | grep -E 'ro.build.(description|fingerprint|version.(release|sdk))|ro.product.(cpu.abi|device|locale|manufacturer|model|name)'" |
            xargs --no-run-if-empty --verbose -I % adb -s % "$@" `: # run the command with provided arguments`
        }
        ```

    === ":simple-apple: macOS"

        ```bash title="~/.zprofile"
        function adbz() {
          adb devices -l 2> /dev/null `: # list devices and ignore daemon messages` |
            tail -n +2 `: # ignore first line` |
            ghead -n -1 `: # ignore last line` |
            cut -d " " -f1 `: # extract device id` |
            fzf --header '📱 Select one or more devices' --border --reverse --multi \
                --preview-window="right:66%" \
                --preview="adb -s {} shell getprop | grep -E   'ro.build.(description|fingerprint|version.(release|sdk))|ro.product.(cpu.abi|device|locale|manufacturer|model|name)'" |
            xargs -t -I % adb -s % adb -s % "$@" `: # run your command of choice`
        }
        ```

    Then simply execute your regular `adb` command with `#!bash adbz install app.apk`

### APK MIME type

`application/vnd.android.package-archive`

[🔗](https://en.wikipedia.org/wiki/Apk_(file_format))

### App Links

!!! quote
    To test an existing statement file, you can use the official [Statement List Generator and Tester](https://developers.google.com/digital-asset-links/tools/generator) tool.  
    During app install/update, an Android service will verify if the App Links configuration complies with the server side `assetlinks.json` file.  
    The results will be sent to logcat, with these tags: `IntentFilterIntentSvc` and `SingleHostAsyncVerifier`.  

The following command will filter the appropriate logcat messages:  
```bash
adb logcat -s "IntentFilterIntentSvc:*" "SingleHostAsyncVerifier:*" "AppLinksAsyncVerifierV2:*" "AppLinksHostsVerifierV2:*"
```

???+ "Logcat"

    === "Android 12+"
    
        !!! success
            ```
            AppLinksAsyncVerifierV2  I  Verification result: checking for a statement with source https://smarquis.fr, relation delegate_permission/common.handle_all_urls, and target fr.smarquis.applinks --> true. [CONTEXT service_id=244 ]
            AppLinksHostsVerifierV2  I  Verification fr.smarquis.applinks complete. Successful hosts: smarquis.fr. Failed hosts: . Error hosts: . [CONTEXT service_id=244 ]
            ```
    
        !!! failure
            ```
            AppLinksAsyncVerifierV2  I  Verification result: checking for a statement with source https://smarquis.fr, relation delegate_permission/common.handle_all_urls, and target fr.smarquis.applinks --> false. [CONTEXT service_id=244 ]
            AppLinksHostsVerifierV2  I  Verification fr.smarquis.applinks complete. Successful hosts: . Failed hosts: smarquis.fr. Error hosts: . [CONTEXT service_id=244 ]
            ```
    
    === "Android 11"
    
        !!! success
            ```
            I/IntentFilterIntentSvc: Verifying IntentFilter. verificationId:0 scheme:"https" hosts:"smarquis.fr" package:"fr.smarquis.applinks".
            I/SingleHostAsyncVerifier: Verification result: checking for a statement with source a <
                                         a: "https://smarquis.fr"
                                       >
                                       , relation delegate_permission/common.handle_all_urls, and target b <
                                         a: "fr.smarquis.applinks"
                                         b <
                                           a: "D2:18:2B:0E:34:38:3B:FD:A7:80:AC:21:88:F1:F7:1F:13:33:AD:CB:E3:94:2A:75:96:FB:A1:7A:0B:6B:CE:68"
                                         >
                                       >
                                        --> true.
            I/IntentFilterIntentSvc: Verification 0 complete. Success:true. Failed hosts:.
            ```
    
        !!! failure
            ```
            I/IntentFilterIntentSvc: Verifying IntentFilter. verificationId:1 scheme:"https" hosts:"smarquis.fr" package:"fr.smarquis.applinks".
            I/SingleHostAsyncVerifier: Verification result: checking for a statement with source a <
                                         a: "https://smarquis.fr"
                                       >
                                       , relation delegate_permission/common.handle_all_urls, and target b <
                                         a: "fr.smarquis.applinks"
                                         b <
                                           a: "D2:18:2B:0E:34:38:3B:FD:A7:80:AC:21:88:F1:F7:1F:13:33:AD:CB:E3:94:2A:75:96:FB:A1:7A:0B:6B:CE:68"
                                         >
                                       >
                                        --> false.
            I/IntentFilterIntentSvc: Verification 1 complete. Success:false. Failed hosts:smarquis.fr.
            ```

[🔗](https://simonmarquis.github.io/Android-App-Linking/#app-links) 

ADB also offers some commands to troubleshoot App Links:

- Reset the state of App Links
  ```bash
  adb shell pm set-app-links --package <package.name> 0 all
  ```
- Restart the verification process
  ```bash
  adb shell pm verify-app-links --re-verify <package.name>
  ```
- Dump the current status
  ```bash
  adb shell pm get-app-links <package.name>
  ```

[🔗](https://developer.android.com/training/app-links/verify-site-associations)

### AutoCleanedValue

```kotlin
import androidx.fragment.app.Fragment
import androidx.lifecycle.DefaultLifecycleObserver
import androidx.lifecycle.Lifecycle.State.INITIALIZED
import androidx.lifecycle.LifecycleOwner
import androidx.lifecycle.Observer
import kotlin.properties.ReadWriteProperty
import kotlin.reflect.KProperty

class AutoCleanedValue<T : Any>(
    fragment: Fragment,
    private val initializer: (() -> T)?
) : ReadWriteProperty<Fragment, T> {

    private var _value: T? = null

    init {
        fragment.lifecycle.addObserver(object : DefaultLifecycleObserver {
            val viewLifecycleOwnerObserver = Observer<LifecycleOwner> {
                it?.lifecycle?.addObserver(object : DefaultLifecycleObserver {
                    override fun onDestroy(owner: LifecycleOwner) {
                        _value = null
                    }
                })
            }

            override fun onCreate(owner: LifecycleOwner) =
                fragment.viewLifecycleOwnerLiveData.observeForever(viewLifecycleOwnerObserver)

            override fun onDestroy(owner: LifecycleOwner) =
                fragment.viewLifecycleOwnerLiveData.removeObserver(viewLifecycleOwnerObserver)
        })
    }

    override fun getValue(thisRef: Fragment, property: KProperty<*>): T = _value ?: run {
        if (!thisRef.viewLifecycleOwner.lifecycle.currentState.isAtLeast(INITIALIZED)) throw IllegalStateException("Fragment might have been destroyed or is not initialized yet!")
        if (initializer == null) throw IllegalStateException("No default initializer provided!")
        initializer.invoke().also { _value = it }
    }

    override fun setValue(thisRef: Fragment, property: KProperty<*>, value: T) {
        _value = value
    }
}

fun <T : Any> Fragment.autoCleaned(
    initializer: (() -> T)? = null
): AutoCleanedValue<T> = AutoCleanedValue(this, initializer)
```

```kotlin
class MyFragment : Fragment() {

    private val adapter: MyAdapter by autoCleaned(::MyAdapter)
    private var binding: MyBinding by autoCleaned()

    override fun onCreateView(
        inflater: LayoutInflater,
        container: ViewGroup?,
        savedInstanceState: Bundle?
    ): View = MyBinding.inflate(inflater, container, false).also { binding = it }.root

}
```

[🔗](https://www.scalereal.com/android/2021/03/12/let-your-delegates-auto-nullify-references.html) [🔗](https://itnext.io/an-update-to-the-fragmentviewbindingdelegate-the-bug-weve-inherited-from-autoclearedvalue-7fc0a89fcae1)

### BottomSheetBehavior extensions

```kotlin
fun <V : View> V.behavior(): BottomSheetBehavior<V> = BottomSheetBehavior.from(this)

fun BottomSheetBehavior<*>.isExpanded(): Boolean = state == STATE_EXPANDED
fun BottomSheetBehavior<*>.isHalfExpanded(): Boolean = state == STATE_HALF_EXPANDED
fun BottomSheetBehavior<*>.isCollapsed(): Boolean = state == STATE_COLLAPSED
fun BottomSheetBehavior<*>.isHidden(): Boolean = state == STATE_HIDDEN
fun BottomSheetBehavior<*>.isDragging(): Boolean = state == STATE_DRAGGING
fun BottomSheetBehavior<*>.isSettling(): Boolean = state == STATE_SETTLING

fun BottomSheetBehavior<*>.collapse() { state = STATE_COLLAPSED }
fun BottomSheetBehavior<*>.expand() { state = STATE_EXPANDED }
fun BottomSheetBehavior<*>.halfExpand() { state = STATE_HALF_EXPANDED }
fun BottomSheetBehavior<*>.hide() { state = STATE_HIDDEN }

fun BottomSheetBehavior<*>.toggle() { if (isExpanded()) collapse() else expand() }

/**
 * @param onBottomSheetStateChanged [BottomSheetCallback.onStateChanged]
 */
fun BottomSheetBehavior<*>.addBottomSheetStateChangedCallback(onBottomSheetStateChanged: (bottomSheet: View, newState: Int) -> Unit): BottomSheetCallback = object : BottomSheetCallback() {
    override fun onStateChanged(bottomSheet: View, @BottomSheetBehavior.State newState: Int) = onBottomSheetStateChanged(bottomSheet, newState)
    override fun onSlide(bottomSheet: View, slideOffset: Float) = Unit
}.also(this::addBottomSheetCallback)

/**
 * @param onBottomSheetSlide [BottomSheetCallback.onSlide]
 */
fun BottomSheetBehavior<*>.addBottomSheetSlideCallback(onBottomSheetSlide: (bottomSheet: View, slideOffset: Float) -> Unit): BottomSheetCallback = object : BottomSheetCallback() {
    override fun onStateChanged(bottomSheet: View, @BottomSheetBehavior.State newState: Int) = Unit
    override fun onSlide(bottomSheet: View, slideOffset: Float) = onBottomSheetSlide(bottomSheet, slideOffset)
}.also(this::addBottomSheetCallback)
```

### ConcatAdapter find global position

```kotlin
/**
 * @return the (global) position for the (local) [position] of the [adapter], or [NO_POSITION] if the [adapter] is not part of [this].
 */
fun ConcatAdapter.findPositionOf(
    position: Int,
    adapter: Adapter<*>,
): Int {
    var offset = 0
    adapters.forEach {
        if (it == adapter) return offset + position
        offset += it.itemCount
    }
    return NO_POSITION
}
```

### Debuggable APK

```bash
aapt dump badging <path-to-apk> | grep -c application-debuggable
```

### Deeplinks

```bash
adb shell am start -a android.intent.action.VIEW \
    -c android.intent.category.BROWSABLE \
    -d "https://example.com"
```

Or shorter:

```bash
adb shell "am start 'https://example.com'"
```

Note: Nested double/simple quotes might be necessary if the url contains special characters.

### Disable Samsung VR

```bash
adb shell pm hide com.samsung.android.hmt.vrsvc
```

### Disable unnecessary instrumented tests

```kotlin
/**
 * Disable unnecessary Android instrumented tests for the [project] if there is no `androidTest` folder.
 * Otherwise, these projects would be compiled, packaged, installed and ran only to end-up with the following message:
 *
 * > Starting 0 tests on AVD
 *
 * Note: this could be improved by checking other potential sourceSets based on buildTypes and flavors.
 */
internal fun LibraryAndroidComponentsExtension.disableUnnecessaryAndroidTests(
    project: Project,
) = beforeVariants {
    val base = "${project.projectDir}/src/androidTest"
    val buildTyped = base + it.buildType?.capitalized()
    val flavored = base + it.flavorName?.capitalized()
    val variant = flavored + it.buildType?.capitalized()
    val dirs = sequenceOf(base, buildTyped, flavored, variant).map(project::file)
    it.enableAndroidTest = it.enableAndroidTest && dirs.any(File::exists)
}
```

### Download APK files

```bash
adb shell pm list packages 2> /dev/null `: # List packages` |
  cut -d ':' -f2 `: # Extract package name` |
  fzf --header '📱 Select one or more packages to download' --border --reverse --multi |
  xargs --no-run-if-empty -I % sh -c '
    mkdir -p "%";
    for path in $(adb shell pm path "%" | sed "s/package://g")
    do
        package=$(basename $path);
        adb pull "$path" "%/$package";
    done'
```

### Edit SharePreferences

```bash
~ adb shell am force-stop <packageName>
~ adb shell run-as <packageName>
$ ls shared_prefs
$ cat shared_prefs/<fileName>.xml
$ echo '<?xml version="1.0" encoding="utf-8" standalone="yes" ?>
<map>
    <!-- Prefs here -->
</map>
' > shared_prefs/<fileName>.xml
```

or

```bash
cat > shared_prefs/<fileName>.xml
<?xml version='1.0' encoding='utf-8' standalone='yes' ?>
<map>
    <!-- Prefs here -->
</map>
Ctrl+C
```

### Ellipsized TextView

```kotlin
fun TextView.isEllipsized(): Boolean = layout?.let { !TextUtils.equals(text, it.text) } ?: false
```

### Environment variables

=== ":simple-apple: macOS"

    ```bash
    export ANDROID_HOME="/Users/$USER/Library/Android/sdk"
    export PATH="$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools"
    ```

=== ":material-microsoft-windows: Windows"

    ```bash
    export ANDROID_HOME=$HOME/android
    export ANDROID_SDK_ROOT=${ANDROID_HOME}
    export PATH=${ANDROID_HOME}/cmdline-tools/latest/bin:${ANDROID_HOME}/platform-tools:${ANDROID_HOME}/tools:${ANDROID_HOME}/tools/bin:${PATH}
    ```

[🔗](https://developer.android.com/tools/variables)

### Espresso AppNotIdleException

On API <= 21, indeterminate `ProgressBar`s would animate forever and trigger the following exception when running Espresso tests: 

```
android.support.test.espresso.AppNotIdleException: Looped for [...] iterations over 60 SECONDS. The following Idle Conditions failed .
```

A simple solution is to disable such `ProgressBar`s by replacing their `indeterminateDrawable` with a static (non-animated) `Drawable`:

```kotlin
fun Activity.disableProgressBarAnimations() = window.decorView.rootView.disableProgressBarAnimations()

fun Fragment.disableProgressBarAnimations() = requireView().disableProgressBarAnimations()

fun View.disableProgressBarAnimations(
    replacement: Drawable = ColorDrawable(Color.BLUE),
) = recursiveChildren().filterIsInstance<ProgressBar>().forEach {
    it.indeterminateDrawable = replacement
}
```

This can also happen for `AnimatedVectorDrawable`s.

### Espresso extensions 

```kotlin
/**
 * Simplify [View] assertions by executing the [matches] predicate on the reified instance of [T].
 *
 * ```kotlin
 * onView(withId(id)).check(matches(
 *     that<TextView>("has non-blank text") {
 *         !it.text.isNullOrBlank()
 *     }
 * ))
 * ```
 */
inline fun <reified T : View> that(
    description: String? = null,
    noinline matches: (T) -> Boolean,
) = object : BoundedMatcher<View, T>(T::class.java) {
    override fun matchesSafely(view: T) = matches(view)
    override fun describeTo(desc: Description) {
        desc.appendText(description ?: matches.toString())
    }
}
```

```kotlin
/**
 * Simplify [ViewAction] actions by executing the [perform] block on the reified instance of [T].
 *
 * ```kotlin
 * onView(withId(id)).perform(
 *     action<ImageView>("reset image drawable") {
 *         it.setImageDrawable(null)
 *     }
 * )
 * ```
 */
inline fun <reified T : View> action(
    description: String? = null,
    noinline perform: (T) -> Unit,
) = object : ViewAction {
    override fun getDescription() = description ?: perform.toString()
    override fun getConstraints() = isAssignableFrom(T::class.java)
    override fun perform(uiController: UiController?, view: View) = perform(view as T)
}
```

### Exclude Proguard (R8) rules from dependency

```kotlin title="build.gradle.kts"
android {
    buildTypes {
        release {
            optimization {
                keepRules {
                    ignoreFrom(
                        "groupId:artifactId:version",
                        "groupId:artifactId",
                    )
                }
            }
        }
    }
}
```

### Firebase Analytics debug

[🔗](https://firebase.google.com/docs/analytics/debugview#enabling_debug_mode) Enabling debug mode forces the app to send events immediately instead of waiting for batches.

```bash
# Enable
adb shell setprop debug.firebase.analytics.app my.package.name
# Disable
adb shell setprop debug.firebase.analytics.app .none.
```

[🔗](https://developers.google.com/analytics/devguides/collection/ga4/send-events?technology=android#view_events_in_the_android_studio_debug_log) To enable Firebase logs in logcat:

```bash
adb shell setprop log.tag.FA VERBOSE
adb shell setprop log.tag.FA-SVC VERBOSE
adb logcat -v time -s FA FA-SVC
```

### Forcing Lint version

This allows to run a specific version of Lint without changing the Android Gradle plugin (AGP).

```properties title="gradle.properties"
# lint = agp + 23.0.0
# https://googlesamples.github.io/android-custom-lint-rules/api-guide.html#example:samplelintcheckgithubproject/lintversion?
android.experimental.lint.version = 8.2.0-alpha07
```

[🔗](https://googlesamples.github.io/android-custom-lint-rules/user-guide.html#combiningagpwithnewerlint/configuringthelintversion)

### Google Maps Outlined Marker Label

| 📹 | 🖼️ |
|:---:|:---:|
| <video controls muted autoplay loop width="250" height="145"><source src="./../assets/google-maps-label.mp4" type="video/mp4"></video> | ![google-maps-label-on-blue](assets/google-maps-label-on-blue.png)<br/>![google-maps-label-on-earth](assets/google-maps-label-on-earth.png) |

```kotlin
import android.content.Context
import android.graphics.Canvas
import android.graphics.Paint
import android.graphics.Paint.Cap
import android.graphics.Paint.Join
import android.graphics.Paint.Style
import android.graphics.Typeface
import android.text.Layout.Alignment.ALIGN_CENTER
import android.text.StaticLayout
import android.text.TextPaint
import android.text.style.TextAppearanceSpan
import android.view.View
import androidx.annotation.ColorInt
import androidx.annotation.Px
import androidx.annotation.StyleRes
import androidx.core.graphics.withTranslation
import com.google.android.gms.maps.model.Marker

/**
 * Simulates Google Maps outlined labels on [Marker]s.
 * The current solution uses a [StaticLayout] and draws it twice for each [onDraw] call, modifying its [TextPaint] [TextPaint.setColor] and [TextPaint.setStyle].
 * </br>
 * Alternate solutions are:
 * - Single [android.widget.TextView] drawing twice on each [onDraw] call (must prevent infinite loop when modifying text color)
 * - Single [android.widget.TextView] with [android.widget.TextView.setShadowLayer] and draw multiple times to get a more opaque shadow:
 *      <pre>override fun onDraw(canvas: Canvas?) = repeat(x) { super.onDraw(canvas) }</pre>
 * - Custom Span using [android.text.style.MetricAffectingSpan]
 * - Two stacked [android.widget.TextView]s, one with {@code paint.style = STROKE} the other with {@code paint.style = FILL}
 */
class OutlinedMarkerLabel constructor(
    context: Context,
    @ColorInt val textColor: Int,
    @ColorInt val strokeColor: Int,
    @Px val strokeWidth: Float,
    @Px val maxWidth: Int = Int.MAX_VALUE,
    @StyleRes val textAppearance: Int,
) : View(context) {

    private val textPaint = TextPaint(Paint.ANTI_ALIAS_FLAG).apply {
        val span = TextAppearanceSpan(context, textAppearance)
        typeface = Typeface.create(span.family, span.textStyle)
        textSize = span.textSize.toFloat()
        strokeWidth = this@OutlinedMarkerLabel.strokeWidth
        strokeCap = Cap.ROUND
        strokeJoin = Join.ROUND
    }

    private var staticLayout: StaticLayout? = null

    private fun newStaticLayout(text: String): StaticLayout? {
        if (text.isBlank()) return null
        // Here we could improve the requiredWidth computation a bit by going through all lines and clamp to the largest
        val width = minOf(textPaint.measureText(text).toInt(), maxWidth)
        return StaticLayout.Builder.obtain(text, 0, text.length, textPaint, width)
            .setIncludePad(false)
            .setAlignment(ALIGN_CENTER)
            .build()
    }

    override fun onMeasure(widthMeasureSpec: Int, heightMeasureSpec: Int) {
        val layout = staticLayout ?: return super.onMeasure(widthMeasureSpec, heightMeasureSpec)
        val offset = layout.paint.strokeWidth.toInt()
        setMeasuredDimension(layout.width + offset, layout.height + offset)
    }

    override fun onDraw(canvas: Canvas?) {
        with(staticLayout ?: return) {
            with(paint) {
                canvas?.withTranslation(strokeWidth / 2F, strokeWidth / 2F) {
                    color = strokeColor
                    style = Style.FILL_AND_STROKE
                    draw(canvas)
                    color = textColor
                    style = Style.FILL
                    draw(canvas)
                }
            }
        }
    }

    fun bind(marker: Marker) {
        staticLayout = newStaticLayout(marker.title.orEmpty())
        requestLayout()
    }

}
```

### Gradle Managed Virtual Devices

```kotlin
testOptions {
    animationsDisabled = true
    managedDevices {
        devices {
            create<ManagedVirtualDevice>("pixel2") {
                device = "Pixel 2"
                apiLevel = 30
                require64Bit = true
                systemImageSource = "google" /* "google-atd", "aosp", or "aosp-atd" */
            }
        }
    }
    groups {
        create("pixels") {
            targetDevices += devices.getByName("pixel2")
        }
    }
}
```

```bash
# Run tests on a single device
gradlew pixel2DebugAndroidTest
# or on a group of devices
gradlew pixelsGroupDebugAndroidTest
```

[🔗](https://android-developers.googleblog.com/2021/10/whats-new-in-scalable-automated-testing.html) [🔗](https://developer.android.com/studio/preview/features?hl=fr#gmd)

### Hilt navigation args

```kotlin
@Module
@InstallIn(ViewModelComponent::class)
object UserScreenNavigationArgsModule {
    @Provides
    @ViewModelScoped
    fun providesUserInfo(ssh: SavedStateHandle) = UserInfo(id = ssh["userId"])
}

@HiltViewModel
class UserViewModel(
    private val userInfo: UserInfo
) : ViewModel()
```

[🔗](https://github.com/Kotlin/kotlinx.coroutines#avoiding-including-the-debug-infrastructure-in-the-resulting-apk)

### Ignore generated baseline profile

This generated file is generally very large (1 to 10 MiB), wastes precious indexing time and fills up search results.

```kotlin
plugins {
    id("idea")
}

idea {
    module {
        excludeDirs = excludeDirs + file("src/main/baseline-prof.txt")
    }
}
```

[🔗](https://docs.gradle.org/current/dsl/org.gradle.plugins.ide.idea.model.IdeaModule.html#org.gradle.plugins.ide.idea.model.IdeaModule:excludeDirs)

### In-memory DataStore

```kotlin
class InMemoryDataStore<T>(initialValue: T) : DataStore<T> {
    override val data: MutableStateFlow<T> = MutableStateFlow(initialValue)
    override suspend fun updateData(transform: suspend (it: T) -> T) = data.updateAndGet { transform(it) }
}
```

### Kill rogue daemons

```bash
jps `: # list VMs` |
  grep -E -i "gradle|kotlin" `: # Kotlin & Gradle daemons` |
  cut -d " " -f1 `: # extract pid` |
  xargs -t -n1 kill -9
```

### Kotlin Coroutines debug probes

!!! quote
    The `kotlinx-coroutines-core` artifact contains a resource file that is not required for the coroutines to operate normally and is only used by the debugger.

```kotlin
android {
    packagingOptions {
        resources.excludes += "DebugProbesKt.bin"
    }
}
```

### Lifecycle CheatSheets

[🔗 JoseAlcerreca/android-lifecycles](https://github.com/JoseAlcerreca/android-lifecycles)

### Lint easter egg

```java
public class Hidden {
    // This looks like a comment, but it's actually code that will be executed when the class is loaded!
    /* \u002a\u002f static { System.out.println("Oh no!"); } \u002f\u002a */
}
```

Fortunately, Kotlin does not seem to be affected by this

```kotlin
class Hidden {
    // This is correctly parsed as a comment
    /* \u002A\u002F companion object { init { println("Oh no!") } } \u002F\u002A */
}
```

[🔗](https://googlesamples.github.io/android-custom-lint-rules/checks/EasterEgg.md.html)

### Lint Issue Index

[🔗 googlesamples.github.io/android-custom-lint-rules](https://googlesamples.github.io/android-custom-lint-rules/checks/index.md.html)

### Lint UAST dump

```kotlin hl_lines="4"
public class FooDetector : Detector(), SourceCodeScanner {
    override fun getApplicableMethodNames() = listOf("foo")
    override fun visitMethodCall(context: JavaContext, node: UCallExpression, method: PsiMethod) =
        println(node.asRecursiveLogString())
}
```

```kotlin title="Snippet"
fun foo(bar: String, baz: Int) = Unit
foo(bar = "BAR", baz = 42)
```

<div class="result" markdown>

```kotlin
UCallExpression (kind = UastCallKind(name='method_call'), argCount = 2))
    UIdentifier (Identifier (foo))
    USimpleNameReferenceExpression (identifier = foo, resolvesTo = null)
    ULiteralExpression (value = "BAR")
    ULiteralExpression (value = 42)
```

</div>

### List AOSP ATD devices

```bash
"$ANDROID_HOME"/cmdline-tools/latest/bin/sdkmanager --list --channel=3 | grep atd | cut -d ' ' -f 3
```
<div class="result" markdown>
```
system-images;android-30;aosp_atd;arm64-v8a
system-images;android-30;aosp_atd;x86
system-images;android-30;aosp_atd;x86_64
system-images;android-30;google_atd;arm64-v8a
system-images;android-30;google_atd;x86
system-images;android-30;google_atd;x86_64
system-images;android-31;aosp_atd;x86_64
system-images;android-31;google_atd;x86_64
```
</div>

### List resources at runtime

```kotlin
/* Colors */
R.color::class.java.fields.forEach {
    val name = it.name
    val colorRes /*@ColorRes*/ = it.getInt(null)
    val colorInt /*@ColorInt*/ = ContextCompat.getColor(this, colorRes)
}

/* Drawables */
R.drawable::class.java.fields.forEach {
    val name = it.name
    val drawableRes /*@DrawableRes*/ = it.getInt(null)
    val drawable = ContextCompat.getDrawable(this, drawableRes)
}

/* Strings */
R.string::class.java.fields.forEach {
    val name = it.name
    val stringRes /*@StringRes*/ = it.getInt(null)
    val string = getString(stringRes)
}
```

### LiveData Events

Previously known as `SingleLiveEvent` [🔗](https://medium.com/androiddevelopers/livedata-with-snackbar-navigation-and-other-events-the-singleliveevent-case-ac2622673150)

```kotlin
/**
 * Used as a wrapper for data that is exposed via a LiveData that represents an event.
 */
open class Event<out T : Any>(private val content: T) {

    var hasBeenHandled = false
        private set

    /**
     * Returns the [content], even if it's already been handled.
     */
    fun peek(): T = content

    /**
     * Returns the [content] and prevents its use again.
     */
    fun getIfNotHandled(): T? = if (hasBeenHandled) null else content.also { hasBeenHandled = true }

    /**
     * Executes the [block] if the [content] has not already been handled.
     */
    fun ifNotHandled(block: (T) -> Unit) = getIfNotHandled()?.let(block)

}
```

[🔗](https://github.com/android/architecture-samples/blob/todo-mvvm-live-kotlin/todoapp/app/src/main/java/com/example/android/architecture/blueprints/todoapp/Event.kt)

```kotlin
/**
 * An [Observer] for [Event]s, simplifying the pattern of checking if the [Event]'s value has already been handled.
 *
 * [onEvent] is *only* called if the [Event]'s contents has not been handled.
 */
class EventObserver<T : Any>(
    private val onEvent: (T) -> Unit,
) : Observer<Event<T>> {
    override fun onChanged(event: Event<T>) {
        event.ifNotHandled(onEvent)
    }
}

fun <T : Any> LiveData<Event<T>>.observeEvent(
    owner: LifecycleOwner,
    onEvent: (T) -> Unit,
) = observe(owner, EventObserver(onEvent))
```

[🔗](https://gist.github.com/JoseAlcerreca/e0bba240d9b3cffa258777f12e5c0ae9)

### LiveData observe non-null data

```kotlin
fun <T> LiveData<T>.observeNotNull(
    owner: LifecycleOwner,
    observer: (data: T & Any) -> Unit,
) = observe(owner) { it?.let(observer) }
```

### LiveData unit testing

```kotlin
/**
 * Gets the value of a [LiveData] or waits for it to have one, with a timeout.
 *
 * Use this extension from host-side (JVM) tests. It's recommended to use it alongside
 * `InstantTaskExecutorRule` or a similar mechanism to execute tasks synchronously.
 */
fun <T> LiveData<T>.awaitValue(
    duration: Duration = 2.seconds,
    afterObserve: () -> Unit = {}
): T {
    var data: T? = null
    val latch = CountDownLatch(1)
    val observer = object : Observer<T> {
        override fun onChanged(o: T?) {
            data = o
            latch.countDown()
            removeObserver(this)
        }
    }
    observeForever(observer)
    afterObserve.invoke()
    if (!latch.await(duration.inWholeMilliseconds, MILLISECONDS)) {
        removeObserver(observer)
        throw TimeoutException("LiveData value was never set.")
    }
    @Suppress("UNCHECKED_CAST")
    return data as T
}

/**
 * Observes a [LiveData] until the `block` is done executing.
 */
suspend fun <T> LiveData<T>.test(block: suspend () -> Unit) {
    val observer = Observer<T> { }
    try {
        observeForever(observer)
        block()
    } finally {
        removeObserver(observer)
    }
}
```

[🔗](https://medium.com/androiddevelopers/unit-testing-livedata-and-other-common-observability-problems-bb477262eb04)

### Locate APK files

```bash
adb shell pm list packages -f
adb shell pm path <package-name>
```

### Manually sign APK

```bash
apksigner sign --ks debug.keystore --key-pass pass:android --ks-key-alias androiddebugkey --ks-pass pass:android app-release.apk
```

### Mutliplatform Parcelize plugin

Kotlin's [Parcelize](https://developer.android.com/kotlin/parcelize) plugin works only on Android project.
Wrapping it in a Kotlin Multiplatform project allows us to use it in JVM projects, without leaking Android implementation details.

```kotlin title="build.gradle.kts"
plugins {
    kotlin("multiplatform")
    id("com.android.library")
    id("kotlin-parcelize")
}

android { /* ... */ }

kotlin {
    android()
    jvm()

    sourceSets {
        val commonMain by getting { /* ... */ }
        val commonTest by getting { /* ... */ }
        val jvmMain by getting { /* ... */ }
        val jvmTest by getting { /* ... */ }
        val androidMain by getting { /* ... */ }
        val androidUnitTest by getting { /* ... */ }
        val androidInstrumentedTest by getting { /* ... */ }
    }
}
```
!!! quote ""
    === "Common"
        ```kotlin title="commonMain/kotlin/Parcel.kt"
        expect class Parcel {
            fun writeLong(long: Long)
            fun readLong(): Long
        }
        
        expect interface Parcelable
        ```
        
        ```kotlin title="commonMain/kotlin/Parcelize.kt"
        @OptIn(ExperimentalMultiplatform::class)
        @OptionalExpectation
        @Target(AnnotationTarget.CLASS)
        @Retention(AnnotationRetention.BINARY)
        expect annotation class Parcelize()
        
        @OptIn(ExperimentalMultiplatform::class)
        @OptionalExpectation
        @Repeatable
        @Target(AnnotationTarget.CLASS, AnnotationTarget.PROPERTY)
        expect annotation class TypeParceler<T, P : Parceler<in T>>
        
        expect interface Parceler<T> {
            fun create(parcel: Parcel): T
            fun T.write(parcel: Parcel, flags: Int)
        }
        
        @OptIn(ExperimentalMultiplatform::class)
        @OptionalExpectation
        @Target(AnnotationTarget.PROPERTY)
        @Retention(AnnotationRetention.BINARY)
        expect annotation class IgnoredOnParcel()
        ```
    === "Android"
        ```kotlin title="androidMain/kotlin/Parcel.android.kt"
        actual typealias Parcel = android.os.Parcel
        
        actual typealias Parcelable = android.os.Parcelable
        ```
        
        ```kotlin title="androidMain/kotlin/Parcelize.kt"
        actual typealias Parcelize = kotlinx.parcelize.Parcelize
        
        actual typealias TypeParceler<T, P> = kotlinx.parcelize.TypeParceler<T, P>
        
        actual typealias Parceler<T> = kotlinx.parcelize.Parceler<T>
        
        actual typealias IgnoredOnParcel = kotlinx.parcelize.IgnoredOnParcel
        ```
    === "JVM"
        ```kotlin title="jvmMain/kotlin/Parcel.jvm.kt"
        actual class Parcel {
            actual fun writeLong(long: Long): Unit = TODO()
            actual fun readLong(): Long = TODO()
        }
        
        actual interface Parcelable
        ```
        
        ```kotlin title="jvmMain/kotlin/Parcelize.kt"
        actual annotation class Parcelize
        
        actual annotation class TypeParceler<T, P : Parceler<in T>>
        
        actual interface Parceler<T> {
            actual fun create(parcel: Parcel): T
            actual fun T.write(parcel: Parcel, flags: Int)
        }
        
        actual annotation class IgnoredOnParcel
        ```

### Parcel extensions

```kotlin title="Testing utils"
fun <T> Parcel.use(block: (Parcel) -> T): T = try { block(this) } finally { recycle() }

context(Parceler<T>)
fun <T> T.parcelize(): T = Parcel.obtain().use {
    write(it, 0)
    it.setDataPosition(0)
    create(it)
}

inline fun <reified R : Parcelable> R.marshall(): ByteArray = Parcel.obtain().use {
    it.writeValue(this)
    it.marshall()
}

inline fun <reified R : Parcelable> ByteArray.unmarshall(): R? = Parcel.obtain().use {
    it.unmarshall(this, 0, size)
    it.setDataPosition(0)
    it.readValue(R::class.java.classLoader) as T
}
```

```kotlin title="Reading boxed primitive values"
//region Read boxed primitive values
@SuppressLint("ParcelClassLoader")
fun Parcel.readIntValue(): Int? = readValue(null) as Int?

@SuppressLint("ParcelClassLoader")
fun Parcel.readLongValue(): Long? = readValue(null) as Long?

@SuppressLint("ParcelClassLoader")
fun Parcel.readFloatValue(): Float? = readValue(null) as Float?

@SuppressLint("ParcelClassLoader")
fun Parcel.readDoubleValue(): Double? = readValue(null) as Double?

@SuppressLint("ParcelClassLoader")
fun Parcel.readBooleanValue(): Boolean? = readValue(null) as Boolean?
//endregion
```

```kotlin title="Read/Write nullable values"
/**
 * This will check an [Int] flag to switch between `null` and non-`null` value:
 *  - `0` means the value is `null` and nothing must be read
 *  - `1` means the value is non-`null` and can be read
 */
inline fun <T> Parcel.readNullable(reader: Parcel.() -> T) =
    if (readInt() != 0) reader() else null

/**
 * This will write an [Int] flag to switch between `null` and non-`null` value:
 * - `0` when the value is `null`
 * - `1` when the value is non-`null`
 */
inline fun <T> Parcel.writeNullable(value: T?, writer: Parcel.(value: T) -> Unit) {
    if (value == null) return writeInt(0)
    writeInt(1)
    writer(value)
}
```

### Parcelize and TypeParceler

```kotlin
class Foo

object FooParceler : Parceler<Foo?> {
    override fun create(parcel: Parcel): Foo? = TODO()
    override fun Foo?.write(parcel: Parcel, flags: Int) = TODO()
}

// typealias helpers
typealias FooTypeParceler = TypeParceler<Foo, FooParceler>
typealias FooNullableTypeParceler = TypeParceler<Foo?, FooParceler>

@Parcelize
@FooTypeParceler
@FooNullableTypeParceler
class Data(val foo: Foo, val nullableFoo: Foo?) : Parcelable
```

[🔗](https://developer.android.com/kotlin/parcelize)

### Print APK certificates

```bash
find . -name '*.apk' -type f -exec echo "APK: {}" \; -exec keytool -printcert -jarfile "{}" \;
```

### Print keystore entries

```bash
keytool -list -v -keystore ~/.android/debug.keystore
```
<div class="result" markdown>
```
Keystore type: PKCS12
Keystore provider: SUN
Your keystore contains 1 entry
Alias name: androiddebugkey
Creation date: 24 Aug 2021
Entry type: PrivateKeyEntry
Certificate chain length: 1
Certificate[1]:
Owner: C=US, O=Android, CN=Android Debug
Issuer: C=US, O=Android, CN=Android Debug
Serial number: 1
Valid from: Tue Aug 24 14:21:42 CEST 2021 until: Thu Aug 17 14:21:42 CEST 2051
Certificate fingerprints:
         SHA1: 9C:2B:0E:AD:D2:12:ED:68:42:00:F5:41:4A:29:A8:10:FD:4F:94:62
         SHA256: 35:21:3A:55:E0:8E:2F:98:34:B6:B1:0B:13:DD:2B:25:A7:E5:9E:39:85:8C:4E:C3:F1:82:CD:33:2E:91:57:4D
Signature algorithm name: SHA1withRSA (weak)
Subject Public Key Algorithm: 2048-bit RSA key
Version: 1
```
</div>

### Project view by default

`Help` → `Edit Custom Properties` → `studio.projectview=true`

### Recursive View children sequence

```kotlin
fun View.recursiveChildren(): Sequence<View> = sequence {
    yield(this@recursiveChildren)
    if (this@recursiveChildren !is ViewGroup) return@sequence
    children.forEach { yieldAll(it.recursiveChildren()) }
}
```

### Resource identifier for MATCH_PARENT and WRAP_CONTENT 

```xml
<resources xmlns:tools="http://schemas.android.com/tools">
    <!-- ViewGroup.LayoutParams.MATCH_PARENT -->
    <item name="match_parent" type="dimen" format="integer" tools:ignore="ResourceName">-1</item>
    <!-- ViewGroup.LayoutParams.WRAP_CONTENT -->
    <item name="wrap_content" type="dimen" format="integer" tools:ignore="ResourceName">-2</item>
</resources>
```

### Resources abstraction

=== ":simple-kotlin: `BooleanResource.kt`"
    ```kotlin
    import android.content.res.Resources
    import androidx.annotation.BoolRes

    sealed class BooleanResource {
        companion object {
            fun from(boolean: Boolean): BooleanResource = BooleanValueResource(boolean)
            fun fromColorId(@BoolRes id: Int): BooleanResource = BooleanIdResource(id)
        }
    }

    private data class BooleanValueResource(val value: Boolean) : BooleanResource()
    private data class BooleanIdResource(@BoolRes val id: Int) : BooleanResource()

    fun BooleanResource.toBoolean(resources: Resources): Boolean = when (this) {
        is BooleanValueResource -> value
        is BooleanIdResource -> resources.getBoolean(id)
    }
    ```
=== ":simple-kotlin: `ColorResource.kt`"
    ```kotlin
    import android.content.res.ColorStateList
    import android.content.res.Resources
    import android.graphics.Color
    import androidx.annotation.ColorInt
    import androidx.annotation.ColorRes
    import androidx.core.content.res.ResourcesCompat

    sealed class ColorResource {
        companion object {
            fun from(color: String): ColorResource = ColorStringResource(color)
            fun fromColorId(@ColorRes id: Int): ColorResource = ColorIdResource(id)
        }
    }

    private data class ColorStringResource(val value: String) : ColorResource()
    private data class ColorIdResource(@ColorRes val id: Int) : ColorResource()

    @ColorInt
    fun ColorResource.toColorInt(resources: Resources, theme: Resources.Theme? = null): Int = when (this) {
        is ColorStringResource -> Color.parseColor(value)
        is ColorIdResource -> ResourcesCompat.getColor(resources, id, theme)
    }

    fun ColorResource.toColorStateList(resources: Resources, theme: Resources.Theme? = null): ColorStateList? = when (this) {
        is ColorStringResource -> ColorStateList.valueOf(toColorInt(resources))
        is ColorIdResource -> ResourcesCompat.getColorStateList(resources, id, theme)
    }
    ```
=== ":simple-kotlin: `DrawableResource.kt`"
    ```kotlin
    import android.content.res.Resources
    import android.graphics.Bitmap
    import android.graphics.drawable.Drawable
    import androidx.annotation.DrawableRes
    import androidx.core.content.res.ResourcesCompat
    import androidx.core.graphics.drawable.toDrawable

    sealed class DrawableResource {
        companion object {
            fun from(drawable: Drawable): DrawableResource = DrawableValueResource(drawable)
            fun fromBitmap(bitmap: Bitmap): DrawableResource = DrawableBitmapResource(bitmap)
            fun fromDrawableId(@DrawableRes id: Int): DrawableResource = DrawableIdResource(id)
        }
    }

    private data class DrawableValueResource(val drawable: Drawable) : DrawableResource()
    private data class DrawableBitmapResource(val bitmap: Bitmap) : DrawableResource()
    private data class DrawableIdResource(@DrawableRes val id: Int) : DrawableResource()

    fun DrawableResource.toDrawable(resources: Resources, theme: Resources.Theme? = null): Drawable? = when (this) {
        is DrawableValueResource -> drawable
        is DrawableBitmapResource -> bitmap.toDrawable(resources)
        is DrawableIdResource -> ResourcesCompat.getDrawable(resources, id, theme)
    }
    ```
=== ":simple-kotlin: `TextResource.kt`"
    ```kotlin
    import android.content.res.Resources
    import androidx.annotation.PluralsRes
    import androidx.annotation.StringRes
    import java.text.MessageFormat

    sealed class TextResource {
        companion object {
            fun none(): TextResource = NullTextResource
            fun fromString(text: CharSequence): TextResource = StringTextResource(text)
            fun fromStringId(@StringRes id: Int, vararg args: Any = emptyArray()): TextResource = StringIdTextResource(id, args.toList())
            fun fromPluralId(@PluralsRes id: Int, quantity: Int, vararg args: Any = emptyArray()): TextResource = PluralIdTextResource(id, quantity, args.toList())
            fun fromMessage(@StringRes id: Int, vararg args: Any = emptyArray()): TextResource = MessageIdTextResource(id, args.toList())
        }

        @Deprecated(
                message = "Suspicious toString() usage, please use toString(resources) if you need to resolve the TextResource.",
                replaceWith = ReplaceWith("toString(resources)"),
                level = DeprecationLevel.WARNING
        )
        override fun toString(): String = super.toString()

    }

    private object NullTextResource : TextResource()
    private data class StringTextResource(val text: CharSequence) : TextResource()
    private data class StringIdTextResource(@StringRes val id: Int, val args: List<Any>) : TextResource()
    private data class PluralIdTextResource(@PluralsRes val id: Int, val quantity: Int, val args: List<Any>) : TextResource()
    private data class MessageIdTextResource(@StringRes val id: Int, val args: List<Any>) : TextResource()

    fun TextResource?.orNone(): TextResource = this ?: TextResource.none()

    fun TextResource.toText(resources: Resources): CharSequence? = when (this) {
        NullTextResource -> null
        is StringTextResource -> text
        is StringIdTextResource -> if (args.isEmpty()) resources.getText(id) else toString(resources)
        is PluralIdTextResource -> if (args.isEmpty()) resources.getQuantityText(id, quantity) else toString(resources)
        is MessageIdTextResource -> if (args.isEmpty()) MessageFormat.format(resources.getString(id)) else toString(resources)
    }

    fun TextResource.toString(resources: Resources): String? = when (this) {
        NullTextResource -> null
        is StringTextResource -> text.toString()
        is StringIdTextResource -> if (args.isEmpty()) resources.getString(id) else resources.getString(id, *args.mapTextResourceToString(resources))
        is PluralIdTextResource -> if (args.isEmpty()) resources.getQuantityString(id, quantity) else resources.getQuantityString(id, quantity, *args.mapTextResourceToString(resources))
        is MessageIdTextResource -> if (args.isEmpty()) MessageFormat.format(resources.getString(id)) else MessageFormat.format(resources.getString(id), *args.mapTextResourceToString(resources))
    }

    private fun <E> List<E>.mapTextResourceToString(resources: Resources) = map { if (it is TextResource) it.toString(resources) else it }.toTypedArray()
    ```

### Robolectric fake Browser Activity

```kotlin
import org.robolectric.RuntimeEnvironment.getApplication
import org.robolectric.Shadows.shadowOf

fun addFakeWebBrowserActivity() = shadowOf(getApplication().packageManager).apply {
    with(ComponentName(getApplication().packageName, "FakeBrowserActivity")) {
        addActivityIfNotPresent(this)
        addIntentFilterForActivity(
            this,
            IntentFilter(Intent.ACTION_VIEW).apply {
                addDataScheme("https")
                addCategory(Intent.CATEGORY_DEFAULT)
                addCategory(Intent.CATEGORY_BROWSABLE)
            },
        )
    }
}
```

### Run command as a specific application user-id

```bash
adb shell run-as <package-name> <command> [<args>]
```

### screencap

```bash
adb shell screencap -p "/sdcard/screencap.png" && adb pull "/sdcard/screencap.png" "$USER/Desktop/%time::=-%%random%.png" && adb shell rm "/sdcard/screencap.png"
```

```pwsh
%comspec% /c adb shell screencap -p "/sdcard/screencap.png" && adb pull "/sdcard/screencap.png" "%UserProfile%\Desktop\%time::=-%%random%.png" && adb shell rm "/sdcard/screencap.png"
```

### scrcpy

[GitHub](https://github.com/Genymobile/scrcpy)

- record
    ```bash
    scrcpy -m 1080 --show-touches --no-display --record "$USER/Desktop/%time::=-%%random%.mp4"
    ```

    ```pwsh
    %comspec% /c scrcpy -m 1080 --show-touches --no-display --record "%UserProfile%\Desktop\%time::=-%%random%.mp4"
    ```
- mirror
    ```bash
    scrcpy -m 1080 --show-touches
    ```

    ```pwsh
    %comspec% /c scrcpy -m 1080 --show-touches
    ```

### Step by step installation

```bash
# Installing OpenJDK
# https://openjdk.org/install/
sudo apt-get update
sudo apt-get install openjdk-17-jdk

# Installing Android Command Line Tools
# https://developer.android.com/studio#command-line-tools-only
cd ~
curl https://dl.google.com/android/repository/commandlinetools-linux-9477386_latest.zip -o /tmp/cmd-tools.zip
mkdir -p android/cmdline-tools
unzip -q -d android/cmdline-tools /tmp/cmd-tools.zip
mv android/cmdline-tools/cmdline-tools android/cmdline-tools/latest
rm /tmp/cmd-tools.zip

# Setting up environment variables
export ANDROID_HOME=$HOME/android
export ANDROID_SDK_ROOT=${ANDROID_HOME}
export PATH=${ANDROID_HOME}/cmdline-tools/latest/bin:${ANDROID_HOME}/platform-tools:${ANDROID_HOME}/tools:${ANDROID_HOME}/tools/bin:${PATH}

# Accepting SDK licenses
yes | sdkmanager --licenses

# Installing SDK components
sdkmanager --update
sdkmanager --list
sdkmanager --list_installed
sdkmanager --install "platforms;android-33"
```

### Strict Modes

```kotlin
StrictMode.ThreadPolicy.Builder()
    .detectAll()
    .penaltyFlashScreen()
    .penaltyLog()
    .build()
    .let(StrictMode::setThreadPolicy)

StrictMode.VmPolicy.Builder()
    .detectAll()
    .penaltyLog()
    .build()
    .let(StrictMode::setVmPolicy)

FragmentStrictMode.defaultPolicy = FragmentStrictMode.Policy.Builder()
    .detectFragmentReuse()
    .detectFragmentTagUsage()
    .detectRetainInstanceUsage()
    .detectTargetFragmentUsage()
    .detectWrongFragmentContainer()
    .detectSetUserVisibleHint()
    .penaltyLog().build()
```

### Suppress unsupported options

```properties title="gradle.properties"
android.suppressUnsupportedOptionWarnings=android.suppressUnsupportedOptionWarnings,\
  android.enableR8.fullMode,\
  android.enableUnitTestBinaryResources,\
  ...
```

### Tools sample resources as JSON files

```json title="./sampledata/users.json"
{
    "data": [
        {
            "name": "Mike Barrett",
            "address": "4898 Locust Rd",
            "avatar": "@sample/avatars"
        },
        {
            "name": "Kylie Long",
            "address": "2659 Taylor St",
            "avatar": "@sample/avatars"
        }
    ]
}
```

```xml
<ImageView
    android:id="@+id/avatar"
    tools:src="@sample/users.json/data/avatar" />
 
<TextView
    android:id="@+id/name"
    tools:text="@sample/users.json/data/name" />
 
  <TextView
    android:id="@+id/address"
    tools:text="@sample/users.json/data/address" />
```

[🔗 `@tools:sample/*`](https://developer.android.com/studio/write/tool-attributes#toolssample_resources)

### Uninstall apps by package name

```bash
adb shell pm list packages `: # List packages` |
  cut -d ':' -f2 `: # Extract package name` |
  grep ^com. `: # Optional pattern` |
  xargs --verbose -n1 adb uninstall
```

Or with fzf

```bash
adb shell pm list packages `: # List packages` |
  cut -d ':' -f2 `: # Extract package name` |
  fzf --header '📦 Select one or more packages to uninstall' --border --reverse --multi |
  xargs --no-run-if-empty --verbose -n1 adb uninstall
```

### USSD and secret codes

These codes must be typed in the dialer app.

- `*#06#`: IMEI
- `*#*#4636#*#*`: Device info
- `*#*#7780#*#*`: Factory reset ♻️

I've created [Secret Codes](https://github.com/SimonMarquis/Android-SecretCodes) to help you find theses codes directly on your device.

[🔗](https://cs.android.com/search?q=android_secret_code)

### ViewBinding extension

```kotlin
fun <Binding : ViewBinding> AppCompatActivity.setContentView(
    inflate: (LayoutInflater) -> Binding
): Binding = inflate(layoutInflater).also {
    setContentView(it.root)
}
```

```kotlin
private lateinit var binding: MainViewBinding

override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    binding = setContentView(MainViewBinding::inflate)
}
```

### ViewBinding one-liner

```kotlin
private lateinit var binding: MainViewBinding

override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    setContentView(MainViewBinding.inflate(layoutInflater).also { binding = it }.root)
}
```

### ViewModel in custom View

```kotlin
class CustomView @JvmOverloads constructor(context: Context, attrs: AttributeSet? = null, defStyleAttr: Int = 0) : View(context, attrs, defStyleAttr) {

  private val viewModel by lazy { ViewModelProvider(findViewTreeViewModelStoreOwner()!!).get<CustomViewModel>() }

  override fun onAttachedToWindow() {
    super.onAttachedToWindow()
    viewModel.state.observe(findViewTreeLifecycleOwner()!!) { TODO() }
  }

}
```

### WebView Safe Browsing

```xml
<manifest>
    <meta-data android:name="android.webkit.WebView.EnableSafeBrowsing" android:value="true" />
    <!-- ... -->
</manifest>
```

[🔗](https://android-developers.googleblog.com/2017/06/whats-new-in-webview-security.html)

### WorkManager diagnostic 

[🔗](https://developer.android.com/topic/libraries/architecture/workmanager/how-to/debugging#request-diagnostic-information-from-workmanager-2.4.0) This provides information on:

- Work requests that were completed in the last 24 hours.
- Work requests that are currently running.
- Scheduled work requests.

```bash
adb shell am broadcast -a "androidx.work.diagnostics.REQUEST_DIAGNOSTICS" -p my.package.name
```
