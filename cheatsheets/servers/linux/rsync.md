---
layout: page
title: "rsync Cheatsheet"
description: "rsync Cheatsheet"
tagline: "A cheatsheet for the rsync command line tool in the Linux environment"

---
{% include JB/setup %}

<small>[Home](/) >> [Cheatsheets](/cheatsheets) >> [Linux/Unix](/cheatsheets/servers/linux) >> rsync</small>

### rsync <small>[(manpage)](http://manpages.ubuntu.com/manpages/precise/en/man1/rsync.1.html)</small>

#### Brief Description

Rsync is a fast and extraordinarily versatile file copying tool. It can copy locally, to/from another host over any remote shell, or to/from a remote rsync daemon. It offers a large number of options that control every aspect of its behavior and permit very flexible specification of the set of files to be copied. It is famous for its delta-transfer algorithm, which reduces the amount of data sent over the network by sending only the differences between the source files and the existing files in the destination. Rsync is widely used for backups and mirroring and as an improved copy command for everyday use.

#### Examples

##### Sync directory with remote server

{% highlight bash %}
# Sync current directory with remote server specific directory
rsync -zvr --delete . user@server:/directory/to/sync
{% endhighlight %}

