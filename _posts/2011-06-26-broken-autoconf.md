---
layout: post
title: autoconf issues
---

# Autoconf Issue #
{% highlight console %}

ashee:foonly amitava$ aclocal 
/usr/bin/gm4: INTERNAL ERROR: recursive push_string!
autom4te: /usr/bin/gm4 failed with exit status: 1
aclocal: /usr/bin/autom4te failed with exit status: 1

{% endhighlight %}

## Broken M4
M4 that ships with Leopard (1.4.6) is broken. See

* <http://hints.macworld.com/article.php?story=20080101160622573&utm_source=feedburner&utm_medium=feed&utm_campaign=Feed%253A+macosxhints%252Frecent+%2528Mac+OS+X+Hints%2529>
* <http://www.ultimate-apple.com/2008/01/08/105-fix-a-broken-gnu-m4-in-105/>

## Homebrew install M4
I use homebrew for most source installs as opposed to macports or fink.
{% highlight console %}

ashee:local amitava$ sudo brew create http://ftp.wayne.edu/pub/gnu/m4/m4-1.4.16.tar.gz
Password:
Version detected as 1.4.16.
==> Downloading http://ftp.wayne.edu/pub/gnu/m4/m4-1.4.16.tar.gz
######################################################################## 100.0%
Please \`brew audit m4\` before submitting, thanks.

ashee:local amitava$ sudo brew install m4 
==> Downloading http://ftp.wayne.edu/pub/gnu/m4/m4-1.4.16.tar.gz
File already downloaded in /Library/Caches/Homebrew
==> ./configure --disable-debug --disable-dependency-tracking --prefix=/usr/local/Cellar/m4/1.4.
==> make install
/usr/local/Cellar/m4/1.4.16: 10 files, 860K, built in 39 seconds

ashee:local amitava$ ls /usr/local/Cellar/m4
1.4.16
	

{% endhighlight %}

## Replace original m4 ##
{% highlight console %}
ashee:local amitava$ gm4 --version
GNU M4 1.4.6
Copyright (C) 2006 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

Written by Rene' Seindal.

ashee:local amitava$ which gm4 
/usr/bin/gm4

ashee:local amitava$ file /usr/bin/gm4
/usr/bin/gm4: Mach-O universal binary with 2 architectures
/usr/bin/gm4 (for architecture x86_64):	Mach-O 64-bit executable x86_64
/usr/bin/gm4 (for architecture i386):	Mach-O executable i386

ashee:local amitava$ sudo mv /usr/bin/gm4 /usr/bin/gm4.orig
ashee:local amitava$ sudo mv /usr/bin/m4 /usr/bin/m4.orig 

ashee:local amitava$ sudo ln -s /usr/local/Cellar/m4/1.4.16/bin/m4 /usr/bin/m4
ashee:local amitava$ sudo ln -s /usr/local/Cellar/m4/1.4.16/bin/m4 /usr/bin/gm4
{% endhighlight %}
