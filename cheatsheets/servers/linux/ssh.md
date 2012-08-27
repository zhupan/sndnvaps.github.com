---
layout: page
title: "ssh Cheatsheet"
description: "ssh Cheatsheet"
tagline: "A cheatsheet for the ssh command line tool in the Linux environment"

---
{% include JB/setup %}

<small>[Home](/) >> [Cheatsheets](/cheatsheets) >> [Linux/Unix](/cheatsheets/servers/linux) >> ssh</small>

### ssh <small>[(manpage)](http://manpages.ubuntu.com/manpages/precise/en/man1/ssh.1.html)</small>

{% highlight bash %}
# Typical connection to remote server
ssh ubuntu@<REMOTE_SERVER_ADDRESS>

# Using a specific identity key
ssh -i ~/.ssh/rsa_id ubuntu@<REMOTE_SERVER_ADDRESS>

{% endhighlight %}

### ssh-keygen

### ssh-agent

### ssh-add

### ssh-copy-id