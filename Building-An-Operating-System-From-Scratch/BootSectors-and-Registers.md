---
title: Boot Sector and Registers
date: 13-08-2021
private: false
---

## Boot Sector

512 bytes @ cylinder 0, head 0, sector 0 that ends in `0xAA55` so the BIOS knows it's legit.

```nasm
e9 fd ff 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
[ 29 more lines with sixteen zero-bytes each ]
00 00 00 00 00 00 00 00 00 00 00 00 00 00 55 aa
```

```nasm
; Infinite loop (e9 fd ff)
loop:
    jmp loop

; Fill with 510 zeros minus the size of the previous code
times 510-($-$$) db 0
; Magic number
dw 0xaa55
```

Instead of just writing 0's, throw some text up:

```nasm
mov ah, 0x0e ; tty mode
mov al, 'H'
int 0x10
mov al, 'e'
int 0x10
mov al, 'l'
int 0x10
int 0x10 ; 'l' is still on al, remember?
mov al, 'o'
int 0x10

jmp $ ; jump to current address = infinite loop

; padding and magic number
times 510 - ($-$$) db 0
dw 0xaa55
```

Write each character of the "Hello" word into the register al (lower part of ax), the bytes 0x0e into ah (the higher part of ax) and raise interrupt 0x10 which is a general interrupt for video services.

FP registers are 128-bit XMM registers, later extended to 256-bit YMM registers with AVX/AVX2 and 512-bit ZMM0-ZMM31 registers with AVX-512.
All x86 CPUs have four general purpose registers, ax, bx, cx, and dx

An interrupt is a response by the processor to an event that needs attention from the software. An interrupt condition alerts the processor and serves as a request for the processor to interrupt the currently executing code when permitted, so that the event can be processed in a timely manner. If the request is accepted, the processor responds by suspending its current activities, saving its state, and executing a function called an interrupt handler (or an interrupt service routine, ISR) to deal with the event.
