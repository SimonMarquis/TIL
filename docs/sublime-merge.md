---
title: 🔀 Sublime Merge
---

### Custom commands

> `Preferences` → `Browse Packages`  
> [Documentation](https://www.sublimemerge.com/docs/custom_commands)

=== "`Action.sublime-menu`"
    ```json
    [
        {
            "caption": "Open Repository in Explorer…",
            "command": "open_dir",
            "args": {
                "dir": "$working_dir"
            }
        }
    ]
    ```

=== "`Commit.sublime-menu`"
    ```json
    [
        {
            "caption": "Gerrit: Open commit $short_commit",
            "command": "git",
            "args": { "argv": ["gerrit-query", "commit:", "$commit"] }
        }
    ]
    ```

=== "`Default.sublime-commands`"
    ```json
    [
        {
            "caption": "Status\tgit status",
            "command": "git",
            "args": {"argv": ["status", "--untracked-files", "--verbose"]}
        },
        {
            "caption": "Status: short\tgit status --short",
            "command": "git",
            "args": {"argv": ["status", "--short", "--untracked-files", "--verbose"]}
        },
        {
            "caption": "Cleanup\tgit gc",
            "command": "git",
            "args": {"argv": ["gc"]}
        },
        {
            "caption": "Version\tgit --version",
            "command": "git",
            "args": {"argv": ["--version"]}
        },
        // Listing
        {
            "caption": "List branches with commit…",
            "command": "git",
            "args": {"argv": ["branch", "--sort=-committerdate", "--format=%(committerdate:short) %(refname:short)", "--contains", "$select_commit"]}
        },
        {
            "caption": "List tags with commit…",
            "command": "git",
            "args": {"argv": ["tag", "--sort=-creatordate", "--format=%(creatordate:short) %(refname:short)", "--contains", "$select_commit"]}
        },
        {
            "caption": "List branches merged into branch…",
            "command": "git",
            "args": {"argv": ["branch", "--merged", "$select_branch"]}
        },
        {
            "caption": "List branches not merged into branch…",
            "command": "git",
            "args": {"argv": ["branch", "--no-merged", "$select_branch"]}
        },
        // Gerrit UI
        // git config gerrit.web-ui-url "https://..."
        // git config --global alias.gerrit-query "!f() { IFS='' ; URL=\"$(git config gerrit.web-ui-url)/q/$*\" ; explorer \"$URL\" ; }; f"
        {
            "caption": "Gerrit: Search…\t/q/<query>",
            "command": "git",
            "args": { "argv": ["gerrit-query", "$text"] }
        },
        {
            "caption": "Gerrit: Open commit…\t/q/commit:<commit>",
            "command": "git",
            "args": { "argv": ["gerrit-query", "commit:", "$select_commit"] }
        },
        {
            "caption": "Gerrit: Open branch…\t/q/branch:<branch>",
            "command": "git",
            "args": { "argv": ["gerrit-query", "branch:", "$select_local_branch"] }
        },
        // Gerrit Review
        {
            "caption": "Review…\tgit review <branch>",
            "command": "git",
            "args": {"argv": ["review", "$text", "--no-rebase", "--yes", "--verbose"]}
        },
        {
            "caption": "Review: Setup\tgit review --setup",
            "command": "git",
            "args": {"argv": ["review", "--setup", "--verbose"]}
        },
        {
            "caption": "Review: List open reviews\tgit review ---list",
            "command": "git",
            "args": {"argv": ["review", "--list", "--verbose"]}
        },
        {
            "caption": "Review: New ChangeId…\tgit review --new-changeid",
            "command": "git",
            "args": {"argv": ["review", "--new-changeid", "--no-rebase", "--verbose"]}
        },
        {
            "caption": "Review: Dry run…\tgit review <branch> --dry-run",
            "command": "git",
            "args": {"argv": ["review", "$text", "--dry-run", "--no-rebase", "--yes", "--verbose"]}
        },
        {
            "caption": "Review: Work in progress…\tgit review <branch> --work-in-progress",
            "command": "git",
            "args": {"argv": ["review", "$text", "--work-in-progress", "--no-rebase", "--yes", "--verbose"]}
        },
        {
            "caption": "Review: Draft…\tgit review <branch> ---draft",
            "command": "git",
            "args": {"argv": ["review", "$text", "--draft", "--no-rebase", "--yes", "--verbose"]}
        },
        {
            "caption": "Review: Private…\tgit review <branch> --private",
            "command": "git",
            "args": {"argv": ["review", "$text", "--private", "--no-rebase", "--yes", "--verbose"]}
        },
        {
            "caption": "Review: Download…\tgit review --download <change>",
            "command": "git",
            "args": {"argv": ["review", "-d", "$text", "--verbose"]}
        },
        // Misc
        // git config --global alias.hello "!f() { echo \"Hello, ${1:-World}!\" ; }; f"
        { 
            "caption": "Test commands \tHello, World!", 
            "command": "git", 
            "args": {"argv": ["hello", "$text"] }
        }
    ]
    ```

=== "`Diff Context.sublime-menu`"
    ```json
    [
        {
            "caption": "Stash file",
            "command": "git",
            "args": {"argv": ["stash", "push", "$path"] }
        }
    ]
    ```

=== "`Preferences.sublime-settings`"
    ```json
    {
        "hide_menu": true,
        "always_show_command_status": true
    }
    ```
