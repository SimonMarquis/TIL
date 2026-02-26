---
title: 🍎 Mac
---

### [AltTab](https://github.com/lwouis/alt-tab-macos)

> AltTab brings the power of Windows alt-tab to macOS.

### [Brewfile](https://docs.brew.sh/Manpage#bundle-subcommand)

```bash
# Generate Brewfile
brew bundle dump

# Install content of Brewfile
brew bundle install --file <path>
```

### Case Sensitive Volume

```bash
diskutil list # to list all disks

# sudo diskutil apfs addVolume <disk> APFSX <name> -mountpoint /Users/<username>/<name>
sudo diskutil apfs addVolume disk3 APFSX dev -mountpoint /Users/simon.marquis/dev

# if mountpoint does not persist
ln -s /Volumes/dev ~/dev
```

### [Defaults](https://macos-defaults.com/)

```bash
# Set the icon size of Dock items in pixels.
defaults write com.apple.dock "tilesize" -int 36 && killall Dock
# Show recently used apps in a separate section of the Dock.
defaults write com.apple.dock "show-recents" -bool false && killall Dock
# Change the Dock minimize animation.
defaults write com.apple.dock "mineffect" -string "scale" && killall Dock
# Faster keyboard execution.
defaults write NSGlobalDomain InitialKeyRepeat -int 15
defaults write NSGlobalDomain KeyRepeat -int 2
# Show all file extensions in the Finder.
defaults write NSGlobalDomain "AppleShowAllExtensions" -bool true && killall Finder
# Show hidden files in the Finder.
defaults write com.apple.finder "AppleShowAllFiles" -bool true && killall Finder
# Show path bar in the bottom of the Finder windows
defaults write com.apple.finder "ShowPathbar" -bool true && killall Finder
# Choose whether to display a warning when changing a file extension.
defaults write NSGlobalDomain NSAutomaticPeriodSubstitutionEnabled -bool false
# Disable automatic capitalization
defaults write NSGlobalDomain NSAutomaticCapitalizationEnabled -bool false
# Disable smart dashes
defaults write NSGlobalDomain NSAutomaticDashSubstitutionEnabled -bool false
# Disable smart quotes
defaults write NSGlobalDomain NSAutomaticQuoteSubstitutionEnabled -bool false
# Disable auto-correct
defaults write NSGlobalDomain NSAutomaticSpellingCorrectionEnabled -bool false
# Disable the annoying line marks
defaults write com.apple.Terminal ShowLineMarks -bool false

# Restart the service in order to propagate changes.
killall SystemUIServer
```

### [Karabiner](https://github.com/pqrs-org/Karabiner-Elements)

> Karabiner-Elements is a powerful utility for keyboard customization on macOS  
> Location: `~/.config/karabiner`

### [Oh My Posh](https://ohmyposh.dev/)

... (unchanged content omitted for brevity in this commit) ...

- 🪄 Select Android Device • 📥(assets/Select Android Device.shortcut){: download="Select Android Device.shortcut" } • ▶️(shortcuts://run-shortcut?name=Select%20Android%20Device) • [`#!bash adb devices -l`](https://developer.android.com/tools/adb#devicestatus)

- 📸 Screenshot • 📥(assets/Screenshot.shortcut){: download="Screenshot.shortcut" } • ▶️(shortcuts://run-shortcut?name=Screenshot) • [`#!bash adb shell screencap`](https://developer.android.com/tools/adb#screencap)

- 🪞 Mirror • 📥(assets/Mirror.shortcut){: download="Mirror.shortcut" } • ▶️(shortcuts://run-shortcut?name=Mirror) • [`#!bash scrcpy`](https://github.com/Genymobile/scrcpy?tab=readme-ov-file)

- 📹 Record • 📥(assets/Record.shortcut){: download="Record.shortcut" } • ▶️(shortcuts://run-shortcut?name=Record) • [`#!bash scrcpy --record`](https://github.com/Genymobile/scrcpy/blob/master/doc/recording.md)

- ♻️ Kill Gradle & Kotlin daemons • 📥(assets/Kill daemons.shortcut){: download="Kill daemons.shortcut" } • ▶️(shortcuts://run-shortcut?name=Kill%20daemons) • [`#!bash pkill`](https://linux.die.net/man/1/pkill)

- 🥑 avocado • 📥(assets/🥑 avocado.shortcut){: download="🥑 avocado.shortcut" } • ▶️(shortcuts://run-shortcut?name=🥑%20avocado) • [`#!bash avocado`](https://github.com/alexjlockwood/avocado)

- 🖼️ Diff images • 📥(assets/Diff.shortcut){: download="Diff.shortcut" } • ▶️(shortcuts://run-shortcut?name=Diff) • [`#!bash magick compare <l> <r> -compose src <output>`](https://imagemagick.org/script/compare.php)

- 🛜 Network details • 📥(assets/Network.shortcut){: download="Network.shortcut" } • ▶️(shortcuts://run-shortcut?name=Network)

- ☕ Caffeinate • 📥(assets/Caffeinate.shortcut){: download="Caffeinate.shortcut" } • ▶️(shortcuts://run-shortcut?name=Caffeinate)

