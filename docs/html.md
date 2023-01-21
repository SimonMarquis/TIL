---
title: 📜 HTML
---

## Elements

### [`blockquote`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/blockquote) [`figure`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/figure) [`figcaption`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/figcaption)

```html
<figure>
	<blockquote cite="https://example.org/">
		<p>This domain is for use in illustrative examples in documents. You may use this domain in literature without prior coordination or asking for permission.</p>
	</blockquote>
	<figcaption>—Example Domain, <cite>@example.org</cite></figcaption>
</figure>
```
<div class="result" markdown>
<figure>
	<blockquote cite="https://example.org/">
		<p>This domain is for use in illustrative examples in documents. You may use this domain in literature without prior coordination or asking for permission.</p>
	</blockquote>
	<figcaption>—Example Domain, <cite>@example.org</cite></figcaption>
</figure>
</div>

### [`del`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/del) [`ins`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/ins)

```html
<blockquote>
    There is <del>nothing</del> <ins>no code</ins> either good or bad, but <del>thinking</del> <ins>running it</ins> makes it so.
</blockquote>
```
<div class="result" markdown>
<blockquote>
    There is <del>nothing</del> <ins>no code</ins> either good or bad, but <del>thinking</del> <ins>running it</ins> makes it so.
</blockquote>
</div>

### [`details`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/details) [`summary`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/summary)

```html
<details open>
    <summary>Details</summary>
    <p>Something small enough to escape casual notice.</p>
</details>
```
<div class="result" markdown>
<details open>
    <summary>Details</summary>
    <p>Something small enough to escape casual notice.</p>
</details>
</div>

### [`input`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input)

#### [`button`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/button)

```html
<input type="button" value="Button">
```
<div class="result" markdown>
<input type="button" value="Button">
</div>

#### [`checkbox`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/checkbox)

```html
<fieldset>
	<legend>Select:</legend>
	<input type="checkbox" id="check" name="check" checked>
	<label for="check">Checkbox</label>
</fieldset>
```
<div class="result" markdown>
<fieldset>
	<legend>Select:</legend>
	<input type="checkbox" id="check" name="check" checked>
	<label for="check">Checkbox</label>
</fieldset>
</div>

#### [`color`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/color)

```html
<input type="color" value="#000000">
```
<div class="result" markdown>
<input type="color" value="#000000">
</div>

#### [`date`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/date)

```html
<input type="date" value="2038-01-19" min="2000-01-01" max="2100-12-31">
```
<div class="result" markdown>
<input type="date" value="2038-01-19" min="2000-01-01" max="2100-12-31">
</div>

#### [`datetime-local`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/datetime-local)

```html
<input type="datetime-local" value="2038-01-19T03:14:08" min="2000-01-01T00:00" max="2100-12-31T23:59:59">
```
<div class="result" markdown>
<input type="datetime-local" value="2038-01-19T03:14:08" min="2000-01-01T00:00" max="2100-12-31T23:59:59">
</div>

#### [`email`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/email)

```html
<input type="email" placeholder="user@example.org">
```
<div class="result" markdown>
<input type="email" placeholder="user@example.org">
</div>

#### [`file`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/file)

```html
<input type="file" accept="image/png, image/jpeg">
```
<div class="result" markdown>
<input type="file" accept="image/png, image/jpeg">
</div>

#### [`image`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/image)

```html
<input type="image" src="../assets/images/favicon.png">
```
<div class="result" markdown>
<input type="image" src="../assets/images/favicon.png">
</div>

#### [`month`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/month)

```html
<input type="month" value="2050-06" min="2000-01" max="2100-12">
```
<div class="result" markdown>
<input type="month" value="2050-06" min="2000-01" max="2100-12">
</div>

#### [`number`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/number)

```html
<input type="number" value="50" min="0" max="100">
```
<div class="result" markdown>
<input type="number" value="50" min="0" max="100">
</div>

#### [`password`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/password)

