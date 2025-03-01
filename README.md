# colorswitch

This small Swift program for sketchybar that will run a command whenever the dark mode status changes on macOS. 

## Usage

Use make to compile the program, then run directly:

- shell

.build/release/colorswitch <your-program>


Alternatively you can install it by doing 

`make install`.

The program will be run immediately when the command starts, and every time the OS goes from dark mode to light mode or back. The environment variable `DARKMODE` will be set to either `1` or `0`.

## -----  Background agent

To keep this program running in the background, compile the binary to somewhere and create the following file at 

`~/Library/LaunchAgents/com.user.colorswitch.plist`. 

Don't forget to replace the arguments and the path to the logs (which comes in handy for debugging)

----------------------------------------------------------------------

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN"
"http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>com.user.colorswitch</string>
    <key>KeepAlive</key>
    <true/>
    <key>StandardErrorPath</key>
    <string>~/.config/sketchybar/helpers/colorswitch/colorswitch-stderr.log</string>
    <key>StandardOutPath</key>
    <string>~/.config/sketchybar/helpers/colorswitch/colorswitch-stdout.log</string>
    <key>ProgramArguments</key>
    <array>
       <string>/usr/bin/env/colorswitch</string>
       <string>~/.config/sketchybar/helpers/colorswitch/colorswitch.sh</string>
    </array>
</dict>
</plist>
```

--------------------------------------------------------------------

Then 

`launchctl load -w ~/Library/LaunchAgents/com.user.colorswitch.plist` 

will keep it running on boot.

## Credit

This script is a lightly modified version of https://github.com/mnewt/dotemacs/blob/master/bin/dark-mode-notifier.swift
