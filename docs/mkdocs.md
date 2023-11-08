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

### Downloadable file

```md
[:material-launch:](assets/example.json){: .md-button }
[:material-download:](assets/example.json){: .md-button download="example.json" }
```
<div class="result" markdown>

[:material-launch:](assets/example.json){: .md-button }
[:material-download:](assets/example.json){: .md-button download="example.json" }

</div>

### Environment variables

```yaml title="mkdocs.yml"
plugins:
  - foo-plugin:
      enabled: !ENV [CI, GITHUB_ACTIONS, False]
```

[🔗](https://www.mkdocs.org/user-guide/configuration/#environment-variables)

### Open link in new tab

```md
[Open :material-launch:](https://example.org){: target=_blank rel=noopener }
```
<div class="result" markdown>

[Open :material-launch:](https://example.org){: target=_blank rel=noopener }

</div>

### Result box

```bash title="Say hello!"
echo "Hello, World!"
```
<div class="result" markdown>
```
Hello, World!
```
</div>
