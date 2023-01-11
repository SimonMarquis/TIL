---
title: 🧪 JUnit
---

### Flaky TestRule

```kotlin
import org.junit.rules.TestRule
import org.junit.runner.Description
import org.junit.runners.model.Statement

/**
 * @property reason The reason explaining what is flaky in the test, and any corresponding JIRA ticket.
 * @property retry The number of retry allowed to make the test pass successfully.
 */
annotation class Flaky(
    val reason: String,
    val retry: Int = DEFAULT_RETRY_COUNT,
) {
    companion object {
        internal const val DEFAULT_RETRY_COUNT = 3
    }
}

/**
 * Repeat a test multiple times and ignore errors until the retry count is reached.
 *
 * ```
 * @get:Rule
 * val rule = FlakyTestRule()
 *
 * @Test @Flaky(retry = 10)
 * fun test() { ... }
 * ```
 */
class FlakyTestRule(private val applyToAll: Boolean = false) : TestRule {

    private fun Description.iterations() = annotations.filterIsInstance<Flaky>()
        .takeUnless { it.isEmpty() }
        ?.sumOf { it.retry }
        ?.also { require(it > 0) { "Flaky retry count must be > 0" } }
        ?.inc() ?: DEFAULT_RETRY_COUNT.takeIf { applyToAll }

    override fun apply(
        statement: Statement,
        description: Description,
    ): Statement = when (val iterations = description.iterations()) {
        null -> statement
        else -> object : Statement() {
            override fun evaluate() {
                var cause: Throwable? = null
                repeat(iterations) { iteration ->
                    runCatching { statement.evaluate() }.fold(
                        onSuccess = { return println("FlakyTestRule: [${description.displayName}] ${"succeeded after ${iteration.inc()} iterations."}") },
                        onFailure = { cause = it.also { it.printStackTrace() } },
                    )
                }
                throw FlakyTestRuleException(iterations, description, cause)
            }
        }
    }

    private class FlakyTestRuleException(iterations: Int, description: Description, cause: Throwable?) : IllegalStateException("Giving up on test [${description.displayName}] after $iterations iterations.", cause)

}
```

### Locale TestRule

```kotlin
import org.junit.rules.ExternalResource
import java.util.Locale
import java.util.Locale.*

class LocaleTestRule(private val locale: Locale) : ExternalResource() {

    private lateinit var default: Locale

    override fun before() {
        default = getDefault()
        setDefault(locale)
    }

    override fun after() = setDefault(default)

}
```

### Repeat TestRule

```kotlin
import org.junit.rules.TestRule
import org.junit.runner.Description
import org.junit.runners.model.Statement

/**
 * @property iterations The number to repeated iterations required to let a [org.junit.Test] pass successfully.
 */
annotation class Repeat(val iterations: Int)

/**
 * Repeat a test multiple times and throw any occurring error.
 * Inspiration taken from [ShampooRule](https://gist.github.com/JakeWharton/7fe7deb1f7f4a795c120) by Jake Wharton.
 *
 * ```
 * @get:Rule
 * val rule = RepeatTestRule()
 *
 * @Test @Repeat(iterations = 10)
 * fun test() { ... }
 * ```
 */
class RepeatTestRule : TestRule {

    private fun Description.iterations() = annotations.filterIsInstance<Repeat>()
        .takeUnless { it.isEmpty() }
        ?.sumOf { it.iterations }
        ?.also { require(it > 0) { "Repeat count must be > 0" } }
        ?.inc()

    override fun apply(
        statement: Statement,
        description: Description,
    ): Statement = when (val iterations = description.iterations()) {
        null -> statement
        else -> object : Statement() {
            override fun evaluate() = repeat(iterations) { iteration ->
                kotlin.runCatching {
                    statement.evaluate()
                }.onFailure {
                    throw RepeatTestRuleException(iteration.inc(), description, cause = it)
                }
            }
        }
    }

    private class RepeatTestRuleException(iterations: Int, description: Description, cause: Throwable?) : IllegalStateException("[${description.displayName}] failed after $iterations iterations.", cause)

}
```

### TimeZone TestRule

```kotlin
import org.junit.rules.ExternalResource
import java.util.TimeZone
import java.util.TimeZone.*

class TimeZoneTestRule(private val tz: TimeZone) : ExternalResource() {

    private lateinit var default: TimeZone

    override fun before() {
        default = getDefault()
        setDefault(tz)
    }

    override fun after() = setDefault(default)

}
```
