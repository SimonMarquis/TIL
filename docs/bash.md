---
title: 🖥️ Bash
---

### Arrays

{{{% raw %}}}

- Definitions:
  ```bash
  Persons=('Alice' 'Bob' 'Charlie')
  Persons[0]="Alice"
  Persons[1]="Bob"
  Persons[2]="Charlie"
  ```

- Getters:
  ```bash
  echo "${Persons[0]}"     # Element #0
  echo "${Persons[-1]}"    # Last element
  echo "${Persons[@]}"     # All elements, space-separated
  echo "${#Persons[@]}"    # Number of elements
  echo "${#Persons}"       # String length of the 1st element
  echo "${#Persons[3]}"    # String length of the Nth element
  echo "${Persons[@]:3:2}" # Range (from position 3, length 2)
  echo "${!Persons[@]}"    # Keys of all elements, space-separated
  ```

- Setters:
  ```bash
  Persons=("${Persons[@]}" "Dave")         # Push
  Persons+=('Dave')                        # Also Push
  Persons=( "${Persons[@]/Al*/}" )         # Remove by regex match
  unset Persons[2]                         # Remove one item
  Persons=("${Persons[@]}")                # Duplicate
  Persons=("${Persons[@]}" "${Others[@]}") # Concatenate
  Persons=(`cat "persons.txt"`)            # Read from file
  ```

- Iterations:
  ```bash
  for p in "${Persons[@]}"; do
    echo "$p"
  done
  ```

{{{% endraw %}}}

### Dictionaries

{{{% raw %}}}

- Definitions:
  ```bash
  declare -A sounds
  sounds[dog]="bark"
  sounds[cow]="moo"
  sounds[bird]="tweet"
  sounds[wolf]="howl"
  ```

- Getters/Setters:
  ```bash
  echo "${sounds[dog]}" # Dog's sound
  echo "${sounds[@]}"   # All values
  echo "${!sounds[@]}"  # All keys
  echo "${#sounds[@]}"  # Number of elements
  unset sounds[dog]     # Delete dog
  ```

- Iterations:
  ```bash title="keys"
  for key in "${!dictionary[@]}"; do
    echo "$key"
  done
  ```

  ```bash title="values"
  for value in "${dictionary[@]}"; do
    echo "$value"
  done
  ```

{{{% endraw %}}}

### Check if command exists

```bash
command -v foo >/dev/null || error 'foo is required'
```

```bash
if command -v foo >/dev/null; then
    echo "foo is available"
else
    echo "foo is required"
    exit 1
fi
```

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
foo `: # This is a comment` |
  bar `: # This is another comment` |
  baz `: # This is the last comment`
```

This method uses both the buit-in no-op command `:` together with the comment character `#` to support shell with `interactive_comments` disabled.

### Multiline comment

```bash
<< 'COMMENT'
  Lorem ipsum dolor sit amet, consectetur adipiscing elit.
  Fusce in justo faucibus, venenatis libero vitae, rutrum sem.
  Donec ut aliquam urna. Nulla facilisi.
COMMENT
```

```bash
: '
  Lorem ipsum dolor sit amet, consectetur adipiscing elit.
  Fusce in justo faucibus, venenatis libero vitae, rutrum sem.
  Donec ut aliquam urna. Nulla facilisi.
'
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

### Run command and ignore result

```bash
foo &>/dev/null || :
```

### Safer scripts

```bash
#!/usr/bin/env bash
set -euo pipefail
```

[🔗](https://explainshell.com/explain?cmd=set+-euo+pipefail)

### Write variable to file

```bash title="echo"
echo "$var" > out.txt
```

```bash title="printf"
printf "%s\n" "$var" > out.txt
```

```bash title="here string"
cat <<< "$var" > out.txt
```

```bash title="here doc"
cat << EOF > out.txt
$var
EOF
```

### Special parameters

- `#!bash $0` Name of the script
- `#!bash $#` Number of arguments
- `#!bash $*` Arguments joined as a String
- `#!bash $@` Arguments as an array
- `#!bash $?` Exit status of last command
- `#!bash $!` PID of last background command
- `#!bash $$` PID of current shell
- `#!bash $-` Set of option flags in current shell
- `#!bash $_` Last argument of the last command
