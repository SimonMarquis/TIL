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

??? example "Personal Brewfile"

    ```bash
    tap "hashicorp/tap"
    tap "homebrew/bundle"
    tap "homebrew/cask"
    tap "homebrew/core"
    tap "jakewharton/repo"
    tap "mdogan/zulu"
    brew "jpeg-xl"
    brew "autojump"
    brew "bat"
    brew "cloc"
    brew "commitizen"
    brew "coreutils"
    brew "fdupes"
    brew "unbound"
    brew "gnutls"
    brew "tesseract"
    brew "ffmpeg"
    brew "node"
    brew "firebase-cli"
    brew "gh"
    brew "git-lfs"
    brew "python@3.10"
    brew "git-review"
    brew "gitleaks"
    brew "gnupg"
    brew "gping"
    brew "libheif"
    brew "libraw"
    brew "imagemagick"
    brew "jadx"
    brew "jdupes"
    brew "jq"
    brew "kdoctor"
    brew "kotlin"
    brew "mitmproxy"
    brew "mkdocs"
    brew "ncdu"
    brew "node-sass"
    brew "node@14"
    brew "pinentry-mac"
    brew "scrcpy"
    brew "tree"
    brew "hashicorp/tap/vault"
    brew "jakewharton/repo/dependency-watch"
    brew "jakewharton/repo/diffuse"
    cask "android-platform-tools"
    cask "docker"
    cask "flipper"
    cask "google-cloud-sdk"
    cask "keystore-explorer"
    cask "stats"
    cask "zulu-jdk11"
    cask "zulu-jdk17"
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
defaults write com.apple.finder "FXEnableExtensionChangeWarning" -bool false && killall Finder
# Flash clock time separators
defaults write com.apple.menuextra.clock "FlashDateSeparators" -bool true && killall SystemUIServer
# Set menubar digital clock format
defaults write com.apple.menuextra.clock "DateFormat" -string "\"EEE d MMM HH:mm:ss\"" && killall SystemUIServer
# How frequently Activity Monitor should update its data, in seconds.
defaults write com.apple.ActivityMonitor "UpdatePeriod" -int 1 && killall Activity\ Monitor
# Disable full stop with double-space.
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

PC-Style configuration:

```json
{
    "global":{
    "check_for_updates_on_startup":true,"show_in_menu_bar":true,"show_profile_name_in_menu_bar":false},
    "profiles":[
        {
            "complex_modifications": {
                "parameters":{"basic.simultaneous_threshold_milliseconds":50,"basic.to_delayed_action_delay_milliseconds":500,"basic.to_if_alone_timeout_milliseconds":1000,"basic.to_if_held_down_threshold_milliseconds":500,"mouse_motion_to_scroll.speed":100},
                "rules":[
                    {"description":"Option(Alt)+Tab as Switch Application (Command+Tab)","manipulators":[{"from":{"key_code":"tab","modifiers":{"mandatory":["option"],"optional":["any"]}},"to":[{"key_code":"tab","modifiers":["left_command"]}],"type":"basic"}]},
                    {"description":"PC-Style Copy/Paste/Cut","manipulators":[{"from":{"key_code":"c","modifiers":{"mandatory":["control"],"optional":["left_shift"]}},"to":[{"key_code":"c","modifiers":["left_command"]}],"type":"basic"},{"from":{"key_code":"v","modifiers":{"mandatory":["control"],"optional":["left_shift"]}},"to":[{"key_code":"v","modifiers":["left_command"]}],"type":"basic"},{"from":{"key_code":"x","modifiers":{"mandatory":["control"],"optional":["left_shift"]}},"to":[{"key_code":"x","modifiers":["left_command"]}],"type":"basic"}]},
                    {"description":"PC-Style Undo","manipulators":[{"from":{"key_code":"z","modifiers":{"mandatory":["control"],"optional":["left_shift"]}},"to":[{"key_code":"z","modifiers":["left_command"]}],"type":"basic"}]},
                    {"description":"PC-Style Select-All","manipulators":[{"from":{"key_code":"a","modifiers":{"mandatory":["control"],"optional":["left_shift"]}},"to":[{"key_code":"a","modifiers":["left_command"]}],"type":"basic"}]},
                    {"description":"PC-Style Save","manipulators":[{"from":{"key_code":"s","modifiers":{"mandatory":["control"],"optional":["left_shift"]}},"to":[{"key_code":"s","modifiers":["left_command"]}],"type":"basic"}]},
                    {"description":"PC-Style New","manipulators":[{"from":{"key_code":"n","modifiers":{"mandatory":["control"],"optional":["left_shift"]}},"to":[{"key_code":"n","modifiers":["left_command"]}],"type":"basic"}]},
                    {"description":"PC-Style Command Palette","manipulators":[{"from":{"key_code":"p","modifiers":{"mandatory":["control"],"optional":["left_shift"]}},"to":[{"key_code":"p","modifiers":["left_command"]}],"type":"basic"}]},
                    {"description":"PC-Style Reload(F5, Ctrl+R)","manipulators":[{"from":{"key_code":"r","modifiers":{"mandatory":["control"],"optional":["left_shift"]}},"to":[{"key_code":"r","modifiers":["left_command"]}],"type":"basic"},{"from":{"key_code":"f5","modifiers":{"optional":["any"]}},"to":[{"key_code":"r","modifiers":["left_command"]}],"type":"basic"}]},
                    {"description":"PC-Style New Tab","manipulators":[{"from":{"key_code":"t","modifiers":{"mandatory":["control"],"optional":["left_shift"]}},"to":[{"key_code":"t","modifiers":["left_command"]}],"type":"basic"}]},
                    {"description":"PC-Style Find","manipulators":[{"from":{"key_code":"f","modifiers":{"mandatory":["control"],"optional":["left_shift"]}},"to":[{"key_code":"f","modifiers":["left_command"]}],"type":"basic"},{"from":{"key_code":"g","modifiers":{"mandatory":["control"],"optional":["left_shift"]}},"to":[{"key_code":"g","modifiers":["left_command"]}],"type":"basic"}]},
                    {"description":"PC-Style Open","manipulators":[{"from":{"key_code":"o","modifiers":{"mandatory":["control"],"optional":["left_shift"]}},"to":[{"key_code":"o","modifiers":["left_command"]}],"type":"basic"}]},
                    {"description":"PC-Style Bold/Italic/Underline(Ctrl+B/I/U)","manipulators":[{"from":{"key_code":"b","modifiers":{"mandatory":["control"],"optional":["left_shift"]}},"to":[{"key_code":"b","modifiers":["left_command"]}],"type":"basic"},{"from":{"key_code":"i","modifiers":{"mandatory":["control"],"optional":["left_shift"]}},"to":[{"key_code":"i","modifiers":["left_command"]}],"type":"basic"},{"from":{"key_code":"u","modifiers":{"mandatory":["control"],"optional":["left_shift"]}},"to":[{"key_code":"u","modifiers":["left_command"]}],"type":"basic"}]},
                    {"description":"PC-Style Close Window","manipulators":[{"from":{"key_code":"w","modifiers":{"mandatory":["control"],"optional":["left_shift"]}},"to":[{"key_code":"w","modifiers":["left_command"]}],"type":"basic"}]},
                    {"description":"PC-Style Emoji Picker (Command+.)","manipulators":[{"from":{"key_code":"period","modifiers":{"mandatory":["command"]}},"to":[{"key_code":"spacebar","modifiers":["left_control","left_command"]}],"type":"basic"}]},
                    {"description":"PC-Style Lock Screen","manipulators":[{"from":{"key_code":"l","modifiers":{"mandatory":["option"]}},"to":[{"key_code":"power","modifiers":["left_control","left_shift"]}],"type":"basic"}]},
                    {"description":"PC-Style Quit Application (Alt+F4 to Command+Q)","manipulators":[{"from":{"key_code":"f4","modifiers":{"mandatory":["option"]}},"to":[{"key_code":"q","modifiers":["left_command"]}],"type":"basic"}]},
                    {"description":"Command+E Opens Finder","manipulators":[{"from":{"key_code":"e","modifiers":{"mandatory":["option"]}},"to":[{"shell_command":"open -a 'Finder.app'"}],"type":"basic"}]},
                    {"description":"Control+Shift+Esc Opens Activity Monitor","manipulators":[{"from":{"key_code":"escape","modifiers":{"mandatory":["control","shift"]}},"to":[{"shell_command":"open -a 'Activity Monitor.app'"}],"type":"basic"}]},
                    {"description":"PC-Style Back/Forward (Alt+Left Arrow/Alt+Right Arrow)","manipulators":[{"conditions":[{"bundle_identifiers":["^org\\.mozilla\\.firefox$","^org\\.mozilla\\.nightly$","^com\\.microsoft\\.Edge","^com\\.microsoft\\.edgemac","^com\\.google\\.Chrome$","^com\\.brave\\.Browser$","^com\\.apple\\.Safari$"],"type":"frontmost_application_if"}],"from":{"key_code":"left_arrow","modifiers":{"mandatory":["option"],"optional":["any"]}},"to":[{"key_code":"left_arrow","modifiers":["left_command"]}],"type":"basic"},{"conditions":[{"bundle_identifiers":["^org\\.mozilla\\.firefox$","^org\\.mozilla\\.nightly$","^com\\.microsoft\\.Edge","^com\\.microsoft\\.edgemac","^com\\.google\\.Chrome$","^com\\.brave\\.Browser$","^com\\.apple\\.Safari$"],"type":"frontmost_application_if"}],"from":{"key_code":"right_arrow","modifiers":{"mandatory":["option"],"optional":["any"]}},"to":[{"key_code":"right_arrow","modifiers":["left_command"]}],"type":"basic"}]},
                    {"description":"PC-Style Control+Delete/Backspace","manipulators":[{"from":{"key_code":"delete_or_backspace","modifiers":{"mandatory":["control"],"optional":["any"]}},"to":[{"key_code":"delete_or_backspace","modifiers":["option"]}],"type":"basic"}]}
                ]
            },
            "devices":[],
            "fn_function_keys":[
                {"from":{"key_code":"f1"},"to":[{"consumer_key_code":"display_brightness_decrement"}]},
                {"from":{"key_code":"f2"},"to":[{"consumer_key_code":"display_brightness_increment"}]},
                {"from":{"key_code":"f3"},"to":[{"apple_vendor_keyboard_key_code":"mission_control"}]},
                {"from":{"key_code":"f4"},"to":[{"apple_vendor_keyboard_key_code":"spotlight"}]},
                {"from":{"key_code":"f5"},"to":[{"consumer_key_code":"dictation"}]},
                {"from":{"key_code":"f6"},"to":[{"key_code":"f6"}]},
                {"from":{"key_code":"f7"},"to":[{"consumer_key_code":"rewind"}]},
                {"from":{"key_code":"f8"},"to":[{"consumer_key_code":"play_or_pause"}]},
                {"from":{"key_code":"f9"},"to":[{"consumer_key_code":"fast_forward"}]},
                {"from":{"key_code":"f10"},"to":[{"consumer_key_code":"mute"}]},
                {"from":{"key_code":"f11"},"to":[{"consumer_key_code":"volume_decrement"}]},
                {"from":{"key_code":"f12"},"to":[{"consumer_key_code":"volume_increment"}]}
            ],
            "name":"Default profile",
            "parameters":{"delay_milliseconds_before_open_device":1000},
            "selected":true,
            "simple_modifications":[{"from":{"apple_vendor_top_case_key_code":"keyboard_fn"},"to":[{"key_code":"left_control"}]},{"from":{"key_code":"left_control"},"to":[{"apple_vendor_top_case_key_code":"keyboard_fn"}]}],
            "virtual_hid_keyboard":{"country_code":0,"indicate_sticky_modifier_keys_state":true,"mouse_key_xy_scale":100}
        }
    ]
}
```

[🔗](https://stackoverflow.com/questions/35874608/intellij-default-windows-keymap-on-mac-os-x) [🔗](https://ke-complex-modifications.pqrs.org/#pc_shortcuts)

### [Stats](https://github.com/exelban/stats)

> macOS system monitor in your menu bar

### [UnnaturalScrollWheels](https://github.com/ther0n/UnnaturalScrollWheels)

> Invert scroll direction for physical scroll wheels while maintaining "Natural" scrolling for trackpads on MacOS.
