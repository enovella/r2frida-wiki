# r2frida-wiki
This repo aims at providing examples on how to use r2frida.

Before reading this, it is highly recommended you take a look at the official website of `r2frida` to understand the capabilities of this tool: https://github.com/nowsecure/r2frida/blob/master/README.md

Commands
=========
- \il
- \iE (lib): List exports of library(ies)
```sh
[0xd0d77878]> \iE* frida-agent-32.so
f sym.fun.frida_agent_main = 0xd671a2cd
f sym.var.FRIDA_AGENT_1.0 = 0x0
```

- \ii (lib): List imports of library(ies)
```sh
[0xd0d77878]> \ii frida-agent-32.so~open
0xeeb94eb9 f opendir /system/lib/libc.so
0xeebc9eb5 f freopen /system/lib/libc.so
0xeebc9ce9 f fopen /system/lib/libc.so
0xeebc9e09 f fdopen /system/lib/libc.so
0xeeb97b15 f open /system/lib/libc.so
0xeeb94e31 f fdopendir /system/lib/libc.so
0xeeb97ba1 f openat /system/lib/libc.so
0xef39ac81 f dlopen /system/bin/linker
```
- \db
- \dt

Android
=======

Attaching
---------

Spawning
--------

iOS
===

**TODO**
