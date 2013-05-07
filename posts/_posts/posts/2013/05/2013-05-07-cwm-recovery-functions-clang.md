---
layout: post
title: "给 cwm recovery 添加破解权限的功能"
description: "break the root "
uri: /posts/2013/05
permalink: /posts/2013/05/index.html
tags: [clang,cwm]
tagline: "破解权限"
exerpt: |- 
---

## 1 创建源代码文件 root_device.cpp

{% highlight bash %}
sndnvaps@root# touch root_device.cpp
{% endhighlight %}

## 2. 往文件里面这写入如下的内容

{% highlight c++ %}
/*

    This software is to get the Android system root user perm.
    Copyright (C) <2013>  <sndnvaps@gmail.com>

    This program is free software: you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation, either version 3 of the License, or
    (at your option) any later version.

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.

    You should have received a copy of the GNU General Public License
    along with this program.  If not, see <http://www.gnu.org/licenses/>.

    
*/
#include <fstream>
#include <iostream>
#include <string>
#include <sys/stat.h>
#include <unistd.h>
#include <sys/types.h>
#include <stdlib.h>
#include <stdio.h>

using namespace std;

#define su_file "/system/xbin/su"
#define superuser_file "/system/app/superuser.apk"

class ROOT {
    static int copy_file(string src, string dst, int mode);
    static bool install_file();
    static bool path_exists(string path);
    static bool fix_su_perm();
};

int ROOT::copy_file(string src, string dst, int mode) {
     printf("Copying file %s to %s\n",src.c_str(),dst.c_str());
     ifstream srcfile(src.c_str(), ios::binary);
     ofstream dstfile(dst.c_str(), ios::binary);
     dstfile << srcfile.rdbuf();
     srcfile.close();
     dstfile.close();
     if (chmod(dst.c_str(), mode) != 0)
              return -1;
      return 0;
}

bool ROOT::install_file() {
        if(copy_file("/sbin/su", su_file, 0755)!= 0) {
          printf("failed to copy su binary to /system/xbin\n");
         return false;
        }
        if(copy_file("/sbin/superuser.apk", superuser_file, 0644) != 0) {
            printf("failed to copy superuser app to /system/app\n");
             return false;
            }
        if(!fix_su_perm())
             return false;
        return true;
}

bool ROOT::path_exists(string path) {
       struct stat st;
       if(path.c_str(),&st) == 0) {
          return true;
         }
    return false;
}


bool ROOT::fix_su_perm() {
     if (ROOT::path_exists(su_file)) {
            if(chown(su_file, 0, 0) != 0) {
                printf("Failed to chown %s\n",su_file);
                return false;
              }
            if(chmod(06755,su_file) != 0) {
                printf("Failed to chmod %s\n",su_file);
                return false;
              }
          }
       if(ROOT::path_exists(superuser_file)) {
          if(chown(superuser_file, 0, 0) != 0) {
            printf("Failed to chown %s\n",superuesr_file);
            return false;
            }
           if(chmod(06755,superuser_file) != 0) {
             printf("Failed to chmod %s\n", superuser_file);
             return false;
             }
           }
      return true;
}


int main(int argc, char *argv[]) {
  if (argc < 2 ) {
       printf("input an argumenut...\n");
       printf("%s root \n",argv[0]);
       }
     else {
    if(!strcmp(argv[1],"root")) {
          ROOT::install_file();
           }
      }
    return 0;
}


{% endhighlight %}


##如何调用编译出来的程序

编译出来的程序是静态和动态两种情况，如果想要减少体积，可以考虑动态编译

 下面是我写的makefile

{% highlight makefile %}
       
include $(CLEAR_VARS)
LOCAL_FORCE_STATIC_EXECUTABLE := true
LOCAL_MODULE := root_device
LOCAL_MODULE_PATH := $(TARGET_OUT_OPTIONAL_EXECUTABLES)
LOCAL_MODULE_TAGS := eng
LOCAL_SRC_FILES := root_device.cpp
LOCAL_STATIC_LIBRARIES := libc libstdc++
include $(BUILD_EXECUTABLE)

{% endhighlight %}





    




