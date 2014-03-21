sshp
====

An ssh helper tool, provides a few helpful commands to everyday ssh-related task.


To Setup
--------
1. Add the following to your `~/.ssh/config`. This will use Shared SSH connections
```
Host *
	ForwardAgent yes
	ControlMaster auto
	ControlPath /tmp/%r@%h:%p
	ControlPersist 4h
```

2. Add a list of common host to the prime list
```
$ echo git@github.com git@bitbucket.org host1 host2 host3 >> ~/.ssh/prime
```
3. Add `sshp` to your `~/bin` directory


To Use
------
```
$ sshp
```

	Usage: ./sshp MACHINE [-d]
	Usage: ./sshp info [pattern]
	Usage: ./sshp [-l] #list
	Usage: ./sshp [-e]
	Usage: ./sshp [start|status|stop|proxy] <host..>

Advanced
--------
If you want to separate your configuration files to smaller chunks, you can do so by creating a `~/.ssh/config.d` directory and `sshp` will consolidate all files found in this directory into `~/.ssh/config`
Beware, this will overwrite your `~/.ssh/config` everytime `sshp` is executed.

Reference
---------
For more information on how to configure your `~/.ssh/config`, see http://linux.die.net/man/5/ssh_config
