# r2frida-wiki

Before reading this tutorial, it's highly recommended that you first take a look at the official website of [r2frida](https://github.com/nowsecure/r2frida) to install the tool as well as understand the capabilities of this one.

Commands (`\?`)
===============
In order to get the list of commands, you might want to type: `\?`

## Informative commands (`\i`)
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
- `\i`: Shows target information
```java
[0x00000000]> \i
arch  arm
bits  64
os  linux
pid  14473
uid  10127
objc  false
java  true
cylang  false
```
- `\i*`: Shows target information in `r2` form
```java
[0x00000000]> \i*
e asm.arch=arm
e asm.bits=64
e asm.os=linux
```
- `\ii (lib)`: List imports. Commonly used with the symbol `~`, which is the internal grep of `r2`.
```java
[0x00000000]> \ii libssl.so~+aes
0x7f9419f510 f EVP_aes_128_cbc /system/lib64/libcrypto.so
0x7f941a2740 f EVP_aead_aes_128_cbc_sha1_ssl3 /system/lib64/libcrypto.so
0x7f941a3314 f EVP_aead_aes_128_cbc_sha1_tls /system/lib64/libcrypto.so
0x7f941a3320 f EVP_aead_aes_128_cbc_sha1_tls_implicit_iv /system/lib64/libcrypto.so
0x7f941a332c f EVP_aead_aes_128_cbc_sha256_tls /system/lib64/libcrypto.so
0x7f9419f5b8 f EVP_aead_aes_128_gcm /system/lib64/libcrypto.so
0x7f941a274c f EVP_aead_aes_256_cbc_sha1_ssl3 /system/lib64/libcrypto.so
0x7f941a3338 f EVP_aead_aes_256_cbc_sha1_tls /system/lib64/libcrypto.so
0x7f941a3344 f EVP_aead_aes_256_cbc_sha1_tls_implicit_iv /system/lib64/libcrypto.so
0x7f941a3350 f EVP_aead_aes_256_cbc_sha256_tls /system/lib64/libcrypto.so
0x7f941a335c f EVP_aead_aes_256_cbc_sha384_tls /system/lib64/libcrypto.so
0x7f9419f5c4 f EVP_aead_aes_256_gcm /system/lib64/libcrypto.so
0x7f9419f600 f EVP_has_aes_hardware /system/lib64/libcrypto.so
```

- `\ii* (lib)`: List imports in `r2` form.
```java
[0x00000000]> \ii* libssl.so~+aes
f sym.imp.EVP_aes_128_cbc = 0x7f9419f510
f sym.imp.EVP_aead_aes_128_cbc_sha1_ssl3 = 0x7f941a2740
f sym.imp.EVP_aead_aes_128_cbc_sha1_tls = 0x7f941a3314
f sym.imp.EVP_aead_aes_128_cbc_sha1_tls_implicit_iv = 0x7f941a3320
f sym.imp.EVP_aead_aes_128_cbc_sha256_tls = 0x7f941a332c
f sym.imp.EVP_aead_aes_128_gcm = 0x7f9419f5b8
f sym.imp.EVP_aead_aes_256_cbc_sha1_ssl3 = 0x7f941a274c
f sym.imp.EVP_aead_aes_256_cbc_sha1_tls = 0x7f941a3338
f sym.imp.EVP_aead_aes_256_cbc_sha1_tls_implicit_iv = 0x7f941a3344
f sym.imp.EVP_aead_aes_256_cbc_sha256_tls = 0x7f941a3350
f sym.imp.EVP_aead_aes_256_cbc_sha384_tls = 0x7f941a335c
f sym.imp.EVP_aead_aes_256_gcm = 0x7f9419f5c4
f sym.imp.EVP_has_aes_hardware = 0x7f9419f600
```

- `\il`: List libraries. Commonly used with the symbol `~`, which is the internal grep of `r2`.
```java
[0x00000000]> \il~+keystore,ssl,crypto
0x0000007f94133000 libcrypto.so
0x0000007f93059000 libssl.so
0x0000007f879d8000 libjavacrypto.so
0x0000007f879d3000 libkeystore-engine.so
0x0000007f87985000 libkeystore_binder.so
0x0000007f5c491000 libvisacrypto.so
```
- `\iE (lib)`: List exports of library(ies)
```java
[0x00000000]> \iE
Do you want to print 111759 lines? (y/N) n
```
Filtering by library name:
```java
[0x00000000]> \iE libssl.so~AES
0x7f9307afb4 f SSL_CIPHER_is_AES256CBC
0x7f9307af64 f SSL_CIPHER_is_AES
0x7f9307af8c f SSL_CIPHER_is_AESGCM
0x7f9307af9c f SSL_CIPHER_is_AES128GCM
0x7f9307afa8 f SSL_CIPHER_is_AES128CBC
```
Filtering by library name in `r2` form: (notice the `*`)
```java
[0x00000000]> \iE* libssl.so~AES
f sym.fun.SSL_CIPHER_is_AES256CBC = 0x7f9307afb4
f sym.fun.SSL_CIPHER_is_AES = 0x7f9307af64
f sym.fun.SSL_CIPHER_is_AESGCM = 0x7f9307af8c
f sym.fun.SSL_CIPHER_is_AES128GCM = 0x7f9307af9c
f sym.fun.SSL_CIPHER_is_AES128CBC = 0x7f9307afa8
```

