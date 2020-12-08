---
title: CDDC [Cheat Me]
author: Jason Chua (Coldspot)
date: 2020-07-8 21:24:30 +0800
categories: [CTF, CDDC]
tags: [tech, pwn, patching]
toc: true
comments: true
---

This challenge requires us to run a PE file. It will start a timer and when it reaches a specific time, it will print the flag.

<!--more-->

# Decompilation
When disassembling, ghidra fails to identify the function names. By searching for strings and working backwards, we can identify that FUN_00401040 might be the main() function. 

```c
undefined4 FUN_00401040(void)

{
    char *pcVar1;
    HANDLE hConsoleOutput;
    char *pcVar2;
    int iVar3;
    undefined4 unaff_EDI;
    int iVar4;
    WORD wAttributes;
    undefined uVar5;
    
    while( true ) {
    Sleep(1000);
    system("cls");
    uVar5 = (undefined)unaff_EDI;
    if (DAT_00403398 == -1) {
        if ((DAT_00403394 < 1) && (DAT_00403018 < 1)) {
        DAT_00403398 = 0;
        }
        else {
        DAT_00403394 = DAT_00403394 + -1;
        DAT_00403398 = 0x3b;
        }
    }
    if (DAT_00403394 == -1) {
        if (DAT_00403018 < 1) {
        DAT_00403394 = 0;
        }
        else {
        DAT_00403018 = DAT_00403018 + -1;
        DAT_00403394 = 0x3b;
        }
    }
    if (((DAT_00403018 == 0) && (DAT_00403394 == 0)) && (DAT_00403398 == 0)) break;
    wAttributes = 0xc;
    hConsoleOutput = GetStdHandle(0xfffffff5);
    SetConsoleTextAttribute(hConsoleOutput,wAttributes);
    FUN_00401010("[!W!A!R!N!I!N!G!] No cheating \n",(char)unaff_EDI);
    wAttributes = 0xe;
    hConsoleOutput = GetStdHandle(0xfffffff5);
    SetConsoleTextAttribute(hConsoleOutput,wAttributes);
    FUN_00401010("# This program is running the CHEATING PREVENTION SYSTEM. # \n",(char)unaff_EDI);
    wAttributes = 0xf;
    hConsoleOutput = GetStdHandle(0xfffffff5);
    SetConsoleTextAttribute(hConsoleOutput,wAttributes);
    uVar5 = 0x74;
    FUN_00401010("\n\tBe patient. \n",(char)unaff_EDI);
    FUN_00401010("\tThen, you can get what you want. \n",uVar5);
    wAttributes = 10;
    hConsoleOutput = GetStdHandle(0xfffffff5);
    SetConsoleTextAttribute(hConsoleOutput,wAttributes);
    FUN_00401010("\t---------------------- \n",(char)unaff_EDI);
    uVar5 = 0xc4;
    FUN_00401010("\t|  %02d  |  %02d  |  %02d  | \n",(char)DAT_00403018);
    FUN_00401010("\t---------------------- \n",uVar5);
    DAT_00403398 = DAT_00403398 + -1;
    }
    pcVar1 = &DAT_0040301c;
    do {
    pcVar2 = pcVar1;
    pcVar1 = pcVar2 + 1;
    } while (*pcVar2 != '\0');
    pcVar2 = pcVar2 + -0x40301c;
    iVar3 = DAT_00403398;
    iVar4 = DAT_00403394;
    if (0 < (int)pcVar2) {
    do {
        if (iVar4 < (int)pcVar2) {
        do {
            if (iVar3 < (int)pcVar2) {
            do {
                (&DAT_0040301c)[iVar3] = (&DAT_0040301c)[iVar3] + '\x06';
                iVar3 = iVar3 + 1;
                pcVar1 = &DAT_0040301c;
                do {
                pcVar2 = pcVar1;
                pcVar1 = pcVar2 + 1;
                } while (*pcVar2 != '\0');
                DAT_00403398 = iVar3;
            } while (iVar3 < (int)(pcVar2 + -0x40301c));
            }
            iVar4 = iVar4 + 1;
            pcVar1 = &DAT_0040301c;
            do {
            pcVar2 = pcVar1;
            pcVar1 = pcVar2 + 1;
            } while (*pcVar2 != '\0');
            pcVar2 = pcVar2 + -0x40301c;
            DAT_00403394 = iVar4;
        } while (iVar4 < (int)pcVar2);
        }
        DAT_00403018 = DAT_00403018 + 1;
        pcVar1 = &DAT_0040301c;
        do {
        pcVar2 = pcVar1;
        pcVar1 = pcVar2 + 1;
        } while (*pcVar2 != '\0');
        pcVar2 = pcVar2 + -0x40301c;
    } while (DAT_00403018 < (int)pcVar2);
    }
    wAttributes = 0xc;
    hConsoleOutput = GetStdHandle(0xfffffff5);
    SetConsoleTextAttribute(hConsoleOutput,wAttributes);
    FUN_00401010("[!W!A!R!N!I!N!G!] No cheating \n",uVar5);
    wAttributes = 0xe;
    hConsoleOutput = GetStdHandle(0xfffffff5);
    SetConsoleTextAttribute(hConsoleOutput,wAttributes);
    FUN_00401010("# This program is running the CHEATING PREVENTION SYSTEM. # \n",uVar5);
    wAttributes = 0xf;
    hConsoleOutput = GetStdHandle(0xfffffff5);
    SetConsoleTextAttribute(hConsoleOutput,wAttributes);
    FUN_00401010("\n\tGood Job! \n",uVar5);
    wAttributes = 0xd;
    hConsoleOutput = GetStdHandle(0xfffffff5);
    SetConsoleTextAttribute(hConsoleOutput,wAttributes);
    FUN_00401010("\t\t%s \n",0x1c);
    Sleep(0x317040);
    return 0;
}
```

# Exploit

By patching the sleep(1000) to sleep(0) and using the "speedhack" function in cheat engine, we can retrieve the flag very quickly.


More info 
> Ask me on Discord @Coldspot#7033
