---
layout: post
read_time: true
show_date: true
title:  How to configure Jekyll on Windows?
date:   2020-03-01 08:00:00 +0100
description: How to configure Jekyll on Windows?
img: posts/2020-03-01-Jekyll/Ridk.PNG
tags: [Jekyll]
author: SUN Jiangong
mathjax: yes
canonical_url: 'https://www.sunjiangong.com/how-to-configure-jekyll-on-windows.html'
redirect_from:
  - /2020/03/01/How_to_configure_Jekyll_on_Windows.html
---

Let's see how to configure Jekyll on Windows.

### 1. Install RubyInstaller on Windows

It's recommanded to install rubyinstaller-devkit-2.6.5-1-x64.exe for now.

Download [RubyInstaller](https://rubyinstaller.org/downloads)

<!--more-->

**Check Ruby version:**

```bash
C:\Users\PC>ruby -v
ruby 2.6.5p114 (2019-10-01 revision 67812) [x64-mingw32]
```

### 2. Install Ridk tool

Ridk is a helper tool to manage the runtime environment of RubyInstaller-2.4 and up.

With Ridk tool, you can install **MINGW** and **MSYS2**.

![](./../../../assets/img/posts/2020-03-01-Jekyll/Ridk.PNG)

**MINGW**: **MINimalist Gpu for Windows**, is a minimalist development environment for native Microsoft Windows applications. 

MinGW provides a complete Open Source programming tool set which is suitable for the development of native MS-Windows applications, and which do not depend on any 3rd-party C-Runtime DLLs. 


See more about: [MINGW](http://www.mingw.org/)

**MSYS**: **Minimal SYStem**, is a Bourne Shell command line interpreter system.

 **Offered as an alternative to Microsoft's cmd.exe**, this provides a general purpose command line environment, which is particularly suited to use with MinGW, for porting of many Open Source applications to the MS-Windows platform; a light-weight fork of Cygwin-1.3, it includes a small selection of Unix tools, chosen to facilitate that objective.

**MSYS2** is an independent rewrite of MSYS, based on modern Cygwin (POSIX compatibility layer) and MinGW-w64 with the aim of better interoperability with native Windows software.

See more about: [MSYS2](https://www.msys2.org/)


### 3. Install Jekyll bundler

Install Jekyll bundler with GEM. 

**GEM** is the package manager in Ruby language.
You can search all available packages on [RubyGEMS](https://rubygems.org/).


```
C:\Users\PC>gem install jekyll bundler
Temporarily enhancing PATH for MSYS/MINGW...
Building native extensions. This could take a while...
Successfully installed http_parser.rb-0.6.0
Successfully installed eventmachine-1.2.7-x64-mingw32
Successfully installed em-websocket-0.5.1
Successfully installed concurrent-ruby-1.1.6

HEADS UP! i18n 1.1 changed fallbacks to exclude default locale.
But that may break your application.

If you are upgrading your Rails application from an older version of Rails:

Please check your Rails app for 'config.i18n.fallbacks = true'.
If you're using I18n (>= 1.1.0) and Rails (< 5.2.2), this should be
'config.i18n.fallbacks = [I18n.default_locale]'.
If not, fallbacks will be broken in your app by I18n 1.1.x.

If you are starting a NEW Rails application, you can ignore this notice.

For more info see:
https://github.com/svenfuchs/i18n/releases/tag/v1.1.0

Successfully installed i18n-1.8.2
Successfully installed ffi-1.12.2-x64-mingw32
Successfully installed sassc-2.2.1-x64-mingw32
Successfully installed jekyll-sass-converter-2.1.0
Successfully installed rb-fsevent-0.10.3
Successfully installed rb-inotify-0.10.1
Successfully installed listen-3.2.1
Successfully installed jekyll-watch-2.2.1
Successfully installed kramdown-2.1.0
Successfully installed kramdown-parser-gfm-1.1.0
Successfully installed liquid-4.0.3
Successfully installed mercenary-0.3.6
Successfully installed forwardable-extended-2.6.0
Successfully installed pathutil-0.16.2
Successfully installed rouge-3.16.0
Successfully installed safe_yaml-1.0.5
Successfully installed unicode-display_width-1.6.1
Successfully installed terminal-table-1.8.0
Successfully installed jekyll-4.0.0
Parsing documentation for http_parser.rb-0.6.0
unknown encoding name "chunked\r\n\r\n25" for ext/ruby_http_parser/vendor/http-parser-java/tools/parse_tests.rb, skipping
Installing ri documentation for http_parser.rb-0.6.0
Parsing documentation for eventmachine-1.2.7-x64-mingw32
Installing ri documentation for eventmachine-1.2.7-x64-mingw32
Parsing documentation for em-websocket-0.5.1
Installing ri documentation for em-websocket-0.5.1
Parsing documentation for concurrent-ruby-1.1.6
Installing ri documentation for concurrent-ruby-1.1.6
Parsing documentation for i18n-1.8.2
Installing ri documentation for i18n-1.8.2
Parsing documentation for ffi-1.12.2-x64-mingw32
Installing ri documentation for ffi-1.12.2-x64-mingw32
Parsing documentation for sassc-2.2.1-x64-mingw32
Installing ri documentation for sassc-2.2.1-x64-mingw32
Parsing documentation for jekyll-sass-converter-2.1.0
Installing ri documentation for jekyll-sass-converter-2.1.0
Parsing documentation for rb-fsevent-0.10.3
Installing ri documentation for rb-fsevent-0.10.3
Parsing documentation for rb-inotify-0.10.1
Installing ri documentation for rb-inotify-0.10.1
Parsing documentation for listen-3.2.1
Installing ri documentation for listen-3.2.1
Parsing documentation for jekyll-watch-2.2.1
Installing ri documentation for jekyll-watch-2.2.1
Parsing documentation for kramdown-2.1.0
Installing ri documentation for kramdown-2.1.0
Parsing documentation for kramdown-parser-gfm-1.1.0
Installing ri documentation for kramdown-parser-gfm-1.1.0
Parsing documentation for liquid-4.0.3
Installing ri documentation for liquid-4.0.3
Parsing documentation for mercenary-0.3.6
Installing ri documentation for mercenary-0.3.6
Parsing documentation for forwardable-extended-2.6.0
Installing ri documentation for forwardable-extended-2.6.0
Parsing documentation for pathutil-0.16.2
Installing ri documentation for pathutil-0.16.2
Parsing documentation for rouge-3.16.0
Installing ri documentation for rouge-3.16.0
Parsing documentation for safe_yaml-1.0.5
Installing ri documentation for safe_yaml-1.0.5
Parsing documentation for unicode-display_width-1.6.1
Installing ri documentation for unicode-display_width-1.6.1
Parsing documentation for terminal-table-1.8.0
Installing ri documentation for terminal-table-1.8.0
Parsing documentation for jekyll-4.0.0
Installing ri documentation for jekyll-4.0.0
Done installing documentation for http_parser.rb, eventmachine, em-websocket, concurrent-ruby, i18n, ffi, sassc, jekyll-sass-converter, rb-fsevent, rb-inotify, listen, jekyll-watch, kramdown, kramdown-parser-gfm, liquid, mercenary, forwardable-extended, pathutil, rouge, safe_yaml, unicode-display_width, terminal-table, jekyll after 35 seconds
Successfully installed bundler-2.1.4
Parsing documentation for bundler-2.1.4
Done installing documentation for bundler after 3 seconds
24 gems installed
```

**Check installed Jekyll version:**

```bash
C:\Users\PC>jekyll -v
jekyll 4.0.0
```

**Check all local packages:**

```
C:\Users\PC>gem list

*** LOCAL GEMS ***

addressable (2.7.0)
bigdecimal (default: 1.4.1)
bundler (2.1.4, default: 1.17.2)
cmath (default: 1.0.0)
colorator (1.1.0)
concurrent-ruby (1.1.6)
csv (default: 3.0.9)
date (default: 2.0.0)
dbm (default: 1.0.0)
did_you_mean (1.3.0)
e2mmap (default: 0.1.0)
em-websocket (0.5.1)
etc (default: 1.0.1)
eventmachine (1.2.7 x64-mingw32)
faraday (1.0.0)
fcntl (default: 1.0.0)
ffi (1.12.2 x64-mingw32)
fiddle (default: 1.0.0)
fileutils (default: 1.1.0)
forwardable (default: 1.2.0)
forwardable-extended (2.6.0)
gdbm (default: 2.0.0)
gist (5.1.0)
http_parser.rb (0.6.0)
i18n (1.8.2)
io-console (default: 0.4.7)
ipaddr (default: 1.2.2)
irb (default: 1.0.0)
jekyll (4.0.0)
jekyll-feed (0.13.0)
jekyll-gist (1.5.0)
jekyll-paginate (1.1.0)
jekyll-sass-converter (2.1.0)
jekyll-sitemap (1.4.0)
jekyll-watch (2.2.1)
json (default: 2.1.0)
kramdown (2.1.0)
kramdown-parser-gfm (1.1.0)
liquid (4.0.3)
listen (3.2.1)
logger (default: 1.3.0)
matrix (default: 0.1.0)
mercenary (0.3.6)
minitest (5.11.3)
multipart-post (2.1.1)
mutex_m (default: 0.1.0)
net-telnet (0.2.0)
octokit (4.16.0)
openssl (default: 2.1.2)
ostruct (default: 0.1.0)
pathutil (0.16.2)
power_assert (1.1.3)
prime (default: 0.1.0)
psych (default: 3.1.0)
public_suffix (4.0.3)
rake (12.3.2)
rb-fsevent (0.10.3)
rb-inotify (0.10.1)
rdoc (default: 6.1.2)
rexml (default: 3.1.9)
rouge (3.16.0)
rss (default: 0.2.7)
safe_yaml (1.0.5)
sassc (2.2.1 x64-mingw32)
sawyer (0.8.2)
scanf (default: 1.0.0)
sdbm (default: 1.0.0)
shell (default: 0.7)
stringio (default: 0.0.2)
strscan (default: 1.0.0)
sync (default: 0.5.0)
terminal-table (1.8.0)
test-unit (3.2.9)
thwait (default: 0.1.0)
tracer (default: 0.1.0)
unicode-display_width (1.6.1)
wdm (0.1.1)
webrick (default: 1.4.2)
xmlrpc (0.3.0)
zlib (default: 1.0.0)
```


Start Github pages:

```
D:\site>jekyll serve
Configuration file: D:/site/_config.yml
            Source: D:/site
       Destination: D:/site/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
       Jekyll Feed: Generating feed for posts
                    done in 1.872 seconds.
 Auto-regeneration: enabled for 'D:/site'
    Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.
```
