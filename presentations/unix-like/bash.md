# [Bash](https://en.wikipedia.org/wiki/Bash_(Unix_shell))
Bash is a terminal shell is that is very popular in linux environments. It allows you to configure your bash environment.

## Common locations
Everyone's layout will be a little different as your bash configuration is usually customized to meet your personal workflow
* `~/.bashrc` : Provided as a default implementation by most distributions.
* `~/.bash_aliases` : Your custom aliases for when you're sick of typing `ls -la` you can `alias ll='ls -la'` and now on the command line you run `ll` to get a long listing of your files in your terminal.
* `~/.bash_completion` : Custom completions for your bash environment.
* `~/.bash_history` : The log of commands that have been run
* `~/.bash_profile` : Customizations for your bash environment./c
* `~/.bash_logout` : Commands to run on exit.
* `/etc/bash.bashrc` : system wide bash envrionment configuration
* `/etc/bash_completion.d` : system wide bash completion scripts

## [Bash Completion](https://github.com/scop/bash-completion/blob/master/README.md)
You can save yourself a lot of typing and trying to remember commands and arguments if you install bash completion scripts. They exist for many commerical products and you should definitely use them. If your system administrator will not add them to your work machine you can add them locally. From the FAQ

    Q. Where should I install my own local completions?

    A. Put them in the completions subdir of $BASH_COMPLETION_USER_DIR (defaults to $XDG_DATA_HOME/bash-completion or ~/.local/share/bash-completion if $XDG_DATA_HOME is not set) to have them loaded automatically on demand when the respective command is being completed. See also the next question's answer for considerations for these files' names, they apply here as well. Alternatively, you can write them directly in ~/.bash_completion which is loaded eagerly by our main script.

### Bash Completion as separate scripts
I personally don't like a single file for completions. If you want to locally control completion scripts do the following.
* `mkdir ~/.bash_completion.d/`
* Update the contents of ~/.bash_completion with
```bash
#!/bin/bash 
for bcfile in ~/.bash_completion.d/* ; do
    . $bcfile
done
```
* Copy in any commerical or custom completion scripts into `~/.bash_completion.d`

## Bash Scripting
* [~/bin](https://unix.stackexchange.com/a/36874) is your local home for your custom scripts.
* [ShellCheck is your best friend](https://github.com/koalaman/shellcheck), install it and then add the vscode plugin.
* `pushd / popd` : to move in and out of directories and return where you started