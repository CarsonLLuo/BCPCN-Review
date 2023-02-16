---
title: code
date: 2023-02-16T11:11:59Z
lastmod: 2023-02-17T00:10:52Z
---

# code

# code1

```x86asm
.model small    ; 指定程序模型，这里是 small 模型
.stack 100h     ; 分配堆栈空间
.code           ; 声明下面的代码段开始

main proc       ; 定义一个过程，起始标签为 main
    mov ah,1    ; 将 1 存储到寄存器 AH 中，表示调用 DOS 中断 21h 来读取一个字符
    int 21h     ; 调用 DOS 中断 21h，等待用户输入一个字符，存储在 AL 寄存器中
    mov bl, al  ; 将 AL 寄存器中的值（即用户输入的字符的 ASCII 码）存储到 BL 寄存器中

    mov ah,1    ; 将 1 存储到寄存器 AH 中，表示调用 DOS 中断 21h 来读取一个字符
    int 21h     ; 调用 DOS 中断 21h，等待用户输入一个字符，存储在 AL 寄存器中
    mov bh,al   ; 将 AL 寄存器中的值存储到 BH 寄存器中

    mov ah,2    ; 将 2 存储到寄存器 AH 中，表示调用 DOS 中断 21h 来显示一个字符
    mov dl,bl   ; 将 BL 寄存器中的值（即之前输入的字符的 ASCII 码）存储到 DL 寄存器中
    int 21h     ; 调用 DOS 中断 21h，将 DL 寄存器中的值（即之前输入的字符的 ASCII 码）显示到屏幕上

    mov ah,2    ; 将 2 存储到寄存器 AH 中，表示调用 DOS 中断 21h 来显示一个字符
    mov dl,bh   ; 将 BH 寄存器中的值存储到 DL 寄存器中
    int 21h     ; 调用 DOS 中断 21h，将 DL 寄存器中的值显示到屏幕上

    exit:       ; 定义一个标签 exit
    mov ah,4ch  ; 将 4ch 存储到寄存器 AH 中，表示调用 DOS 中断 21h 来退出程序
    int 21h     ; 调用 DOS 中断 21h，退出程序

main endp       ; 定义过程结束
end main        ; 声明程序结束
```

# code2

```x86asm
.code         
main proc      
	mov ax, @data ;将数据段地址加载到AX寄存器中
	mov ds, ax    ;将AX中的地址值传送到DS寄存器中，用来指示数据段地址

	mov ah,2      ;设置AH寄存器为2，表示打印字符功能
	add msg, 48   ;将msg中的第1个字节加上48，将其转换为ASCII码
	mov dl, msg   ;将msg的第1个字节的地址放到DL寄存器中
	int 21h       ;中断21h调用DOS系统功能，将DL中的字符打印到屏幕上

	mov ah, 1     ;设置AH寄存器为1，表示从键盘输入一个字符
	int 21h       ;中断21h调用DOS系统功能，读取键盘输入的字符，并将其传递到AL寄存器中
	mov msg1, al  ;将AL寄存器的内容存储到msg1中

	mov ah, 2     ;设置AH寄存器为2，表示打印字符功能
	mov dl, 10    ;将10的ASCII码放到DL寄存器中，表示换行
	int 21h       ;中断21h调用DOS系统功能，将DL中的字符打印到屏幕上

	mov dl, 13    ;将13的ASCII码放到DL寄存器中，表示回车
	int 21h       ;中断21h调用DOS系统功能，将DL中的字符打印到屏幕上

	mov ah, 2     ;设置AH寄存器为2，表示打印字符功能
	mov dl, msg1  ;将msg1中的内容放到DL寄存器中
	int 21h       ;中断21h调用DOS系统功能，将DL中的字符打印到屏幕上

exit:   
	mov ah, 4ch   ;设置AH寄存器为4ch，表示退出程序
	int 21h       ;中断21h调用DOS系统功能，程序结束

	main endp
	end main      ;结束程序

```

