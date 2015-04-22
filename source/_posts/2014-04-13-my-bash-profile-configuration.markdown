---
layout: post
title: "my bash profile configuration"
date: 2014-04-13 10:14:26 +0800
comments: true
categories: OSX
---

```
#terminal
export PS1="\u@\h:\w $"
export CLICOLOR=1
export GREP_OPTIONS="--color=auto"

#byobu check ignore
set FORCE_UNSAFE_CONFIGURE=1

#ant path
#ANT_ROOT=/Users/pb/Downloads/adt-bundle-mac-x86_64-20130917/sdk/tools/ant

# gcc 4.8
export PATH=$HOME/Library/gcc-4.8.0/bin:$PATH

export BOOST_ROOT=/usr/local/Cellar/lib
export BOOST_INCLUDEDIR=/usr/local/Cellar/include

##
# Your previous /Users/pb/.bash_profile file was backed up as /Users/pb/.bash_profile.macports-saved_2013-10-12_at_14:01:02
##

# MacPorts Installer addition on 2013-10-12_at_14:01:02: adding an appropriate PATH variable for use with MacPorts.
export PATH=/opt/local/bin:/opt/local/sbin:$PATH
# Finished adapting your PATH environment variable for use with MacPorts.

export CPATH=/opt/local/include
export LIBRARY_PATH=/opt/local/lib
export DYLD_FALLBACK_LIBRARY_PATH=$DYLD_FALLBACK_LIBRARY_PATH:/opt/local/lib
export PATH=/opt/local/bin:$PATH
# To ensure that MacPorts pkg-config can find stuff that rosdep installs in /usr
export PKG_CONFIG_PATH=/usr/lib/pkgconfig

#color
export CLICOLOR=1
export LSCOLORS=ExFxCxDxBxegedabagacad

#wxpython
export VERSIONER_PYTHON_PREFER_32_BIT

#sudo error
unset LD_LIBRARY_PATH
unset DYLD_LIBRARY_PATH

#tornade
export PYTHONPATH=$PYTHONPATH:~/Document/python/software/tornado-3.1.1

#android sdk
export PATH=$PATH:~/Downloads/adt-bundle-mac-x86_64-20130917/sdk/platform-tools

#android ndk
export ANDROID_NDK_ROOT=~/Documents/android/NDK/android-ndk-r9d
export NDK_ROOT=~/Documents/android/NDK/android-ndk-r9d
export ANDROID_SDK_ROOT=~/Downloads/adt-bundle-mac-x86_64-20130917/sdk

#cocos2dx
#export COCOS2DX_ROOT=~/Documents/CocosBuilder-2.1-examples/cocos2d-x-2.2.2

#mysql path
export PATH=$PATH:/usr/local/mysql/bin

#Tomcat
#export PATH=$PATH:/usr/local/apache-tomcat-7.0.52/bin

#colt linear algebra lib
export CLASSPATH=/opt/share/colt/lib/colt.jar:/opt/share/colt/lib/concurrent.jar:$CLASSPATH

#mlpack machinelearning library

export ANT_ROOT=/usr/local/ant


[[ -s "$HOME/.rvm/scripts/rvm" ]] && source "$HOME/.rvm/scripts/rvm" # Load RVM into a shell session *as a function*

export COCOS_CONSOLE_ROOT=/Users/pb/Documents/CocosBuilder-2.1-examples/cocos2d-x-3.0rc0/tools/cocos2d-console/bin
export PATH=$COCOS_CONSOLE_ROOT:$PATH
```
<!--more-->
