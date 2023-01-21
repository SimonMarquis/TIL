---
title: ☕ Java
---

## UncaughtExceptionHandler

!!! quote
	When a thread is about to terminate due to an uncaught exception the Java Virtual Machine will query the thread for its `UncaughtExceptionHandler` using `Thread.getUncaughtExceptionHandler()` and will invoke the handler's `uncaughtException` method, passing the thread and the exception as arguments.

```kotlin
// Keep a reference to the default handler
val default = Thread.getDefaultUncaughtExceptionHandler()

// Override the default handler
Thread.setDefaultUncaughtExceptionHandler { thread: Thread, throwable: Throwable ->
    when (throwable) {
        /* Check if it should be swallowed */
        is MyUncaughtException -> Unit
        /* Otherwise rethrow to the default handler */
        else -> default?.uncaughtException(thread, throwable)
    }
}
```
