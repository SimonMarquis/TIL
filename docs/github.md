---
title: 🐙 GitHub
---

### Checkout current PR branch

By default, `actions/checkout` will checkout PRs in 'detached HEAD' state using `#!bash git checkout --progress --force refs/remotes/pull/#/merge`.

```yaml
- uses: actions/checkout@v4
  with:
    ref: ${{ github.head_ref }}
```

### Clone GitHub gists

```bash
git clone https://gist.github.com/YOUR_REPOSITORY.git
```

[🔗](https://docs.github.com/en/get-started/writing-on-github/editing-and-sharing-content-with-gists/forking-and-cloning-gists#cloning-gists)

### Clone GitHub wikis

```bash
git clone https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.wiki.git
```

[🔗](https://docs.github.com/en/communities/documenting-your-project-with-wikis/adding-or-editing-wiki-pages#adding-or-editing-wiki-pages-locally)

### Comment on new issues and PRs with gh CLI

```yaml title=".github/workflows/comment-new-issue-and-pr.yaml"
name: '💬 Comment on new issue and PRs'

on:
  issues:
    types: [opened]
  pull_request:
    types: [opened]

env:
  GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

jobs:
  comment:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - if: github.event_name == 'issues'
        run: gh issue comment $ISSUE_NUMBER --body "Thank you for opening this issue!"
        env:
          ISSUE_NUMBER: ${{ github.event.issue.number }}

      - if: github.event_name == 'pull_request'
        run: gh issue comment $PR_NUMBER --body "Thank you for opening this pull request!"
        env:
          PR_NUMBER: ${{ github.event.pull_request.number }}
```

[🔗](https://github.com/SimonMarquis/GitHub-Actions-Playground/blob/main/.github/workflows/comment-new-issue-and-pr.yaml)

### Commit from workflow

```yaml
jobs:
  commit:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - run: |
          git config --global user.name "Simon Marquis"
          git config --global user.email "SimonMarquis@users.noreply.github.com"
          git commit -m "Hello, World!" --allow-empty
          git push
```

### Complex conditionals

=== "Multiline strings"

    ```yaml
    # Supported block scalars: `>`, `>-`, `|`, `|-`
    if: >
      (
        github.event_name == 'pull_request'
      )
        ||
      (
        github.event_name == 'issue_comment' &&
        github.event.issue.pull_request &&
        contains(github.event.comment.body, 'specific string')
      )
    ```

=== "Expression syntax"

    ```yaml
    # Supported block scalars: `>-`, `|-`
    if: >-
      ${{
        (
          github.event_name == 'pull_request'
        )
          ||
        (
          github.event_name == 'issue_comment' &&
          github.event.issue.pull_request &&
          contains(github.event.comment.body, 'specific string')
        )
      }}
    ```

### Concurrency

```yaml title="Cancel any in-progress run of the job or workflow"
concurrency:
  group: ${{ github.head_ref }}
  cancel-in-progress: true
```

```yaml title="Cancel jobs or workflows with the same reference"
concurrency:
  group: '${{ github.workflow }}-${{ github.event.pull_request.head.label || github.head_ref || github.ref }}'
  cancel-in-progress: true
```

### Dependabot auto-merge

```yaml title=".github/workflows/dependabot-auto-merge" hl_lines="15"
name: 🤖 Dependabot auto-merge
on: pull_request

permissions:
  contents: write
  pull-requests: write

jobs:
  dependabot:
    runs-on: ubuntu-latest
    if: github.actor == 'dependabot[bot]'
    steps:
      - id: metadata
        uses: dependabot/fetch-metadata@v1
      - if: contains(fromJSON('["version-update:semver-major", "version-update:semver-minor", "version-update:semver-patch"]'), steps.metadata.outputs.update-type)
        run: gh pr merge --auto --merge "$PR_URL"
        env:
          PR_URL: ${{ github.event.pull_request.html_url }}
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

!!! note
    If you use status checks to test pull requests, you should enable Require status checks to pass before merging for the target branch for Dependabot pull requests. This branch protection rule ensures that pull requests are not merged unless all the required status checks pass. For more information, see "[Managing a branch protection rule](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/managing-a-branch-protection-rule)."

[🔗](https://docs.github.com/en/code-security/dependabot/working-with-dependabot/automating-dependabot-with-github-actions#enable-auto-merge-on-a-pull-request)

### Dependabot post update

```
name: 🤖 Dependabot post update
on:
  pull_request:
    # paths:

permissions:
  contents: write
  pull-requests: write

jobs:
  baseline:
    runs-on: ubuntu-latest
    if: github.actor == 'dependabot[bot]' && startsWith(github.head_ref, 'dependabot/')
    steps:
      - uses: actions/checkout@v4
        with:
          ref: ${{ github.head_ref }}
          token: ${{ secrets.DEPENDABOT_PAT }}
      # Setup (java/gradle/etc)
      # Run (script/task/etc)
      - run: |
          git config --global user.name "dependabot[bot]"
          git config --global user.email "49699333+dependabot[bot]@users.noreply.github.com"
          git commit -am "🤖 Dependabot post update" -m "[dependabot skip]"
          git push
```

### Dependabot skip

To allow dependabot to rebase or force push over extra commits, add `[dependabot skip]` , `[skip dependabot]`, `[dependabot-skip]`, or `[skip-dependabot]` to the commit message.

[🔗](https://docs.github.com/en/code-security/dependabot/working-with-dependabot/managing-pull-requests-for-dependency-updates#allowing-dependabot-to-rebase-and-force-push-over-extra-commits)

### Embedded Gists

```html
<script src="https://gist.github.com/<user>/<id>.js"></script>
```

or a specific file:

```html
<script src="https://gist.github.com/<user>/<id>.js?file=<filename>"></script>
```

[🔗](https://docs.github.com/en/get-started/writing-on-github/editing-and-sharing-content-with-gists/creating-gists)

### Environment variables

```yaml
name: Greeting on variable day
on: workflow_dispatch
env:
  DAY_OF_WEEK: Monday
jobs:
  greeting_job:
    runs-on: ubuntu-latest
    env:
      Greeting: Hello
    steps:
      - run: echo "$Greeting $First_Name. Today is $DAY_OF_WEEK!"
        env:
          First_Name: Mona
```

[🔗](https://docs.github.com/en/actions/learn-github-actions/variables#defining-environment-variables-for-a-single-workflow)

### Executing step regardless of status

!!! quote
    **Note:** Avoid using `always()` for any task that could suffer from a critical failure, for example: getting sources, otherwise the workflow may hang until it times out. If you want to run a job or step regardless of its success or failure, use the recommended alternative: `success() || failure()`.
    [🔗](https://docs.github.com/en/actions/learn-github-actions/expressions#always)

```yaml
steps:
  - run: ...

  - name: 👎
    if: ${{ always() }}
    run: ...

  - name: 👍
    if: ${{ success() || failure() }}
    run: ...
```

### Expand all diffs

By default, GitHub will limit the number of expanded diffs in a PR.  
Run this script to force open all diffs (<a href='javascript:{[].forEach.call(document.querySelectorAll("button.load-diff-button"),function(n){n.click()});}'>bookmarklet :material-bookmark:</a>):

```javascript
document
  .querySelectorAll("button.load-diff-button")
  .forEach((node) => node.click());
```

### Fork detection on PR

!!! warning "Can be misleading if the PR comes from the same repository but that repository is a fork itself!"

    ```yaml
    on: pull_request
    jobs:
      non-fork:
        if: ${{ !github.event.pull_request.head.repo.fork }}
        name: Will NOT run on forks
      fork-only:
        if: ${{ github.event.pull_request.head.repo.fork }}
        name: Will ONLY run on forks
    ```

```yaml
on: pull_request
jobs:
  non-fork:
    if: ${{ github.event.pull_request.head.repo.full_name == github.repository }}
    name: Will NOT run on forks
  fork-only:
    if: ${{ github.event.pull_request.head.repo.full_name != github.repository }}
    name: Will ONLY run on forks
```

### Glob patterns checks

If the pattern does not match any files, this returns an empty string.

```yaml
- name: 'Only if it contains any text file'
  if: hashFiles('**/*.txt') != ''
  run: echo "yes"
```

### Google's Maven repository for dependabot

```yml title=".github/dependabot.yml"
version: 2
updates:
  - package-ecosystem: "gradle"
    directory: "/"
    schedule:
      interval: "daily"
    registries: "*"
    labels: [ ]
registries:
  maven-google:
    type: "maven-repository"
    url: "https://maven.google.com"
    replaces-base: true
```

### Java in Codespace

```bash
sdk current java
```
<div class="result" markdown>

  ```bash
  Using java version 17.0.10-ms
  ```

</div>

```bash
sdk list java
```
<div class="result" markdown>

  ```bash
  ================================================================================
  Available Java Versions for Linux 64bit
  ================================================================================
   Vendor        | Use | Version      | Dist    | Status     | Identifier
  --------------------------------------------------------------------------------
   Microsoft     |     | 21.0.3       | ms      |            | 21.0.3-ms           
                 |     | 21.0.2       | ms      | installed  | 21.0.2-ms           
                 |     | 21.0.1       | ms      |            | 21.0.1-ms           
                 |     | 17.0.11      | ms      |            | 17.0.11-ms          
                 | >>> | 17.0.10      | ms      | installed  | 17.0.10-ms          
  ```

</div>

```bash
# Use ↹ to autocomplete version name
sdk default java 21.0.2-ms
```
<div class="result" markdown>

  ```bash
  setting java 21.0.2-ms as the default version for all shells.
  ```

</div>

### Job outputs

```yaml
jobs:
  job1:
    runs-on: ubuntu-latest
    outputs:
      output1: ${{ steps.step1.outputs.foo }}
      output2: ${{ steps.step2.outputs.baz }}
    steps:
      - id: step1
        run: echo "foo=bar" >> $GITHUB_OUTPUT
      - id: step2
        run: echo "baz=qux" >> $GITHUB_OUTPUT
  job2:
    runs-on: ubuntu-latest
    needs: job1
    steps:
      - run: echo ${{needs.job1.outputs.output1}} ${{needs.job1.outputs.output2}}
```

### Job summary

```yaml
- name: Generate Job summary
  run: |
    echo "# Hello, World!" >> $GITHUB_STEP_SUMMARY
    echo "" >> $GITHUB_STEP_SUMMARY # this is a blank line
    echo "- a" >> $GITHUB_STEP_SUMMARY
    echo "- b" >> $GITHUB_STEP_SUMMARY
    echo "- c" >> $GITHUB_STEP_SUMMARY
```
<div class="result" markdown>

  ```markdown
  # Hello, World!

  - a
  - b
  - c
  ```

</div>

### Kotlin scripts caching

```yaml
env:
  KOTLIN_MAIN_KTS_COMPILED_SCRIPTS_CACHE_DIR: ${{ github.workspace }}/.main.kts

jobs:
  run:
    name: Kotlin script
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Cache Kotlin scripts
        uses: actions/cache@v3
        with:
          path: ${{ env.KOTLIN_MAIN_KTS_COMPILED_SCRIPTS_CACHE_DIR }}
          key: kts-${{ runner.os }}-${{ hashFiles('**/*.main.kts') }}

      - name: Ensure the Kotlin scripts cache directory exists
        run: mkdir -p "$KOTLIN_MAIN_KTS_COMPILED_SCRIPTS_CACHE_DIR"

      - run: ./foo.main.kts
```

### List changed files

```yaml
- name: Get changed files
  run: gh pr view ${{ github.event.number }} --json files -q '.files[].path'
```

### Matching multiple steps outcome

!!! warning
    
    A status check function call is **required**, otherwise an implicit `success()` is will be applied.


```yaml
steps:
  - id: foo
    run: ...

  - name: 👎
    if: ${{ always() && (steps.foo.outcome == "success" || steps.foo.outcome == "failure) }}
    run: ...

  - name: 👍
    if: ${{ always() && contains(fromJSON('["success", "failure"]'), steps.foo.outcome) }}
    run: ...
```

[🔗](https://docs.github.com/en/actions/learn-github-actions/expressions#example-matching-an-array-of-strings)

### Matrix strategy

```yaml
jobs:
  job:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        java-version: ['11', '17', '19']
    steps:
      - uses: actions/setup-java@v3
        with:
          distribution: 'temurin'
          java-version: ${{ matrix.java-version }}
      - run: java --version
```

### Matrix strategy from JSON

```yaml  
jobs:
  setup-matrix:
    runs-on: ubuntu-latest
    outputs:
      matrix: ${{ steps.matrix.outputs.matrix }}
    steps:
      - id: matrix
        run: echo "matrix=$(jq --raw-output --compact-output . <<< "$CONFIG")" >> $GITHUB_OUTPUT
        env:
          CONFIG: >-
            [
              {
                "id": "foo",
                "value": "Hello, Foo!",
                "array": [1, 2, 3]
              },
              {
                "id": "bar",
                "value": "Hello, Bar!",
                "array": [3, 2, 1]
              }
            ]

      - run: jq . <<< "$MATRIX"
        env:
          MATRIX: ${{ steps.matrix.outputs.matrix }}


  use-matrix:
    name: Use matrix @${{ matrix.id }}
    needs: setup-matrix
    runs-on: ubuntu-latest
    strategy:
      matrix:
        include: ${{ fromJSON(needs.setup-matrix.outputs.matrix) }}
    steps:
      - run: |
          echo "ID=$ID"
          echo "VALUE=$VALUE"
          echo "ARRAYS=$ARRAYS"
        env:
          ID: ${{ matrix.id }}
          VALUE: ${{ matrix.value }}
          ARRAYS: ${{ join(matrix.array.*, ', ') }}
```

### Multline variables

!!! warning

    Make sure the delimiter you're using won't occur on a line of its own within the value. If the value is completely arbitrary then you shouldn't use this format. Write the value to a file instead.

- Environment variable
  ```yaml
  - run: |
      {
        echo 'RESULT<<EOF'
        curl https://example.com
        echo EOF
      } >> "$GITHUB_ENV"
  ```

- Output parameter
  ```yaml
  - run: |
      {
        echo 'result<<EOF'
        curl https://example.com
        echo EOF
      } >> "$GITHUB_OUTPUT"
  ```

[🔗](https://docs.github.com/en/actions/using-workflows/workflow-commands-for-github-actions#multiline-strings)

### Print messages in workflow steps

```yaml
runs-on: ubuntu-latest
steps:
  - run: echo "::debug::This is a debug message"
  - run: echo "::notice::This is a notice message"
  - run: echo "::warning::This is a warning message"
  - run: |
        echo "::group::Group title"
        echo "Inside group"
        echo "::endgroup::"
```

### Rename workflow at runtime 

```yaml
name: Build
run-name: Build by @${{ github.actor }}
```

### Restrict workflow to a specific repository

```yaml
jobs:
  deploy:
    if: github.repository == 'UserName/RepositoryName'
```

### Reuse local composite action 

```yaml title=".github/actions/hello/action.yml"
name: 'Hello'
description: 'Say Hello to someone'
inputs:
  who:
    description: 'Who?'
    default: 'World'
    required: true
outputs:
  result:
    description: "Random number"
    value: ${{ steps.compute.outputs.result }}
runs:
  using: composite
  steps:
    - id: compute
      run: echo "result=Hello, $WHO!" >> $GITHUB_OUTPUT
      shell: bash
      env:
        WHO: ${{ inputs.who }}
```

```yaml title=".github/workflows/test.yml"
on: workflow_dispatch
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: .github/actions/hello
        with:
          who: Bob

```

[🔗](https://docs.github.com/en/actions/learn-github-actions/finding-and-customizing-actions#using-inputs-and-outputs-with-an-action)

[🔗](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#run-name)

### Secret file in GitHub Actions

Create a new secret with https://github.com/[user]/[project]/settings/secrets/actions/new

- **Name:** `MY_SECRET`
- **Value:** base64 representation of the file content `#!bash base64 --wrap=0 secret.json`

```yaml title=".github/workflows/my_workflow.yml"
jobs:
  my_job:
    name: My Job
    runs-on: ubuntu-latest
    steps:

      - name: Create secret.json
        run: echo "$MY_SECRET" | base64 --decode > secret.json
        env:
          MY_SECRET: ${{ secrets.MY_SECRET }}

      - name: Check file
        run: stat secret.json

      - name: Delete secret.json
        run: rm secret.json
        if: always()
```

[🔗](https://docs.github.com/en/actions/security-guides/encrypted-secrets#storing-base64-binary-blobs-as-secrets)

### Setting an environment variable

```yaml
steps:
  - name: Set the value
    run: echo "foo=bar" >> $GITHUB_ENV
  - name: Use the value
    run: echo "${{ env.foo }}"
```

### Setting an output parameter

```yaml
steps:
  - id: foo
    run: echo "BAR=BAZ" >> $GITHUB_OUTPUT
  - run: echo "${{ steps.foo.outputs.BAR }}"
```

### Share artifacts between jobs

!!! quote

    Note: You can only download artifacts in a workflow that were uploaded during the same workflow run.  
    [🔗](https://docs.github.com/en/actions/using-workflows/storing-workflow-data-as-artifacts#passing-data-between-jobs-in-a-workflow)

```yaml
jobs:
  save-job:
    steps:
      - run: echo "..." > output.txt
      - uses: actions/upload-artifact@v3
        with:
          name: output
          path: output.txt
  load-job:
    needs: save-job
    steps:
      - uses: actions/download-artifact@v3
        with:
          name: output
      - run: cat output.txt


To download an artifact from a separate workflow run, you can use the actions/download-artifact action. For example, you can download the artifact named output-log-file.

jobs:
  example-job:
    steps:
      - name: Download a single artifact
```

### Skipping workflow runs

!!! quote

    Workflows that would otherwise be triggered using `on: push` or `on: pull_request` won't be triggered if you add any of the following strings to the commit message in a push, or the HEAD commit of a pull request:

    - `[skip ci]`
    - `[ci skip]`
    - `[no ci]`
    - `[skip actions]`
    - `[actions skip]`

    Alternatively, you can end the commit message with two empty lines followed by either:

    - `skip-checks:true`
    - `skip-checks: true`

    To *request* checks for a commit, end the commit message with two empty lines followed by `request-checks: true`.

[🔗](https://docs.github.com/en/actions/managing-workflow-runs/skipping-workflow-runs) [🔗](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/collaborating-on-repositories-with-code-quality-features/about-status-checks#skipping-and-requesting-checks-for-individual-commits)

### Ternary operator

```yaml
FOO: ${{ <condition> && <true> || <false> }}
```

!!! example
    ```yaml
    API_ENV: ${{ github.ref_name == 'main' && 'prod' || 'staging' }}
    ```

!!! warning
    If the value of `<true>` is _falsy_, the result of the expression will be `<false>`.

!!! tip "[`case` syntax is now supported](https://docs.github.com/en/actions/reference/workflows-and-actions/expressions#case)"

    ```yaml
    MY_ENV_VAR: |-
      ${{ case(
        github.ref == 'refs/heads/main', 'production',
        github.ref == 'refs/heads/staging', 'staging',
        startsWith(github.ref, 'refs/heads/feature/'), 'development',
        'unknown'
      ) }}
    ```

### Use git as an app's bot user

```yaml
on: [pull_request]

jobs:
  auto-format:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/create-github-app-token@v1
        id: app-token
        with:
          app-id: ${{ vars.APP_ID }}
          private-key: ${{ secrets.PRIVATE_KEY }}
      - name: Get GitHub App User ID
        id: get-user-id
        run: echo "user-id=$(gh api "/users/${APP_SLUG}[bot]" --jq .id)" >> "$GITHUB_OUTPUT"
        env:
          APP_SLUG: ${{ steps.app-token.outputs.app-slug }}
          GH_TOKEN: ${{ steps.app-token.outputs.token }}
      - run: |
          git config --global user.name "${APP_SLUG}[bot]"
          git config --global user.email "${APP_USER_ID}+${APP_SLUG}[bot]@users.noreply.github.com"
        env:
          APP_SLUG: ${{ steps.app-token.outputs.app-slug }}
          APP_USER_ID: ${{ steps.get-user-id.outputs.user-id }}
      - run: |
          git commit -m "Auto-generated changes" -- foo
          git push
```

!!! tip

    The `<BOT USER ID>` is the numeric user ID of the app's bot user, which can be found under `https://api.github.com/users/<app-slug>[bot]`.

    For example, we can check at [`https://api.github.com/users/dependabot[bot]`](https://api.github.com/users/dependabot[bot]) to see the user ID of Dependabot is 49699333.

    Alternatively, you can use the [octokit/request-action](https://github.com/octokit/request-action) to get the ID.

[🔗](https://github.com/actions/create-github-app-token/blob/main/README.md#configure-git-cli-for-an-apps-bot-user)

### Worflow input as command line arguments

```yaml
on:
  workflow_dispatch:
    inputs:
      arguments:
        required: true
        type: string

jobs:
  gradle:
    runs-on: ubuntu-latest
    steps:
      - run: |
          IFS=" " read -ra args <<< "$ARGS"
          ./my-command "${args[@]}"
        env:
          ARGS: ${{ inputs.arguments }}
```

### Workflow input types

```yaml
on:
  workflow_dispatch:
    inputs:
      name:
        type: string
        required: true
      age:
        type: number
        required: true
      size:
        type: choice
        required: true
        options:
        - s
        - m
        - l
      test:
        type: boolean
        default: false
      env:
        type: environment
jobs:
  job:
    runs-on: ubuntu-latest
    steps:
      - run: echo "name=$INPUT_NAME age=$INPUT_AGE size=$INPUT_SIZE test=$INPUT_TEST env=$INPUT_ENV"
        env:
          INPUT_NAME: ${{ github.event.inputs.name }}
          INPUT_AGE:  ${{ github.event.inputs.age }}
          INPUT_SIZE: ${{ github.event.inputs.size }}
          INPUT_TEST: ${{ github.event.inputs.test }}
          INPUT_ENV:  ${{ github.event.inputs.env }}
```

[🔗](https://github.blog/changelog/2021-11-10-github-actions-input-types-for-manual-workflows/)