# code3

```x86asm

.model small    ; 定义程序模型为small
.stack 100h     ; 定义程序的堆栈大小为100h

.code           ; 进入代码段

main proc       ; 程序入口，开始定义主过程

mov ah,1        ; 设置ah为1，表示将要读取一个字符
int 21h         ; 调用21h中断，等待用户输入一个字符，并将其返回在al寄存器中
mov bl,al       ; 将al中的值存入bl寄存器中

mov ah,2        ; 设置ah为2，表示将要向控制台输出字符
mov dl,10       ; 将dl设置为10（换行符）
int 21h         ; 调用21h中断，向控制台输出dl寄存器中的值（即换行符）

mov dl,13       ; 将dl设置为13（回车符）
int 21h         ; 调用21h中断，向控制台输出dl寄存器中的值（即回车符）

mov ah,2        ; 设置ah为2，表示将要向控制台输出字符
mov dl,bl       ; 将dl设置为bl寄存器中的值（用户输入的字符）
int 21h         ; 调用21h中断，向控制台输出dl寄存器中的值（即用户输入的字符）

mov ah,2        ; 设置ah为2，表示将要向控制台输出字符
mov dl,10       ; 将dl设置为10（换行符）
int 21h         ; 调用21h中断，向控制台输出dl寄存器中的值（即换行符）

mov dl,13       ; 将dl设置为13（回车符）
int 21h         ; 调用21h中断，向控制台输出dl寄存器中的值（即回车符）

mov ah,1        ; 设置ah为1，表示将要读取一个字符
int 21h         ; 调用21h中断，等待用户输入一个字符，并将其返回在al寄存器中
mov bh,al       ; 将al中的值存入bh寄存器中

mov ah,2        ; 设置ah为2，表示将要向控制台输出字符
mov dl,10       ; 将dl设置为10（换行符）
int 21h         ; 调用21h中断，向控制台输出dl寄存器中的值（即换行符）

mov dl,13       ; 将dl设置为13（回车符）
int 21h         ; 调用21h中断，向控制台输出dl寄存器中的值（即回车符）

mov ah,2        ; 设置ah为2，表示将要向控制台输出字符
mov dl,bh       ; 将dl设置为bh寄存器中的值（用户输入的字符）
int 21h         ; 调用21h中断，向控制台输出dl寄存器中的值（即用户输入的字符）

mov ah,2
```

这个程序是一个简单的命令行程序，它的作用是从用户那里获取两个数字，计算它们的和，并将结果输出到屏幕上。下面是程序的大致步骤：

1. 声明和初始化存储变量的空间，包括输入的两个数字和计算结果等。
2. 获取用户输入的第一个数字并存储到内存中。
3. 打印回车符和换行符，用于在屏幕上打印下一行信息。
4. 获取用户输入的第二个数字并存储到内存中。
5. 将第一个数字和第二个数字相加并存储到内存中。
6. 打印回车符和换行符，用于在屏幕上打印下一行信息。
7. 打印计算结果到屏幕上。
8. 退出程序。

# code4

