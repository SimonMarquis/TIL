---
title: 🐙 GitHub
---

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
