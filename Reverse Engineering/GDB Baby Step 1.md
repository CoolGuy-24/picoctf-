# GDB Baby Step 1.

This challenge involved finding what is in the eax register at the end of the main function in the file `debugger0_a`.

I used `exiftool` command to check what type of file this is.

```
coolguy24@Vedant-Laptop:~$ exiftool debugger0_a
ExifTool Version Number         : 12.40
File Name                       : debugger0_a
Directory                       : .
File Size                       : 16 KiB
File Modification Date/Time     : 2024:12:08 15:38:07+05:30
File Access Date/Time           : 2024:12:20 19:43:58+05:30
File Inode Change Date/Time     : 2024:12:20 19:43:54+05:30
File Permissions                : -rwxr-xr-x
File Type                       : ELF shared library
File Type Extension             : so
MIME Type                       : application/octet-stream
CPU Architecture                : 64 bit
CPU Byte Order                  : Little endian
Object File Type                : Shared object file
CPU Type                        : AMD x86-64
```

This was not much of a help and I didn't know how to proceed, however the hints were useful. The first hint talked about using `gdb` for this program while the second hint mentioned the `main` function.

So I installed gdb on my WSL and this [Website](https://web.eecs.umich.edu/~sugih/pointers/summary.html) was very useful in learning the basics of `gdb`. I realised `gdb` is a very powerful debugging tool that can be used for C,C++ and Assembly languages.

I knew I had to find the value in the `eax` register at the end of the main function. So what I needed to do was set a breakpoint in the main function and then run the program and then step in to see what is inside the `eax` register.

```
coolguy24@Vedant-Laptop:~$ gdb debugger0_a
GNU gdb (Ubuntu 12.1-0ubuntu1~22.04.2) 12.1
Copyright (C) 2022 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
Type "show copying" and "show warranty" for details.
This GDB was configured as "x86_64-linux-gnu".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:
<https://www.gnu.org/software/gdb/bugs/>.
Find the GDB manual and other documentation resources online at:
    <http://www.gnu.org/software/gdb/documentation/>.

For help, type "help".
Type "apropos word" to search for commands related to "word"...
Reading symbols from debugger0_a...
(No debugging symbols found in debugger0_a)
(gdb) info functions
All defined functions:

Non-debugging symbols:
0x0000000000001000  _init
0x0000000000001030  __cxa_finalize@plt
0x0000000000001040  _start
0x0000000000001070  deregister_tm_clones
0x00000000000010a0  register_tm_clones
0x00000000000010e0  __do_global_dtors_aux
0x0000000000001120  frame_dummy
0x0000000000001129  main
0x0000000000001140  __libc_csu_init
0x00000000000011b0  __libc_csu_fini
0x00000000000011b8  _fini
(gdb) break main
Breakpoint 1 at 0x1131
(gdb) run
Starting program: /home/coolguy24/debugger0_a
[Thread debugging using libthread_db enabled]
Using host libthread_db library "/lib/x86_64-linux-gnu/libthread_db.so.1".

Breakpoint 1, 0x0000555555555131 in main ()
(gdb) step
Single stepping until exit from function main,
which has no line number information.
__libc_start_call_main (main=main@entry=0x555555555129 <main>, argc=argc@entry=1, argv=argv@entry=0x7fffffffe398) at ../sysdeps/nptl/libc_start_call_main.h:74
74      ../sysdeps/nptl/libc_start_call_main.h: No such file or directory.
(gdb) info registers eax
eax            0x86342             549698
```

I was able to get the decimal value as instructed by the challenge and therefore wrappeed inside the file format anf got the flag.

`FLAG:picoCTF{549698}`
