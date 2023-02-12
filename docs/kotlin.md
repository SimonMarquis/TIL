---
title: 🧑‍💻 Kotlin
---

[:simple-kotlin: Kotlin Playground](https://play.kotlinlang.org/)

### BitFlags

```kotlin
import kotlin.experimental.*

inline fun Long.hasFlag(flag: Long): Boolean = flag and this == flag
inline fun Long.withFlag(flag: Long): Long = this or flag
inline fun Long.minusFlag(flag: Long): Long = this and flag.inv()

inline fun Int.hasFlag(flag: Int): Boolean = flag and this == flag
inline fun Int.withFlag(flag: Int): Int = this or flag
inline fun Int.minusFlag(flag: Int): Int = this and flag.inv()

inline fun Short.hasFlag(flag: Short): Boolean = flag and this == flag
inline fun Short.withFlag(flag: Short): Short = this or flag
inline fun Short.minusFlag(flag: Short): Short = this and flag.inv()

inline fun Byte.hasFlag(flag: Byte): Boolean = flag and this == flag
inline fun Byte.withFlag(flag: Byte): Byte = this or flag
inline fun Byte.minusFlag(flag: Byte): Byte = this and flag.inv()
```

### Check if a class is in the classpath

```kotlin
internal inline fun <R> String.ifInClasspath(value: () -> R): R? = if (isInClasspath()) value() else null

internal fun String.isInClasspath(): Boolean = kotlin.runCatching {
    Class.forName(this)
}.fold(
    onSuccess = { true },
    onFailure = { false },
)
```

### Coroutine's CancellationException with runCatching

`kotlin.runCatching` is not coroutines-aware, and therefore does not automatically rethrow `CancellationException`.

```kotlin
package kotlinx.coroutines

/**
 * Executes [kotlin.runCatching] but rethrow any [CancellationException].
 * @see kotlin.runCatching
 */
suspend inline fun <R> runSuspendCatching(block: () -> R): Result<R> = runCatching(block).onFailure {
    if (it is CancellationException) throw it
}

/**
 * Executes [kotlin.runCatching] but rethrow any [CancellationException].
 * @see kotlin.runCatching
 */
suspend inline fun <T, R> T.runSuspendCatching(block: T.() -> R): Result<R> = runCatching(block).onFailure {
    if (it is CancellationException) throw it
}
```

[🧑‍💻](https://play.kotlinlang.org/#eyJ2ZXJzaW9uIjoiMS42LjEwIiwicGxhdGZvcm0iOiJqYXZhIiwiYXJncyI6IiIsIm5vbmVNYXJrZXJzIjp0cnVlLCJ0aGVtZSI6ImlkZWEiLCJjb2RlIjoiaW1wb3J0IGtvdGxpbnguY29yb3V0aW5lcy4qXG5cbmZ1biA8VD4gUmVzdWx0PFQ+LnRocm93SWYoXG4gICAgcHJlZGljYXRlOiAoVGhyb3dhYmxlKSAtPiBCb29sZWFuXG4pOiBSZXN1bHQ8VD4gPSBvbkZhaWx1cmUge1xuICAgIGlmIChwcmVkaWNhdGUoaXQpKSB0aHJvdyBpdFxufVxuXG5zdXNwZW5kIGZ1biA8VD4gcnVuU3VzcGVuZENhdGNoaW5nKFxuICAgIGJsb2NrOiAoKSAtPiBUXG4pOiBSZXN1bHQ8VD4gPSBydW5DYXRjaGluZyhibG9jaykudGhyb3dJZiB7XG4gICAgaXQgaXMgQ2FuY2VsbGF0aW9uRXhjZXB0aW9uXG59XG4ifQ==)

### Execute commands in subprocess

```kotlin
/**
 * ```
 * val status: String = """git status""".exec()
 * ```
 */
fun @receiver:Language("bash") String.exec() = Runtime.getRuntime().exec(this).text()

/**
 * ```
 * val diff: String = """git diff""".execute {
 *     environment() += ("GIT_DIFF_OPTS" to "--unified=10")
 * }.text()
 * ```
 */
fun @receiver:Language("bash") String.execute(
    workingDir: File = Paths.get(".").toFile(),
    redirectOutput: ProcessBuilder.Redirect = ProcessBuilder.Redirect.PIPE,
    redirectError: ProcessBuilder.Redirect = ProcessBuilder.Redirect.PIPE,
    configure: ProcessBuilder.() -> Unit = {},
): Process = ProcessBuilder("""\s""".toRegex().split(this))
    .directory(workingDir)
    .redirectOutput(redirectOutput)
    .redirectError(redirectError)
    .apply(configure)
    .start()

private fun Process.text() = apply { waitFor() }.inputStream.bufferedReader().use { it.readText().trim() }
```

### Expect test failures

The following way of checking a test throws is strongly discouraged because of this single reason: it will succeed wherever the exception comes from, including from the setup code.

```kotlin
@Test(expected = ArithmeticException::class)
fun test() { /* ... */ }
```

Instead, the better solution is to use:

```kotlin
@Test
fun kotlinTest() {
    kotlin.test.assertFailsWith<ArithmeticException> { 1/0 }
}

@Test()
fun junit() {
    org.junit.jupiter.api.assertThrows<ArithmeticException> { 1/0 }
}
```

Also, the `expected` parameter has been removed from JUnit5.

### Extensions

#### Collections

```kotlin
fun <T> Sequence<T>.repeat() = sequence { while (true) yieldAll(this@repeat) }

fun <T> Sequence<T>.repeat(n: Int) = sequence { repeat(n) inner@{ yieldAll(this@repeat) } }

inline fun <T, R> Iterable<T>.foldInPlace(
    initial: R,
    operation: R.(T) -> Unit,
): R = fold(initial) { acc: R, t: T -> acc.apply { operation(t) } }

inline fun <T> Iterable<T>.partitionIndexed(
    predicate: (index: Int, T) -> Boolean,
): Pair<List<T>, List<T>> = withIndex()
    .partition { (index, value) -> predicate(index, value) }
    .map { it.map(IndexedValue<T>::value) }
```

#### Maths

```kotlin
@JvmName("intProduct")
fun Iterable<Int>.product(): Long = fold(1L, Long::times)

@JvmName("longProduct")
fun Iterable<Long>.product(): Long = fold(1L, Long::times)

fun <T> Iterable<T>.cartesianSquare(): List<Pair<T, T>> = flatMap { v -> map { v to it } }

/**
 * Euclid's algorithm for finding the greatest common divisor of a and b.
 */
fun gcd(a: Int, b: Int): Int = if (b == 0) a.absoluteValue else gcd(b, a % b)
fun gcd(f: Int, vararg n: Int): Int = n.fold(f, ::gcd)
fun Iterable<Int>.gcd(): Int = reduce(::gcd)

/**
 * Euclid's algorithm for finding the greatest common divisor of a and b.
 */
fun gcd(a: Long, b: Long): Long = if (b == 0L) a.absoluteValue else gcd(b, a % b)
fun gcd(f: Long, vararg n: Long): Long = n.fold(f, ::gcd)
fun Iterable<Long>.gcd(): Long = reduce(::gcd)

/**
 * Find the least common multiple of a and b using the gcd of a and b.
 */
fun lcm(a: Int, b: Int) = (a * b) / gcd(a, b)
fun lcm(f: Int, vararg n: Int): Long = n.map { it.toLong() }.fold(f.toLong(), ::lcm)
fun Iterable<Int>.lcm(): Long = map { it.toLong() }.reduce(::lcm)

/**
 * Find the least common multiple of a and b using the gcd of a and b.
 */
fun lcm(a: Long, b: Long) = (a * b) / gcd(a, b)
fun lcm(f: Long, vararg n: Long): Long = n.fold(f, ::lcm)
fun Iterable<Long>.lcm(): Long = reduce(::lcm)

/**
 * Simple algorithm to find the primes of the given Long.
 */
fun Long.primes(): Sequence<Long> = sequence {
    var n = this@primes
    var j = 2L
    while (j * j <= n) {
        while (n % j == 0L) {
            yield(j)
            n /= j
        }
        j++
    }
    if (n > 1) yield(n)
}
```

#### Misc

```kotlin
operator fun String.times(n: Int) = repeat(n)

inline fun <T, R> Pair<T, T>.map(transform: (T) -> R): Pair<R, R> = transform(first) to transform(second)
```

### Normalize line endings

```kotlin
fun String.normalizeLineEndings(
    replacement: String = System.lineSeparator(),
) = replace("""\r\n?""".toRegex(), replacement)
```

#### Permutations & Combinations

```kotlin
fun <T> List<T>.permutations(): List<List<T>> {
    if (isEmpty()) return emptyList()
    if (size == 1) return listOf(this)
    val elementToInsert = first()
    return drop(1).permutations().flatMap { p -> List(size) { p.toMutableList().apply { add(it, elementToInsert) } } }
}

fun <T> List<T>.permutationsSequence(): Sequence<List<T>> {
    if (isEmpty()) return emptySequence()
    if (size == 1) return sequenceOf(this)
    val elementToInsert = first()
    return drop(1).permutationsSequence()
        .flatMap { p -> List(size) { p.toMutableList().apply { add(it, elementToInsert) } } }
}

fun <T> List<T>.pairs(): Sequence<Pair<T, T>> = sequence {
    for (i in 0 until size - 1)
        for (j in i + 1 until size) {
            yield(this@pairs[i] to this@pairs[j])
            yield(this@pairs[j] to this@pairs[i])
        }
}
```

### Filter non-null values in a Map

Kotlin already has a `Iterable<T?>.filterNotNull(): List<T>` but nothing for `Map`s. 🤷

```kotlin
/**
 * Returns a map containing all key-value pairs with values that are not `null`.
 * The returned map preserves the entry iteration order of the original map.
 *
 * @see filterNotNull
 */
@Suppress("UNCHECKED_CAST")
fun <K, V: Any> Map<K, V?>.filterNotNullValues(): Map<K, V> = filterValues { it != null } as Map<K, V>
```

### Implicit lamda result with run and let

When using the following syntax, both doSomething() and fallback() will be exectued when the return value of the lambda is null.

```kotlin
// AVOID
somethingNullable?.run { doSomething() } ?: fallback()
somethingNullable?.let { it.doSomething() } ?: fallback()
// PREFER
somethingNullable?.also { it.doSomething() } ?: fallback()
```

### Infinitely repeating Sequence

```kotlin
fun <T> Sequence<T>.repeat() = sequence { while (true) yieldAll(this@repeat) }
fun <T> Sequence<T>.repeat(n: Int) = sequence { repeat(n) inner@{ yieldAll(this@repeat) } }
```

### Invoke operator on Companion objects

```kotlin
class Operation {
    companion object {
        operator fun invoke(block: () -> Unit) = block()
    }
}

fun main() = Operation { }
```

### Invoke operator on Coroutines Dispatchers

```kotlin
import kotlinx.coroutines.invoke
import kotlinx.coroutines.Dispatchers.IO

suspend fun main() = IO { /* ... */ }
```

### Kotlin script

- REPL Worksheet file `*.ws.kts`
- Simple but extendable utility scripts `*.main.kts` [🔗 Keep](https://github.com/Kotlin/KEEP/blob/master/proposals/scripting-support.md) [🔗 Github](https://github.com/Kotlin/kotlin-script-examples/blob/master/jvm/main-kts/MainKts.md) [🔗 Docs](https://kotlinlang.org/docs/custom-script-deps-tutorial.html)

```kotlin
#!/usr/bin/env kotlin

@file:Repository("https://repo1.maven.org/maven2")
@file:DependsOn("org.jetbrains.kotlinx:kotlinx-coroutines-core:1.6.0")
@file:CompilerOptions("-Xopt-in=kotlinx.coroutines.ExperimentalCoroutinesApi")

import kotlinx.coroutines.runBlocking


runBlocking { 
    println("Hello, World!")
}
```

### Language injection

```kotlin
@org.intellij.lang.annotations.Language("JSON")
val json = """{"key": "value"}"""

println(/*language=JSON*/ """{"key": "value"}""")
```

### LazyMutable

```kotlin
var lazyMutable by lazyMutable { Random.nextInt() }

fun <T> lazyMutable(initializer: () -> T): LazyMutable<T> = LazyMutable(initializer)

class LazyMutable<T>(val initializer: () -> T) : ReadWriteProperty<Any?, T> {

    private object NotInitialized

    private var prop: Any? = NotInitialized

    @Suppress("UNCHECKED_CAST")
    override fun getValue(thisRef: Any?, property: KProperty<*>): T =
            if (prop == NotInitialized) {
                synchronized(this) {
                    return if (prop == NotInitialized) initializer().also { prop = it } else prop as T
                }
            } else prop as T

    override fun setValue(thisRef: Any?, property: KProperty<*>, value: T) = synchronized(this) {
        prop = value
    }
}
```

### MainCoroutineRule

[🔗](https://github.com/android/architecture-components-samples/blob/main/LiveDataSample/app/src/test/java/com/android/example/livedatabuilder/util/MainCoroutineRule.kt)

```kotlin
import kotlinx.coroutines.Dispatchers
import kotlinx.coroutines.ExperimentalCoroutinesApi
import kotlinx.coroutines.test.StandardTestDispatcher
import kotlinx.coroutines.test.UnconfinedTestDispatcher
import kotlinx.coroutines.test.resetMain
import kotlinx.coroutines.test.setMain
import org.junit.rules.TestWatcher
import org.junit.runner.Description

/**
 * Sets the main coroutines dispatcher to a [StandardTestDispatcher] for unit testing.
 * A [StandardTestDispatcher] provides control over the execution of coroutines.
 * Alternatively, you can use an [UnconfinedTestDispatcher].
 *
 * Declare it as a JUnit Rule:
 *
 * ```
 * @get:Rule
 * var mainCoroutineRule = MainCoroutineRule()
 * ```
 *
 * Then, use `runTest` to execute your tests.
 */
@ExperimentalCoroutinesApi
class MainCoroutineRule(val dispatcher = StandardTestDispatcher()) : TestWatcher() {

    override fun starting(description: Description) = Dispatchers.setMain(dispatcher)

    override fun finished(description: Description) = Dispatchers.resetMain()

}
```

### Map parallelized

```kotlin
suspend fun <T, R> Iterable<T>.mapParallelized(
    permits: Int = Int.MAX_VALUE,
    transform: suspend (T) -> R,
): List<R> = coroutineScope {
    val semaphore = Semaphore(permits)
    map { async { semaphore.withPermit { transform(it) } } }.awaitAll()
}

suspend fun <T, R> Iterable<T>.mapParallelized(
    dispatcher: CoroutineDispatcher = Dispatchers.Default,
    parallelism: Int = Int.MAX_VALUE,
    transform: suspend (T) -> R,
): List<R> = coroutineScope {
    val limited = dispatcher.limitedParallelism(parallelism)
    map { async(limited) { transform(it) } }.awaitAll()
}
```

[🔗](https://pl.kotl.in/IycUh1l2g)

### MockK extension to wait indefinitely

```kotlin
import io.mockk.*
import kotlinx.coroutines.*

/**
 * Stub block to never return.
 *
 * Used to define what behaviour is going to be mocked.
 * @see [io.mockk.coJustRun]
 */
fun coJustAwait(
    stubBlock: suspend MockKMatcherScope.() -> Unit
) = coEvery(stubBlock) coAnswers {
    awaitCancellation()
}
```

### Property delegate to cancel previous Job

```kotlin
import kotlinx.coroutines.Job
import kotlin.properties.ReadWriteProperty
import kotlin.reflect.KProperty

/**
 * This delegate takes care of cancelling the previous [Job] when a new one is assigned.
 */
class CancelPreviousJob : ReadWriteProperty<Any?, Job?> {
    private var job: Job? = null
    override operator fun getValue(thisRef: Any?, property: KProperty<*>): Job? = job
    override operator fun setValue(thisRef: Any?, property: KProperty<*>, value: Job?) {
        job?.cancel()
        job = value
    }
}
```

```kotlin
var job by CancelPreviousJob()
job = launch { /* ... */ }
/* ... */
job = launch { /* ... */ }
```

### Read resource file

```kotlin
object Resources {
    fun readText(name: String): String = this::class.java.classLoader.getResource(name)?.readText().orEmpty()
}
```

### Recursive flatMap

```kotlin
internal fun <T> T.recursiveFlatMap(
    transform: (T) -> Iterable<T>,
): List<T> = listOf(this) + transform(this).flatMap {
    it.recursiveFlatMap(transform)
}
```

```kotlin
data class Node(val id: String, val children: List<Node> = emptyList())

val node = Node("1", children = listOf(Node("2", children = listOf(Node("3")))))
val nodes = node.recursiveFlatMap(Node::children)
// [Node(id=1, children=[Node(id=2, children=[Node(id=3)])]), Node(id=2, children=[Node(id=3)]), Node(id=3)]
```

### Regex destructuring

```kotlin
val regex = """(\d+)-(\d+)-(\d+)""".toRegex()

fun String.toDate(input: String): Date? = regex.find(this)
    ?.destructured
    ?.let { (y, m, d) ->
        Date(year = y.toInt(), month = m.toInt(), day = d.toInt())
    }
```

### Regex destructuring capturing groups

```kotlin
operator fun MatchResult.getValue(
    thisRef: Any?,
    property: KProperty<*>
): String = groups[property.name]!!.value

val regex = """(?<year>\d{4})-(?<month>\d{1,2})-(?<day>\d{1,2})""".toRegex()
val result = regex.find("2022-10-12") ?: return

val year: String by result
val month: String by result
val day: String by result

println("$year-$month-$day")
```

### Require an instance type

```kotlin
import kotlin.contracts.*

/**
 * Throws an [IllegalArgumentException] if the [value] is not of type [T].
 */
@OptIn(ExperimentalContracts::class)
inline fun <reified T> requireInstanceOf(value: Any?): T {
    contract { returns() implies (value is T) }
    return requireInstanceOf(value) {
        "Required value was ${if (value == null) "null" else value::class.qualifiedName} instead of ${T::class.qualifiedName}"
    }
}

/**
 * Throws an [IllegalArgumentException] with the result of calling [lazyMessage] if the [value] is not of type [T].
 */
@OptIn(ExperimentalContracts::class)
inline fun <reified T> requireInstanceOf(value: Any?, lazyMessage: () -> Any): T {
    contract { returns() implies (value is T) }
    require(value is T, lazyMessage)
    return value
}
```

### Retry coroutine operations

```kotlin
import kotlinx.coroutines.*
import kotlin.time.*

suspend fun <T> retry(
    times: Int,
    delay: Duration,
    block: suspend  () -> T,
): T {
    require(times > 1) { "Expected times > 1, but had $times" }
    repeat(times - 1) {
        kotlin.runCatching { block() }
            .onSuccess { return it }
            .onFailure { delay(delay) }
    }
    return block()
}
```

### Sealed object instances

[:simple-github: SimonMarquis/SealedObjectInstances](https://github.com/SimonMarquis/SealedObjectInstances)

```kotlin
import kotlin.reflect.KClass

fun <T : Any> KClass<T>.sealedObjectInstances() = recursiveSealedObjectInstances()

private tailrec fun <T : Any> KClass<T>.recursiveSealedObjectInstances(
    sealedSubclasses: List<KClass<out T>> = listOf(this),
    acc: Set<T> = emptySet(),
): Set<T> = when {
    sealedSubclasses.isEmpty() -> acc
    else -> recursiveSealedObjectInstances(
        acc = acc + sealedSubclasses.mapNotNull { it.objectInstance },
        sealedSubclasses = sealedSubclasses.flatMap { it.sealedSubclasses },
    )
}
```

```kotlin

fun main() = Sealed::class.sealedObjectInstances()
    .joinToString(separator = "\n") { it.javaClass.name }
    .let(::println)

// Sealed$SealedObject
// Sealed$SealedObject$NestedSealedObject
// ExternalSealedObject
// Sealed$SubSealed$SubSealedObject

sealed class Sealed {
    object SealedObject : Sealed() {
        object NestedSealedObject : Sealed()
    }
    sealed class SubSealed : Sealed() {
        object SubSealedObject : SubSealed()
        data class DataSubSealed(val any: Any) : SubSealed()
    }
}
object ExternalSealedObject : Sealed()
```

[🔗](https://gist.github.com/SimonMarquis/5843c7f42b71659d48fc7de6eb3d4dab)

### SemVer

```kotlin
data class SemVer(
    val major: Int = 0,
    val minor: Int = 0,
    val patch: Int = 0,
    val label: String? = null
) : Comparable<SemVer> {

    companion object {
        fun parse(version: String): SemVer {
            val pattern = Regex("""(\d+)(?:\.(\d+)(?:\.(\d+))?)?(?:-(.+))?""")
            val result = pattern.matchEntire(version)
                ?: throw IllegalArgumentException("Invalid version string [$version]")
            return SemVer(
                major = result.groupValues[1].toIntOrNull() ?: 0,
                minor = result.groupValues[2].toIntOrNull() ?: 0,
                patch = result.groupValues[3].toIntOrNull() ?: 0,
                label = result.groupValues[4].let { it.ifEmpty { null } }
            )
        }
    }

    init {
        require(major >= 0) { "Major version must be a positive number" }
        require(minor >= 0) { "Minor version must be a positive number" }
        require(patch >= 0) { "Patch version must be a positive number" }
        label?.let { require(it.matches(Regex(""".+"""))) { "Label is not valid" } }
    }

    override fun toString(): String = buildString {
        append("$major.$minor.$patch")
        label?.let { append("-$it") }
    }

    /**
     * @return a negative integer, zero, or a positive integer as this object is less than, equal to, or greater than the specified object.
     */
    override fun compareTo(other: SemVer): Int {
        if (major != other.major) return major.compareTo(other.major)
        if (minor != other.minor) return minor.compareTo(other.minor)
        if (patch != other.patch) return patch.compareTo(other.patch)
        if (label == other.label) return 0
        if (label.isNullOrEmpty()) return 1 // 1.0.0 > 1.0.0-alpha
        if (other.label.isNullOrEmpty()) return -1  // 1.0.0-alpha < 1.0.0
        return label.compareTo(other.label, ignoreCase = true)
    }

}
```

### Singleton

```kotlin
open class Singleton<out T, in A>(creator: (A) -> T) {

    private var creator: ((A) -> T)? = creator

    @Volatile
    private var instance: T? = null

    fun instance(arg: A): T {
        val i = instance
        if (i != null) return i
        return synchronized(this) {
            val i2 = instance
            if (i2 != null) {
                i2
            } else {
                val created = creator!!(arg)
                instance = created
                creator = null
                created
            }
        }
    }
}
```

[🔗](https://www.jetbrains.com/help/idea/using-language-injections.html)

### Synchronize a Map with a new Map of values

```kotlin
/**
 * Synchronize this [MutableMap] with a new [Map] of items, based on their keys.
 * @param onRemoved is called for each removed entry.
 * @param update is called for each entry that must be updated, with the corresponding [T] data.
 * @param onAdded is called for each new entry that must be inserted, and for which you need to provide a corresponding [Value].
 */
fun <Key, Value, T> MutableMap<Key, Value>.sync(
    items: Map<Key, T>,
    onRemoved: (entry: Map.Entry<Key, Value>) -> Unit,
    update: (entry: MutableMap.MutableEntry<Key, Value>, data: T) -> Unit,
    onAdded: (entry: Map.Entry<Key, T>) -> Value,
) = apply {
    val itemsToRemove = filterKeys { it !in items }
    val itemsToUpdate = items.filterKeys { it in this }
    val itemsToAdd = items.filterKeys { it !in this }

    // Remove
    entries.removeAll(itemsToRemove.entries)
    itemsToRemove.forEach { onRemoved(it) }

    // Update
    entries.forEach { update(it, itemsToUpdate[it.key]!!) }

    // Add
    itemsToAdd.forEach { put(it.key, onAdded(it)) }
}
```

### takeWhileInclusive

Similar to `#!kotlin fun <T> Sequence<T>.takeWhile(predicate: (T) -> Boolean): Sequence<T>` but also includes the next non-matching element as well.

```kotlin
fun <T> Sequence<T>.takeWhileInclusive(predicate: (T) -> Boolean): Sequence<T> {
    var shouldContinue = true
    return takeWhile { shouldContinue.also { _ -> shouldContinue = predicate(it) } }
}
```

[🔗](https://jivimberg.io/blog/2018/06/02/implementing-takewhileinclusive-in-kotlin/) [🔗](https://gist.github.com/matklad/54776705250e3b375618f59a8247a237)

### Timeout for async operations

```kotlin
suspend fun <T> Deferred<T>.await(
    duration: Duration,
    defaultValue: T,
): T = withTimeout(duration) { await() } ?: defaultValue
```

### NoWhenBranchMatchedException

Using the `java.io.Serializable` interface (or custom `android.os.Parcelable` code) for sealed classe objects might lead to `kotlin.NoWhenBranchMatchedException` while using the Kotlin's `when` expression.  
The reason is fairly simple but not obvious…

When an object is serialized and then deserialized, the result won't be the same object instance anymore.  
But unfortunately, the Kotlin compiler does not warn us about this.  
Which means the following test code will fail without any warning:

```kotlin
sealed class SealedClass : Serializable {
    object SealedObject: SealedClass()
}

@Test
fun test() = SealedObject.serialize().deserialize<SealedObject>().check()

fun SealedClass.check() = when(this) {
    SealedObject -> Unit
    // This will crash here with: kotlin.NoWhenBranchMatchedException
}
```

Even the `Add remaining branches` context action will fall into this issue.   
What must be done instead is to check for **structural** equality (`==`) instead of **referential** equality (`===`).

```kotlin
fun SealedClass.check() = when(this) {
    is SealedObject -> Unit
    // This will no longer crash
}
```

This is also the case when creating mock objects (with MockK or Mockito).
