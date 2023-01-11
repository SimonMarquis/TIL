---
title: 🧰 Utils
---

### Count lines of code

```bash
cloc --fullpath --not-match-d="build" .
```

### Create empty file with specific size

```bash
truncate --size 10M filename
fallocate --length 10M filename
```

### Diff between two PNGs 

Drag&drop two png files, outputs a diff image.

```bat
@echo off
for /f %%a in ('powershell -Command "Get-Date -format yyyyMMdd-HHmmss"') do set datetime=%%a
magick compare %1 %2 -compose src %datetime%-diff.png
```

### mp4 to gif

| Parameter | Description |
|---|---|
| `-ss` | start in seconds |
| `-t` | duration in seconds |

```bash
ffmpeg -i input.mp4 -vf "fps=15,scale=320:-1:flags=lanczos,split[s0][s1];[s0]palettegen[p];[s1][p]paletteuse" -loop 0 output.gif
```

```bash
ffmpeg -y -i input.mp4 -vf fps=15,scale=320:-1:flags=lanczos,palettegen palette.png
ffmpeg -i input.mp4 -i palette.png -filter_complex "fps=15,scale=320:-1:flags=lanczos[x];[x][1:v]paletteuse" output.gif
```

[🔗](https://stackoverflow.com/a/10383546/3615879)

### NCurses Disk Usage

> [🔗](https://dev.yorhel.nl/ncdu) Ncdu is a disk usage analyzer with an ncurses interface

```bash
brew install ncdu
```

### Web crawler

```bash
wget \
    --recursive \
    --no-clobber \
    --page-requisites \
    --html-extension \
    --convert-links \
    --restrict-file-names=windows \
    --domains website.com \
    --no-parent \
    http://www.website.com/
```
