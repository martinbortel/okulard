# Okular-Last

***Okular-Last is a simple way to re-open the last documents previously opened in Okular.***

It works by saving in a file the paths of the last opened files, which are then passed as arguments to okular when we open it again.
A service is created to periodically check the current opend documents in okular.

***Installation:***

First install the files by using this commands:

$ sudo cp okulard /usr/bin
$ sudo cp okulard.service /etc/systemd/system/okulard.service
$ sudo systemctl start okulard.service
$ sudo systemctl enable okulard.service

Then, accordingly to your desktop environment, create a new menu command with this command: 

cat $HOME/.okularLastFiles | xargs -d$'\n' okular

**Notes:**

The script, as I wrote it,  re-open only the documents referenced in the okulard bash script's path, which I chose to be
$HOME/Documents/Books/

You are absolutely free to modify it to your needs or to improve the script.