```html
<input type="password" placeholder="…">
```
<div class="result" markdown>
<input type="password" placeholder="…">
</div>

#### [`radio`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/radio)

```html
<fieldset>
	<legend>Select:</legend>
	<input type="radio" id="a" name="test" checked>
	<label for="a">A</label>
	<input type="radio" id="b" name="test">
	<label for="b">B</label>
	<input type="radio" id="c" name="test">
	<label for="c">C</label>
</fieldset>
```
<div class="result" markdown>
<fieldset>
	<legend>Select:</legend>
	<input type="radio" id="a" name="test" checked>
	<label for="a">A</label>
	<input type="radio" id="b" name="test">
	<label for="b">B</label>
	<input type="radio" id="c" name="test">
	<label for="c">C</label>
</fieldset>
</div>

#### [`range`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/range)

```html
<input type="range" value="5" min="0" max="10">
```
<div class="result" markdown>
<input type="range" value="5" min="0" max="10">
</div>

#### [`reset`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/reset)

```html
<form>
	<input type="text" placeholder="…">
	<input type="reset" value="Reset">
</form>
```
<div class="result" markdown>
<form>
	<input type="text" placeholder="…">
	<input type="reset" value="Reset">
</form>
</div>

#### [`tel`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/tel)

```html
<input type="tel" placeholder="…">
```
<div class="result" markdown>
<input type="tel" placeholder="…">
</div>

#### [`text`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/text)

```html
<input type="text" placeholder="…">
```
<div class="result" markdown>
<input type="text" placeholder="…">
</div>

#### [`time`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/time)

```html
<input type="time" min="08:00" max="18:00">
```
<div class="result" markdown>
<input type="time" min="08:00" max="18:00">
</div>

#### [`url`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/url)

```html
<input type="url" placeholder="…">
```
<div class="result" markdown>
<input type="url" placeholder="…">
</div>

#### [`week`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/week)

```html
<input type="week" min="2000-W10" max="2100-W40">
```
<div class="result" markdown>
<input type="week" min="2000-W10" max="2100-W40">
</div>

### [`mark`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/mark)

```html
Most <mark>salamander</mark>s are nocturnal, and hunt for insects, worms, and other small creatures.
```
<div class="result" markdown>
Most <mark>salamander</mark>s are nocturnal, and hunt for insects, worms, and other small creatures.
</div>

### [`meter`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/meter)

```html
<meter min="0" max="100" low="33" high="66" optimum="80" value="25"></meter>
<meter min="0" max="100" low="33" high="66" optimum="80" value="50"></meter>
<meter min="0" max="100" low="33" high="66" optimum="80" value="75"></meter>
```
<div class="result" markdown>
<meter min="0" max="100" low="33" high="66" optimum="80" value="25"></meter>
<meter min="0" max="100" low="33" high="66" optimum="80" value="50"></meter>
<meter min="0" max="100" low="33" high="66" optimum="80" value="75"></meter>
</div>

### [`progress`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/progress)

```html
<progress max="100" value="75"></progress>
```
<div class="result" markdown>
<progress max="100" value="75"></progress>
</div>

### [`select`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select) [`optgroup`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/optgroup) [`option`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/option)

```html
<select>
    <optgroup label="Theropods">
        <option>Tyrannosaurus</option>
        <option>Velociraptor</option>
        <option>Deinonychus</option>
    </optgroup>
    <optgroup label="Sauropods">
        <option>Diplodocus</option>
        <option>Saltasaurus</option>
        <option>Apatosaurus</option>
    </optgroup>
</select>
```
<div class="result" markdown>
<select>
    <optgroup label="Theropods">
        <option>Tyrannosaurus</option>
        <option>Velociraptor</option>
        <option>Deinonychus</option>
    </optgroup>
    <optgroup label="Sauropods">
        <option>Diplodocus</option>
        <option>Saltasaurus</option>
        <option>Apatosaurus</option>
    </optgroup>
</select>
</div>

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
