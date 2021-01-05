# Secure Connections

# Commands
* `openssl s_client -showcerts -connect <remote_host>:443 < /dev/null` - get certificate information for the remote host.
  * Example `openssl s_client -showcerts -connect cnn.com:443 < /dev/null`
* `sudo traceroute -T -p <Port> <IP>` - See all the hops between your localhost to a remote port. If you see `* * *` until the end, you're not reaching your destination.
  * `sudo traceroute -T -p 443 cnn.com`
* `update-ca-certificates` - Updates the certifcate authorities in the system. This will make them available by default to tools like `curl`.

# Certificates
## Certificate conversion p12/pfx to PEM
* p12 and pfx have converged. They are the same file format.

To use many command line tools, you need to convert your p12/pfx certificates into PEM format. [Common Conversions](https://www.sslshopper.com/article-most-common-openssl-commands.html)

> NOTE: `-nodes` is not 'nodes' is is 'NO DES' which means your keys will not be encrypted with a password. I highly recommend against using this option unless you have no other choice, for instance, you are configuring a service that cannot prompt for a password.
* `openssl pkcs12 -in personal.p12 -out personal.key -nocerts`
* `openssl pkcs12 -in personal.p12 -out personal.crt -nokeys`

# curl
`curl` is the tool in most frequent use to make https requests via the CLI to remote resources. It is very powerful. 
* If you frequently make connections with the same certificates or headers, consider creating a `~/.curlrc` to hold your default information or use `--config <file>` to specifiy another configuration.
```
--cacert ~/certs/self-signed-ca.crt
--cert ~/.ssh/personal.crt
--certtype PEM
--key=~/.ssh/personal.key
--key-type PEM
```
> If you find yourself using `-k` or `--insecure` to make connections, you should be mindful that either your environment or the remote environment is misconfigured for SSL. You should take the time to figure out what is wrong and fix it. It is usually as easy and adding the Certificate Authority that signed the remote host's certificate and calling `update-ca-certificates` see `man update-ca-certificates`.
