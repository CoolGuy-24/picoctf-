# ARMssembly 1

This challenge provided an Assembly file. I recognised it with the .S extension. The contents of the `chall_1.S` file were:
```
	.arch armv8-a
	.file	"chall_1.c"
	.text
	.align	2
	.global	func
	.type	func, %function
func:
	sub	sp, sp, #32
	str	w0, [sp, 12]
	mov	w0, 85
	str	w0, [sp, 16]
	mov	w0, 6
	str	w0, [sp, 20]
	mov	w0, 3
	str	w0, [sp, 24]
	ldr	w0, [sp, 20]
	ldr	w1, [sp, 16]
	lsl	w0, w1, w0
	str	w0, [sp, 28]
	ldr	w1, [sp, 28]
	ldr	w0, [sp, 24]
	sdiv	w0, w1, w0
	str	w0, [sp, 28]
	ldr	w1, [sp, 28]
	ldr	w0, [sp, 12]
	sub	w0, w1, w0
	str	w0, [sp, 28]
	ldr	w0, [sp, 28]
	add	sp, sp, 32
	ret
	.size	func, .-func
	.section	.rodata
	.align	3
.LC0:
	.string	"You win!"
	.align	3
.LC1:
	.string	"You Lose :("
	.text
	.align	2
	.global	main
	.type	main, %function
main:
	stp	x29, x30, [sp, -48]!
	add	x29, sp, 0
	str	w0, [x29, 28]
	str	x1, [x29, 16]
	ldr	x0, [x29, 16]
	add	x0, x0, 8
	ldr	x0, [x0]
	bl	atoi
	str	w0, [x29, 44]
	ldr	w0, [x29, 44]
	bl	func
	cmp	w0, 0
	bne	.L4
	adrp	x0, .LC0
	add	x0, x0, :lo12:.LC0
	bl	puts
	b	.L6
.L4:
	adrp	x0, .LC1
	add	x0, x0, :lo12:.LC1
	bl	puts
.L6:
	nop
	ldp	x29, x30, [sp], 48
	ret
	.size	main, .-main
	.ident	"GCC: (Ubuntu/Linaro 7.5.0-3ubuntu1~18.04) 7.5.0"
	.section	.note.GNU-stack,"",@progbits
```

The description mentioned we needed to find the input which made the program print "You win". So for that I needed to understand the code that is written in this file. 
I decided it would be easier for me to convert this file code into something more readble like C language. So using an onlince ocnverter I converted this assembly code into a C code.

```
#include <stdio.h>
#include <stdlib.h>

int func(int a) {
    int stack[8]; // Simulating stack allocation
    stack[3] = a; // str w0, [sp, 12]
    stack[4] = 85; // str w0, [sp, 16]
    stack[5] = 6; // str w0, [sp, 20]
    stack[6] = 3; // str w0, [sp, 24]

    stack[7] = stack[4] << stack[5]; // lsl w0, w1, w0
    stack[7] = stack[7] / stack[6]; // sdiv w0, w1, w0
    stack[7] = stack[7] - stack[3]; // sub w0, w1, w0

    return stack[7]; // return value
}

int main(int argc, char *argv[]) {
    int input;
    if (argc > 1) {
        input = atoi(argv[1]); // Convert string to integer
    } else {
        return 1; // No input provided
    }

    int result = func(input);
    if (result == 0) {
        puts("You win!");
    } else {
        puts("You Lose :(");
    }

    return 0;
}
```
From this code it becomes clear that the function `func` will return the value at index 7 of the array stack. The calculations performed are:

85 << 6 = 5440

5440/3 = 1813

So therefore a which is the input needs to be 1813 so that the result becomes equal to 0 and the program prints "You win".
Now converting 1813 into hexadecimal and then padding it to 32 bit we get the flag.

`FLAG: picoCTF{00000715}`
