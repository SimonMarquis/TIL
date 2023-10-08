---
title: ☕ Java
---

## `JAVA_HOME`

=== ":simple-apple: macOS"

    ```bash
    export JAVA_HOME="/Library/Java/Home"
    
    # Override current JDK version
    function jdk() {
      sudo ln -nsf "$(/usr/libexec/java_home -v $1)" $JAVA_HOME
      java -version
    }
    
    # Configure default JDK
    if [ ! -L "$JAVA_HOME" ]
    then
         echo "JAVA_HOME symlink is missing, let's configure it" >&2
         jdk 17
    fi
    ```

### JVM utilities

- Heap info
  ```bash
  jps -l `# list VMs` |
    grep -E "*" `# optional filter` |
    cut -d " " -f1 `# extract pid` |
    xargs -t -n1 -I % jcmd % GC.heap_info
  ```
- GC
  ```bash
  jps -l `# list VMs` |
    grep -E "*" `# optional filter` |
    cut -d " " -f1 `# extract pid` |
    xargs -t -n1 -I % jcmd % GC.run
  ```
- Kill
  ```bash
  jps -l `# list VMs` |
    grep -E "*" `# optional filter` |
    cut -d " " -f1 `# extract pid` |
    xargs -t -n1 kill -9
  ```

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
