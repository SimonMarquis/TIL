---
title: 📜 HTML
---

## Emoji favicon

```html
<head>
  <link rel="icon" type="image/svg+xml" href="data:image/svg+xml,<svg xmlns=%22http://www.w3.org/2000/svg%22 width=%22256%22 height=%22256%22 viewBox=%220 0 100 100%22><text x=%2250%%22 y=%2250%%22 dominant-baseline=%22central%22 text-anchor=%22middle%22 font-size=%2290%22>🗓️</text></svg>"/>
</head>
```

And here is the decoded SVG content:

```xml
<svg xmlns="http://www.w3.org/2000/svg" width="256" height="256" viewBox="0 0 100 100">
	<text x="50%" y="50%" dominant-baseline="central" text-anchor="middle" font-size="90">🗓️</text>
</svg>
```

<span class="md-button" onclick='javascript:
	var input = prompt("Enter emoji:",window.getSelection().toString());
	var href = "data:image/svg+xml,<svg xmlns=%22http://www.w3.org/2000/svg%22 width=%22256%22 height=%22256%22 viewBox=%220 0 100 100%22><text x=%2250%%22 y=%2250%%22 dominant-baseline=%22central%22 text-anchor=%22middle%22 font-size=%2290%22>" + input + "</text></svg>";
	document.querySelector("link[rel~=\"icon\"]").href = href;
'>Test</strong>

[🔗](https://css-tricks.com/how-to-create-a-favicon-that-changes-automatically/)
