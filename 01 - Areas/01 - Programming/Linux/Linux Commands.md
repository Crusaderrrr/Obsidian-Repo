### Navigation 
- `pwd` - print current dir
- `cd dir` - change directory (`cd ~` or just `cd` goes home)
- `ls` - list files (`ls -la` shows hidden files and details)
- `tree` - show a directory as a tree

### Files and Folders
- `touch file` - create a file
- `rm file` - remove file
- `mkdir dir` - create a dir
- `rmdir dir` - remove a dir

- `cp src dest` - copy (`-r` for dirs)
- `mv src dest` - move or rename
- `ln -s target link` - create a link (shortcut)

### Reading files
- `cat file` - print the whole file
- `less file` - scroll through a file (`q` quits)
- `head file` / `tail file` - first or last 10 lines
- `wc file` - count lines, words and bytes

### Editing
- `nano file` - simple editor (Ctrl+O saves, Ctrl+X exits)
- `vim file` - opens file in vim editor 

### Searching 
- `grep "text" file` - find lines matching text (`-i` ignore case, `-r` searches recursively)
- `find . -name "*.java"` - find files by name, type, size, etc.
- `which cmd` - show where a command's program lives

### Permissions and ownership
- `chmod` - give permissions
- `sudo` - superuser do (run as root)
- `whoami` - shows current user

### Processes and system
- `ps aux` - list running processes 
- `top` / `htop` - live process monitor
- `kill PID` - kill process

### Networking
- `ping host` - check whether a host is reachable
- `curl url` / `wget url` - fetch a URL or download a file
- `scp file user@host:path` - copy a file over ssh
- `ip a` - show network interfaces and IP addresses