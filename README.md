# okulard

User daemon that tracks currently open Okular documents and rewrites the Okular `.desktop` Exec line to reopen the previous session automatically (no wrapper, correct dock icon).

## One-command setup

Run the installer to configure everything in your user profile:

```
~/Documents/work/sandbox/github/martinbortel/okulard/bin/okulard-install
```

This will:
- Install the daemon to `~/.local/bin/okulard`
- Install the desktop entry to `~/.local/share/applications/org.kde.okular.desktop` with a clean Exec
- Create and enable a systemd user service `okulard.service` to start the daemon at login
- Refresh the desktop database

If systemd user services are not available, the script will still install the files; you can start the daemon manually.

## Uninstall

```
systemctl --user disable --now okulard.service || true
rm -f ~/.config/systemd/user/okulard.service
rm -f ~/.local/bin/okulard
rm -f ~/.local/share/applications/org.kde.okular.desktop
update-desktop-database ~/.local/share/applications || true
```

## Notes

- The daemon updates the Exec line to include up to 15 last-open files and keeps `%U` so newly selected items are added too.
- It only injects files that still exist to avoid errors.
- The tracked list lives in `~/.okular/open_files` and `~/.okular/previous_files`.

*okulard is a simple way to re-open the last documents previously opened in Okular.*

It works by saving in a file the paths of the last opened files, which are then passed as arguments to okular when we open it again.
A service is created to periodically check the current opened documents in okular.

## installation

First install the files by using this commands:

$ cp ./bin/okulard ~/bin/
$ sudo cp ./etc/systemd/system/okulard.service /etc/systemd/system/okulard.service
$ sudo systemctl start okulard.service
$ sudo systemctl enable okulard.service

Then, accordingly to your desktop environment, create a new menu command with this command: 

cat $HOME/.okular/open_files | xargs -d$'\n' okular

## notes

The script, re-opens only the documents referenced in the okulard bash script's path, which is by default:
`$HOME`

You are absolutely free to modify it to your needs or to improve the script.
