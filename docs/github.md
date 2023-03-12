---
title: 🐙 GitHub
---

### Cancel workflows with the same reference

```yaml
concurrency:
  group: ${{ github.head_ref }}
  cancel-in-progress: true
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

### Fork detection on PR

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