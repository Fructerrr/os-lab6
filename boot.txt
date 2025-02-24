BITS 16
ORG 0x7C00

start:
    cli
    xor ax, ax
    mov ds, ax
    mov es, ax
    mov ss, ax
    mov sp, 0x7C00
    sti

    ; Вывод ASCII-арта
    mov si, logo
print_logo:
    lodsb
    or al, al
    jz done
    cmp al, 10
    jne print_char
    mov ah, 0x0E
    mov al, 0x0D
    int 0x10
    mov al, 0x0A
    int 0x10
    jmp print_logo

print_char:
    mov ah, 0x0E
    int 0x10
    jmp print_logo

done:
    jmp $

logo 	db "boot.asm",10
	db "  ____    _      ____   ____  _  ",10
     	db " |  _ \  / \    | __ ) |  _ \| | ",10
     	db " | |_) |/ _ \   |  _ \ | |_) | | ",10
     	db " |  _ <| ___ \  | |_) ||  _ <|_| ",10
     	db " |_| \_\_/   \_\|____/ |_| \_\(_) ",10
     	db 0

times 510-($-$$) db 0
dw 0xAA55
