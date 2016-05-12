# Terminal

This script (`terminal.py`) allows you to open a new terminal window to execute
some command in Windows, Cygwin, Ubuntu and OS X. And prompts you "press any key to continue ..." before exit.

When I am using some gui editor (atom, gvim/macvim/local vim, sublime, gedit) to debug my source, I wish to open a new terminal window to execute it instead of running and output result in the bottom panel (no interactive) or stop the editor to wait for my program. 

Opening a new terminal window to execute commands in different operating systems is a tricky thing: arguments must be carefully escaped and passed in correct way, intermediate script (shell script, AppleScript or batch script) must be carefully generated and passed through pipe, and different terminal in all systems must be invoked in different methods.

So `terminal.py` is created to do these dirty stuff altogether in a single script file and provide a unique interface under different operating systems.

# Features

- Open a new cmd window to execute commands in Windows
- Open a new Terminal/iTerm window to execute commands in Mac OS X
- Open a new xterm window to execute commands in Mac os x (require xquartz)
- Open a new xterm/gnome-terminal window to execute commands in Linux desktop
- Read commands from both arguments or stdin
- Open a cygwin bash/mintty window to execute commands in Windows (outside cygwin)
- Using cygwin bash to execute commands (without creating a new window) in Windows
- Open a new bash/mintty window to execute commands inside cygwin
- Open a new cmd window to execute windows batch command inside cygwin
- Using cmd to execute windows bash commands (without new window) inside cygwin
- After commands finished, prompts user to press any key to quit (optional)
- Run some other commands before quit (after waiting user pressing key)
- Set terminal profile (only enabled in Terminal/iTerm/gnome-terminal)
- Set the title of the terminal window (not available in some terminal)

# Usage

```text
$ python terminal.py
Usage: terminal.py [options] command [args ...]

Execute program in a new terminal window

Options:
  --version             show program's version number and exit
  -h, --help            show this help message and exit
  -t TITLE, --title=TITLE
                        title of new window
  -m TERMINAL, --terminal=TERMINAL
                        available terminals: terminal (default), iterm
  -p PROFILE, --profile=PROFILE
                        terminal profile
  -d CWD, --cwd=CWD     working directory
  -w, --wait            wait before exit
  -o POST, --post=POST  post action
  -s, --stdin           read commands from stdin 
```

# Windows 

Open a new cmd window to execute command:

	python terminal.py d:\hello.exe

Open a new cmd window to execute command and pause after finish:

	python terminal.py --wait d:\hello.exe

Open a new cmd window and set title:
    
	python terminal.py --wait -t mytitle d:\hello.exe 
	
Open a new cmd window and execute commands which is passed from stdin:

    python terminal.py --wait --stdin 
	dir c:\
	echo Hello from a new cmd window !!
	^Z
	
# Linux (ubuntu)

Open a new window (xterm by default) to execute command:

	python terminal.py --wait ls -la
	
Open a new gnome-terminal to execute command:

	python terminal.py -m gnome-terminal --wait ls -la
	
Open gnome-terminal in given profile (create a new profile in gnome-terminal's settings):

	python terminal.py -m gnome-terminal -p myprofile --wait ls -la
	
Open a new gnome-terminal and execute commands which is passed from stdin:

	python terminal.py --wait -m gnome-terminal --stdin
	ls -la
	echo "Hello from a new gnome-terminal"
	^D

# Mac OS X

Open a new Terminal window to execute command:

	python terminal.py --wait ls -la
	
Open Terminal in given profile (create a new profile in Terminal's preferences):

	python terminal.py --wait -p DevelopProfile ls -la
	
Open Terminal and execute commands which is passed from stdin:

	python terminal.py --wait --stdin
	ls -la
	echo "Hello from a new Terminal window"
	^D

Open iTerm and execute command:

	python terminal.py --wait -m iterm ls -la
	

