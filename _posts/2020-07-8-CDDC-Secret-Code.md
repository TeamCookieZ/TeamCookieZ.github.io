---
title: CDDC [Secret Code]
author: Jason Chua (Coldspot)
date: 2020-07-8 21:24:30 +0800
categories: [CTF, CDDC]
tags: [tech, pwn, gdb]
toc: true
comments: true
---

This challenge was very weird. Since it was a binary we could download and we were suppose to extract the flag from it, I decided to do use GDB to retrieve the flag.

<!--more-->

# Running

On the initial run, the output looks like this

```
jason@kali:~/cddc$ ./SecretCode 
         __                                     _           
 / / _   ) )     _   ) o  _ o _)_ _       _    / ` _   _ _  
(_/ ) ) /_/ (_( )_) (  ( (_ ( (_ (_) (_( (    (_. (_) ) )_) 
               (                         _)            (    

[S][E][C][R][E][T] [C][O][D][E]:
```

# Decompilation
The disassembly of the main function seems to compare a local variable with a hardcoded value and calls another function.

```c
undefined4 main(void)

{
  undefined4 uVar1;
  int in_GS_OFFSET;
  int local_18;
  int local_14;
  undefined *local_10;
  
  local_10 = &stack0x00000004;
  local_14 = *(int *)(in_GS_OFFSET + 0x14);
  local_18 = 0;
  puts("         __                                     _           ");
  puts(" / / _   ) )     _   ) o  _ o _)_ _       _    / ` _   _ _  ");
  puts("(_/ ) ) /_/ (_( )_) (  ( (_ ( (_ (_) (_( (    (_. (_) ) )_) ");
  puts("               (                         _)            (    \n");
  printf("[S][E][C][R][E][T] [C][O][D][E]: ");
  __isoc99_scanf(&DAT_000109b2,&local_18);
  if (local_18 == -0xff23502) {
    check(0xf00dcafe);
  }
  else {
    check(local_18);
  }
  uVar1 = 0;
  if (local_14 != *(int *)(in_GS_OFFSET + 0x14)) {
    uVar1 = __stack_chk_fail_local();
  }
  return uVar1;
}
```

I ran the binary with gdb and disassemble main.


```
(gdb) disas main
Dump of assembler code for function main:
    0x565556f6 <+0>:     lea    0x4(%esp),%ecx
    0x565556fa <+4>:     and    $0xfffffff0,%esp
    0x565556fd <+7>:     pushl  -0x4(%ecx)
    0x56555700 <+10>:    push   %ebp
    0x56555701 <+11>:    mov    %esp,%ebp
    0x56555703 <+13>:    push   %ebx
    0x56555704 <+14>:    push   %ecx
    0x56555705 <+15>:    sub    $0x10,%esp
    0x56555708 <+18>:    call   0x56555500 <__x86.get_pc_thunk.bx>
    0x5655570d <+23>:    add    $0x18bf,%ebx
    0x56555713 <+29>:    mov    %gs:0x14,%eax
    0x56555719 <+35>:    mov    %eax,-0xc(%ebp)
    0x5655571c <+38>:    xor    %eax,%eax
    0x5655571e <+40>:    movl   $0x0,-0x10(%ebp)
    0x56555725 <+47>:    sub    $0xc,%esp
    0x56555728 <+50>:    lea    -0x173c(%ebx),%eax
    0x5655572e <+56>:    push   %eax
    0x5655572f <+57>:    call   0x56555480 <puts@plt>
    0x56555734 <+62>:    add    $0x10,%esp
    0x56555737 <+65>:    sub    $0xc,%esp
    0x5655573a <+68>:    lea    -0x16fc(%ebx),%eax
    0x56555740 <+74>:    push   %eax
    0x56555741 <+75>:    call   0x56555480 <puts@plt>
    0x56555746 <+80>:    add    $0x10,%esp
    0x56555749 <+83>:    sub    $0xc,%esp
    0x5655574c <+86>:    lea    -0x16bc(%ebx),%eax
    0x56555752 <+92>:    push   %eax
    0x56555753 <+93>:    call   0x56555480 <puts@plt>
    0x56555758 <+98>:    add    $0x10,%esp
    0x5655575b <+101>:   sub    $0xc,%esp
    0x5655575e <+104>:   lea    -0x167c(%ebx),%eax
    0x56555764 <+110>:   push   %eax
    0x56555765 <+111>:   call   0x56555480 <puts@plt>
    0x5655576a <+116>:   add    $0x10,%esp
    0x5655576d <+119>:   sub    $0xc,%esp
    0x56555770 <+122>:   lea    -0x163c(%ebx),%eax
    0x56555776 <+128>:   push   %eax
    0x56555777 <+129>:   call   0x56555460 <printf@plt>
    0x5655577c <+134>:   add    $0x10,%esp
    0x5655577f <+137>:   sub    $0x8,%esp
    0x56555782 <+140>:   lea    -0x10(%ebp),%eax
    0x56555785 <+143>:   push   %eax
    0x56555786 <+144>:   lea    -0x161a(%ebx),%eax
    0x5655578c <+150>:   push   %eax
    0x5655578d <+151>:   call   0x565554a0 <__isoc99_scanf@plt>
    0x56555792 <+156>:   add    $0x10,%esp
    0x56555795 <+159>:   mov    -0x10(%ebp),%eax
    0x56555798 <+162>:   cmp    $0xf00dcafe,%eax
    0x5655579d <+167>:   jne    0x565557b0 <main+186>
--Type <RET> for more, q to quit, c to continue without paging--c
    0x5655579f <+169>:   mov    -0x10(%ebp),%eax
    0x565557a2 <+172>:   sub    $0xc,%esp
    0x565557a5 <+175>:   push   %eax
    0x565557a6 <+176>:   call   0x565555fd <check>
    0x565557ab <+181>:   add    $0x10,%esp
    0x565557ae <+184>:   jmp    0x565557bf <main+201>
    0x565557b0 <+186>:   mov    -0x10(%ebp),%eax
    0x565557b3 <+189>:   sub    $0xc,%esp
    0x565557b6 <+192>:   push   %eax
    0x565557b7 <+193>:   call   0x565555fd <check>
    0x565557bc <+198>:   add    $0x10,%esp
    0x565557bf <+201>:   mov    $0x0,%eax
    0x565557c4 <+206>:   mov    -0xc(%ebp),%edx
    0x565557c7 <+209>:   xor    %gs:0x14,%edx
    0x565557ce <+216>:   je     0x565557d5 <main+223>
    0x565557d0 <+218>:   call   0x56555860 <__stack_chk_fail_local>
    0x565557d5 <+223>:   lea    -0x8(%ebp),%esp
    0x565557d8 <+226>:   pop    %ecx
    0x565557d9 <+227>:   pop    %ebx
    0x565557da <+228>:   pop    %ebp
    0x565557db <+229>:   lea    -0x4(%ecx),%esp
    0x565557de <+232>:   ret    
End of assembler dump.
```

# Exploit

I set a breakpoint at address 0x56555798 as it is the comparison. Next, I continued the process and entered a random string as input. When it hit the break point, I ran "set $eax=0xf00dcafe" and disassemble check.


```
(gdb) disas check
Dump of assembler code for function check:
   0x565555fd <+0>:     push   %ebp
   0x565555fe <+1>:     mov    %esp,%ebp
   0x56555600 <+3>:     push   %edi
   0x56555601 <+4>:     push   %esi
   0x56555602 <+5>:     push   %ebx
   0x56555603 <+6>:     sub    $0x4c,%esp
   0x56555606 <+9>:     call   0x565557df <__x86.get_pc_thunk.ax>
   0x5655560b <+14>:    add    $0x19c1,%eax
   0x56555610 <+19>:    mov    %eax,-0x54(%ebp)
   0x56555613 <+22>:    mov    %gs:0x14,%eax
   0x56555619 <+28>:    mov    %eax,-0x1c(%ebp)
   0x5655561c <+31>:    xor    %eax,%eax
   0x5655561e <+33>:    movb   $0x0,-0x3d(%ebp)
   0x56555622 <+37>:    movl   $0x43444443,-0x33(%ebp)
   0x56555629 <+44>:    movl   $0x457b3032,-0x2f(%ebp)
   0x56555630 <+51>:    movl   $0x567a7135,-0x2b(%ebp)
   0x56555637 <+58>:    movl   $0x7a347036,-0x27(%ebp)
   0x5655563e <+65>:    movl   $0x6b653b5a,-0x23(%ebp)
   0x56555645 <+72>:    movw   $0x7d73,-0x1f(%ebp)
   0x5655564b <+78>:    movb   $0x0,-0x1d(%ebp)
   0x5655564f <+82>:    movl   $0xdeadbeef,-0x3c(%ebp)
   0x56555656 <+89>:    movl   $0xbabeface,-0x38(%ebp)
   0x5655565d <+96>:    mov    -0x3c(%ebp),%ecx
   0x56555660 <+99>:    sub    -0x38(%ebp),%ecx
   0x56555663 <+102>:   mov    %ecx,%esi
   0x56555665 <+104>:   mov    $0x0,%edi
   0x5655566a <+109>:   mov    0x8(%ebp),%ecx
   0x5655566d <+112>:   mov    $0x0,%ebx
   0x56555672 <+117>:   add    $0x33e0f923,%ecx
   0x56555678 <+123>:   adc    $0xffffffff,%ebx
   0x5655567b <+126>:   mov    %esi,%eax
   0x5655567d <+128>:   xor    %ecx,%eax
   0x5655567f <+130>:   mov    %eax,-0x50(%ebp)
   0x56555682 <+133>:   mov    %edi,%eax
   0x56555684 <+135>:   xor    %ebx,%eax
   0x56555686 <+137>:   mov    %eax,-0x4c(%ebp)
   0x56555689 <+140>:   mov    -0x50(%ebp),%ebx
   0x5655568c <+143>:   mov    -0x4c(%ebp),%esi
   0x5655568f <+146>:   mov    %ebx,%eax
   0x56555691 <+148>:   or     %esi,%eax
   0x56555693 <+150>:   test   %eax,%eax
   0x56555695 <+152>:   jne    0x565556dc <check+223>
   0x56555697 <+154>:   movb   $0x0,-0x3d(%ebp)
   0x5655569b <+158>:   jmp    0x565556c4 <check+199>
   0x5655569d <+160>:   movzbl -0x3d(%ebp),%eax
   0x565556a1 <+164>:   add    $0x7,%eax
   0x565556a4 <+167>:   movzbl -0x33(%ebp,%eax,1),%ecx
   0x565556a9 <+172>:   movzbl -0x3d(%ebp),%edx
   0x565556ad <+176>:   movzbl -0x3d(%ebp),%eax
--Type <RET> for more, q to quit, c to continue without paging--
   0x565556b1 <+180>:   add    $0x7,%eax
   0x565556b4 <+183>:   xor    %ecx,%edx
   0x565556b6 <+185>:   mov    %dl,-0x33(%ebp,%eax,1)
   0x565556ba <+189>:   movzbl -0x3d(%ebp),%eax
   0x565556be <+193>:   add    $0x1,%eax
   0x565556c1 <+196>:   mov    %al,-0x3d(%ebp)
   0x565556c4 <+199>:   cmpb   $0xd,-0x3d(%ebp)
   0x565556c8 <+203>:   jbe    0x5655569d <check+160>
   0x565556ca <+205>:   sub    $0xc,%esp
   0x565556cd <+208>:   lea    -0x33(%ebp),%eax
   0x565556d0 <+211>:   push   %eax
   0x565556d1 <+212>:   mov    -0x54(%ebp),%ebx
   0x565556d4 <+215>:   call   0x56555480 <puts@plt>
   0x565556d9 <+220>:   add    $0x10,%esp
   0x565556dc <+223>:   nop
   0x565556dd <+224>:   mov    -0x1c(%ebp),%eax
   0x565556e0 <+227>:   xor    %gs:0x14,%eax
   0x565556e7 <+234>:   je     0x565556ee <check+241>
   0x565556e9 <+236>:   call   0x56555860 <__stack_chk_fail_local>
   0x565556ee <+241>:   lea    -0xc(%ebp),%esp
   0x565556f1 <+244>:   pop    %ebx
   0x565556f2 <+245>:   pop    %esi
   0x565556f3 <+246>:   pop    %edi
   0x565556f4 <+247>:   pop    %ebp
   0x565556f5 <+248>:   ret    
End of assembler dump.
```

This function seems to check the input to the function and does some xor magic to obtain the flag. I will set a breakpoint after the first test instruction at 0x56555695 and continue the process. Next, I will hit the second breakpoint at check() and jump to the instruction after the jne instruction to skip the check.

```
(gdb) jump *0x56555697
Continuing at 0x56555697.
CDDC20{E4syR3v3rS1ng~}
[Inferior 1 (process 2135) exited normally]
```

More info 
>> Ask me on Discord @Coldspot#7033