```x86asm
;Loop and Function Call
include "emu8086.inc"   ;包含emu8086.inc文件，定义了一些宏和程序来简化汇编代码的编写
org    100h            ;指令指针初始地址为100h

.model small           ;定义模型为small
.stack 100h            ;定义堆栈大小为100h  
.data                  ;数据段
        msg db "Loop Concept $"  ;定义msg变量，用于存储字符串
.code                  ;代码段
main proc              ;主过程开始

	mov ax, @data         ;将数据段地址赋值给ax寄存器
	mov ds,ax             ;将ax寄存器中的地址赋值给ds寄存器

	mov ah,9              ;设置ah寄存器的值为9
	lea dx,msg            ;将msg的地址赋值给dx寄存器
	int 21h               ;打印字符串

    call print_nline       ;调用print_nline函数，打印回车换行

	print '-----------------------' ;打印分隔线

	call print_nline       ;再次调用print_nline函数，打印回车换行

	mov cx,26              ;将cx寄存器赋值为26
print "The result is:"   ;打印字符串"The result is:"
call print_nline         ;调用print_nline函数，打印回车换行

	level1:                ;定义标签level1
		mov ah,2            ;将2赋值给ah寄存器
	        mov dl,'A'         ;将字符A赋值给dl寄存器
		int 21h             ;打印字符
		inc dl             ;dl寄存器加1
	loop level1           ;cx寄存器减1，当cx不为0时跳转到level1标签处执行

print_nline:             ;定义函数print_nline
    mov ah,2              ;将2赋值给ah寄存器
	mov dl,10             ;将10赋值给dl寄存器，用于打印回车
	int 21h               ;调用dos中断21h，打印回车换行
	mov dl,13             ;将13赋值给dl寄存器，用于打印换行
	int 21h               ;调用dos中断21h，打印回车换行
	ret                   ;返回函数调用

exit:                   ;定义标签exit
mov ah, 4ch             ;将4Ch赋值给ah寄存器，表示退出程序
int 21h                 ;调用dos中断21h

main endp               ;主过程结束
end main                ;程序结束

include "emu8086.inc" ; 包含emulate8086库
org 100h              ; 指定代码段的开始地址

.model small          ; 定义程序模型
.stack 100h           ; 定义堆栈大小为100h

.data                 ; 数据段
a db "Jump Concept $" ; 定义字符串a
b db "Assembly Language $" ; 定义字符串b
c db "Programming $" ; 定义字符串c

.code                  ; 代码段开始
main proc              ; 声明主过程
	mov ax, @data       ; 把数据段的地址传给寄存器ax
	mov ds,ax           ; 把数据段的地址放到ds寄存器中

	mov ah,9            ; 调用dos的9号功能，显示字符串
	lea dx,a            ; 将字符串a的地址存储到寄存器dx中
	int 21h             ; 中断21h，执行ah寄存器所指向的功能

	call print_nline    ; 调用print_nline函数，输出空行

	jmp n               ; 无条件跳转到标签n，即继续执行下面的语句

m:                     ; 定义标签m，标签名后需带冒号
	call print_nline    ; 调用print_nline函数，输出空行
	mov ah,9            ; 调用dos的9号功能，显示字符串
	lea dx,b            ; 将字符串b的地址存储到寄存器dx中
	int 21h             ; 中断21h，执行ah寄存器所指向的功能

	call print_nline    ; 调用print_nline函数，输出空行
	jmp exit            ; 无条件跳转到标签exit，即跳过下面的语句

n:                     ; 定义标签n
	mov ah,9            ; 调用dos的9号功能，显示字符串
	lea dx,c            ; 将字符串c的地址存储到寄存器dx中
	int 21h             ; 中断21h，执行ah寄存器所指向的功能

	jmp m               ; 无条件跳转到标签m，即执行m后面的语句

print_nline:           ; 定义子过程print_nline
	mov ah,2            ; 将2号功能码存入ah寄存器，表示显示字符
	mov dl,10           ; 将10存入dl寄存器，表示换行符
	int 21h             ; 中断21h，执行ah寄存器所指向的功能
	mov dl,13           ; 将13存入dl寄存器，表示回车符
	int 21h             ; 中断21h，执行ah寄存器所指向的功能
	ret                  ; 返回到调用print_nline函数的指令地址

exit:                  ; 定义标签exit
	mov ah, 4ch         ; 将4ch存入ah寄存器，表示退出程序
	int 21h             ; 中断21h，执行ah寄存器所指向的功能

	main endp               ;主过程结束
	end main                ;程序结束
```

# code5

