---
title: 🔀 Sublime Merge
---

### Custom commands

!!! example "`Preferences` → `Browse Packages`"

    - [Menus](https://www.sublimemerge.com/docs/menus)
    - [Custom Commands](https://www.sublimemerge.com/docs/custom_commands)

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

=== "`Branch.sublime-menu`"
    ```json
    [
        { "caption": "-", "id": "end" },
        {
            "caption": "🔗 Open Branch $branch",
            "command": "git",
            "args": { "argv": ["open", "branch", "$branch"] }
        },
        {
            "caption": "🔗 Open Pull Request on $branch",
            "command": "git",
            "args": { "argv": ["open", "pr", "$branch"] }
        },
        // git config --global alias.sync '!f() { \
        //   local branch="${1:?Error: Missing <branch> argument!}"; \
        //   local upstream=$(git config "branch.${branch}.remote") || (echo "Error: No upstream remote found for branch [$branch]." >&2; return 1); \
        //   local upstream_branch=$(git config "branch.${branch}.merge" | sed "s#refs/heads/##") || (echo "Error: No upstream branch configured for branch [$branch]." >&2; return 1); \
        //   git fetch "$upstream" "$upstream_branch":"$branch"; \
        // }; f'
        {
            "caption": "⏫ Sync branch with upstream…\tgit sync $branch",
            "command": "git",
            "args": {"argv": ["sync", "$branch"]}
        }
    ]
    ```

=== "`Commit.sublime-menu`"
    ```json
    [
        { "caption": "-", "id": "end" },
        {
            "caption": "🔗 Open Commit $short_commit",
            "command": "git",
            "args": { "argv": ["open", "commit", "$commit"] }
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
        // Code Review
        {
            "caption": "🔗 Open Repository…",
            "command": "git",
            "args": { "argv": ["open", "repo"] }
        },
        {
            "caption": "🔗 Open Branch…",
            "command": "git",
            "args": { "argv": ["open", "branch", "$select_branch"] }
        },
        {
            "caption": "🔗 Open Pull Request…",
            "command": "git",
            "args": { "argv": ["open", "pr", "$select_branch"] }
        },
        {
            "caption": "🔗 Open Tag…",
            "command": "git",
            "args": { "argv": ["open", "tag", "$select_tag"] }
        },
        {
            "caption": "🔗 Open Commit…",
            "command": "git",
            "args": { "argv": ["open", "commit", "$select_commit"] }
        },
        {
            "caption": "🔗 Open Search…",
            "command": "git",
            "args": { "argv": ["open", "search", "$text"] }
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

=== "`Remote Branch.sublime-menu`"
    ```json
    [
        { "caption": "-", "id": "end" },
        {
            "caption": "🔗 Open Branch $branch",
            "command": "git",
            "args": { "argv": ["open", "branch", "$branch"] }
        },
        {
            "caption": "🔗 Open Pull Request on $branch",
            "command": "git",
            "args": { "argv": ["open", "pr", "$branch"] }
        }
    ]
    ```

=== "`Tag.sublime-menu`"
    ```json
    [
        { "caption": "-", "id": "end" },
        {
            "caption": "🔗 Open Tag $tag_name",
            "command": "git",
            "args": { "argv": ["open", "tag", "$tag_name"] }
        }
    ]
    ```
