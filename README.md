# fileManagement


[quotes.txt](https://github.com/user-attachments/files/21811503/quotes.txt)

1. Challenges:

  One of the main challenges was correctly using Linux system calls with the proper register setup.

  Since these require precise values in registers, mixing them up leads to errors that are hard to debug.

  Calculating the length of strings in assembly for writing with sys_write was tricky.

  Using NASM syntax correctly & managing sections.



2. Working Code:

[quotes.txt](https://github.com/user-attachments/files/21811506/quotes.txt)
section .data
    filename db "quotes.txt", 0

    quote1 db "To be, or not to be, that is the question.", 10
    len1 equ $ - quote1

    quote2 db "A fool thinks himself to be wise, but a wise man knows himself to be a fool.", 10
    len2 equ $ - quote2

    quote3 db "Better three hours too soon than a minute too late.", 10
    len3 equ $ - quote3

    quote4 db "No legacy is so rich as honesty.", 10
    len4 equ $ - quote4

section .bss
    fd resd 1

section .text
    global _start

_start:
    mov eax, 8          
    mov ebx, filename
    mov ecx, 0666o      
    int 0x80
    mov [fd], eax       

    mov eax, 4          
    mov ebx, [fd]
    mov ecx, quote1
    mov edx, len1
    int 0x80

    mov eax, 4          
    mov ebx, [fd]
    mov ecx, quote2
    mov edx, len2
    int 0x80

    mov eax, 19         
    mov ebx, [fd]
    mov ecx, 0          
    mov edx, 2          
    int 0x80

    mov eax, 4          
    mov ebx, [fd]
    mov ecx, quote3
    mov edx, len3
    int 0x80

    mov eax, 4          ; sys_write
    mov ebx, [fd]
    mov ecx, quote4
    mov edx, len4
    int 0x80

    mov eax, 6          
    mov ebx, [fd]
    int 0x80

    mov eax, 1          
    xor ebx, ebx
    int 0x80
    mov eax, 1          ; sys_exit
    xor ebx, ebx
    int 0x80



![filem](https://github.com/user-attachments/assets/2f083c02-9007-4926-ad13-6ed6668be4c4)


![quotes](https://github.com/user-attachments/assets/51de2c6e-407e-45d0-a20d-e67af7a57578)