```x86asm
;Jump
include "emu8086.inc"
org    100h

.model small
.stack 100h
;%%%%%%%%%% DATA SEGMENT START HERE %%%%%%%%%%
.data
        a db "Jump Concept $"  ; a variable to hold a string
	b db "Assembly Language $"  ; b variable to hold a string
	c db "Programming $"  ; c variable to hold a string
;%%%%%%%%% DATA SEGMENT END HERE %%%%%%%%%%%%

;%%%%%%%%%%%% CODE SEGMENT START HERE %%%%%%%
.code
main proc
	mov ax, @data  ; 将数据段地址加载到AX中
	mov ds,ax      ; 设置DS寄存器指向数据段

	mov ah,9       ; Set the function number to display a string
	lea dx,a       ; 将变量a中的字符串地址加载到DX
	int 21h        ; 调用中断21h来显示DX中的字符串
    call print_nline  ; 调用函数print_nline打印新行
    jmp n         ; Jump to function n	

	m:             ; Function m 
	call print_nline ; 调用函数print_nline打印新行
	mov ah,9        ; Set the function number to display a string
	lea dx,b        ;将变量b中的字符串地址加载到DX
	int 21h         ; 调用中断21h来显示DX中的字符串
	call print_nline  ; 调用函数print_nline打印新行
	jmp exit        ; Jump to exit

	n:              ; Function n
	mov ah,9        ; 设置函数号以显示字符串
	lea dx,c        ; 将变量c中的字符串地址加载到DX
	int 21h         ; 调用中断21h来显示DX中的字符串

	jmp m          ; Jump to function m  

print_nline:      ; Function print_nline to print a new line
	mov ah,2        ; Set the function number to display a character
	mov dl,10       ; 设置DL寄存器以保存换行字符的ASCII值
	int 21h         ; 调用中断21h显示换行字符
	mov dl,13       ; 设置DL寄存器以保存回车字符的ASCII值
	int 21h         ; 调用中断21h显示回车符
	ret             ; 从函数返回

exit:             ; Label for exit
	mov ah, 4ch     ; Set the function number to terminate the program
	int 21h         ; Call interrupt 21h to terminate the program

main endp         ; End of the main procedure
end main          ; End of the program

```

# code6

```x86asm
.model small         ; 模型设置为小模型 
.stack 100h          ; 堆栈大小设置为100h 

.data                ; 数据段开始
	a db 'Input First Digit  : $'   ; 存放“请输入第一个数字：”字符串
	b db 10, 13, 'Input Second Digit: $' ; 存放“请输入第二个数字：”字符串
        c db 10, 13, 'Input Third Digit: $'  ; 存放“请输入第三个数字：”字符串
	d db 10, 13, '--------------------$'  ; 存放“--------------------”字符串
	e db 10, 13, 'Result             : $'  ; 存放“结果为：”字符串 

.code                ; 代码段开始 
main proc            ; 主函数开始
	mov ax, @data    ; 将数据段地址存储在AX寄存器中
	mov ds,ax        ; 将数据段地址传递给DS寄存器

	mov ah,9         ; 设置AH寄存器为9，用于显示字符串
	lea dx,a         ; 将字符串a的地址传递给DX寄存器
	int 21h          ; 调用DOS系统功能，显示“请输入第一个数字：”字符串 

	mov ah,1         ; 设置AH寄存器为1，用于读取一个字符
	int 21h          ; 读取一个字符并存储在AL寄存器中
	mov bl,al        ; 将输入的字符存储在BL寄存器中

	mov ah,9         ; 设置AH寄存器为9，用于显示字符串
	lea dx,b         ; 将字符串b的地址传递给DX寄存器
	int 21h          ; 调用DOS系统功能，显示“请输入第二个数字：”字符串 

	mov ah,1         ; 设置AH寄存器为1，用于读取一个字符
	int 21h          ; 读取一个字符并存储在AL寄存器中
	mov bh,al        ; 将输入的字符存储在BH寄存器中

	mov ah,9         ; 设置AH寄存器为9，用于显示字符串
	lea dx,c         ; 将字符串c的地址传递给DX寄存器
	int 21h          ; 调用DOS系统功能，显示“请输入第三个数字：”字符串 

	mov ah,1         ; 设置AH寄存器为1，用于读取一个字符
	int 21h          ; 读取一个字符并存储在AL寄存器中
	mov cl,al        ; 将输入的字符存储在CL寄存器中

	mov ah,9         ; 设置AH寄存器为9，用于显示字符串
	lea dx,d         ; 将字符串d的地址传递给DX寄存器
	int 21h          ; 调用DOS系统功能，显示“--------------------”字符串 

	add bl, bh       ; 将输入的两个字符相加，并存储在BL寄存器中
	sub bl,48        ; 由于ASCII码中0~9的字符编码分别为48~57，因此减去48
	add bl,cl  ; 将第三个数字的 ASCII 码值转换为数值加到前面的结果上
    	sub bl,48  ; 将第一个数字、第二个数字、第三个数字的值相加后，减去 ASCII 码值的偏移量 48，计算出其数值

	mov ah,2   ; 设置输出函数的功能码，即 2（AH=2）
	mov dl,bl  ; 将数值转换为 ASCII 码值
	int 21h    ; 调用 21h 中断，将 ASCII 码值输出到屏幕上

exit:        ; 定义程序的结束点
	mov ah, 4ch ; 设置退出程序的功能码，即 4C（AH=4Ch）
	int 21h    ; 调用 21h 中断，结束程序
	main endp   ; 程序结束点
	end main   ; 终止程序
```

