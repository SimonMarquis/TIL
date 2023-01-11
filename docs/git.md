---
title: 💽 Git
---

### Alias to function

```bash title="~/.gitconfig"
[alias]
    hello = "!f() { echo \"Hello, ${1:-World}!\" ; }; f"
```

### Authors with commit count

```bash title="~/.gitconfig"
[alias]
    authors = "!git log --pretty=format:%aN | sort | uniq -c | sort -rn"
```

### Change author without changing dates

```bash
git -c rebase.instructionFormat='%s%nexec GIT_COMMITTER_DATE="%cD" git commit --amend --author=<author> --no-edit' rebase -i <refspec>
```

### Check if something can be pushed

```bash
git log <sha1>..HEAD [--oneline] --exit-code # 1:yes, 0:no
```

### Check if something has changed

```bash
git diff [--cached] [--stat] [--quiet] --exit-code -- [<pathspec>…] # 1:yes, 0:no
```

or

```bash
git diff-index [--cached] [--stat] [--quiet] --exit-code HEAD # 1:yes, 0:no
```

### Default commit message

```bash
git config --global commit.template ~/.gitmessage
```

### Diffing Gzip-ed JSON files

```bash title="~/.gitattributes"
*.json.gz diff=json.gz
```

```bash title="~/.gitconfig"
[core]
    attributesFile = ~/.gitattributes
[diff "json.gz"]
    binary = true
    textconv = "f() { uncompress -c \"$1\" | jq ; }; f"
    # OR # textconv = sh -c 'uncompress -c "$0" | jq'
    # OR with: zcat, gzcat, etc.
```

- Before
  ```diff
  diff --git a/example.json.gz b/example.json.gz
  index 4ecec5e..ae04c42 100644
  Binary files a/example.json.gz and b/example.json.gz differ
  ```

- After
  ```diff
  diff --git a/example.json.gz b/example.json.gz
  index 4ecec5e..ae04c42 100644
  --- a/example.json.gz
  +++ b/example.json.gz
  @@ -1,3 +1,3 @@
   {
  -  "key": true
  +  "key": false
   }
  ```

[🔗](https://git-scm.com/docs/gitattributes#_performing_text_diffs_of_binary_files)

### Diffing with patience

```bash title="~/.gitconfig"
[diff]
    # git config --global diff.algorithm patience
    algorithm = patience
```

### Ignoring commits in the blame view

```bash title=".git-blame-ignore-revs"
# Reformat code
44e8ca9a329dbb7a673b55cd25fbe982f10572fa
# Add newline at end of files
2f5f618ff431f87687e7446f0980849a88d01d9a
```

- Manually
    ```bash
    git blame --ignore-revs-file .git-blame-ignore-revs <file>
    ```
- Automatically
    ```bash
    # Ignore revisions listed in the file, one unabbreviated object name per line.
    git config --global blame.ignoreRevsFile .git-blame-ignore-revs
    # Mark any lines that have had a commit skipped using --ignore-rev with a `?`
    git config --global blame.markIgnoredLines true
    # Mark any lines that were added in a skipped commit and can not be attributed with a `*`
    git config --global blame.markUnblamableLines true
    ```

[🔗](https://docs.github.com/en/repositories/working-with-files/using-files/viewing-a-file#ignore-commits-in-the-blame-view)

### List objects by size

```bash
git rev-list --objects --all |
  git cat-file --batch-check='%(objecttype) %(objectname) %(objectsize) %(rest)' |
  sed -n 's/^blob //p' |
  sort --numeric-sort --key=2 |
  cut -c 1-12,41- |
  $(command -v gnumfmt || echo numfmt) --field=2 --to=iec-i --suffix=B --padding=7 --round=nearest
```

[🔗](https://stackoverflow.com/a/42544963/3615879)

### Print changes between two refs

```bash
git log --topo-order --pretty=format:"%h ~ %s" $1..$2 --no-merges
```

### Rebase dependent branch

```bash
# git rebase --onto <what-branch> <from-exclusive>@{1} <up-to-inclusive>
git rebase --onto featureA featureA@{1} featureB
```

### Recursive gc

```bash
find . -name '*.git' -execdir sh -c 'cd {} && git gc' \;
```

### Signing commits with GPG

[🔗](https://docs.github.com/en/authentication/managing-commit-signature-verification/signing-commits) [🔗](https://withblue.ink/2020/05/17/how-and-why-to-sign-git-commits.html)
