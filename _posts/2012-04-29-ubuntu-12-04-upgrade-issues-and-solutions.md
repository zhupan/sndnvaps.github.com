---
layout: post
title: "Resolving Ubuntu 12.04 Upgrade Issues"
description: "Documenting issues resolved with a Ubuntu 12.04 upgrade"
tagline: "Documenting issues resolved with a Ubuntu 12.04 upgrade"
tags: [ubuntu, linux]
exerpt: |-

---
{% include JB/setup %}

### System Description

Dell Vostro 1400... need I say more. :(

### Broadcom STA Wireless drivers not working

After upgrading my laptop from Ubuntu 11.10 to 12.04 I had issues with the Broadcom STA Wireless drivers not installing and/or working correctly. I found this post which resolved the issue: [Broadcom STA Wireless drivers not working on Acer aspire 5750G, Ubuntu 12.04](http://ubuntuforums.org/showpost.php?p=11882998&postcount=4)

And in case the link no longer works here is what I did:

{% highlight bash %}
$ sudo apt-get install --reinstall bcmwl-kernel-source
$ sudo modprobe ml
{% endhighlight %}