# code7

```x86asm
.model small             ; 定义程序的数据模型为 small
.stack 100h              ; 程序栈的大小为 256 字节

.data                    ; 数据段开始
a db         'Lower form $'  ; 声明一个存放小写字母的字符串 a
b db 10, 13, 'Upper form $'  ; 声明一个存放换行符和大写字母提示信息的字符串 b

.code                    ; 代码段开始

main proc                ; 定义一个过程 main
	mov ax,@data         ; 将数据段的地址放入 ax 寄存器中
	mov ds, ax           ; 将 ax 寄存器的值（数据段地址）放入 ds 寄存器中

	mov ah,2             ; 设置中断号为 2，即显示字符
	lea dx, a            ; 将字符串 a 的地址放入 dx 寄存器中
	int 21h              ; 调用 DOS 中断，显示字符串 a

	mov ah,1             ; 设置中断号为 1，即从键盘读取一个字符
	int 21h              ; 调用 DOS 中断，从键盘读取一个字符
	mov bl, al           ; 将读取到的字符放入 bl 寄存器中

	mov ah,2             ; 设置中断号为 2，即显示字符
	lea dx, a            ; 将字符串 a 的地址放入 dx 寄存器中
	int 21h              ; 调用 DOS 中断，显示字符串 a

	mov ah,2             ; 设置中断号为 2，即显示字符
	sub bl,32            ; 将小写字母转换为大写字母
	mov dl,bl            ; 将转换后的字符放入 dl 寄存器中
	int 21h              ; 调用 DOS 中断，显示转换后的字符

exit:                    ; 定义一个标签 exit，表示程序的结束位置
	mov ah,4ch           ; 设置中断号为 4Ch，表示程序的结束
	int 21h              ; 调用 DOS 中断，结束程序

main endp               ; 定义 main 过程结束
	end main         ; 声明程序结束

```

# code8

