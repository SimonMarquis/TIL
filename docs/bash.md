---
title: 🖥️ Bash
---

### Aliases

```bash
alias cat='bat'

# LS
alias ls='lsd'
alias la='ls -al'
alias ll='ls -alF'
alias lt='ls --tree'

# Quick edit dotfiles
alias bash_aliases="open ~/.bash_aliases"
alias bashrc="open ~/.bashrc"
alias zshrc="open ~/.zshrc"
alias zprofile="open ~/.zprofile"
alias gitconfig="open ~/.gitconfig"
alias gitattributes="open ~/.gitattributes"
```

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

### Directory of script

```bash
dir=${0%/*}
```

### Parameter expansions

{{{% raw %}}}

- Substitutions:
  ```bash
  # Remove suffix
  ${foo%suffix}
  # Remove prefix
  ${foo#prefix}
  # Remove long suffix
  ${foo%%suffix}
  # Remove long suffix
  ${foo/%suffix}
  # Remove long prefix
  ${foo##prefix}
  # Remove long prefix
  ${foo/#prefix}
  # Replace first match
  ${foo/old/new}
  # Replace all instances
  ${foo//old/new}
  # Replace suffix
  ${foo/%old/new}
  # Replace prefix
  ${foo/#old/new}
  ```

- Substrings:
  ```bash
  ${foo:offset:length}
  # offset from right
  ${foo:(-offset):length}
  ```

- Default values:
  ```bash
  # $foo, or val if unset (or null)
  ${foo:-val}
  # set $foo to val if unset (or null)
  ${foo:=val}
  # val if $foo is set (and not null)
  ${foo:+val}
  # print error and exit if $foo is unset (or null)
  ${foo:?error} 
  ```

- Misc:
  ```bash
  # length of string or array
  ${#foo}
  # lowercase 1st char
  ${foo,}
  # lowercase all chars
  ${foo,,}
  # uppercase 1st char
  ${foo^}
  # uppercase 1st char
  ${foo^^}
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

### Debugging

This `DEBUG` trap pauses the script execution on each line, prints the command that will be executed, and prompts the user to continue.

```bash hl_lines="2"
#!/usr/bin/env bash
trap 'read -p "[$BASH_SOURCE:$LINENO] $BASH_COMMAND"' DEBUG

echo "Foo"
echo "Bar"
echo "Baz"
```
<div class="result" markdown>

```bash
./script.sh
[./script.sh:4] echo "Foo"
Foo
[./script.sh:5] echo "Bar"
Bar
[./script.sh:6] echo "Baz"
Baz
```

</div>

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

### jq

!!! abstract ""
    - [jqlang.github.io/jq/manual](https://jqlang.github.io/jq/manual/){: title="jq Manual"}
    - [jqplay.org](https://jqplay.org/){: title="A playground for jq"}

```bash title="Basic filters"
# Identity:
.

# Object Identifier-Index:
.foo, .foo.bar

# Optional Object Identifier-Index:
.foo?

# Object Index:
.[<string>] 

# Array Index:
.[<number>] 

# Array/String Slice:
.[<number>:<number>]

# Array/Object Value Iterator:
.[]

# Comma:
,

# Pipe:
|
```

```bash title="Builtin operators and functions"
# Addition:
+

# Subtraction:
- 

# Multiplication, division, modulo:
*, /, % 

# Length (array, object, string, number, etc.):
length

# Keys of an object as an array:
keys, keys_unsorted

# Presence of the given key:
has(key) 

# Presence of input key in the given object:
in(object)

# Apply f to each of the values in the input array or object:
map(f), map_values(f)

# Convert between an object and an array of key-value pairs:
to_entries, from_entries, with_entries(f)

# Filter input with predicate:
select(f)

# Remove a key and its corresponding value from an object:
del(path_expression)

# Add elements of the input array (summed, concatenated, or merged):
add

# Sort the input array
sort, sort_by(path_expression)

# Group elements by expression 
group_by(path_expression)
```

```bash title="Map entries"
curl -s 'https://api.github.com/repos/github/.github/commits' \
  | jq '.[] | {message: .commit.message, name: .commit.author.name}'
