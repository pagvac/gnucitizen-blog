---
title: Landing Proxify
author: petko-d-petkov
date: Wed, 06 Feb 2013 23:28:40 GMT
template: this/views/post.jade
---

I am really happy to announce the first release of proxify. I started writing this tool several years ago but I was never able to finished it. The first release (version 1.0) is now available for [download](http://code.google.com/p/gnucitizen/downloads/list) on all platforms: Linux, Mac and Windows.

### What is Proxify

The idea behind Proxify is to create a proxy that is just good at doing proxying. It is the proxy of all proxies so-to-say. Proxify is lightweight, streamlined, concurrent and very efficient proxy utility that is easy to integrate into other tools. There is a good need for such tools because proxies are quite complex and not trivial to write even if you choose to use a high-level language such as Java, Python or Ruby.

This tool is written in C and comes with all dependencies pre-included in the package. This means that it is very portable on all platforms and you do not need any special setup. Having all files in the same folder is just enough to make it run.

Proxify is multithreaded and can in theory make optimal use of multi-cpu environments. The tool is non-buffering which means that it is really fast. It supports WebSockets, WebRTS and other streaming protocols. It fully understands HTTP. It does SSL interception and clones certificates on the fly.

### Integration At Its Core

As mentioned earlier, Proxify is great if you need to create a custom proxy application or you want to embed proxy functionalities into your own app. The tool will do all the hard work and you just need to provide a very simple restful HTTP service to do the forwarding of data between the browser and the remote target. The protocol is based on the HTTP proxy specifications with the only difference that you don't have to support the CONNECT method or do any SSL interception. Additionally, Proxify automatically detects end of streams when certain types of protocols are used. This makes the tool very handy, easy, re-usable technology that can be used in situations when we just want to write simple scripts to da a trivial job without to understand completely how the whole stack works. Everything is pretty much magically handled for you: and there is a lot going on behind the scene.

### Other Usages

Proxify can be used for many things. Here is an example of how you will launch the tool to hex dump all the trafic to the screen:

```bash
./proxify -p 8080 -x
```

The output of this command will look like this:

```bash
xxxxxx:xxxxx pdp$ xxx/proxify -p 8080 -x
Proxify Version 1.0

Copyright 2013 GNUCITIZEN. All rights reserved.
Commercial use of this software is strictly prohibited.
For commercial options please contact us at http://www.gnucitizen.org/.

[0000]   47 45 54 20 2F 20 48 54   54 50 2F 31 2E 31 0D 0A   GET...HT TP.1.1..
[0000]   55 73 65 72 2D 41 67 65   6E 74 3A 20 63 75 72 6C   User.Age nt..curl
[bfc8]   2F 37 2E 32 37 2E 30 0D   0A 48 6F 73 74 3A 20 77   .7.27.0. .Host..w
[f4c9]   77 77 2E 67 6E 75 63 69   74 69 7A 65 6E 2E 6F 72   ww.gnuci tizen.or
[cea4]   67 0D 0A 41 63 63 65 70   74 3A 20 2A 2F 2A 0D 0A   g..Accep t.......
[609f]   50 72 6F 78 79 2D 43 6F   6E 6E 65 63 74 69 6F 6E   Proxy.Co nnection
[f2e5]   3A 20 4B 65 65 70 2D 41   6C 69 76 65 0D 0A 0D 0A   ..Keep.A live....
```

If we want to dump all requests and responses into individual files than we can use the following command:

```bash
./proxify -p 8080 -D /path/to/folder
```

This will also capture everything that is streamed as well, which means that you can even record video, audio and whatever is streaming over HTTP. You can mix and match all options for bets result and please check the command flags for more information.

### Tool Readiness

Proxify is essentially ready for most use-cases although there are several things which needs to be improved especially around the SSL interception. Please use the tool with caution because it may have memory leaks or even memory corruption bugs. A huge portions of the code is not throughly tested. This is something I am working to improve in the near future. I am also planning to add more options for even better control over the process.

### Fair Use

The tool is free! You can use it right away. However, comercial use is strictly prohibited at this stage. If you want to use the tool for comercial purposes, please get in touch to discuss your options.
