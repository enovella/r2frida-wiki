# r2frida-wiki

Before reading this tutorial, it's highly recommended that you first take a look at the official website of [r2frida](https://github.com/nowsecure/r2frida) to install the tool as well as understand the capabilities of this one.

Commands
=========
## Informative commands
```java
[0x00000000]> \?~^i
i                          Show target information
ii[*]                      List imports
il                         List libraries
is[*] <lib>                List symbols of lib (local and global ones)
iE[*] <lib>                Same as is, but only for the export global ones
iEa[*] (<lib>) <sym>       Show address of export symbol
isa[*] (<lib>) <sym>       Show address of symbol
ic <class>                 List Objective-C classes or methods of <class>
ip <protocol>              List Objective-C protocols or methods of <protocol>
```
- \il
- \iE (lib): List exports of library(ies)
```java
[0xd0d77878]> \iE* frida-agent-32.so
f sym.fun.frida_agent_main = 0xd671a2cd
f sym.var.FRIDA_AGENT_1.0 = 0x0
```

- \ii (lib): List imports of library(ies)
```java
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
