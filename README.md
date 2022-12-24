.model small
.code
org 100h
start:
    jmp mulai
nama        db 13,10,'Nama Costumer : $'
nomor       db 13,10,'Nomor Meja Yang digunakan : $'
lanjut      db 13,10,'tekan y untuk lanjut >>>>>>>>>>>>> $'
tampung_nama        db 30,?,30 dup(?)
tampung_nomor       db 13,?,13 dup(?)

a db 01
b db 02
c db 03
d db 04
e db 05
f db 06
j dw 15

daftar  db 13,10,'+-----------------------------------------------+'
        db 13,10,'+------------DAFTAR Menu Warmindo---------------+'
        db 13,10,'+-----------------------------------------------+'
        db 13,10,'|Kode|    Nama         |        HARGA           |'
        db 13,10,'+--+--------------------------------------------+'
        db 13,10,'| 01 |  Intel Goreng   |      Rp.8000           |'
        db 13,10,'+--+--------------------------------------------+'
        db 13,10,'| 02 |  Magelangan     |      Rp.11000          |'
        db 13,10,'+--+----------------+---------------------------+'
        db 13,10,'| 03 |  Es Teh         |      Rp.3000           |'
        db 13,10,'+--+----------------+---------------------------+'
        db 13,10,'| 04 |  Ayam Geprek    |      Rp.13000          |'
        db 13,10,'+--+----------------+---------------------------+','$'




error       db 13,10,'Yang anda masukan salah $'

pilih_spt   db 13,10,'Silahkan pilih Kodenya $'
succes      db 13,10,'anda berhasil $'

mulai:
    mov ah,09h
    lea dx,nama
    int 21h
    mov ah,0ah
    lea dx,tampung_nama
    int 21h
    push dx

    mov ah,09h
    lea dx,nomor
    int 21h
    mov ah,0ah
    lea dx,tampung_nomor
    int 21h
    push dx

    mov ah,09h
    mov dx,offset daftar
    int 21h
    mov ah,09h
    mov dx,offset lanjut
    int 21h
    mov ah,01h
    int 21h
    cmp al,'y'
    je proses
    jne error_nsg

error_nsg:
    mov ah,09h
    mov dx,offset error
    int 21h
    int 20h

proses:
    mov ah,09h
    mov dx,offset pilih_spt
    int 21h

    mov ah,1
    int 21h
    mov bh,al
    mov ah,1
    int 21h
    mov bl,al
    cmp bh,'0'
    cmp bl,'1'
    je hasil1

    cmp bh,'0'
    cmp bl,'2'
    je hasil2


    cmp bh,'0'
    cmp bl,'3'
    je hasil3


    cmp bh,'0'
    cmp bl,'4'
    je hasil4


;--------------------------------------------------------------------------

hasil1:
    mov ah,09h
    lea dx,teks1
    int 21h
    int 20h

hasil2:
    mov ah,09h
    lea dx,teks2
    int 21h
    int 20h

hasil3:
    mov ah,09h
    lea dx,teks3
    int 21h
    int 20h

hasil4:
    mov ah,09h
    lea dx,teks4
    int 21h
    int 20h

;--------------------------------------------------------------------------

teks1       db 13,10,'                                       '
        db 13,10,'Anda memesan intel goreng'
        db 13,10,'Total harga yang harus anda bayar : Rp.8000'
        db 13,10,'Terima Kasih Sudah Berbelanja di Warmindo Kami$'

teks2       db 13,10,'                                       '
        db 13,10,'Anda memesan magelangan'
        db 13,10,'Total harga yang harus anda bayar : Rp.11000'
        db 13,10,'Terima Kasih Sudah Berbelanja di Warmindo Kami$' 

teks3       db 13,10,'                                       '
        db 13,10,'Anda memesan es teh '
        db 13,10,'Total harga yang harus anda bayar : Rp.3000'
        db 13,10,'Terima Kasih Sudah Berbelanja di Warmindo Kami$' 

teks4       db 13,10,'                                       '
        db 13,10,'Anda memesan ayam geprek'
        db 13,10,'Total harga yang harus anda bayar : Rp.13000'
        db 13,10,'Terima Kasih Sudah Berbelanja di Warmindo Kami$' 

end start
