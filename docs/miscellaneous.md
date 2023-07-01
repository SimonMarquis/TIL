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

### Fonts with ligatures

- [FiraCode](https://github.com/tonsky/FiraCode)
- [Hack](https://sourcefoundry.org/hack/)
- [JetBrains Mono](https://www.jetbrains.com/lp/mono/)

### Gmail templates

- Create a new Google Docs https://docs.new
- Insert →  Building blocks → Email draft

Or simply type `@email draft`.

### Tiniest data URLs images

[`data:[<mediatype>][;base64],<data>`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/Data_URLs)

??? example "`data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg'/>`"
    ![](data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg'/>){ style="outline: 1px solid red;" }

??? example "`data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==` [🔗](http://probablyprogramming.com/2009/03/15/the-tiniest-gif-ever)"
    ![](data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==){ style="outline: 1px solid red;" }

??? example "`data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAQAAAC1HAwCAAAAC0lEQVQYV2NgYAAAAAMAAWgmWQ0AAAAASUVORK5CYII=`"
    ![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAQAAAC1HAwCAAAAC0lEQVQYV2NgYAAAAAMAAWgmWQ0AAAAASUVORK5CYII=){ style="outline: 1px solid red;" }

??? example "`data:image/x-icon;base64,AAABAAEAAQECAAEAAQA4AAAAFgAAACgAAAABAAAAAgAAAAEAAQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACAAAAA`"
    ![](data:image/x-icon;base64,AAABAAEAAQECAAEAAQA4AAAAFgAAACgAAAABAAAAAgAAAAEAAQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACAAAAA){ style="outline: 1px solid red;" }

??? example "`data:image/jpg;base64,/9j/4AAQSkZJRgABAQEASABIAAD/2wBDAP//////////////////////////////////////////////////////////////////////////////////////wgALCAABAAEBAREA/8QAFBABAAAAAAAAAAAAAAAAAAAAAP/aAAgBAQABPxA=`"
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

### Youtube monkey error

<figure>
    <svg id="monkey" viewBox="0 0 490 525" width="250">
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
