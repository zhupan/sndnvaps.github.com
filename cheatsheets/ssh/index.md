---
layout: page
title: "SSH Cheatsheet"
description: "SSH Cheat Sheet"
tagline: "A cheat Sheet reference guide for SSH"

---
{% include JB/setup %}

## SSH

All man pages are linked to the Ubuntu manage resources located at http://manpages.ubuntu.com

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

