---
layout: post
title: "modify cwm librecovery __system() function to support busybox"
description: "modify cwm source code"
uri: /posts/2013/08
permalink: /posts/2013/08/index.html
tags: [cwm,clang]
tagline: "cwm source code modify"
exerpt: |-
---


## 解释说明：
    1.修改cwm librecovery system.c 源代码，让其直接支持调用busybox
    2.用到宏定义，可以根据不同的环境设置_BASH_SHELL_的居然位置
    3.提供一个测试用例test.c
##如何编译：
    在ics源代码或者是更高级的源代码目录里面创建一个目录：
{% highlight bash %}
      mkdir -p $ICS_SOURCE_TOP/external/librun_cmd
{% endhighlight %}
    再把下面提供的代码复制到创建的不同的文件中
再使用make test_run_cmd (需要在源代码目录的顶层使用)
    把生成的librun_cmd.so ,test_run_cmd push 到手机的不同目录目录下面。
    再用adb shell test_run_cmd进行测试。





##execv.c -> srcfile of librun_cmd.so  

{% highlight c %}

/* Copyright (c) 2013 The software  Author sndnvaps. 
* All rights reserved.
* Redistribution and use in source and binary forms, with or without
* modification, are permitted provided that the following conditions are met:
*
*     * Redistributions of source code must retain the above copyright
*       notice, this list of conditions and the following disclaimer.
*     * Redistributions in binary form must reproduce the above copyright
*       notice, this list of conditions and the following disclaimer in the
*       documentation and/or other materials provided with the distribution.
*     * Neither the name of  sndnvaps nor the
*       names of its contributors may be used to endorse or promote products
*       derived from this software without specific prior written permission.
*
* THIS SOFTWARE IS PROVIDED BY THE REGENTS AND CONTRIBUTORS "AS IS" AND ANY
* EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED
* WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
* DISCLAIMED. IN NO EVENT SHALL THE REGENTS AND CONTRIBUTORS BE LIABLE FOR ANY
* DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES
* (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES;
* LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND
* ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
* (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
* SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
*/

#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <unistd.h>
#include <sys/wait.h>
#include <string.h>
#include <signal.h>
#include <fcntl.h>
#include <paths.h>
#include "common.h"

#ifdef _ANDROID_SYSTEM_   //for android system
    #define _BASH_SHELL_ "/system/xbin/sh" 
#endif

#ifdef   _ANDROID_RECOVERY_                   //for recovery mode 
   #define _BASH_SHELL_ "/sbin/sh"
#endif

#ifdef _LINUX_X86                            //for linux-x86 
   #define _BASH_SHELL_ "/bin/sh"
#endif


char *env[] = {(char*) NULL};
int run_cmd(const char *command) {
	pid_t pid;
	sig_t intsave, quitsave;
	sigset_t mask, omask;
	int pstat;
#ifdef _HAVE_BUSYBOX_
	char tmp_busybox[256];
#endif 
	char **argv = malloc(sizeof(char*) * 4);
	
	if (!command) {
		return 1;
	}

	argv[0] = "sh";
	argv[1] = "-c";
#ifdef _HAVE_BUSYBOX_
	sprintf(tmp_busybox,"busybox %s",(char *)command);
	argv[2] = tmp_busybox;	
#else 
	argv[2] = (char *)command;
#endif 
	argv[3] = NULL;

	sigemptyset(&mask);
	sigaddset(&mask,SIGCHLD);
	sigprocmask(SIG_BLOCK,&mask,&omask);
	switch (pid = vfork()) {
		case -1: /* error */
			sigprocmask(SIG_SETMASK,&omask,NULL);
			return -1;
		case 0: /* child */
			sigprocmask(SIG_SETMASK,&omask,NULL);
			execve(_BASH_SHELL_,argv,env);

		_exit(127);
	}
	intsave = (sig_t) bsd_signal(SIGINT, SIG_IGN);
	quitsave = (sig_t) bsd_signal(SIGQUIT, SIG_IGN);
	pid = waitpid(pid, (int *)&pstat, 0);
	(void)bsd_signal(SIGINT,intsave);
	(void)bsd_signal(SIGQUIT,quitsave);
	return (pid == -1 ? -1 : pstat);
}

{% endhighlight %}



##common.h -> head file of execv.c 
{% highlight c %}

//head file for execv.c
int run_cmd(const char *command);

{% endhighlight %}

##test.c -> for test the librun_cmd.so 

{% highlight c %}

#include <stdio.h>
#include <stdlib.h>
#include "common.h"

int main() {
	const char *test = "df -h";
	run_cmd(test);
	return 0;
}

{% endhighlight %}


##Makefile -> Android.mk

{% highlight makefile %}

LOCAL_PATH:= $(call my-dir)
include $(CLEAR_VARS)
LOCAL_MODULE := librun_cmd
LOCAL_SRC_FILES := execv.c
LOCAL_MODULE_TAGS := optional
LOCAL_CFLAGS := -D_ANDROID_SYSTEM_ -D_HAVE_BUSYBOX_ 
LOCAL_SHARED_LIBRARIES := libc libstdc++ libm
include $(BUILD_SHARED_LIBRARY)

include $(CLEAR_VARS)
LOCAL_MODULE := test_run_cmd
LOCAL_SRC_FILES := test.c
LOCAL_MODULE_TAGS := optional
LOCAL_SHARED_LIBRARIES := librun_cmd 
include $(BUILD_EXECUTABLE)

{% endhighlight %}


