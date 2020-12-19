
# Basics
* [Cheatsheets are great!](https://cheatography.com/davechild/cheat-sheets/linux-command-line/) Seriously, bookmark a couple of them.

## Commands

* `history | grep some_command` : _What was that command I ran yesterday?_
  * `!<history_id>` : rerun a command from the history.
* `man <command>` : read the manual
* `less some_file` : less is more. Use `/search_term` and n to skip to the part you're looking for.
* `ls -ltrc` : sort files by time in reverse. I find I'm always looking for a recently modified file.
* `pkill -U <userid>` : kill all processes for a user (force a logout)
* `ps -ef | grep process_name` : find a process id (so you can then kill it)
* `redirect_some_command 2>&1` : redirect some_commands's stderr to same place as stdout
* `tail -f` : follow that log file
* `top` : find the hot running processes

# Environments
If you can isolate your development environments away from your host system's configuration the better off you'll be. Having to switch development from java8 to java11 or python 3.5 to python 3.6 and not mangling the configuration can be tricky.
* `virtualenv` and `venv` for python2 and python3 isolation respectivly. The commands are different because python users hate other python users.
* [Sdkman](https://sdkman.io/) - Manage java, gradle, maven, kotlin releases.

# Find Recipes
## Search in file for contents
```bash
find . -name "*.java" | xarsg grep "str"
```

## Fix file and directory permissions
* I've seen numerous times where someone as root modifies a directory or applies permissions that are out of whack. I usually run something like this:
```bash
# fix the ownership
sudo chown -R apache:users .

# find all the directories, fix the directory permission
find . -type d -exec chmod 775 {} \;

# find al the files, fix the file permissions 
find . -type f -exec chmod 664 {} \;

# find all the scripts, add the executable flag
find . -type f -name "*.sh" -exec chmod a+x {} \;
```

# Scripts Recipes
* [~/bin](https://unix.stackexchange.com/a/36874) is your local home for your custom scripts.
)
* [ShellCheck is your best friend](https://github.com/koalaman/shellcheck), install it and then add the vscode plugin.
* `pushd / popd` : to move in and out of directories and return where you started

# SSH Receipes
## Add your keys to your session
* [Read all about it!](https://www.ssh.com/ssh/agent)
> For the love of god, stop storing your certs unencrypted.
```bash
# Starts the ssh-agent
eval `ssh-agent`

# Adds a key the agent
ssh-add
```
* [Update your logout](https://kb.iu.edu/d/aeww)
```bash
vi ~/.bash_logout
...
 kill $SSH_AGENT_PID
...
```

