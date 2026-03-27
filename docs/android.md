(Top unchanged)

    === ":simple-apple: macOS"

    ```bash title="~/.zprofile"
    function adbz() {
      adb devices -l 2> /dev/null `: # list devices and ignore daemon messages` |
        tail -n +2 `: # ignore first line` |
        ghead -n -1 `: # ignore last line` |
        cut -d " " -f1 `: # extract device id` |
        fzf --header '📱 Select one or more devices' --border --reverse --multi \
            --preview-window="right:66%" \
            --preview="adb -s {} shell getprop | grep -E   'ro.build.(description|fingerprint|version.(release|sdk))|ro.product.(cpu.abi|device|locale|manufacturer|model|name)'" |
        xargs -t -I % adb -s % adb -s % "$@" `: # run your command of choice`
    }
    ```
