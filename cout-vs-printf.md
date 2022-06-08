---
title: C++ cout VS printf
date: 18-05-2022
private: false
---

Since C++ supports (most) of C's functions, let's test the new and improved IO utils performance!

Most notably `cout` and, the classic, `printf`

`cout.cc`

```c++
#include "iostream"

int main() {
  std::cout << "Hello World!\n";
}
```

`printf.cc`

```c++
#include "iostream"

int main() {
  printf("Hello World!\n");
}
```

Running `g++ -fno-asynchronous-unwind-tables -fno-exceptions -fno-rtti -fverbose-asm -Wall -Wextra printf.cc -O3 -masm=intel -S -o printf`

```nasm
 .section __TEXT,__text,regular,pure_instructions
 .build_version macos, 12, 0 sdk_version 12, 3
 .intel_syntax noprefix
 .globl _main                           ## -- Begin function main
 .p2align 4, 0x90
_main:                                  ## @main
## %bb.0:
 push rbp
 mov rbp, rsp
 lea rdi, [rip + L_str]
 call _puts
 xor eax, eax
 pop rbp
 ret
                                        ## -- End function
 .section __TEXT,__cstring,cstring_literals
L_str:                                  ## @str
 .asciz "Hello World!"

.subsections_via_symbols
```

And using `objdump -d` on the compiled binary from standard `g++ printf.cc`:

```nasm
printf: file format mach-o 64-bit x86-64

Disassembly of section __TEXT,__text:

0000000100003f70 <_main>:
100003f70: 55                           pushq %rbp
100003f71: 48 89 e5                     movq %rsp, %rbp
100003f74: 48 8d 3d 2b 00 00 00         leaq 43(%rip), %rdi          ## 0x100003fa6 <dyld_stub_binder+0x100003fa6>
100003f7b: b0 00                        movb $0, %al
100003f7d: e8 04 00 00 00               callq 0x100003f86 <dyld_stub_binder+0x100003f86>
100003f82: 31 c0                        xorl %eax, %eax
100003f84: 5d                           popq %rbp
100003f85: c3                           retq

Disassembly of section __TEXT,__stubs:

0000000100003f86 <__stubs>:
100003f86: ff 25 74 40 00 00            jmpq *16500(%rip)            ## 0x100008000 <dyld_stub_binder+0x100008000>

Disassembly of section __TEXT,__stub_helper:

0000000100003f8c <__stub_helper>:
100003f8c: 4c 8d 1d 75 40 00 00         leaq 16501(%rip), %r11       ## 0x100008008 <__dyld_private>
100003f93: 41 53                        pushq %r11
100003f95: ff 25 65 00 00 00            jmpq *101(%rip)              ## 0x100004000 <dyld_stub_binder+0x100004000>
100003f9b: 90                           nop
100003f9c: 68 00 00 00 00               pushq $0
100003fa1: e9 e6 ff ff ff               jmp 0x100003f8c <__stub_helper>
```

Compare this to the `cout` implementation:

