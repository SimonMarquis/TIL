(Top portion unchanged)

    === ":simple-git: `~/.gitattributes`"

    ```bash
    * text=auto eol=lf

    *.{bat,[bB][aA][tT]} text eol=crlf
    *.{cmd,[cC][mM][dD]} text eol=crlf

    *.jar binary
    *.png binary
    *.gif binary
    *.jpg binary
    *.jpeg binary

    *.json.gz diff=json.gz
    ```

    === "🖥️ `~/setup-code-review.sh`"

    ```bash
    #!/usr/bin/env bash

    git config --global alias.open '!f() {
        local type="${1:-branch}"
        local target="${2:-HEAD}"
        local current_upstream="$(git for-each-ref --format="%(upstream:remotename)" "$(git symbolic-ref -q "$target")")"
        local first_remote="$(git remote show | head -n 1)"
        local remote=${current_upstream:-$first_remote}
        remote=${upstream:-origin}

        if [ "$type" = "branch" ] || [ "$type" = "pr" ]; then
            # get full name (i.e. refs/heads/*; refs/remotes/*/*); src: https://stackoverflow.com/a/9753364
            target="$(git rev-parse --symbolic-full-name "$target")"

            if [ "$target" != "${target#"refs/remotes/"}" ]; then
                # extract from remote branch reference
                target="${target#"refs/remotes/"}"
            else
                # extract from local branch reference; src: https://stackoverflow.com/a/9753364
                target="$(git for-each-ref --format="%(upstream:short)" "$target")"
            fi
            # split remote/branch
            remote="${target%%/*}"
            target="${target#"$remote/"}"

            if [ -z "$remote" ]; then
                echo "Branch ($2) does not point to a remote repository." >&2
                return 2
            fi
        fi

        local repo_url="$(git remote get-url "$remote" | sed -E -e "s/(\.(com|org|io)):/\1\/" -e "s/git@/https:\/\/" -e "s/\.git$//")"
    ```
