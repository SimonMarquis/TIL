---
title: 📖 MkDocs
---

### Attribute Lists

```md
[Hello, World!](#){: #someid .someclass somekey='some value' }
```
<div class="result" markdown>

[Hello, World!](#){: #someid .someclass somekey='some value' }

</div>

[🔗](https://python-markdown.github.io/extensions/attr_list)

### Dependency management

```python title="docs/requirements.txt"
mkdocs==1.4.3
mkdocs-material==9.1.16
```

```bash
pip install --requirement docs/requirements.txt
```

### Environment variables

```yaml title="mkdocs.yml"
plugins:
  - foo-plugin:
      enabled: !ENV [CI, GITHUB_ACTIONS, False]
```

[🔗](https://www.mkdocs.org/user-guide/configuration/#environment-variables)

### Result box

```bash title="Say hello!"
echo "Hello, World!"
```
<div class="result" markdown>
```
Hello, World!
```
</div>