```nasm
 .section __TEXT,__text,regular,pure_instructions
 .build_version macos, 12, 0 sdk_version 12, 3
 .intel_syntax noprefix
 .globl _main                           ## -- Begin function main
 .p2align 4, 0x90
_main:                                  ## @main
## %bb.0:
 push rbp
 mov rbp, rsp
 mov rdi, qword ptr [rip + __ZNSt3__14coutE@GOTPCREL]
 lea rsi, [rip + L_.str]
 mov edx, 13
 call __ZNSt3__124__put_character_sequenceIcNS_11char_traitsIcEEEERNS_13basic_ostreamIT_T0_EES7_PKS4_m
 xor eax, eax
 pop rbp
 ret
                                        ## -- End function
 .globl __ZNSt3__124__put_character_sequenceIcNS_11char_traitsIcEEEERNS_13basic_ostreamIT_T0_EES7_PKS4_m ## -- Begin function _ZNSt3__124__put_character_sequenceIcNS_11char_traitsIcEEEERNS_13basic_ostreamIT_T0_EES7_PKS4_m
 .weak_def_can_be_hidden __ZNSt3__124__put_character_sequenceIcNS_11char_traitsIcEEEERNS_13basic_ostreamIT_T0_EES7_PKS4_m
 .p2align 4, 0x90
__ZNSt3__124__put_character_sequenceIcNS_11char_traitsIcEEEERNS_13basic_ostreamIT_T0_EES7_PKS4_m: ## @_ZNSt3__124__put_character_sequenceIcNS_11char_traitsIcEEEERNS_13basic_ostreamIT_T0_EES7_PKS4_m
## %bb.0:
 push rbp
 mov rbp, rsp
 push r15
 push r14
 push r13
 push r12
 push rbx
 sub rsp, 40
 mov r14, rdx
 mov r13, rsi
 mov rbx, rdi
 lea rdi, [rbp - 80]
 mov rsi, rbx
 call __ZNSt3__113basic_ostreamIcNS_11char_traitsIcEEE6sentryC1ERS3_
 cmp byte ptr [rbp - 80], 0
 je LBB1_5
## %bb.1:
 mov rax, qword ptr [rbx]
 mov rax, qword ptr [rax - 24]
 mov rdi, qword ptr [rbx + rax + 40]
 lea r12, [rbx + rax]
 mov ecx, 176
 and ecx, dword ptr [rbx + rax + 8]
 add r14, r13
 cmp ecx, 32
 mov r15, r13
 cmove r15, r14
 mov eax, dword ptr [rbx + rax + 144]
 cmp eax, -1
 jne LBB1_3
## %bb.2:
 lea rax, [rbp - 56]
 mov qword ptr [rbp - 64], rdi       ## 8-byte Spill
 mov rdi, rax
 mov rsi, r12
 call __ZNKSt3__18ios_base6getlocEv
 mov rsi, qword ptr [rip + __ZNSt3__15ctypeIcE2idE@GOTPCREL]
 lea rdi, [rbp - 56]
 call __ZNKSt3__16locale9use_facetERNS0_2idE
 mov rcx, qword ptr [rax]
 mov rdi, rax
 mov esi, 32
 call qword ptr [rcx + 56]
 mov byte ptr [rbp - 41], al         ## 1-byte Spill
 lea rdi, [rbp - 56]
 call __ZNSt3__16localeD1Ev
 mov rdi, qword ptr [rbp - 64]       ## 8-byte Reload
 movsx eax, byte ptr [rbp - 41]        ## 1-byte Folded Reload
 mov dword ptr [r12 + 144], eax
LBB1_3:
 movsx r9d, al
 mov rsi, r13
 mov rdx, r15
 mov rcx, r14
 mov r8, r12
 call __ZNSt3__116__pad_and_outputIcNS_11char_traitsIcEEEENS_19ostreambuf_iteratorIT_T0_EES6_PKS4_S8_S8_RNS_8ios_baseES4_
 test rax, rax
 jne LBB1_5
## %bb.4:
 mov rax, qword ptr [rbx]
 mov rax, qword ptr [rax - 24]
 lea rdi, [rbx + rax]
 mov esi, dword ptr [rbx + rax + 32]
 or esi, 5
 call __ZNSt3__18ios_base5clearEj
LBB1_5:
 lea rdi, [rbp - 80]
 call __ZNSt3__113basic_ostreamIcNS_11char_traitsIcEEE6sentryD1Ev
 mov rax, rbx
 add rsp, 40
 pop rbx
 pop r12
 pop r13
 pop r14
 pop r15
 pop rbp
 ret
                                        ## -- End function
 .private_extern __ZNSt3__116__pad_and_outputIcNS_11char_traitsIcEEEENS_19ostreambuf_iteratorIT_T0_EES6_PKS4_S8_S8_RNS_8ios_baseES4_ ## -- Begin function _ZNSt3__116__pad_and_outputIcNS_11char_traitsIcEEEENS_19ostreambuf_iteratorIT_T0_EES6_PKS4_S8_S8_RNS_8ios_baseES4_
 .globl __ZNSt3__116__pad_and_outputIcNS_11char_traitsIcEEEENS_19ostreambuf_iteratorIT_T0_EES6_PKS4_S8_S8_RNS_8ios_baseES4_
 .weak_def_can_be_hidden __ZNSt3__116__pad_and_outputIcNS_11char_traitsIcEEEENS_19ostreambuf_iteratorIT_T0_EES6_PKS4_S8_S8_RNS_8ios_baseES4_
 .p2align 4, 0x90
__ZNSt3__116__pad_and_outputIcNS_11char_traitsIcEEEENS_19ostreambuf_iteratorIT_T0_EES6_PKS4_S8_S8_RNS_8ios_baseES4_: ## @_ZNSt3__116__pad_and_outputIcNS_11char_traitsIcEEEENS_19ostreambuf_iteratorIT_T0_EES6_PKS4_S8_S8_RNS_8ios_baseES4_
## %bb.0:
 push rbp
 mov rbp, rsp
 push r15
 push r14
 push r13
 push r12
 push rbx
 sub rsp, 56
 test rdi, rdi
 je LBB2_19
## %bb.1:
 mov r14, r8
 mov r15, rcx
 mov r13, rdi
 mov dword ptr [rbp - 44], r9d       ## 4-byte Spill
 mov rax, rcx
 sub rax, rsi
 mov rcx, qword ptr [r8 + 24]
 xor r12d, r12d
 sub rcx, rax
 cmovg r12, rcx
 mov qword ptr [rbp - 88], rdx       ## 8-byte Spill
 mov rbx, rdx
 sub rbx, rsi
 test rbx, rbx
 jle LBB2_3
## %bb.2:
 mov rax, qword ptr [r13]
 mov rdi, r13
 mov rdx, rbx
 call qword ptr [rax + 96]
 cmp rax, rbx
 jne LBB2_19
LBB2_3:
 test r12, r12
 jle LBB2_15
## %bb.4:
 cmp r12, 23
 mov qword ptr [rbp - 80], r14       ## 8-byte Spill
 jae LBB2_8
## %bb.5:
 lea eax, [r12 + r12]
 mov byte ptr [rbp - 72], al
 lea r14, [rbp - 71]
 jmp LBB2_9
LBB2_8:
 lea rbx, [r12 + 16]
 and rbx, -16
 mov rdi, rbx
 call __Znwm
 mov r14, rax
 mov qword ptr [rbp - 56], rax
 or rbx, 1
 mov qword ptr [rbp - 72], rbx
 mov qword ptr [rbp - 64], r12
LBB2_9:
 mov eax, dword ptr [rbp - 44]       ## 4-byte Reload
 movzx esi, al
 mov rdi, r14
 mov rdx, r12
 call _memset
 mov byte ptr [r14 + r12], 0
 test byte ptr [rbp - 72], 1
 je LBB2_11
## %bb.10:
 mov rsi, qword ptr [rbp - 56]
 jmp LBB2_12
LBB2_11:
 lea rsi, [rbp - 71]
LBB2_12:
 mov r14, qword ptr [rbp - 80]       ## 8-byte Reload
 mov rax, qword ptr [r13]
 mov rdi, r13
 mov rdx, r12
 call qword ptr [rax + 96]
 mov rbx, rax
 test byte ptr [rbp - 72], 1
 je LBB2_14
## %bb.13:
 mov rdi, qword ptr [rbp - 56]
 call __ZdlPv
LBB2_14:
 cmp rbx, r12
 jne LBB2_19
LBB2_15:
 mov rsi, qword ptr [rbp - 88]       ## 8-byte Reload
 sub r15, rsi
 test r15, r15
 jle LBB2_17
## %bb.16:
 mov rax, qword ptr [r13]
 mov rdi, r13
 mov rdx, r15
 call qword ptr [rax + 96]
 cmp rax, r15
 jne LBB2_19
LBB2_17:
 mov qword ptr [r14 + 24], 0
 jmp LBB2_20
LBB2_19:
 xor r13d, r13d
LBB2_20:
 mov rax, r13
 add rsp, 56
 pop rbx
 pop r12
 pop r13
 pop r14
 pop r15
 pop rbp
 ret
                                        ## -- End function
 .section __TEXT,__cstring,cstring_literals
L_.str:                                 ## @.str
 .asciz "Hello World!\n"

.subsections_via_symbols
```

And a disassembled dump that is **too big** to put here!

## results

| process                      | printf | cout |
| ---------------------------- | ------ | ---- |
| `g++` -> asm (with cleaning) | 20     | 223  |
| `g++` -> asm (no cleaning)   | 25     | 1585 |
| `objdump` on binary          | 29     | 1028 |

It's weird that the disassembled binary has **fewer** SLOC than the standard assembly output - but printf is still undeniably faster!

So why use `cout`?
