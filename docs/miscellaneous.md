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
