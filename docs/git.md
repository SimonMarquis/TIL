---
title: 💽 Git
---

??? example "Personal Git config files"

    === ":simple-git: `~/.gitconfig`"

        ```bash
        [user]
            name = Simon Marquis
            email = contact@simon-marquis.fr

        [branch]
            autosetuprebase = always

        [alias]
            authors = !git log --pretty=format:%aN | sort | uniq -c | sort -rn
            branches = branch -a
            changelog = "!f() { git log --topo-order --pretty=format:\"%h ~ %s\" \"$1..${2:-HEAD}\" --no-merges; }; f"
            last = log -1 --stat
            lg = log --all --graph --pretty=format:"%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %Cblue<%an>%Creset" --abbrev-commit --date=relative
            remotes = remote -v
            start = !git init && git commit --allow-empty -m 'Initial commit'
            tags = tag -n
            this = !git init && git add --all && git commit -m 'Initial commit'
            # git rebase --onto <what-branch> <from-exclusive>@{1} <up-to-inclusive>
            rebase-onto = "!f() { git rebase --onto \"$1\" \"$1@{1}\" \"$2\"; }; f"
            undo = reset --soft HEAD^
            unstage = reset HEAD --
            whoami= !git config --global user.name && git config --global user.email

        [commit]
            template = ~/.gitmessage

        [core]
            attributesFile = ~/.gitattributes
            excludesfile = ~/.gitignore_global

        [diff]
            algorithm = patience

        [diff "json.gz"]
            binary = true
            textconv = "!f(){ gzcat --suffix .gz \"$1\" | jq; }; f"

        [filter "lfs"]
            required = true
            clean = git-lfs clean -- %f
            smudge = git-lfs smudge -- %f
            process = git-lfs filter-process

        [fetch]
            prune = true

        [gitreview]
            notopic = true

        [init]
            defaultBranch = main

        [merge]
            ff = false
            autoStash = true

        [pull]
            rebase = true

        [push]
            default = current

        [rebase]
            autoSquash = true
            autoStash = true

        [rerere]
            enabled = true
        ```

    === ":simple-git: `~/.gitignore_global`"

        ```bash
        ### Java / Kotlin ###
        # Compiled class file
        *.class

        # Log file
        *.log

        # BlueJ files
        *.ctxt

        # Mobile Tools for Java (J2ME)
        .mtj.tmp/

        # virtual machine crash logs
        hs_err_pid*
        replay_pid*

        ### Linux ###
        *~

        # temporary files which can be created if a process still has a handle open of a deleted file
        .fuse_hidden*

        # KDE directory preferences
        .directory

        # Linux trash folder which might appear on any partition or disk
        .Trash-*

        # .nfs files are created when an open file is removed but is still being accessed
        .nfs*

        ### macOS ###
        # General
        .DS_Store
        .AppleDouble
        .LSOverride

        # Icon must end with two \r
        Icon


        # Thumbnails
        ._*

        # Files that might appear in the root of a volume
        .DocumentRevisions-V100
        .fseventsd
        .Spotlight-V100
        .TemporaryItems
        .Trashes
        .VolumeIcon.icns
        .com.apple.timemachine.donotpresent

        # Directories potentially created on remote AFP share
        .AppleDB
        .AppleDesktop
        Network Trash Folder
        Temporary Items
        .apdisk

        ### macOS Patch ###
        # iCloud generated files
        *.icloud

        ### Windows ###
        # Windows thumbnail cache files
        Thumbs.db
        Thumbs.db:encryptable
        ehthumbs.db
        ehthumbs_vista.db

        # Dump file
        *.stackdump

        # Folder config file
        [Dd]esktop.ini

        # Recycle Bin used on file shares
        $RECYCLE.BIN/

        # Windows Installer files
        *.cab
        *.msi
        *.msix
        *.msm
        *.msp

        # Windows shortcuts
        *.lnk
        ```

    === ":simple-git: `~/.gitattributes`"

        ```bash
        *.json.gz diff=json.gz
        ```

### Alias to function

```bash title="~/.gitconfig"
[alias]
    hello = "!f() { echo \"Hello, ${1:-World}!\" ; }; f"
```

### Authors with commit count

```bash title="~/.gitconfig"
[alias]
    authors = !git log --pretty=format:%aN | sort | uniq -c | sort -rn
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

### Commit with message from standard input

```bash
( \
  echo -e "Hello, World!" ; \
  any-command-that-will-produce-text-output ; \
) | git commit --file -
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
git log --topo-order --pretty=format:"%h ~ %s" "$1..${2:-HEAD}" --no-merges
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
