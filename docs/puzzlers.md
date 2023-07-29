---
title: 🧩 Puzzlers
---

## _if-else_ priorities

```kotlin
if (a) {
  /**/
} else if (b) {
  /**/
} else {
  /**/
} + x
```

??? tip " "

    ```kotlin
    if (a) {
      /**/
    } else {
        if (b) {
          /**/
        } else {
          /**/
        } + x
    }
    ```