```
<div class="result" markdown>

```json
{
  "message": "Merge pull request #340 from trishanu-init/patch-1\n\nchanged the content structure in CODE_OF_CONDUCT.md",
  "name": "Zack Koppert"
}
{/*...*/}
{
  "message": "Create README.md",
  "name": "Ben Balter"
}
```
</div>

```bash title="Collect into JSON array"
curl -s 'https://api.github.com/repos/github/.github/commits' \
  | jq '[.[] | {message: .commit.message, name: .commit.author.name}]'
```
<div class="result" markdown>

```json
[
  {
    "message": "Merge pull request #340 from trishanu-init/patch-1\n\nchanged the content structure in CODE_OF_CONDUCT.md",
    "name": "Zack Koppert"
  },
  {/*...*/},
  {
    "message": "Create README.md",
    "name": "Ben Balter"
  }
]
```
</div>

```bash title="Nested collect and map"
curl -s 'https://api.github.com/repos/github/.github/commits' \
  | jq '[.[] | {message: .commit.message, name: .commit.author.name, parents: [.parents[].html_url]}]'
```
<div class="result" markdown>

```json
[
  {
    "message": "Merge pull request #340 from trishanu-init/patch-1\n\nchanged the content structure in CODE_OF_CONDUCT.md",
    "name": "Zack Koppert",
    "parents": [
      "https://github.com/github/.github/commit/d9c05dfc6b02cafe78a6342a73e9e9096273c4fd",
      "https://github.com/github/.github/commit/b41159a31d90042b9e612b3eadeb607ac880ce02"
    ]
  },
  {/*...*/},
  {
    "message": "Create README.md",
    "name": "Ben Balter",
    "parents": [
      "https://github.com/github/.github/commit/d707be9dc0c8e9ebf6e198aa925f89f88486c273"
    ]
  }
]
```
</div>

```bash title="Group and count"
curl -s 'https://api.github.com/repos/github/.github/commits' \
  | jq 'group_by(.commit.author.name) | map({(.[0].commit.author.name): length}) | add'
```
<div class="result" markdown>

```json
{
  "Alex Webb": 1,
  "Ashley Wolf": 6,
  "Ben Balter": 3,
  "Daniel Adams": 1,
  "Diana Moore": 1,
  "Dinakar": 1,
  "Fayas Noushad": 1,
  "Justin Hutchings": 1,
  "Matthias Wenz": 1,
  "Nihaal Sangha": 1,
  "Paranoïd User": 1,
  "Phil Turnbull": 3,
  "Trishanu Nayak": 2,
  "Zack Koppert": 7
}
```
</div>

### Merge SARIF reports

```bash
find . -type f -name "*.sarif" -print0 | xargs -0 jq -n '
  {
    "$schema": "https://json.schemastore.org/sarif-2.1.0.json",
    version: "2.1.0",
    runs: (
      reduce inputs.runs[] as $r ([]; . + [$r])
    )
  }
'
```

[🔗 microsoft's SARIF Multitool](https://github.com/microsoft/sarif-sdk/blob/main/docs/multitool-usage.md)

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

### Process substitution

```bash
diff <(ls foo/) <(ls bar/) 
```

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

### Split string into array

```bash
INPUT="a (b)   \"c\""
IFS=" " read -ra array <<< "$INPUT"
printf '%s\n' "${array[@]}"
```
<div class="result" markdown>
```bash
a
(b)
"c"
```
</div>

### Strip XML comments

```bash
cat foo.xml |
  sed 's/<!--/\x0<!--/g;s/-->/-->\x0/g' `: # Add null chars before and after delimiters` |
  grep -zv '^<!--' `: # Set null chars as grep delimiter and invert match` |
  tr -d '\0' `: # Remove null chars` |
  xmllint --format - `: # Optional reformat to remove empty lines`
```

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

### Total size of files

```bash
find . -type f -name "*.log" -print0 `: # find all .log files` |
  xargs -0 du --total --human-readable `: # compute total space usage` |
  awk 'END{print $1}' `: # extract total value`
```
