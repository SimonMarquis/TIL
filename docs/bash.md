---
title: 🖥️ Bash
---

### Command options and positional arguments

!!! quote
    A double dash `--` is used in most Bash built-in commands and many other commands to signify the end of command options, after which only positional arguments are accepted.  
    Example use: Let's say you want to grep a file for the string `-v`.  
    Normally `-v` will be considered the option to reverse the matching meaning (only show lines that do not match), but with `--` you can grep for the string `-v` like this:

```bash
grep -- -v file
```

[🔗](https://unix.stackexchange.com/a/11382)

### Delete empty directories

```bash
find . -type d -empty -print -delete
```

### Dynamic command arguments

```bash
args=()
[[ -n "$INPUT" ]] && args+=( '--input' "$INPUT" )
foo "${args[@]}"
```

### Find and run commands in parallel

```bash
find . -type f -name "*" -print0 | xargs -0 --verbose --max-args=1 --max-procs=0 -I % echo "%"
```

[🔗](https://explainshell.com/explain?cmd=find+.+-type+f+-name+%22*%22+-print0+%7C+xargs+-0+--verbose+--max-args%3D1+--max-procs%3D0+-I+%25+echo+%22%25%22)

### Heredoc

```bash title="General syntax"
[cmd] <<[-] delimeter [cmd]
    content
delimeter
```

!!! note "Notes"
    - `<<-` instead of `<<` to ignore leading (tab-only) indentation
    - `|| true` to suppress the return code (1 by default)
    - `'EOF'` to disable command and variable expansion
    - `>/dev/null` to not echo content to stdout

```bash title="Multiline content to variable"
read -d '' my_var << EOF || true
↓↓↓
$PWD
↑↑↑
EOF
```
<div class="result" markdown>
```
↓↓↓
/home/user
↑↑↑
```
</div>

```bash title="Multiline content without expansion to variable"
read -d '' my_var << 'EOF' || true
↓↓↓
$PWD
↑↑↑
EOF
```
<div class="result" markdown>
```
↓↓↓
$PWD
↑↑↑
```
</div>

```bash title="Multiline content to file (overwrite)"
tee file << EOF >/dev/null || true
↓↓↓
$PWD
↑↑↑
EOF
```

```bash title="Multiline content to file (append)"
tee file.txt << EOF >/dev/null || true
↓↓↓
$PWD
↑↑↑
EOF
```

### Inline comment on multiline commands

```bash
cmd1 `# This is a comment` \
  cmd2 # This is another comment
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

### Merge files together

```bash
time {
    echo "↓↓↓"
    find . -type f -name "*.txt" -print0 | xargs -0 cat
    echo "↑↑↑"
} > merged.log
```

### Multiline commands output to variable

```bash
RESULT=$( \
    echo "↓↓↓" ;\
    echo "Hello, $RANDOM!" ;\
    echo "↑↑↑" ;\
)
```

And to capture `stderr` as well:

```bash
RESULT=$(( \
    echo "↓↓↓" ;\
    >&2 echo "Hello, $RANDOM!" ;\
    echo "↑↑↑" ;\
) 2>&1 )
```

### Prefered Bash shebang

```bash
#!/usr/bin/env bash
```

[🔗](https://stackoverflow.com/a/10383546/3615879)

### Prune find results

```bash
find . -path "*/build" -prune -o -name "*.kt" -print
```

### Remove ANSI escape sequences

```bash
sed -e 's/\x1b\[[0-9;]*m//g'
```

[🔗](https://superuser.com/a/380778/733209)

### Safer scripts

```bash
#!/usr/bin/env bash
set -euo pipefail
```

[🔗](https://explainshell.com/explain?cmd=set+-euo+pipefail)
