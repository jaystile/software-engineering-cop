# [SSH](https://www.ssh.com/ssh/)
* `ssh` :  is the secure way to connect to other hosts. 
* `ssh-keygen` : [Generating key pairs.](https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

## Common locations
* ~/.ssh : contains all of your security information. This folder needs to be locked down with permissions `700` (a.k.a. user access only)
* ~/.ssh/authorized_keys : The list of public keys that you accept to connect to this account.
* ~/.ssh/config : Saved connection configurations so you don't have to look up in your `history` or notes on how to connect to a remote host.
* ~/.ssh/id_rsa : A private key file. Make your keys read only to prevent accidental modification
* ~/.ssh/id_rsa.pub : A public key file
* ~/.ssh/known_hosts : Hosts that you have trusted.


## Add your SSH keys to your session
* [Read all about it!](https://www.ssh.com/ssh/agent)
> For the love of god, stop storing your keys unencrypted.
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

## SSH Key Exchange (a.k.a. passwordless login)
Append the contents of your public key `id_rsa.pub` to your remote host's `~/.ssh/authorized_keys` file. If you've added your private key to your ssh-agent you'll connect without any further prompts for authentication.

## SSH Port-Fowarding
Port-Fowarding is often used to make a remote application appear locally. Consider the scenario: You have a graphical database application like PgAdmin, but your database exists on a remote server which does not allow external connections. You solve this by forwarding a local port connection to the remote host's port. [Read all about it!](https://www.postgresql.org/docs/current/ssh-tunnels.html). After the port-foward is established you can configure PgAdmin to connect to `localhost:63333` and work on the remote system.

## SSH Port-Fowarding with a Bastion
Nothing has given me greater stress than setting up port forwarding through a [Bastion host](https://en.wikipedia.org/wiki/Bastion_host). I don't use it frequently enough to remember and it is finicky enough that it either works prefectly or not at all. [Read all about it!](https://www.redhat.com/sysadmin/ssh-proxy-bastion-proxyjump) I've found that I've had to use ProxyCommand over ProxyJump in the workplace.
