---
title: 🪢 JavaScript
---

### Comments in JSON

> TL;DR: JSON is data-only. If you include a comment, then it must be data too.

```json
{
    "//": "This is a comment",
    "key": "value"
}
```

[🔗](https://www.json.org/json-en.html)

### Conditional array/object content

```javascript
const foo = [
    "bar",
    ...(truty ? ["baz"] : []),
    ...(falsy ? ["qux"] : []),
];
```
<div class="result" markdown>

  ```json
  ["bar", "baz"]
  ```

</div>

```javascript
const foo = {
    bar: "bar",
    ...(truthy && { baz: 'baz' }),
    ...(falsy && { qux: 'qux' }),
};
```
<div class="result" markdown>

  ```json
  {"bar": "bar", "baz": "baz"}
  ```

</div>

### Map object entries

```javascript
const mapObject = (obj, fn) => Object.fromEntries(Object.entries(obj).map(([k, v]) => [k, fn(v)]));
```

!!! example "JSON stringify object values"

    ```javascript
    mapObject({key: {foo: "bar"}}, (v) => JSON.stringify(v));
    ```
    <div class="result" markdown>
    ```javascript
    {key: '{"foo":"bar"}'}
    ```
    </div>

### Named capturing group regex

```js
const semver = /^(?<major>\d+)(?:\.(?<minor>\d+)(?:\.(?<patch>\d+))?)?(?:-(?<label>.+))?$/;

const result = "1.2.3-alpha".match(semver);
result.groups.major; // '1'
result.groups.minor; // '2'
result.groups.patch; // '3'
result.groups.label; // 'alpha'
```

[🔗](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions/Groups_and_Backreferences) [🔗](https://caniuse.com/mdn-javascript_builtins_regexp_named_capture_groups) [🔗](https://www.regular-expressions.info/named.html)

### Optional chaining operator

```js
// The old way
val result = (obj || {}).data;
// The new way
val result = obj?.data;
```

[🔗](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining) [🔗](https://caniuse.com/mdn-javascript_operators_optional_chaining)