- `\ii (lib)`: List imports of library(ies)
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

## Search commands (`\/`)
```java
[0x00000000]> \?~^/
/[x][j] <string|hexpairs>  Search hex/string pattern in memory ranges (see search.in=?)
/w[j] string               Search wide string
/v[1248][j] value          Search for a value honoring `e cfg.bigendian` of given width
```

## Dynamic/Debugging commands (`\d`)
```java
[0x00000000]> \?~^d
db (<addr>|<sym>)          List or place breakpoint
db- (<addr>|<sym>)|*       Remove breakpoint(s)
dc                         Continue breakpoints or resume a spawned process
dd[-][fd] ([newfd])        List, dup2 or close filedescriptors
dm[.|j|*]                  Show memory regions
dma <size>                 Allocate <size> bytes on the heap, address is returned
dmas <string>              Allocate a string inited with <string> on the heap
dmad <addr> <size>         Allocate <size> bytes on the heap, copy contents from <addr>
dmal                       List live heap allocations created with dma[s]
dma- (<addr>...)           Kill the allocations at <addr> (or all of them without param)
dmp <addr> <size> <perms>  Change page at <address> with <size>, protection <perms> (rwx)
dmm                        List all named squashed maps
dmh                        List all heap allocated chunks
dmhj                       List all heap allocated chunks in JSON
dmh*                       Export heap chunks and regions as r2 flags
dmhm                       Show which maps are used to allocate heap chunks
dp                         Show current pid
dpt                        Show threads
dr                         Show thread registers (see dpt)
dl libname                 Dlopen a library
dl2 libname [main]         Inject library using Frida's >= 8.2 new API
dt (<addr>|<sym>) ...      Trace list of addresses or symbols
dth (<addr>|<sym>) (x y..) Define function header (z=str,i=int,v=hex barray,s=barray)
dt-                        Clear all tracing
dtr <addr> (<regs>...)     Trace register values
dtf <addr> [fmt]           Trace address with format (^ixzO) (see dtf?)
dtSf[*j] [sym|addr]        Trace address or symbol using the stalker (Frida >= 10.3.13)
dtS[*j] seconds            Trace all threads for given seconds using the stalker
di[0,1,-1] [addr]          Intercept and replace return value of address
dx [hexpairs]              Inject code and execute it (TODO)
dxc [sym|addr] [args..]    Call the target symbol with given args
```

- `\dt (<addr>|<sym>) ...`: Trace list of addresses or symbols. Similar to `frida-trace`
```java
[0x00000000]> \dt fopen; \dth fopen z; \dc
[TRACE] 0x7f942bf1e8 ( fopen ) ["/proc/self/maps"]
 - 0x7f5bf72d98 libtarget.so!scan_executable+0xf0
 - 0x7f5bf72d94 libtarget.so!scan_executable+0xec
 - 0x7f5bf721b4 libtarget.so!secchecks+0x90
 - 0x7f5bf6cdb8 libtarget.so!Java_com_super_secure_App+0x1710
 - 0x7f69e6a7e0 base.odex!oatexec+0x4e7e0
```
## Evaluable variables (`\e`)
- `e[?] [a[=b]]`: List/get/set config evaluable vars
```java
[0x00000000]> \e
e patch.code=true
e search.in=perm:r--
e search.quiet=false
e stalker.event=compile
e stalker.timeout=300
e stalker.in=raw
```
## Environment variables (`\env`)
- `\env`: Get/set environment variable

Set env variable:
```java
[0x00000000]> \env LD_PRELOAD=/data/local/tmp/libhook.so
LD_PRELOAD=/data/local/tmp/libhook.so
```

Get env variable:
```java
[0x00000000]> \env LD_PRELOAD
LD_PRELOAD=/data/local/tmp/libhook.so
```

List all variables:
```java
[0x00000000]> \env
PATH=/su/bin:/sbin:/vendor/bin:/system/sbin:/system/bin:/su/xbin:/system/xbin
ANDROID_BOOTLOGO=1
ANDROID_ROOT=/system
ANDROID_ASSETS=/system/app
ANDROID_DATA=/data
ANDROID_STORAGE=/storage
EXTERNAL_STORAGE=/sdcard
ASEC_MOUNTPOINT=/mnt/asec
ANDROID_SOCKET_zygote=9
ANDROID_LOG_TAGS=*:s
```

## Frida scripts (`\. script.js`)
JS code to be run in the target can be load with `\. script.js`. A common practice is always to call this script `agent.js` to remember that's the code to be run inside the target.
```java
[0x00000000]> .\ agent.js
[0x00000000]> \dc
resumed spawned process.
```


Android
=======

Attaching
---------

Spawning
--------

iOS
===

**TODO**
