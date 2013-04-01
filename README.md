sshp
====

An ssh helper tool, provides a few helpful commands to everyday ssh-related task.


To setup
========
1. Add the following to use Shared SSH connections
```
Host *
	ForwardAgent yes
	ControlMaster auto
	ControlPath /tmp/%r@%h:%p
```

2. Add a list of common host to the prime list
```
$ echo git@github.com git@bitbucket.org host1 host2 host3 >> ~/.ssh/prime
```

To use
======
```
$ sshp
```

	Usage: ./sshp MACHINE [-d]
	Usage: ./sshp info [pattern]
	Usage: ./sshp [-l] #list
	Usage: ./sshp [-e]
	Usage: ./sshp [start|status|stop] <host..>
