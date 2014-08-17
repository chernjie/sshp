sshp
====

An ssh helper tool, provides a few helpful commands to everyday ssh-related task.


To Setup
--------
* Add the following to your `~/.ssh/config`. This will use Shared SSH connections
```
Host *
	ForwardAgent yes
	ControlMaster auto
	ControlPath /tmp/%r@%h:%p
	ControlPersist 4h
```

* Add a list of common host to the prime list
```
$ echo git@github.com git@bitbucket.org host1 host2 host3 >> ~/.ssh/prime
```
* Add `sshp` to your `~/bin` directory


To Use
------
```
$ sshp
```
	sshp <HOST> [-d]
		Login to MACHINE and start a screen session
		-d for no screen
	sshp [info|grep] [pattern]
		search your ~/.ssh/config and accepts all options of grep
	sshp [list|-l]
		list all hosts
	sshp [start|status|stop] <HOST..>
		Check the SSH connection status of a HOST
	sshp proxy <HOST>
		HOST as proxy server

Advanced
--------
If you want to separate your configuration files to smaller chunks, you can do so by creating a `~/.ssh/config.d` directory and `sshp` will consolidate all files found in this directory into `~/.ssh/config`
Beware, this will overwrite your `~/.ssh/config` whenever there are changes in `~/.ssh/config.d`.

Reference
---------
For more information on how to configure your `~/.ssh/config`, see http://linux.die.net/man/5/ssh_config
