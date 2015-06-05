sshp
====

An ssh helper tool, provides a few helpful commands to everyday ssh-related task.


#### To Setup

1. Add the following to your `~/.ssh/config`. This will use Shared SSH connections
    ```
Host *
	ForwardAgent yes
	ControlMaster auto
	ControlPath /tmp/%r@%h:%p
	ControlPersist 4h
	KeepAlive yes
```

2. Add a list of common host to the prime list
    ```bash
$ echo git@github.com git@bitbucket.org host1 host2 host3 >> ~/.ssh/prime
```

3. Add `sshp` to your `~/bin` directory


#### To Use

```bash
$ sshp
```
	sshp <HOST>
		Login to MACHINE and start a screen session

	sshp [info] [pattern]
	sshp [grep] [pattern]
	sshp [s|search] [pattern]
		search your ~/.ssh/config and accepts all options of grep

	sshp [list|-l]
		list all hosts

	sshp [start|status|stop] <HOST..>
		Check the SSH connection status of a HOST

	sshp proxy <HOST>
		HOST as proxy server

#### Advanced

If you want to separate your configuration files to smaller chunks, you can do so by creating a `~/.ssh/config.d` directory and `sshp` will consolidate all files found in this directory into `~/.ssh/config`
Beware, this will overwrite your `~/.ssh/config` whenever there are changes in `~/.ssh/config.d`.

### Host chaining

`sshp` supports host chaining, this take advantage of `ProxyCommand` and establish a connection for you. Your proxy machine will need to have `nc` installed for this to work.

```shell
$ sshp host1+host2
```

This will first attempt a connection to `host1`, then once a connection is established it will reuse that connection to login to `host2`

Configuration for both `host1` and `host2` can be configured in `~/.ssh/config`. Alternatively you can also set it directly.

```shell
$ sshp user1@host1+user2@host2
```

Chaining multiple host with `+` can work too.

Additionally, you can set the following in your `~/.ssh/config` so that you use `ssh` command directly.

```
Host *+*
	ProxyCommand sshp ProxyCommand %h %p
```

##### Example

```
$ ssh host1+host2
```


#### Reference

For more information on how to configure your `~/.ssh/config`, see http://linux.die.net/man/5/ssh_config