```x86asm
.model small    ; 指定程序的内存模型
.stack 100h      ; 指定堆栈大小

.data            ; 数据段开始

a db         'Input first number :  $'   ; 存储字符串 “Input first number :” 并在结尾处添加“$”
b db 10, 13, 'Input Second number:  $'   ; 存储字符串 “Input Second number:” 并在结尾处添加“$”
c db 10, 13, '-------------------:  $'  ; 存储字符串 “-------------------:” 并在结尾处添加“$”
d db 10, 13, 'Largest Number     :  $'  ; 存储字符串 “Largest Number     :” 并在结尾处添加“$”

.code         ; 代码段开始
main proc     ; 程序的主过程

	mov ax, @data   ; 将数据段的地址存储在AX中
	mov ds, ax      ; 将DS寄存器的值设置为AX中存储的数据段地址

	mov ah,9        ; 将AH寄存器的值设为9（显示字符串的功能号）
	lea dx,a        ; 将DX寄存器中存储的a字符串的地址传递给INT 21h
	int 21h         ; 显示字符串 “Input first number :”

	mov ah,1        ; 将AH寄存器的值设为1（读取单个字符的功能号）
	int 21h         ; 读取从键盘输入的单个字符并将其存储在AL寄存器中
	mov bl,al       ; 将AL寄存器中的值传递给BL寄存器

	mov ah,9        ; 将AH寄存器的值设为9（显示字符串的功能号）
	lea dx,b        ; 将DX寄存器中存储的b字符串的地址传递给INT 21h
	int 21h         ; 显示字符串 “Input Second number:”

	mov ah,1        ; 将AH寄存器的值设为1（读取单个字符的功能号）
	int 21h         ; 读取从键盘输入的单个字符并将其存储在AL寄存器中
	mov bh,al       ; 将AL寄存器中的值传递给BH寄存器

	mov ah,9        ; 将AH寄存器的值设为9（显示字符串的功能号）
	lea dx,c        ; 将DX寄存器中存储的c字符串的地址传递给INT 21h
	int 21h         ; 显示字符串 “-------------------:”

biggest:
	cmp bl,bh        ;比较 bl 和 bh 的值
	jg L1            ;如果 bl 大于 bh，则跳转到 L1 标签
	jmp L2           ;否则跳转到 L2 标签

L2: 
	mov ah,9         ;调用 DOS 的 09h 功能，用于打印字符串
	lea dx,d         ;将字符串 d 的地址加载到 DX 寄存器
	int 21h          ;调用 DOS 的 21h 中断，打印字符串

       mov ah,2         ;调用 DOS 的 02h 功能，用于将 AL 的值输出到标准输出
       mov dl,bh        ;将 bh 的值移动到 DL 寄存器
       int 21h          ;调用 DOS 的 21h 中断，将 DL 寄存器中的值输出到标准输出

       jmp exit        ;跳转到 exit 标签

L1:
        mov ah,9         ;调用 DOS 的 09h 功能，用于打印字符串
	lea dx,d         ;将字符串 d 的地址加载到 DX 寄存器
	int 21h          ;调用 DOS 的 21h 中断，打印字符串

       mov ah,2         ;调用 DOS 的 02h 功能，用于将 AL 的值输出到标准输出
       mov dl,bl        ;将 bl 的值移动到 DL 寄存器
       int 21h          ;调用 DOS 的 21h 中断，将 DL 寄存器中的值输出到标准输出
	jmp exit        ;跳转到 exit 标签

exit:
	mov ah, 4ch       ;调用 DOS 的 4ch 功能，程序退出
	int 21h
	main endp         ;主程序过程结束
	end main         ;程序结束

```

# code9

