# Week 4


**4.5 Lab Tasks**

1. Write a program that asks the user to enter an integer and then displays the number of 1’s in the binary representation of that integer. For example, if the user enters **9**, then the program should display **2**.

2. Write a program that asks the user to enter two integers: **n1** and **n2** and prints the sum of all numbers from **n1** to **n2**.
   For example, if the user enters **n1 = 3** and **n2 = 7**, then the program should display the sum as **25**.

3. Write a program that asks the user to enter an integer and then display the **hexadecimal** representation of that integer.

4. The Fibonacci sequence is:
   **0, 1, 1, 2, 3, 5, 8, 13, 21, 34, ...**
   Each number is the sum of the previous two.
   Write a program that asks the user to enter a positive number **n** and prints the **n-th** Fibonacci number.

---

# **Task 1 — Count Number of 1’s in Binary**

```mips
.data
name: .asciiz "Program by: Muhammad Qasim\n"
ask: .asciiz "Enter an integer: "
out: .asciiz "Number of 1's in binary = "

.text
main:
    # Print Name
    li $v0, 4
    la $a0, name
    syscall

    # Ask input
    li $v0, 4
    la $a0, ask
    syscall

    # Read integer
    li $v0, 5
    syscall
    move $t0, $v0       # t0 = number

    li $t1, 0           # count = 0

loop:
    beq $t0, $zero, print   # stop when number = 0
    andi $t2, $t0, 1        # get last bit
    add $t1, $t1, $t2       # count += last bit
    srl $t0, $t0, 1         # shift right
    j loop

print:
    li $v0, 4
    la $a0, out
    syscall

    li $v0, 1
    move $a0, $t1
    syscall

    li $v0, 10
    syscall
```

---

# **Task 2 — Sum from n1 to n2**

```mips
.data
name: .asciiz "Program by: Muhammad Qasim\n"
msg1: .asciiz "Enter n1: "
msg2: .asciiz "Enter n2: "
msg3: .asciiz "Sum = "

.text
main:
    # Print Name
    li $v0, 4
    la $a0, name
    syscall

    # Read n1
    li $v0, 4
    la $a0, msg1
    syscall

    li $v0, 5
    syscall
    move $t0, $v0   # n1

    # Read n2
    li $v0, 4
    la $a0, msg2
    syscall

    li $v0, 5
    syscall
    move $t1, $v0   # n2

    li $t2, 0       # sum = 0

add_loop:
    bgt $t0, $t1, show_sum
    add $t2, $t2, $t0
    addi $t0, $t0, 1
    j add_loop

show_sum:
    li $v0, 4
    la $a0, msg3
    syscall

    li $v0, 1
    move $a0, $t2
    syscall

    li $v0, 10
    syscall
```

---

# **Task 3 — Display Hexadecimal**

```mips
.data
name: .asciiz "Program by: Muhammad Qasim\n"
msg: .asciiz "Enter number: "
hexmsg: .asciiz "Hex value: "

.text
main:
    # Print Name
    li $v0, 4
    la $a0, name
    syscall

    # Ask input
    li $v0, 4
    la $a0, msg
    syscall

    li $v0, 5
    syscall
    move $a0, $v0       # number to a0

    li $v0, 4
    la $a0, hexmsg
    syscall

    li $v0, 34          # print integer in HEX
    move $a0, $v0
    syscall

    li $v0, 10
    syscall
```

---

# **Task 4 — Fibonacci Number**

```mips
.data
name: .asciiz "Program by: Muhammad Qasim\n"
msg: .asciiz "Enter n: "
ans: .asciiz "Fibonacci = "

.text
main:
    # Print Name
    li $v0, 4
    la $a0, name
    syscall

    # Ask input
    li $v0, 4
    la $a0, msg
    syscall

    li $v0, 5
    syscall
    move $t0, $v0       # n

    li $t1, 0           # fib0
    li $t2, 1           # fib1

    blt $t0, 1, print0

    li $t3, 2           # i = 2

loop:
    bgt $t3, $t0, done
    move $t4, $t1       # temp
    move $t1, $t2       # fib0 = fib1
    add $t2, $t2, $t4   # fib1 = fib1 + temp
    addi $t3, $t3, 1
    j loop

done:
    move $t5, $t2
    j show

print0:
    move $t5, $t1

show:
    li $v0, 4
    la $a0, ans
    syscall

    li $v0, 1
    move $a0, $t5
    syscall

    li $v0, 10
    syscall
```
---
