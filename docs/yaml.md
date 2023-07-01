---
title: 📋 YAML
---

> [**Y**AML **A**in't **M**arkup **L**anguage](https://yaml.org/)

### Front Matter

Front matter is metadata written in YAML, located at the top of a file and wrapped between `---`.

```yaml
---
title: 💎 Miscellaneous
author: Simon Marquis
lang: en
keywords:
  - Miscellaneous
  - Random
---
```

### Types

#### [!!null](https://yaml.org/type/null.html)

> Devoid of value.

!!! quote "regexp"
    ```regex
    ~ # (canonical)
    |null|Null|NULL # (English)
    | # (Empty)
    ```

```yaml
# A document may be null.
---
```

```yaml
empty:
canonical: ~
english: null
english2: Null
english3: NULL
~: null key
```

#### [!!bool](https://yaml.org/type/bool.html)

> Mathematical Booleans.

!!! quote "regexp"
    ```regex
    y|Y|yes|Yes|YES|n|N|no|No|NO
    |true|True|TRUE|false|False|FALSE
    |on|On|ON|off|Off|OFF
    ```

```yaml
canonical: y
answer: NO
logical: True
option: on
```

#### [!!int](https://yaml.org/type/int.html)

> Mathematical integers.

!!! quote "regexp"
    ```regex
    [-+]?0b[0-1_]+ # (base 2)
    |[-+]?0[0-7_]+ # (base 8)
    |[-+]?(0|[1-9][0-9_]*) # (base 10)
    |[-+]?0x[0-9a-fA-F_]+ # (base 16)
    |[-+]?[1-9][0-9_]*(:[0-5]?[0-9])+ # (base 60)
    ```

```yaml
canonical: 685230
decimal: +685_230
octal: 02472256
hexadecimal: 0x_0A_74_AE
binary: 0b1010_0111_0100_1010_1110
sexagesimal: 190:20:30
```

#### [!!float](https://yaml.org/type/float.html)

> Floating-point approximation to real numbers.

!!! quote "regexp"
    ```regex
    [-+]?([0-9][0-9_]*)?\.[0-9.]*([eE][-+][0-9]+)? (base 10)
    |[-+]?[0-9][0-9_]*(:[0-5]?[0-9])+\.[0-9_]* (base 60)
    |[-+]?\.(inf|Inf|INF) # (infinity)
    |\.(nan|NaN|NAN) # (not a number)
    ```

```yaml
canonical: 6.8523015e+5
exponentioal: 685.230_15e+03
fixed: 685_230.15
sexagesimal: 190:20:30.15
negative infinity: -.inf
not a number: .NaN
```

#### [!!str](https://yaml.org/type/str.html)

> Unicode strings, a sequence of zero or more Unicode characters.

```yaml
canonical: Hello, World!
single quotes: 'Hello, World!'
double quotes: "Hello, World!"
folded: >
  Hello,
  World!
literal: |
  Hello,
  World!
```

- Block Scalar Style [🔗](https://yaml.org/spec/1.2.2/#812-literal-style)
    - `folded` (**`>`**): converts new lines into spaces
    - `literal` (**`|`**): preserves new lines and trailing spaces

- Block Chomping [🔗](https://yaml.org/spec/1.2.2/#8112-block-chomping-indicator)
    - `clip`: single newline at end
    - `strip` (**`-`**): no newline at end
    - `keep` (**`+`**): all newlines from end

[🔗](https://yaml-multiline.info/)

#### [!!timestamp](https://yaml.org/type/timestamp.html)

> A point in time.

!!! quote "regexp"
    ```regex
    [0-9][0-9][0-9][0-9]-[0-9][0-9]-[0-9][0-9] # (ymd)
    |[0-9][0-9][0-9][0-9] # (year)
     -[0-9][0-9]? # (month)
     -[0-9][0-9]? # (day)
     ([Tt]|[ \t]+)[0-9][0-9]? # (hour)
     :[0-9][0-9] # (minute)
     :[0-9][0-9] # (second)
     (\.[0-9]*)? # (fraction)
     (([ \t]*)Z|[-+][0-9][0-9]?(:[0-9][0-9])?)? # (time zone)
    ```

```yaml
canonical:        2001-12-15T02:59:43.1Z
valid iso8601:    2001-12-14t21:59:43.10-05:00
space separated:  2001-12-14 21:59:43.10 -5
no time zone (Z): 2001-12-15 2:59:43.10
date (00:00:00Z): 2002-12-14
```

#### [!!binary](https://yaml.org/type/binary.html)

> A sequence of zero or more octets (8 bit values).

```yaml
canonical: !!binary "\
 R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw=="
generic: !binary |
 R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==
```

#### [!!seq](https://yaml.org/type/seq.html)

> Collections indexed by sequential integers starting with zero.

```yaml
Block style: !!seq
- A
- B
- C
Flow style: !!seq [ A, B, C ]
```

#### [!!set](https://yaml.org/type/set.html)

> Unordered set of non-equal values.

```yaml
Block style: !!set
  ? A
  ? B
  ? C
Flow style: !!set { A, B, C }
```

#### [!!pairs](https://yaml.org/type/pairs.html)

> Ordered sequence of key:value pairs allowing duplicates.

```yaml
Block style: !!pairs
  - A: a
  - B: b
  - C: c
Flow style: !!pairs [ A: a, B: b, C: c ]
```

#### [!!map](https://yaml.org/type/map.html)

> Associative container, where each key is unique in the association and mapped to exactly one value.

```yaml
Block style: !!map
  A: a
  B: b
  C: c
Flow style: !!map { A: a, B: b, C: c }
```

#### [!!omap](https://yaml.org/type/omap.html)

> Ordered sequence of key:value pairs without duplicates.

```yaml
Block style: !!omap
  A: a
  B: b
  C: c
Flow style: !!omap { A: a, B: b, C: c }
```