```x86asm
.model small          ; 定义代码模型，这里为 small
.stack 100h           ; 定义堆栈大小

.data                 ; 数据段开始
a db 'Input first number :  $'   ; 存储第一个数字的输入提示信息
b db 10, 13, 'Input Second number:  $'  ; 存储第二个数字的输入提示信息
c db 10, 13, 'Input Third number:  $'   ; 存储第三个数字的输入提示信息
d db 10, 13, '-------------------:  $' ; 存储分割线
e db 10, 13, 'Largest Number     :  $' ; 存储输出最大值的提示信息

.code                 ; 代码段开始
main proc             ; 定义程序入口
	mov ax, @data     ; 将数据段地址存入寄存器 ax
	mov ds, ax        ; 将数据段地址存入 ds 寄存器

	mov ah,9          ; 将字符输出服务的功能号存入寄存器 ah
	lea dx,a          ; 将第一个数字输入提示信息的地址存入寄存器 dx
	int 21h           ; 调用 DOS 的中断 21h 来输出提示信息

	mov ah,1          ; 将字符输入服务的功能号存入寄存器 ah
	int 21h           ; 调用 DOS 的中断 21h 来等待用户输入第一个数字
	mov bl,al         ; 将用户输入的第一个数字存入寄存器 bl 中

	mov ah,9          ; 将字符输出服务的功能号存入寄存器 ah
	lea dx,b          ; 将第二个数字输入提示信息的地址存入寄存器 dx
	int 21h           ; 调用 DOS 的中断 21h 来输出提示信息

	mov ah,1          ; 将字符输入服务的功能号存入寄存器 ah
	int 21h           ; 调用 DOS 的中断 21h 来等待用户输入第二个数字
	mov bh,al         ; 将用户输入的第二个数字存入寄存器 bh 中

	mov ah,9          ; 将字符输出服务的功能号存入寄存器 ah
	lea dx,c          ; 将第三个数字输入提示信息的地址存入寄存器 dx
	int 21h           ; 调用 DOS 的中断 21h 来输出提示信息

	mov ah,1          ; 将字符输入服务的功能号存入寄存器 ah
	int 21h           ; 调用 DOS 的中断 21h 来等待用户输入第三个数字
	mov cl,al         ; 将用户输入的第三个数字存入寄存器 cl 中

	mov ah,9          ; 将字符输出服务的功能号存入寄存器 ah
	lea dx,d          ; 将分割线信息的地址存入寄存器 dx
	int 21h           ; 调用 DOS 的中断 21h 来输出分割线
biggest:
	cmp bl,bh   ; 比较BL和BH寄存器中的值
	jge L1      ; 如果BL的值大于或等于BH的值，跳转到L1
	jmp L2      ; 否则跳转到L2


L1:
	cmp bl,cl   ; 比较BL和CL寄存器中的值
	jge L4      ; 如果BL的值大于或等于CL的值，跳转到L4

	mov ah,9    ; 将AH设置为9，表示将要使用DOS功能号9中的字符串打印服务
	lea dx,e    ; 将DX寄存器设置为e（定义在数据段中的字符串的地址）
	int 21h     ; 调用21h中断（打印字符串）

	mov ah,2    ; 将AH设置为2，表示将要使用DOS功能号2中的字符打印服务
	mov dl,cl   ; 将DL寄存器设置为CL的值
	int 21h     ; 调用21h中断（打印字符）
	jmp exit    ; 跳转到程序结束


L2: 
	cmp bh,cl   ; 比较BH和CL寄存器中的值
	jge L3      ; 如果BH的值大于或等于CL的值，跳转到L3

	mov ah,9    ; 将AH设置为9，表示将要使用DOS功能号9中的字符串打印服务
	lea dx,e    ; 将DX寄存器设置为e（定义在数据段中的字符串的地址）
	int 21h     ; 调用21h中断（打印字符串）

	mov ah,2    ; 将AH设置为2，表示将要使用DOS功能号2中的字符打印服务
	mov dl,cl   ; 将DL寄存器设置为CL的值
	int 21h     ; 调用21h中断（打印字符）
	jmp exit    ; 跳转到程序结束

L3:
	mov ah,9    ; 将AH设置为9，表示将要使用DOS功能号9中的字符串打印服务
	lea dx,e    ; 将DX寄存器设置为e（定义在数据段中的字符串的地址）
	int 21h     ; 调用21h中断（打印字符串）

	mov ah,2    ; 将AH设置为2，表示将要使用DOS功能号2中的字符打印服务
	mov dl,bh   ; 将DL寄存器设置为BH的值
	int 21h     ; 调用21h中断（打印字符）
	jmp exit    ; 跳转到程序结束
L4:    ; 将显示字符串 'Largest Number     :  $' 存储在e变量中
    	mov ah,9
    	lea dx,e
   	 int 21h

   	; 将寄存器ah设置为2，表示进行字符输出，将bl寄存器中存储的最大值打印到控制台
   	mov ah,2
   	mov dl,bl
   	int 21h

   ; 跳转到exit标签，结束程序
   jmp exit
exit:
	mov ah, 4ch
	int 21h
	main endp
	end main


```

