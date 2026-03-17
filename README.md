# Dune Mud TinTin++ Helpers

These are TinTin++ scripts to help [Dune Mud](http://dunemud.com/) players.

## Setup

These are the steps you should use to start using these scripts / environment. These steps require that you already have created a character in the mud.

1. Copy `characters/example.tin` to a name that matches your character's name (e.g. `characters/george.tin`).
2. Edit the newly created file.
  * Replace `<Name>` with your character's name.
  * Replace `<Password>` with your character's password.
  * Change the `#read guilds/...` line to read whatever guild your character is associated with.
  * Put whatever other character specific configurations in this file.

## How to Use

If you have TinTin++ installed (e.g. Linux, BSD, OSX):
* Open a terminal (e.g. iTerm)
* Clone or extract the project somewhere.
```
cd ~/source
git clone https://github.com/njlg/dune-tintin.git
```
* Run `tt++ -r main.tin`

If you have WinTin++ installed (e.g. Windows):
* Clone or copy the files to where you installed WinTin++ (e.g. `C:\Program Files\WinTin++`).
* Run WinTin++
* Input `#read main.tin`


## Folder Layout

* characters &mdash; All character specific configurations
* guilds &mdash; All guild specific configurations
* maps &mdash; Maps for all locations. (coming soon)
* paths &mdash; Paths for looping in certain areas. (coming soon)
