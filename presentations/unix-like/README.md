
# Basics
* [Cheatsheets are great!](https://cheatography.com/davechild/cheat-sheets/linux-command-line/) Seriously, bookmark a couple of them.
* `vimtutor` : Learn to use `vim` a terminal editor by using vim.

## Commands
* `history | grep some_command` : _What was that command I ran yesterday?_
  * `!<history_id>` : rerun a command from the history.
* `man <command>` : read the manual
* `less <file>` : Print file contents a page at a time. _less is more_. `more` also prints file contents, but `less` is more feature rich. Use a regex like `/search_term` and `n` to skip to search pattern match. 
* `ls -ltrc` : sort files by time in reverse. I find I'm always looking for a recently modified file.
* `redirect_some_command 2>&1` : redirect some_commands's stderr to same place as stdout
* `ssh` : Secure shell for accessing remote hosts and transferring files. [Read all about it!](https://www.ssh.com/ssh/command/)
* `sudo <command>` : [run a command as root](https://xkcd.com/149/)
* `xdg-open` : Open a file with the configured application for the file type.

## Monitoring
Software is error prone and users are hoarders. Quite often you will find yourself out of memory or out of CPU.
* `du` : disk usage
  * `du -h --max-depth=1 <target_directory> | sort -h` : Find the folders with the most usage.
* `df -h` : disk free
* `kill`: terminate a process
  *  `kill -9 <process_id>` : _“I tried being reasonable, but I didn't like it.”_
* `pkill -U <userid>` : kill all processes for a user (forces a logout)  
* `ps -ef | grep process_name` : find a process id (so you can then kill it)
* `tail -f` : follow that log file
* `top` : find the hot running processes
* `watch` : run a command periodically
  * `watch -n 1 -d date --iso-8601=seconds` : Run once a second and show the differences in the output.

## Compression
* `tar` : Creates an uncompressed archive to store multiple files behind one file handle. 
  * `tar -zcvf tarfile.tar.gz <directory>` creates a gzipped compressed archive of the tI personally don't like a single file for completions. If you want to locally control completion scripts do the following.

arget directcory.
  * `tar -zxvf tarfile.tar.gz` Uncompress and unpack the archive in one step.
* `zip -r filename.zip <directory>` : Creates a compressed archive of the target directory.
  * `less zipfile.zip` to see the zip contents.
  * `unzip filename.zip` : Uncompressed and unpack the archive
  * `zip -e -r filename.zip <target>` : Got sensitive information? encrypt the archive with a password.

# Environments
If you can isolate your development environments away from your host system's configuration you'll be better off. Having to switch development environments from java8 to java11 or python 3.5 to python 3.6 and not mangling the configuration can be tricky.

## Java
* [Sdkman](https://sdkman.io/) - Manage java, gradle, maven, kotlin releases.

## Python
* `virtualenv` and `venv` for python2 and python3 isolation respectivly. The commands are different because python users hate other python users.


# Recipes
## Search for files and search for a string they contain
```bash
find . -name "*.java" | xargs grep "some_string"
```

## Fix file and directory permissions
* I've seen numerous times where someone as root modifies a directory or applies permissions that are out of whack. I usually run something like this:
```bash
# fix the ownership
sudo chown -R apache:users .

# find all the directories, fix the directory permission
find . -type d -exec chmod 775 {} \;

# find all the files, fix the file permissions 
find . -type f -exec chmod 664 {} \;

# find all the scripts, add the executable flag
find . -type f -name "*.sh" -exec chmod a+x {} \;
```

## Leave a process running after logout
* `nohup`

# Guides
* [Bash](./bash.md)
* [SSH](./ssh.md)