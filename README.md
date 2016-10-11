# Hermit

**Application launcher for GNU/Linux.**

A simple tabbed window shows icons that will launch commands specified
by .desktop files found in /usr/share/applications and user defined locations.

## Licence

Public domain.

## Author

nullpathos

## Requirements / dependencies

* python 2.7
* python-gtk2
* (optional) python-keybinder, use your distribution repositories or https://github.com/engla/keybinder
* other python libraries: os, glib, shlex, lxml, syslog, signal

## Usage

It's just one python script, download it, run it (use python or change permissions and execute).

By default, hermit will appear after pressing Super_R (right Meta key) if python-keybinder is installed.
Alternatively, send hermit a USR1 signal:
`pkill -USR1 -x hermit.py`  (this should work if hermit was executed directly)
Use your desktop environment to map a global hotkey or some other action to this command.

Hermit will create an XML file of settings in ~/.config/hermit/

Create an XML file tabs.xml (see included example_tabs.xml) in the same directory to specify your
own choice of .desktop launchers. (restart hermit to load)

Change settings directly in the XML file (needs restart) or using the last tab.

## Example Openbox integration

Add to the end of ~/.config/openbox/autostart :

python /wherever_you_saved_it/hermit.py &
xdotool behave_screen_edge --delay 0 --quiesce 500 left exec --sync xte "key Super_R" &

This will show hermit when your mouse pointer touches the left screen edge by simulating a press
of the hotkey, in this case Super_R. You'll have to install xdotool and xautomation (which
contains the xte command).

Alternatively, have hermit appear when right-clicking on the desktop background:
Edit ~/.config/openbox/rc.xml to change the selection within the "Root" context:
>      <mousebind button="Right" action="Press">
>        <action name="Execute">
>          <command>xte "key Super_R"</command>
>        </action>
>      </mousebind>
>      <mousebind button="C-Right" action="Press">
>        <action name="ShowMenu">
>          <menu>root-menu</menu>
>        </action>
>      </mousebind>
The normal openbox menu will still be available using control-rightclick.

## Future stuff

* Inclusion of other system locations (other than /usr/share/applications).
* More comprehensive settings, including a hotkey chooser.
* User defined tabs/launcher editor.
* Support for programs that require a terminal.