# code10

```x86asm
.model small
.stack 100h

.data 

a db         'Input a HEX number :  $'
b db 10, 13, 'Decimal Number     :  $'

.code
main proc
	mov ax, @data ; 将数据段地址赋值给AX寄存器
	mov ds, ax ; 将数据段地址加载到DS寄存器中


	mov ah,9 ; 显示字符串的BIOS功能号为9
	lea dx,a ; 将要显示的字符串的地址存储在DX中
	int 21h ; 调用BIOS中断以显示字符串

	mov ah,1 ; 读取一个字符的BIOS功能号为1
	int 21h ; 调用BIOS中断以读取输入的字符

	mov bl,al ; 将读取到的字符存储在BL寄存器中
	sub bl,17d ; 将BL寄存器的值减去17，将输入的十六进制字符转换成十进制数

	mov ah,9 ; 显示字符串的BIOS功能号为9
	lea dx,b ; 将要显示的字符串的地址存储在DX中
	int 21h ; 调用BIOS中断以显示字符串

    	mov dl,49d ; 将数字字符"1"的ASCII码值存储在DL寄存器中
    	mov ah,2 ; 显示字符的BIOS功能号为2
    	int 21h ; 调用BIOS中断以显示DL寄存器中存储的值

	mov ah,2 ; 显示字符的BIOS功能号为2
	mov dl,bl ; 将转换后的十进制数存储在DL寄存器中
	int 21h ; 调用BIOS中断以显示DL寄存器中存储的值

exit:
	mov ah, 4ch ; 程序终止的BIOS功能号为4Ch
	int 21h ; 调用BIOS中断以退出程序
	main endp ; 主过程结束
	end main ; 指示程序结束

```

# code11

```x86asm
.model small
.stack 100h

.data 

msg db 10, 13, 'Star Relted Problem $' ;声明一个字符串变量，其中包含一条消息

.code

main proc
	mov ax, @data
	mov ds, ax

	mov ah,9
	lea dx, msg ;将字符串变量的地址传递给DX寄存器
	int 21h ;使用21h中断向控制台打印消息

	mov cx,10 ;设置循环次数

L1:  
    mov bx,cx ;将CX的值存储在BX中
    mov cx,5 ;设置内部循环的次数
    L2:
    	 mov ah,2 ;将2存储在AH中，表示要向控制台打印一个字符
    	 mov dl, '*' ;将星号（*）存储在DL中，表示要打印一个星号
     	 int 21h  ;使用21h中断打印星号
     loop L2 ;将CX减1，如果CX不为0，则跳转回L2

    mov ah,2 ;将2存储在AH中，表示要向控制台打印一个字符
    mov dl,10 ;将10存储在DL中，表示要换行
    int 21h ;使用21h中断打印换行符
    mov dl,13 ;将13存储在DL中，表示要将光标移动到行首
    int 21h  ;使用21h中断移动光标

    mov cx,bx ;将BX的值存储在CX中
loop L1 ;将CX减1，如果CX不为0，则跳转回L1

exit:
	mov ah,4ch ;将4C存储在AH中，表示正常程序终止
	int 21h ;使用21h中断终止程序
	main endp ;结束main过程
	end main ;结束程序

```
