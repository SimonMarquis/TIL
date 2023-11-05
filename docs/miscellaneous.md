---
title: 💎 Miscellaneous
---

### Anonymous Google profile images

{{{% set users = ['alligator', 'anteater', 'armadillo', 'auroch', 'axolotl', 'badger', 'bat', 'beaver', 'buffalo', 'camel', 'chameleon', 'cheetah', 'chipmunk', 'chinchilla', 'chupacabra', 'cormorant', 'coyote', 'crow', 'dingo', 'dinosaur', 'dolphin', 'duck', 'elephant', 'ferret', 'fox', 'frog', 'giraffe', 'gopher', 'grizzly', 'hedgehog', 'hippo', 'hyena', 'jackal', 'ibex', 'ifrit', 'iguana', 'koala', 'kraken', 'lemur', 'leopard', 'liger', 'llama', 'manatee', 'mink', 'monkey', 'narwhal', 'orangutan', 'otter', 'panda', 'penguin', 'platypus', 'python', 'pumpkin', 'quagga', 'rabbit', 'raccoon', 'rhino', 'sheep', 'shrew', 'skunk', 'squirrel', 'turtle', 'walrus', 'wolf', 'wolverine', 'wombat'] %}}}

!!! quote ""

    {{{% for user in users %}}} ![{{{ user }}}](https://ssl.gstatic.com/docs/common/profile/{{{user}}}_sm.png "{{{ user }}}") {{{% endfor %}}}

    ??? quote "Larger images…"

        {{{% for user in users %}}} ![{{{ user }}}](https://ssl.gstatic.com/docs/common/profile/{{{user}}}_lg.png "{{{ user }}}") {{{% endfor %}}}

### Apache distributed configuration file

Directory indexing:

```text title=".htaccess"
Options +Indexes
IndexOptions Charset=UTF-8 IgnoreCase FancyIndexing FoldersFirst NameWidth=*
```

[🔗](https://httpd.apache.org/docs/2.4/mod/mod_autoindex.html#indexoptions)

### Arrows

!!! quote "`2190–21FF` [Arrows](https://en.wikipedia.org/wiki/Arrows)"

    <div style="font-size: x-large;">
    ```
    ←  ↑  →  ↓  ↔  ↕  ↖  ↗  ↘  ↙  ↚  ↛  ↜  ↝  ↞  ↟
    ↠  ↡  ↢  ↣  ↤  ↥  ↦  ↧  ↨  ↩  ↪  ↫  ↬  ↭  ↮  ↯
    ↰  ↱  ↲  ↳  ↴  ↵  ↶  ↷  ↸  ↹  ↺  ↻  ↼  ↽  ↾  ↿
    ⇀  ⇁  ⇂  ⇃  ⇄  ⇅  ⇆  ⇇  ⇈  ⇉  ⇊  ⇋  ⇌  ⇍  ⇎  ⇏
    ⇐  ⇑  ⇒  ⇓  ⇔  ⇕  ⇖  ⇗  ⇘  ⇙  ⇚  ⇛  ⇜  ⇝  ⇞  ⇟
    ⇠  ⇡  ⇢  ⇣  ⇤  ⇥  ⇦  ⇧  ⇨  ⇩  ⇪  ⇫  ⇬  ⇭  ⇮  ⇯
    ⇰  ⇱  ⇲  ⇳  ⇴  ⇵  ⇶  ⇷  ⇸  ⇹  ⇺  ⇻  ⇼  ⇽  ⇾  ⇿
    ```
    </div>

!!! quote "`27F0–27FF` [Supplemental Arrows-A](https://en.wikipedia.org/wiki/Supplemental_Arrows-A)"

    <div style="font-size: x-large;">
    ```
    ⟰  ⟱  ⟲  ⟳  ⟴  ⟵  ⟶  ⟷  ⟸  ⟹  ⟺  ⟻  ⟼  ⟽  ⟾  ⟿
    ```
    </div>

!!! quote "`2900–297F` [Supplemental Arrows-B](https://en.wikipedia.org/wiki/Supplemental_Arrows-B)"

    <div style="font-size: x-large;">
    ```
    ⤀  ⤁  ⤂  ⤃  ⤄  ⤅  ⤆  ⤇  ⤈  ⤉  ⤊  ⤋  ⤌  ⤍  ⤎  ⤏
    ⤐  ⤑  ⤒  ⤓  ⤔  ⤕  ⤖  ⤗  ⤘  ⤙  ⤚  ⤛  ⤜  ⤝  ⤞  ⤟
    ⤠  ⤡  ⤢  ⤣  ⤤  ⤥  ⤦  ⤧  ⤨  ⤩  ⤪  ⤫  ⤬  ⤭  ⤮  ⤯
    ⤰  ⤱  ⤲  ⤳  ⤴  ⤵  ⤶  ⤷  ⤸  ⤹  ⤺  ⤻  ⤼  ⤽  ⤾  ⤿
    ⥀  ⥁  ⥂  ⥃  ⥄  ⥅  ⥆  ⥇  ⥈  ⥉  ⥊  ⥋  ⥌  ⥍  ⥎  ⥏
    ⥐  ⥑  ⥒  ⥓  ⥔  ⥕  ⥖  ⥗  ⥘  ⥙  ⥚  ⥛  ⥜  ⥝  ⥞  ⥟
    ⥠  ⥡  ⥢  ⥣  ⥤  ⥥  ⥦  ⥧  ⥨  ⥩  ⥪  ⥫  ⥬  ⥭  ⥮  ⥯
    ⥰  ⥱  ⥲  ⥳  ⥴  ⥵  ⥶  ⥷  ⥸  ⥹  ⥺  ⥻  ⥼  ⥽  ⥾  ⥿
    ```
    </div>

!!! quote "`1F800–1F8FF` [Supplemental Arrows-C](https://en.wikipedia.org/wiki/Supplemental_Arrows-C)"

    <div style="font-size: x-large;">
    ```
    🠀  🠁  🠂  🠃  🠄  🠅  🠆  🠇  🠈  🠉  🠊  🠋           
    🠐  🠑  🠒  🠓  🠔  🠕  🠖  🠗  🠘  🠙  🠚  🠛  🠜  🠝  🠞  🠟
    🠠  🠡  🠢  🠣  🠤  🠥  🠦  🠧  🠨  🠩  🠪  🠫  🠬  🠭  🠮  🠯
    🠰  🠱  🠲  🠳  🠴  🠵  🠶  🠷  🠸  🠹  🠺  🠻  🠼  🠽  🠾  🠿
    🡀  🡁  🡂  🡃  🡄  🡅  🡆  🡇                       
    🡐  🡑  🡒  🡓  🡔  🡕  🡖  🡗  🡘  🡙                 
    🡠  🡡  🡢  🡣  🡤  🡥  🡦  🡧  🡨  🡩  🡪  🡫  🡬  🡭  🡮  🡯
    🡰  🡱  🡲  🡳  🡴  🡵  🡶  🡷  🡸  🡹  🡺  🡻  🡼  🡽  🡾  🡿
    🢀  🢁  🢂  🢃  🢄  🢅  🢆  🢇                       
    🢐  🢑  🢒  🢓  🢔  🢕  🢖  🢗  🢘  🢙  🢚  🢛  🢜  🢝  🢞  🢟
    🢠  🢡  🢢  🢣  🢤  🢥  🢦  🢧  🢨  🢩  🢪  🢫  🢬  🢭  
    ```
    </div>

!!! quote "`2B00–2BFF` [Miscellaneous Symbols and Arrows](https://en.wikipedia.org/wiki/Miscellaneous_Symbols_and_Arrows)"

    <div style="font-size: x-large;">
    ```
    ⬀  ⬁  ⬂  ⬃  ⬄  ⬅  ⬆  ⬇  ⬈  ⬉  ⬊  ⬋  ⬌  ⬍  ⬎  ⬏
    ⬐  ⬑  ⬒  ⬓  ⬔  ⬕  ⬖  ⬗  ⬘  ⬙  ⬚  ⬛  ⬜  ⬝  ⬞  ⬟
    ⬠  ⬡  ⬢  ⬣  ⬤  ⬥  ⬦  ⬧  ⬨  ⬩  ⬪  ⬫  ⬬  ⬭  ⬮  ⬯
    ⬰  ⬱  ⬲  ⬳  ⬴  ⬵  ⬶  ⬷  ⬸  ⬹  ⬺  ⬻  ⬼  ⬽  ⬾  ⬿
    ⭀  ⭁  ⭂  ⭃  ⭄  ⭅  ⭆  ⭇  ⭈  ⭉  ⭊  ⭋  ⭌  ⭍  ⭎  ⭏
    ⭐  ⭑  ⭒  ⭓  ⭔  ⭕  ⭖  ⭗  ⭘  ⭙  ⭚  ⭛  ⭜  ⭝  ⭞  ⭟
    ⭠  ⭡  ⭢  ⭣  ⭤  ⭥  ⭦  ⭧  ⭨  ⭩  ⭪  ⭫  ⭬  ⭭  ⭮  ⭯
    ⭰  ⭱  ⭲  ⭳        ⭶  ⭷  ⭸  ⭹  ⭺  ⭻  ⭼  ⭽  ⭾  ⭿
    ⮀  ⮁  ⮂  ⮃  ⮄  ⮅  ⮆  ⮇  ⮈  ⮉  ⮊  ⮋  ⮌  ⮍  ⮎  ⮏
    ⮐  ⮑  ⮒  ⮓  ⮔  ⮕     ⮗  ⮘  ⮙  ⮚  ⮛  ⮜  ⮝  ⮞  ⮟
    ⮠  ⮡  ⮢  ⮣  ⮤  ⮥  ⮦  ⮧  ⮨  ⮩  ⮪  ⮫  ⮬  ⮭  ⮮  ⮯
    ⮰  ⮱  ⮲  ⮳  ⮴  ⮵  ⮶  ⮷  ⮸  ⮹  ⮺  ⮻  ⮼  ⮽  ⮾  ⮿
    ⯀  ⯁  ⯂  ⯃  ⯄  ⯅  ⯆  ⯇  ⯈  ⯉  ⯊  ⯋  ⯌  ⯍  ⯎  ⯏
    ⯐  ⯑  ⯒  ⯓  ⯔  ⯕  ⯖  ⯗  ⯘  ⯙  ⯚  ⯛  ⯜  ⯝  ⯞  ⯟
    ⯠  ⯡  ⯢  ⯣  ⯤  ⯥  ⯦  ⯧  ⯨  ⯩  ⯪  ⯫  ⯬  ⯭  ⯮  ⯯
    ```
    </div>

### AutoHotkey

```ahk
;   ! = alt
;   + = shift
;   ^ = ctrl
;   # = win

#NoEnv  ; Recommended for performance and compatibility with future AutoHotkey releases.
; #Warn  ; Enable warnings to assist with detecting common errors.
SendMode Input  ; Recommended for new scripts due to its superior speed and reliability.
SetWorkingDir %A_ScriptDir%  ; Ensures a consistent starting directory.

; make the scroll lock key (ScrLk) toggle all hotkeys.
$ScrollLock::Suspend

::``right::→
::``left::←
::``up::↑
::``down::↓
::``r::→
::``l::←
::``u::↑
::``d::↓
::``ur::↗︎
::``ul::↖
::``dr::↘
::``dl::↙
::``lte::≤
::``gte::≥

::èuro::€
```

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

- <a class="md-button" href='javascript:{let o=void 0===_debug_layout_;[].forEach.call(document.querySelectorAll("*"),(function(l){l.style.outline=o?"1px solid #"+(~~(Math.random()*16777216)).toString(16):""}));var _debug_layout_=!!o||void 0}'>CSS boxes</a>
  ```javascript
  let d = typeof _debug_layout_ === "undefined";
  [].forEach.call(document.querySelectorAll("*"), function (a) {
    a.style.outline = d
      ? "1px solid #" + (~~(Math.random() * (1 << 24))).toString(16)
      : "";
  });
  var _debug_layout_ = d ? true : undefined;
  ```
- <a class="md-button" href='javascript:var _size=400,_left=screen.width/2-_size/2,_top=screen.height/2-_size/2,_input=prompt("QRcode input",window.getSelection().toString());null!=_input&&window.open("https://chart.googleapis.com/chart?cht=qr&chs="+_size+"x"+_size+"&chld=L|0&choe=UTF-8&chl="+encodeURIComponent(_input),"_blank","titlebar=no,menubar=no,scrollbars=no,status=no,width="+_size+",height="+_size+",top="+_top+",left="+_left);'>QrCode</a>
  ```javascript
  var _size = 400;
  var _left = screen.width / 2 - _size / 2;
  var _top = screen.height / 2 - _size / 2;
  var _input = prompt("QRcode input", window.getSelection().toString());
  if (_input != null)
    window.open(
      "https://chart.googleapis.com/chart?cht=qr" +
        "&chs=" + _size + "x" + _size +
        "&chld=L|0&choe=UTF-8" +
        "&chl=" + encodeURIComponent(_input),
      "_blank",
      "titlebar=no,menubar=no,scrollbars=no,status=no" +
        ",width=" + _size + ",height=" + _size + ",top=" + _top + ",left=" + _left
    );
  ```
- <a class="md-button" href='javascript:var decoded=prompt("URL encoder input:",window.getSelection().toString());null!=decoded&&prompt("URL encoder output:",encodeURIComponent(decoded));void 0'>URL encoder</a>
  ```javascript
  var decoded = prompt("URL encoder input:", window.getSelection().toString());
  if (decoded != null) prompt("URL encoder output:", encodeURIComponent(decoded));
  ```
- <a class="md-button" href='javascript:var encoded=prompt("URL decoder input:",window.getSelection().toString());null!=encoded&&prompt("URL decoder output:",decodeURIComponent(encoded));void 0'>URL decoder</a>
  ```javascript
  var encoded = prompt("URL decoder input:", window.getSelection().toString());
  if (encoded != null) prompt("URL decoder output:", decodeURIComponent(encoded));
  ```
- <a class="md-button" href='javascript:var decoded=prompt("Base64 encoder input:",window.getSelection().toString());try{prompt("Base64 encoder output:",btoa(decoded))}catch(e){alert(e)};void 0'>Base64 encoder</a>
  ```javascript
  var decoded = prompt("Base64 encoder input:", window.getSelection().toString());
  try {
    prompt("Base64 encoder output:", btoa(decoded));
  } catch (error) {
    alert(error);
  }
  ```
- <a class="md-button" href='javascript:var encoded=prompt("Base64 decoder input:",window.getSelection().toString());try{prompt("Base64 decoder output:",atob(encoded))}catch(e){alert(e)};void 0'>Base64 decoder</a>
  ```javascript
  var encoded = prompt("Base64 decoder input:", window.getSelection().toString());
  try {
    prompt("Base64 decoder output:", atob(encoded));
  } catch (error) {
    alert(error);
  }
  ```
- <a class="md-button" href='javascript:document.body.contentEditable="true",document.designMode="on";void 0'>Edit website</a>
  ```javascript
  document.body.contentEditable = "true";
  document.designMode = "on";
  ```
- <a class="md-button" href="data:text/html;charset=utf-8,">Raw HTML</a>
  ```
  data:text/html;charset=utf-8,
  ```

[🔗](https://en.wikipedia.org/wiki/Bookmarklet)

### Box drawing characters

<div style="font-size: x-large;">

```
┌ ┬ ─ ┐ ┏ ┳ ━ ┓ ╔ ╦ ═ ╗
├ ┼ ─ ┤ ┣ ╋ ━ ┫ ╠ ╬ ═ ╣
│ │ │ │ ┃ ┃ ┃ ┃ ║ ║ ║ ║
└ ┴ ─ ┘ ┗ ┻ ━ ┛ ╚ ╩ ═ ╝

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

◲◱
◳◰

◶◵
◷◴

◐◓
◒◑
```

</div>

[🔗](https://en.wikipedia.org/wiki/Box-drawing_character)

### EditorConfig

```ini title=".editorconfig"
root = true

[*]
charset = utf-8
indent_size = 4
indent_style = space
insert_final_newline = true
max_line_length = 200
tab_width = 4

[{*.kt,*.kts}]
ij_kotlin_code_style_defaults = KOTLIN_OFFICIAL
ij_kotlin_allow_trailing_comma = true
ij_kotlin_allow_trailing_comma_on_call_site = true
ij_kotlin_name_count_to_use_star_import = 2147483647
ij_kotlin_name_count_to_use_star_import_for_members = 2147483647
ij_kotlin_packages_to_use_import_on_demand = unset

[{*.md,*.mdown,*.markdown}]
indent_size = 2
indent_style = space
trim_trailing_whitespace = false

[{*.yml,*.yaml}]
indent_size = 2
indent_style = space

[*.json]
indent_size = 2
indent_style = space
```

[🔗](https://www.jetbrains.com/help/idea/editorconfig.html)

### Error pages illustrations

!!! quote "Youtube monkey error"

    <figure>
        <svg id="monkey" viewBox="0 0 490 525" width="200">
          <path fill="#6A1B9A" d="M325 85c1 12-1 25-5 38-8 29-31 52-60 61-26 8-54 14-81 18-37 6-26-37-38-72l-4-4c0-17-9-33 4-37l33-4c9-2 9-21 11-30 1-7 3-14 5-21 8-28 40-42 68-29 18 9 36 19 50 32 13 11 16 31 17 48z"/>
          <path fill="none" stroke="#6A1B9A" stroke-width="24" stroke-linecap="round" stroke-miterlimit="10" d="M431 232c3 15 21 19 34 11 15-9 14-30 5-43-12-17-38-25-59-10-23 18-27 53-21 97s1 92-63 108"/>
          <path fill="#6A1B9A" d="M284 158c35 40 63 85 86 133 24 52-6 113-62 123-2 0-4 1-6 1-53 9-101-33-101-87V188l83-30z"/>
          <path fill="#F7CB4D" d="M95 152c-3-24 13-57 46-64l27-5c9-2 16-19 17-28l3-15 20-3c44 14 42 55 18 69 22 0 39 26 32 53-5 18-20 32-39 36-13 3-26 5-40 8-50 8-80-14-84-51z"/>
          <path fill="#6A1B9A" d="M367 392c-21 18-77 70-25 119h-61c-27-29-32-69 1-111l85-8z"/>
          <path fill="#6A1B9A" d="M289 399c-21 18-84 62-32 111h-61c-37-34-5-104 43-134l50 23z"/>
          <path fill="#EDB526" d="M185 56l3-15 20-3c25 8 35 25 35 41-12-18-49-29-58-23z"/>
          <path fill="#E62117" d="M190 34c8-28 40-42 68-29 18 9 36 19 50 32 10 9 14 23 16 37L187 46l3-12z"/>
          <path fill="#8E24AA" d="M292 168c0 0 0 201 0 241s20 98 91 85l-16-54c-22 12-31-17-31-37 0-20 0-108 0-137S325 200 292 168z"/>
          <path fill="#F7CB4D" d="M284 79c11-9 23-17 35-23 25-12 54 7 59 38v1c4 27-13 51-36 53-12 1-25 1-37 0-22-1-39-27-32-52v-1c2-6 6-12 11-16z"/>
          <path fill="#6A1B9A" d="M201 203s0 84-95 140l22 42s67-25 89-86-16-96-16-96z"/>
          <path fill="#BE2117" d="M224 54l-67-14c-10-2-13-15-5-21s18-6 26 0l46 35z"/>
          <circle fill="#4A148C" cx="129" cy="161" r="12"/>
          <circle fill="#4A148C" cx="212" cy="83" r="7"/>
          <circle fill="#4A148C" cx="189" cy="79" r="7"/>
          <path fill="#F7CB4D" d="M383 493c11-3 19-8 25-13 7-10 4-16-5-20 8-9 2-22-8-18 1-1 1-2 1-3 3-9-9-15-15-8-3 4-8 7-13 9l15 53z"/>
          <path fill="#EDB526" d="M252 510c5 6 0 15-9 15h-87c-10 0-16-8-13-15 5-12 21-19 36-16l73 16z"/>
          <ellipse transform="rotate(19.126 278.35 14.787)" fill="#E62117" cx="278" cy="15" rx="9" ry="7"/>
          <path fill="#F7CB4D" d="M341 510c5 6 0 15-9 15h-87c-10 0-16-8-13-15 5-12 21-19 36-16l73 16z"/>
          <path fill="#EDB526" d="M357 90c-12-19-35-23-55-11-19 12-25 32-13 52"/>
          <path fill="#E62117" d="M110 427l21-9c5-2 7-8 5-13l-42-94c-3-6-9-9-15-6l-11 5c-6 2-9 9-7 15l36 97c2 5 8 7 13 5z"/>
          <path fill="#B0BEC5" d="M37 278l41-17c11-4 22-5 33-1 5 2 10 4 14 6 6 3 4 11-3 11-9 0-18 1-26 3l2 12c1 6-2 11-8 13l-36 15c-5 2-10 1-14-2l-9-7-2 17c0 2-2 4-4 5l-3 1c-3 1-7 0-8-3L1 300c-1-3 0-7 4-9l4-2c2-1 5 0 7 1l12 10 1-11c0-5 3-9 8-11z"/>
          <path fill="#F7CB4D" d="M103 373c10 2 14 10 8 19 6-1 10 4 10 9 0 3-3 6-6 7l-26 11c-2 1-5 1-8 0-6-3-7-9-2-16-7-1-13-9-6-17-8-1-12-8-8-15l3-3 23-11c9-4 19 8 12 16z"/>
          <ellipse transform="rotate(173.3 233.455 334.51)" fill="#8E24AA" cx="234" cy="335" rx="32" ry="46"/>
        </svg>
      <figcaption>Something went wrong…</figcaption>
    </figure>

!!! quote "Youtube offline"

    <figure>
        <svg viewBox="0 0 192 195" focusable="false" style="pointer-events: none; display: block; width: 100%; height: 100%;" width="200">
          <defs>
            <path d="M0 194.555V.675h191.961v193.88z"></path>
            <path d="M.668 18.586C8.545 12.047 15.125 3.19 25.082.49v20.673H.668v-2.577z"></path>
          </defs>
          <g fill="none" fill-rule="evenodd">
            <path d="M63.227 57.833s-4.403 1.068-5.938 1.483c-1.456.393-4.553 1.79-4.443 6.532.112 4.74.112 4.463.223 5.85.11 1.389 1.11 3.444 3.053 3.999 1.944.555 2.834 1.777 2.444 6.386-.389 4.609 17.055-6.552 17.055-6.552l-5.41-15.82-6.984-1.878z" fill="#DDD"></path>
            <g transform="translate(0 -.341)">
              <mask fill="#fff">
                <use xlink:href="#a"></use>
              </mask>
              <path d="M96.24.675c-17.36 0-24.86 17.956-38.835 24.25-9.382 4.226-31.732.669-39.879 14.75C9.38 53.757 20.86 65.52 15.12 74.544 9.38 83.568-.48 85.263.02 99.774c.5 14.51 20.374 19.494 22.32 30.4 1.946 10.908-4.853 13.059 0 28.997s18.193 17.626 35.867 18.065c17.673.439 14.368 12.34 32.52 16.64 18.153 4.299 29.831-13.08 43.992-16.64 14.161-3.561 24.004.189 32.504-11.311 8.5-11.5-2.77-30.212 3.23-38.855 6-8.643 22.896-13.127 21.418-30.728-1.167-13.883-11.99-16.16-15.24-26.777-3.438-11.225 4.75-21.285-4.25-33.253-10.85-14.428-29.882-3.073-41.805-14.656C118.653 10.072 113.88.675 96.24.675" fill="#6F38D4" mask="url(#b)"></path>
            </g>
            <path d="M127.519 54.153c1.374-2.688 3.936-3.375 6.061-3.375h31.375c2.188 0 5.418 2.011 3.625 5.875-1.75 3.77-8.833 17.628-9.812 19.625-.9 1.834-2.5 3.562-6.25 3.562h-33.124c-2.5 0-4.064-2.812-2.189-6.5 1.876-3.687 10.314-19.187 10.314-19.187" fill="#282828"></path>
            <path fill="#FF76DA" d="M132.08 54.522h32.314L153.518 75.96h-33.224z"></path>
            <path d="M130.91 72.181c1.96-.157 2.745.471 5.414 0 2.67-.47 3.141-2.617 5.025-2.722 1.884-.105 4.45-.366 6.543-2.04 2.094-1.676 2.827-4.608 1.1-6.073-1.729-1.466-2.723-.262-4.397-.785-1.675-.524-.733-2.513-2.879-3.036-2.147-.524-3.664.471-5.078-.105-1.262-.514-2.104-1.039-2.532-2.898h-2.025L120.294 75.96h4.83c.918-1.467 3.824-3.622 5.785-3.779" fill="#FFD61D"></path>
            <path fill="#FFF771" d="M149.736 64.156l-20.166-5.068-5.573 10.135 23.96-2.388z"></path>
            <path fill="#FFF" d="M148.02 63.81l-18.033 1.087 17.456 2.105z"></path>
            <path d="M166.335 155.314c-7.65-5.535-13.913.717-21.104-6.867-7.19-7.584-.204-10.69-9.321-18.884-9.118-8.193-13.5.819-19.298-4.991-5.797-5.811-2.957-14.741-8.792-20.643-5.834-5.903-16.191.678-22.72-5.88-6.528-6.555-1.388-14.961-9.761-19.945-8.372-4.985-15.748 1.04-21.691-4.531-6.12-5.74-2.37-14.698-9.37-19.05-6.645-4.131-12.298-.594-18.355-3.744-5.782-3.007-7.52-8.195-6.902-13.63a18.305 18.305 0 00-1.495 2.185c-8.147 14.08 3.333 25.845-2.407 34.869-5.74 9.024-15.6 10.719-15.1 25.23.5 14.51 20.374 19.494 22.32 30.4 1.947 10.908-4.853 13.059 0 28.997s18.193 17.626 35.867 18.065c17.673.439 14.368 12.34 32.52 16.64 18.153 4.299 29.832-13.08 43.993-16.64 14.16-3.561 24.004.189 32.504-11.311 1.397-1.891 2.253-3.98 2.746-6.183-.978-1.607-2.172-3.03-3.634-4.087" fill="#4620AE"></path>
            <path d="M35.996 149.688c-2.405-27.576 22.517-52.274 55.666-55.167 38.958-3.398 61.973 17.118 64.378 44.693 2.406 27.576-22.517 52.275-55.666 55.167-33.149 2.892-61.972-17.118-64.378-44.693" fill="#BD79FF"></path>
            <path d="M86.795 123.632c.465 4.071-3.06 7.3-7.8 7.84-4.74.542-9.502-1.3-10.046-6.06-.465-4.072 3.729-7.22 8.468-7.762 4.74-.542 8.869 1.528 9.378 5.982M143.194 136.755c.405 3.685-2.99 6.613-7.52 7.112-4.532.498-9.062-1.16-9.537-5.47-.405-3.685 3.628-6.542 8.16-7.041 4.531-.498 8.454 1.368 8.897 5.399M132.987 159.146c.488 4.187-3.937 7.61-9.808 8.294-5.872.685-11.72-1.087-12.292-5.983-.488-4.186 4.763-7.545 10.634-8.23 5.871-.685 10.932 1.34 11.466 5.92M111.496 185.225c-5.791-4.012-1.343-13.936-7.953-16.37-6.611-2.436-13.361 5.055-18.123-2.686-3.035-4.933 2.563-10.26-3.661-15.454-6.225-5.193-13.257 3.38-18.386-.189-5.128-3.568 1.68-10.789-3.346-16.624-5.026-5.835-13.957 1.822-19.095-2.435-1.026-.849-1.173-2.245-1.072-3.56-3.1 6.776-4.528 14.168-3.864 21.781 2.406 27.575 31.229 47.585 64.378 44.693 10.788-.94 20.694-4.203 29.081-9.11-4.525 2.412-12.183 3.956-17.959-.046" fill="#9A4DFF"></path>
            <path d="M101.622 77.33c5.125 9.375 20.396 11.317 28.646 2.505h-5.5c-1.375 0-1.5-2.063-.75-2.688s2.688-1.312 1.938-2.875c-.75-1.562-3.063-.125-5.625.5-2.563.625-5.5.267-7.5-.937-1.557-.937-4.188-3.438-4.563-10.063-.286-5.054-6.646 13.558-6.646 13.558" fill="#EEE"></path>
            <path d="M67.394 83.835s-.75 8-.876 11.5c-.124 3.5-.874 9.625 5 12.25 5.876 2.625 7 3.375 8.626 4.625 1.624 1.25 3.188 2.937 3.561 5.375.376 2.438-.436 9.188 0 12 .439 2.813 1 3.75 1 3.75h20.48c3.105-6.75-2.553-6.375-4.442-5.935-1.995.466-2.766-1.002-2.078-2.94.686-1.937 3.43-10.182 1.082-14.5-1.938-3.563-5.791-6.094-5.166-7.813.55-1.511 2.727-.812 5.644-.062 2.919.75 5.544 1.562 7.482 2.75 1.937 1.187 2.603 3.372 1.978 6.874-.626 3.5-1.063 7.814-.626 10.126.439 2.313 1 3.375 1 3.375h20.084c2.292-4.833-1-6.542-4.084-5.833-2.082.479-3.602-.854-3.165-2.917.438-2.063 3-9.125 3-13.438 0-4.312-1.793-9.562-7.876-11.854-5.528-2.082-15-4.833-13.5-13.166 1.5-8.334 1.584-10.584 3.334-12.667s9.041-5.875 11.522-12.572c2.706-7.3-.522-14.428-10.19-17.844-9.665-3.417-23.901-3.907-37.25 1.916-12.415 5.417-21.415 17.584-5.915 26.5 10.587 6.09 1.374 20.5 1.374 20.5" fill="#FFF"></path>
            <path d="M69.02 65.847s1.286 1.658-1.579 5.381c-1.798 2.337-9.923 9.606-12.007 12.19-2.083 2.583-5.083 8-5 14 .084 6 1.417 8.25-.833 11.5s-4.276 5.325-3.222 7.121c1.055 1.795 9.805-5.205 9.805-5.205s-.925 3.417 1.08 3.25c2.004-.166 5.254-4.583 5.504-9.666.25-5.084.344-8.433 3.927-12.183 3.584-3.75 7.66-9.05 6.49-16.65-.667-4.334-.915-7.655-4.165-9.738" fill="#EEE"></path>
            <path d="M75.621 52.085c2.147 10.817 16.602 13.624 26.001 13.083 4.385-.251 7.945-1.781 10.578-3.436 2.662-2.165 5.731-5.073 7.175-8.97 2.704-7.298-.524-14.427-10.191-17.844-2.557-.904-5.442-1.595-8.539-2.026-13.794-1.325-27.452 6.957-25.024 19.193" fill="#DDD"></path>
            <path d="M105.5 38.136c-2.586-.818-5.441-1.595-8.538-2.026-6.697-.643-13.357.983-18.165 4.222-2.746 3.17-4.082 7.186-3.176 11.753 2.148 10.817 16.602 13.624 26 13.083 4.145-.238 5.92-.656 8.505-2.203 3.395-2.095 4.27-6.633 4.265-10.714-.006-4.312.166-11.25-8.89-14.115" fill="#FF76DA"></path>
            <path d="M97.283 57.765s.792 2.836 3.21 2.836c2.707 0 3.25-2.836 3.25-2.836" stroke="#4620AE" stroke-width="1.5" stroke-linecap="round"></path>
            <path d="M86.706 70.952c-2.188 0-3.75 1.902-4.062 3.589-.313 1.688 1.062 3.563 3.19 3.563 2.091 0 3.688-1.25 4.061-3.313.374-2.062-.876-3.84-3.189-3.84" fill="#FF76DA"></path>
            <path d="M96.41 71.51h4.452c.625 0 .988.812.76 1.719a84.627 84.627 0 00-.697 3.156c-.125.625-.657.906-1.344.906h-4.53c-.595 0-1.064-.594-.876-1.47.187-.873.515-2.78.765-3.467.25-.688.625-.844 1.47-.844" fill="red"></path>
            <path d="M94.943 79.511h4.453c.625 0 .99.812.761 1.72-.23.905-.19.628-.315 1.253-.125.625-.656.906-1.343.906h-4.532c-.593 0-1.062-.593-.875-1.468.188-.875.132-.88.382-1.567.25-.688.625-.844 1.47-.844" fill="#00D4B5"></path>
            <path d="M101.204 49.454c-.329 2.401-1.975 4.056-3.728 4.068-1.752.013-3.224-1.365-2.839-4.173.329-2.402 2.204-3.968 3.956-3.98 1.753-.012 2.971 1.458 2.611 4.085" fill="#FFF"></path>
            <path d="M101.204 49.454c.343-2.503-.753-3.939-2.371-4.06l-2.957 7.671a2.834 2.834 0 001.6.457c1.753-.012 3.399-1.667 3.728-4.068" fill="#4620AE"></path>
            <path d="M104.177 49.44c.329-2.402 1.976-4.057 3.729-4.069 1.75-.012 3.223 1.365 2.838 4.174-.33 2.401-2.203 3.967-3.956 3.98-1.753.012-2.97-1.458-2.611-4.085" fill="#FFF"></path>
            <path d="M110.744 49.549c.362-2.643-.92-4.018-2.532-4.161l-2.951 7.657c.426.313.943.488 1.527.484 1.753-.012 3.627-1.578 3.956-3.98M87.91 45.315c.562-3.03 2.388-5.916 5.08-5.916h15.45a24.551 24.551 0 00-2.939-1.263c-2.558-.904-5.443-1.595-8.539-2.026-6.698-.643-13.358.983-18.165 4.222-2.746 3.17-4.082 7.186-3.176 11.753.658 3.317 2.477 5.877 4.95 7.823 5.04-4.733 6.904-12.245 7.34-14.593" fill="#4620AE"></path>
            <path d="M83.706 129.585c.437 2.813 1 3.75 1 3.75h20.479c3.104-6.75-2.552-6.375-4.442-5.935-1.996.466-2.766-1.003-2.079-2.94a40.677 40.677 0 001.519-5.488H83.801c.059 3.017-.466 8.227-.095 10.613M109.684 111.708c-.624 3.501-1.061 7.814-.624 10.126.438 2.313 1 3.375 1 3.375h20.083c2.292-4.833-1-6.54-4.084-5.833-2.082.48-3.603-.854-3.165-2.917.197-.937.837-2.91 1.474-5.188h-14.622c-.022.148-.034.285-.061.437" fill="#EEE"></path>
            <path d="M85.223 132.604h19.812a1.063 1.063 0 110 2.125H85.223a1.062 1.062 0 010-2.125M110.556 124.604h19.812a1.063 1.063 0 110 2.125h-19.812a1.062 1.062 0 010-2.125M49.602 108.918c-2.25 3.25-4.276 5.326-3.222 7.121 1.054 1.796 9.804-5.204 9.804-5.204s-.924 3.416 1.08 3.25c2.005-.167 5.255-4.584 5.505-9.667.102-2.075.181-3.859.479-5.502H50.486c.242 4.898 1.167 7.04-.884 10.002M150.654 62.194c-1.233 1.457-2.734 2.486-4.527 3.286-.459.206-.51.838-.077 1.094 1.025.605 1.386 1.649 1.505 2.937a.618.618 0 001.088.349c1.381-1.58 2.95-2.694 4.694-3.44.434-.186.523-.777.14-1.053-1.006-.725-1.563-1.695-1.748-2.895-.079-.508-.742-.672-1.075-.278" fill="#FFF"></path>
            <path d="M152.672 63.118c-1.558.43-2.922.342-4.232-.116-.414-.144-.874.147-.844.584.105 1.497-.647 2.935-1.778 4.463-.355.479.09 1.12.667.967 1.686-.45 3.12-.401 4.36.063.39.145.816-.102.843-.516.097-1.57.66-3.047 1.633-4.482.32-.473-.1-1.115-.65-.963M130.268 79.839h-5.5c-1.375 0-1.5-2.063-.75-2.688s2.688-1.312 1.938-2.874c-.75-1.563-3.063-.125-5.625.5a11.12 11.12 0 01-5.16-.011l-5.046 9.582c6.893 2.464 17.022 1.17 20.143-4.51M57.805 89.604c2.353-3.097 1.502-7.375.834-9.547-1.391 1.37-2.575 2.58-3.204 3.36-1.532 1.9-3.556 5.336-4.488 9.406 2.04-.07 4.922-.672 6.858-3.22" fill="#FFF"></path>
            <path d="M91.184 111.492c-.596 2.674 3.376 5.067 9.437 4.404.168-2.171.002-4.326-.873-5.936-.444-.814-.988-1.572-1.555-2.281-3.201.24-6.453 1.326-7.008 3.813M116.437 98.588c-.598 2.677 3.384 5.072 9.455 4.402-.006-2.685-.706-5.73-2.704-8.194-3.117.278-6.21 1.371-6.75 3.791" fill="#EEE"></path>
            <path d="M24.872 84.989c.476 1.649-.427 3.134-1.944 3.57-1.515.437-3.227-.103-3.784-2.032-.474-1.65.655-3.131 2.17-3.568 1.515-.437 3.038.225 3.558 2.03M41.888 74.31c.947 3.286-1.01 6.286-4.222 7.212-3.213.926-6.807-.096-7.914-3.937-.947-3.284 1.487-6.288 4.699-7.214 3.213-.926 6.402.347 7.437 3.94" fill="#BD79FF"></path>
            <g transform="translate(65 .659)">
              <mask fill="#fff">
                <use xlink:href="#c"></use>
              </mask>
              <path d="M24.617 6.552c1.838 6.374-1.958 12.195-8.192 13.992-6.235 1.797-13.207-.185-15.356-7.638-1.837-6.374 2.885-12.202 9.12-14 6.234-1.796 12.42.674 14.428 7.646" fill="#BD79FF" mask="url(#d)"></path>
            </g>
            <g fill="#BD79FF">
              <path d="M164.33 92.07c2.266 2.426 2.012 5.775-.217 7.858-2.228 2.082-5.652 2.653-8.303-.183-2.266-2.426-1.621-5.97.609-8.053 2.228-2.082 5.432-2.275 7.911.378"></path>
              <path d="M169.264 87.026c-1.634 0-7.03 5.042-9.735 7.569-7.73 7.221-9.117 9.51-8.92 10.159 1.03 1.026 6.113-3.715 9.816-7.186l2.438-2.273c3.522-3.269 6.848-6.357 6.876-7.801a.439.439 0 00-.138-.349c-.081-.081-.194-.119-.337-.119m-18.335 19.338a1.89 1.89 0 01-1.397-.576c-.201-.2-.437-.555-.427-1.111.03-1.752 2.665-4.886 9.4-11.178 6.295-5.882 10.253-9.32 12.156-7.414.388.387.587.884.577 1.437-.038 2.082-3.108 4.93-7.355 8.872l-2.432 2.269c-4.63 4.339-8.217 7.701-10.522 7.701M113.169 17.511c.507 1.758-.456 3.34-2.071 3.806-1.616.465-3.44-.11-4.033-2.166-.506-1.759.698-3.338 2.313-3.804 1.615-.465 3.236.241 3.79 2.164M170.296 109.446c.308 1.065-.275 2.023-1.255 2.306-.978.28-2.084-.067-2.442-1.313-.308-1.065.422-2.021 1.4-2.304.979-.282 1.96.146 2.297 1.31M33.03 107.177c.306 1.065-.277 2.023-1.256 2.306-.978.281-2.083-.067-2.442-1.313-.307-1.065.422-2.022 1.4-2.304.98-.282 1.961.146 2.297 1.311"></path>
            </g>
          </g>
        </svg>
        <figcaption>Connect to the internet<br/><small>You're offline. Check your connection.</small></figcaption>
    </figure>

### Fonts with ligatures

- [FiraCode](https://github.com/tonsky/FiraCode)
- [Hack](https://sourcefoundry.org/hack/)
- [JetBrains Mono](https://www.jetbrains.com/lp/mono/)

### Gmail templates

- Create a new Google Docs https://docs.new
- Insert →  Building blocks → Email draft

Or simply type `@email draft`.

### Links

- [No hello](https://nohello.net/)
  > Imagine calling someone on the phone, going hello! then putting them on hold... 🤦‍♀️
- [The XY Problem](https://xyproblem.info/)
  > The XY problem is asking about your attempted solution rather than your actual problem. This leads to enormous amounts of wasted time and energy, both on the part of people asking for help, and on the part of those providing help.
- [Don't ask to ask, just ask](https://dontasktoask.com/)
- [How do I ask a good question?](https://stackoverflow.com/help/how-to-ask)
- [How to create a Minimal, Reproducible Example](https://stackoverflow.com/help/mcve)

### Tiniest data URLs images

[`data:[<mediatype>][;base64],<data>`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/Data_URLs)

!!! example "`data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg'/>`"
    ![](data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg'/>){ style="outline: 1px solid red;" }

!!! example "`data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==` [🔗](http://probablyprogramming.com/2009/03/15/the-tiniest-gif-ever)"
    ![](data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==){ style="outline: 1px solid red;" }

!!! example "`data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAQAAAC1HAwCAAAAC0lEQVQYV2NgYAAAAAMAAWgmWQ0AAAAASUVORK5CYII=`"
    ![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAQAAAC1HAwCAAAAC0lEQVQYV2NgYAAAAAMAAWgmWQ0AAAAASUVORK5CYII=){ style="outline: 1px solid red;" }

!!! example "`data:image/x-icon;base64,AAABAAEAAQECAAEAAQA4AAAAFgAAACgAAAABAAAAAgAAAAEAAQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACAAAAA`"
    ![](data:image/x-icon;base64,AAABAAEAAQECAAEAAQA4AAAAFgAAACgAAAABAAAAAgAAAAEAAQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACAAAAA){ style="outline: 1px solid red;" }

!!! example "`data:image/jpg;base64,/9j/4AAQSkZJRgABAQEASABIAAD/2wBDAP//////////////////////////////////////////////////////////////////////////////////////wgALCAABAAEBAREA/8QAFBABAAAAAAAAAAAAAAAAAAAAAP/aAAgBAQABPxA=`"
    ![](data:image/jpg;base64,/9j/4AAQSkZJRgABAQEASABIAAD/2wBDAP//////////////////////////////////////////////////////////////////////////////////////wgALCAABAAEBAREA/8QAFBABAAAAAAAAAAAAAAAAAAAAAP/aAAgBAQABPxA=){ style="outline: 1px solid red;" }

### URI

```
                    hierarchical part
        ┌───────────────────┴─────────────────────┐
                    authority               path
        ┌───────────────┴───────────────┐┌───┴────┐
  abc://username:password@example.com:123/path/data?key=value#fragid1
  └┬┘   └───────┬───────┘ └────┬────┘ └┬┘           └───┬───┘ └──┬──┘
scheme  user information     host     port            query   fragment
```

??? example "Examples"

    ```
            userinfo       host      port
            ┌──┴───┐ ┌──────┴──────┐ ┌┴┐
    https://john.doe@www.example.com:123/forum/questions/?tag=networking&order=newest#top
    └─┬─┘   └─────────────┬────────────┘└───────┬───────┘ └────────────┬────────────┘ └┬┘
    scheme          authority                  path                  query           fragment
    
    ldap://[2001:db8::7]/c=GB?objectClass?one
    └┬─┘   └─────┬─────┘└─┬─┘ └──────┬──────┘
    scheme   authority   path      query
    
    mailto:John.Doe@example.com
    └─┬──┘ └────┬─────────────┘
    scheme     path
    
    news:comp.infosystems.www.servers.unix
    └┬─┘ └─────────────┬─────────────────┘
    scheme            path
    
    tel:+1-816-555-1212
    └┬┘ └──────┬──────┘
    scheme    path
    
    telnet://192.0.2.16:80/
    └─┬──┘   └─────┬─────┘│
    scheme     authority  path
    
    urn:oasis:names:specification:docbook:dtd:xml:4.1.2
    └┬┘ └──────────────────────┬──────────────────────┘
    scheme                    path
    ```

[🔗](https://en.wikipedia.org/wiki/Uniform_Resource_Identifier)
