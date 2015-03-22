---
layout: post
title: find the real website ip  with  CloudFlare service
tags:
- 技术,
- 原创,
- python3
---

#代码如下：

{% highlight python linenos %}  

#!/usr/bin/env python3
# -*- coding : utf-8 -*-
# author : pythoner
# filename : findip
# date : 2014-08-28
# find the real website ip  with  CloudFlare service
# demo: findip.py xxx.com  

import sys
import urllib.request
import urllib.parse
import re

if len(sys.argv)< 2:
    print("Error!!!,look help 'findip.py --help' ")
    
elif sys.argv[1].startswith("-"):
    options = sys.argv[1][2:] 
    
    if options == "version":
        print("Version 0.1")
        
    elif options == "help":
        print('''This is find ip with python3\t
demo: findip.py xxx.com\t
version: findip.py --version\t
help: findip.py --help''')

    else:
        print("Unknown option.")
    sys.exit()
    
else:
    domina = sys.argv[1]
    url = r"http://www.crimeflare.com/cgi-bin/cfsearch.cgi"
    header = {"Host": "www.crimeflare.com",
              "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8",
              "Origin": "http://www.crimeflare.com",
              "User-Agent": "Mozilla/5.0 (Windows NT 6.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/38.0.2125.8 Safari/537.36",
              "Content-Type": "application/x-www-form-urlencoded",
              "Referer": "http://www.crimeflare.com/cfs.html",
              "Accept-Encoding": "gzip,deflate",
              "Accept-Language": "zh-CN,zh;q=0.8"
              }    
    postdate = {'cfS': domina}
    post = urllib.parse.urlencode(postdate).encode("utf-8")
    res = urllib.request.urlopen(url, post)
    data = res.read().decode("utf-8")
    redata = (re.findall(r'<LI>.\S*.\S*.\S*.\S*', data))
    
    if len(redata) == 0:
        print("not find real ip")
        
    else:
        print(redata)
        

{% endhighlight %}  


[Url](http://www.crimeflare.com/cfs.html)

