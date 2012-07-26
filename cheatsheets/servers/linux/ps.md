---
layout: page
title: "Linux Cheatsheet"
description: "Linux Cheatsheet"
tagline: "A cheatsheet for command line tools in the Linux environment"

---
{% include JB/setup %}

### ps <small>[(manpage)](http://manpages.ubuntu.com/manpages/precise/en/man1/ps.1posix.html)</small>

**ps** displays information about a selection of the active processes. If you want a repetitive update of the selection and the displayed information, use top(1) instead.

#### Examples

Each process has a unique number, the PID. A list of all running process is retrieved with ps.

{% highlight bash %}
$ ps -auxefw                # Extensive list of all running process`
{% endhighlight %}

However more typical usage is with a pipe or with pgrep: 

{% highlight bash %}
$ ps axww | grep cron
>> 586 ?? Is 0:01.48 /usr/sbin/cron -s

$ ps axjf                   # All processes in a tree format (Linux)
$ ps aux | grep 'ss[h]'     # Find all ssh pids without the grep pid
$ pgrep -l sshd             # Find the PIDs of processes by (part of) name
$ echo $$                   # The PID of your shell
$ fuser -va 22/tcp          # List processes using port 22 (Linux)
$ pmap PID                  # Memory map of process (hunt memory leaks) (Linux)
$ fuser -va /home           # List processes accessing the /home partition
$ strace df                 # Trace system calls and signals
$ truss df                  # same as above on FreeBSD/Solaris/Unixware
{% endhighlight %}

A good one is to find what is called a Zombie process:

{% highlight bash %}
$ ps -el | grep 'Z'`
{% endhighlight %}

The following example finds all the Zombie processes in a clean fashion with it's parent process id [ppid]:

{% highlight bash %}
$ ps -A -ostat,ppid,pid,cmd | grep -e '^[Zz]' 
{% endhighlight %}

To Kill the parents of the Zombies we can run the following script:

{% highlight bash %}
$ kill -HUP `ps -A -ostat,ppid,pid,cmd | grep -e '^[Zz]' | awk '{print $2}'` 
{% endhighlight %}