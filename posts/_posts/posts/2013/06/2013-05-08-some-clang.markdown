---
layout: post
title: "struct stat st; st.st_mode"
description: "unsigned int mode_t"
uri: /posts/2013/06
permalink: /posts/2013/06/index.html
tags: [clang]
tagline: "unsigned int mode_t"
exerpt: |-
---



{% highlight c %}

#include <stdio.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <stdlib.h>

static const mode_t who_mask[] = {
        S_ISUID | S_ISGID | S_ISVTX | S_IRWXU | S_IRWXG | S_IRWXO, /* a  -> 07777  */ 
        S_ISUID | S_IRWXU,           /* u -> 04700 */ 
        S_ISGID | S_IRWXG,           /* g  -> 02070 */ 
        S_IRWXO                      /* o  -> 0007 */ 
    };
    static const mode_t perm_mask[] = {
        S_IRUSR | S_IRGRP | S_IROTH, /* r  ->  0444 */
        S_IWUSR | S_IWGRP | S_IWOTH, /* w -> 0222 */
        S_IXUSR | S_IXGRP | S_IXOTH, /* x  -> 0111 */
        S_IXUSR | S_IXGRP | S_IXOTH, /* X -- special -- see below  -> 0111 */ 
        S_ISUID | S_ISGID,           /* s  -> 06000 */ 
        S_ISVTX                      /* t  -> 01000 */ 
    };


{% endhighlight %}




