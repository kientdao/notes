---
title: Reverse Engineering C Binaries
date: 25-06-2022
private: false
---

Learning `gdb`

## The Objective:

Analyse the binary from the following C code and determine the correct number.

Don't use `gcc -O0` or `gcc -g` it's cheating!
(I may give up on this, but -g is EZ)

```c
#include "stdio.h"

int genAns() {
  int a = 3, b = 4, c = 2;
  return a*b*c;
}

int main(void) {
  int ans = genAns();
  int input;
  printf("enter a number:\n");
  scanf("%d", &input);

  if (input == ans) {
    printf("Correct!");
  } else {
    printf("Incorrect!");
  }

  return 0;
}
```

## GDB

- `run` - runs specified program
- `disass` - disassembles specified program

intel > AT&T 
- `set disassembly-flavor intel` in `~/.gdbinit`

2-3 consequent zeros. Might indicate an int32 value.

`info func`:
0x0000000100000000  _mh_execute_header
0x0000000100003ec0  genAns
0x0000000100003ef0  main

`disass genAns`:
```asm
0x0000000100003ec0 <+0>:     push   rbp
0x0000000100003ec1 <+1>:     mov    rbp,rsp
0x0000000100003ec4 <+4>:     mov    DWORD PTR [rbp-0x4],0x3
0x0000000100003ecb <+11>:    mov    DWORD PTR [rbp-0x8],0x4
0x0000000100003ed2 <+18>:    mov    DWORD PTR [rbp-0xc],0x2
0x0000000100003ed9 <+25>:    mov    eax,DWORD PTR [rbp-0x4]
0x0000000100003edc <+28>:    imul   eax,DWORD PTR [rbp-0x8]
0x0000000100003ee0 <+32>:    imul   eax,DWORD PTR [rbp-0xc]
0x0000000100003ee4 <+36>:    pop    rbp
0x0000000100003ee5 <+37>:    ret
0x0000000100003ee6 <+38>:    cs nop WORD PTR [rax+rax*1+0x0]
```

`disass main`:
```asm
0x0000000100003ef0 <+0>:     push   rbp
0x0000000100003ef1 <+1>:     mov    rbp,rsp
0x0000000100003ef4 <+4>:     sub    rsp,0x10
0x0000000100003ef8 <+8>:     mov    DWORD PTR [rbp-0x4],0x0
0x0000000100003eff <+15>:    call   0x100003ec0 <genAns>
0x0000000100003f04 <+20>:    mov    DWORD PTR [rbp-0x8],eax
0x0000000100003f07 <+23>:    lea    rdi,[rip+0x7e]        # 0x100003f8c
0x0000000100003f0e <+30>:    mov    al,0x0
0x0000000100003f10 <+32>:    call   0x100003f5c
0x0000000100003f15 <+37>:    lea    rdi,[rip+0x81]        # 0x100003f9d
0x0000000100003f1c <+44>:    lea    rsi,[rbp-0xc]
0x0000000100003f20 <+48>:    mov    al,0x0
0x0000000100003f22 <+50>:    call   0x100003f62
0x0000000100003f27 <+55>:    mov    eax,DWORD PTR [rbp-0xc]
0x0000000100003f2a <+58>:    cmp    eax,DWORD PTR [rbp-0x8]
0x0000000100003f2d <+61>:    jne    0x100003f46 <main+86>
0x0000000100003f33 <+67>:    lea    rdi,[rip+0x66]        # 0x100003fa0
0x0000000100003f3a <+74>:    mov    al,0x0
0x0000000100003f3c <+76>:    call   0x100003f5c
0x0000000100003f41 <+81>:    jmp    0x100003f54 <main+100>
0x0000000100003f46 <+86>:    lea    rdi,[rip+0x5c]        # 0x100003fa9
0x0000000100003f4d <+93>:    mov    al,0x0
0x0000000100003f4f <+95>:    call   0x100003f5c
0x0000000100003f54 <+100>:   xor    eax,eax
0x0000000100003f56 <+102>:   add    rsp,0x10
0x0000000100003f5a <+106>:   pop    rbp
0x0000000100003f5b <+107>:   ret
```

at +58 we see a compare to rbp-0x8

Comes up quite a lot in genAns, huh?

We can see taht we init 3 variables to 0x3, 0x4 and 0x2, and then multiply them for the return value.
alternatively, we can set a breakpoint at *0x0000000100003f2a and look directly at the value in rbp-0x8.



