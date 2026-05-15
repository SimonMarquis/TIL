---
title: 📖 Zensical
render_macros: true
include_yaml:
  sample: data/sample.yaml
---

# 📖 Zensical (mkdocs)

### Anchors

{{{% raw %}}}

```md
#### Heading producing an anchor

#### Another heading {#custom-anchor-for-heading-using-attr-list}

<a id="raw-anchor"></a>

[](){#markdown-anchor-using-attr-list}
```
<div class="result" markdown>

#### Heading producing an anchor

#### Another heading {#custom-anchor-for-heading-using-attr-list}

<a id="raw-anchor"></a>

[](){#markdown-anchor-using-attr-list}

</div>

{{{% endraw %}}}

### Attribute Lists

```md
[Hello, World!](#){: #someid .someclass somekey='some value' }
```
<div class="result" markdown>

[Hello, World!](#){: #someid .someclass somekey='some value' }

</div>

[🔗](https://python-markdown.github.io/extensions/attr_list)

### Downloadable file

```md
[:lucide-external-link:](assets/example.json){: .md-button }
[:lucide-download:](assets/example.json){: .md-button download="example.json" }
```
<div class="result" markdown>

[:lucide-external-link:](assets/example.json){: .md-button }
[:lucide-download:](assets/example.json){: .md-button download="example.json" }

</div>

### Environment variables

```yaml title="mkdocs.yml"
plugins:
  - foo-plugin:
      enabled: !ENV [CI, GITHUB_ACTIONS, False]
```

### Macros extension

[🔗 Declaring external YAML files](https://zensical.org/docs/setup/extensions/macros/)

{{{ context(sample) | pretty }}}

### [Meta plugin](https://github.com/zensical/backlog/issues/31)

[🔗 Metadata for groups of pages](https://squidfunk.github.io/mkdocs-material/plugins/meta/)

{{{ context(page.meta) | pretty }}}

### Open link in new tab

```md
[Open :lucide-external-link:](https://example.org){: target=_blank rel=noopener }
```
<div class="result" markdown>

[Open :lucide-external-link:](https://example.org){: target=_blank rel=noopener }

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
