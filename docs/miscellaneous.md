---
title: 💎 Miscellaneous
---

### Bell code

`echo ^G` 🔔

(`^G` is <kbd>Ctrl</kbd> + <kbd>G</kbd>)

[🔗](https://en.wikipedia.org/wiki/Bell_character)

### Binary prefix

<table>
   <tbody>
      <tr>
         <td>
            <table>
               <tbody>
                  <tr>
                     <th colspan="3">Decimal</th>
                  </tr>
                  <tr>
                     <th colspan="1">Value</th>
                     <th colspan="2">SI</th>
                  </tr>
                  <tr>
                     <td>1000</td>
                     <td>k</td>
                     <td>kilo</td>
                  </tr>
                  <tr>
                     <td>1000<sup>2</sup></td>
                     <td>M</td>
                     <td>mega</td>
                  </tr>
                  <tr>
                     <td>1000<sup>3</sup></td>
                     <td>G</td>
                     <td>giga</td>
                  </tr>
                  <tr>
                     <td>1000<sup>4</sup></td>
                     <td>T</td>
                     <td>tera</td>
                  </tr>
                  <tr>
                     <td>1000<sup>5</sup></td>
                     <td>P</td>
                     <td>peta</td>
                  </tr>
                  <tr>
                     <td>1000<sup>6</sup></td>
                     <td>E</td>
                     <td>exa</td>
                  </tr>
                  <tr>
                     <td>1000<sup>7</sup></td>
                     <td>Z</td>
                     <td>zetta</td>
                  </tr>
                  <tr>
                     <td>1000<sup>8</sup></td>
                     <td>Y</td>
                     <td>yotta</td>
                  </tr>
               </tbody>
            </table>
         </td>
         <td>
            <table>
               <tbody>
                  <tr>
                     <th colspan="5">Binary</th>
                  </tr>
                  <tr>
                     <th colspan="1">Value</th>
                     <th colspan="2">IEC</th>
                     <th colspan="2">Legacy</th>
                  </tr>
                  <tr>
                     <td>1024</td>
                     <td>Ki</td>
                     <td>kibi</td>
                     <td>K</td>
                     <td>kilo</td>
                  </tr>
                  <tr>
                     <td>1024<sup>2</sup></td>
                     <td>Mi</td>
                     <td>mebi</td>
                     <td>M</td>
                     <td>mega</td>
                  </tr>
                  <tr>
                     <td>1024<sup>3</sup></td>
                     <td>Gi</td>
                     <td>gibi</td>
                     <td>G</td>
                     <td>giga</td>
                  </tr>
                  <tr>
                     <td>1024<sup>4</sup></td>
                     <td>Ti</td>
                     <td>tebi</td>
                     <td>T</td>
                     <td>tera</td>
                  </tr>
                  <tr>
                     <td>1024<sup>5</sup></td>
                     <td>Pi</td>
                     <td>pebi</td>
                     <td>–</td>
                     <td></td>
                  </tr>
                  <tr>
                     <td>1024<sup>6</sup></td>
                     <td>Ei</td>
                     <td>exbi</td>
                     <td>–</td>
                     <td></td>
                  </tr>
                  <tr>
                     <td>1024<sup>7</sup></td>
                     <td>Zi</td>
                     <td>zebi</td>
                     <td>–</td>
                     <td></td>
                  </tr>
                  <tr>
                     <td>1024<sup>8</sup></td>
                     <td>Yi</td>
                     <td>yobi</td>
                     <td>–</td>
                     <td></td>
                  </tr>
               </tbody>
            </table>
         </td>
      </tr>
   </tbody>
</table>

[🔗](https://en.wikipedia.org/wiki/Binary_prefix)

### Bookmarklets

- CSS boxes
  ```javascript
  javascript:{let d=(typeof _debug_layout_==='undefined');[].forEach.call(document.querySelectorAll("*"),function(a){a.style.outline=d?"1px solid #"+(~~(Math.random()*(1<<24))).toString(16):""});var _debug_layout_=d?true:undefined;}
  ```
- QrCode
  ```javascript
  javascript:var _size=400;var _left=(screen.width/2)-(_size/2);var _top=(screen.height/2)-(_size/2);var _input = prompt("QRcode input",window.getSelection().toString());if(_input!=null)window.open("https://chart.googleapis.com/chart?cht=qr&chs="+_size+"x"+_size+"&chld=L|0&choe=UTF-8&chl="+encodeURIComponent(_input), "_blank", "titlebar=no,menubar=no,scrollbars=no,status=no,width="+_size+",height="+_size+",top="+_top+",left="+_left);
  ```
- URL encoder
  ```javascript
  javascript: var decoded = prompt("URL encoder input:",window.getSelection().toString()); if(decoded!=null) prompt('URL encoder output:', encodeURIComponent(decoded));
  ```
- URL decoder
  ```javascript
  javascript: var encoded = prompt("URL decoder input:",window.getSelection().toString()); if(encoded!=null) prompt('URL decoder output:', decodeURIComponent(encoded));
  ```
- Base64 encoder
  ```javascript
  javascript: var decoded = prompt("Base64 encoder input:",window.getSelection().toString()); if(decoded != null) try {prompt('Base64 encoder output:', btoa(decoded)); } catch(error) { alert(error); }
  ```
- Base64 decoder
  ```javascript
  javascript: var encoded = prompt("Base64 decoder input:",window.getSelection().toString()); if(encoded != null) try {prompt('Base64 decoder output:', atob(encoded)); } catch(error) { alert(error); }
  ```
- Raw HTML
  ```javascript
  data:text/html;charset=utf-8,
  ```
- Edit website
  ```javascript
  javascript:document.body.contentEditable = 'true'; document.designMode='on'; void 0
  ```

[🔗](https://en.wikipedia.org/wiki/Bookmarklet)

### Box drawing characters

```
┌ ─ ┬ ┐ ┏ ┳ ━ ┓ ╔ ╦ ═ ╗
│ │ │ │ ┣ ╋ ━ ┫ ╠ ╬ ═ ╣
├ ─ ┼ ┤ ┃ ┃ ┃ ┃ ║ ║ ║ ║
└ ─ ┴ ┘ ┗ ┻ ━ ┛ ╚ ╩ ═ ╝

╒ ╤ ╕ ╓ ╥ ╖ ┍ ┯ ┑
╞ ╪ ╡ ╟ ╫ ╢ ┝ ┿ ┥
╘ ╧ ╛ ╙ ╨ ╜ ┕ ┷ ┙

╌ ╎ ╍ ╏
┄ ┆ ┊ ┈
┅ ┇ ┉ ┋

╭ ╮
╰ ╯

▁ ▂ ▃ ▄ ▅ ▆ ▇ █

▉ ▊ ▋ ▌ ▍ ▎ ▏

░ ▒ ▓
```

[🔗](https://en.wikipedia.org/wiki/Box-drawing_character)

### Gmail templates

- Create a new Google Docs https://docs.new
- Insert →  Building blocks → Email draft

Or simply type `@email draft`.
