---
layout: lab
num: lab05
ready: true
desc: "Functions in MIPS"
assigned: 2020-02-06 08:00:00.00-7
due: 2020-02-14 23:59:59.00-7
---

# Lab 5: Functions in MIPS

**Due Friday, February 14th at 11:59:59 PM**

***Yes, you have extra time to submit this lab!***

## Goals for This Week

By the time you have completed this work, you should be able to call a predefined function properly.

**Provided files:**

[conversion.asm](/w20/lab/lab05/conversion.asm)

[print_array.asm](/w20/lab/lab05/print_array.asm)

[routines.asm](/w20/lab/lab05/routines.asm)

**Documentation:**

[MIPS Reference Card](/w20/lab/documentation/MIPS_reference_card.pdf)

[SPIM Manual](/w20/lab/documentation/spim.pdf) 

[Grading Policies Regarding MIPS Assembly Instructions](/w20/lab/documentation/mips_instruction_policy.html)


## Step by Step Instructions

You will perform 3 tasks. You may complete them in any order, though it is recommended to start with Task 1.
You may use any ***approved*** MIPS instructions or psuedoinstructions you want in order to implement these tasks.
The initial step below describes how to get the files you will need into the appropriate place.

Remember that when writing assembly code for functions to always put the arguments into $a0/$a1 registers and the return into the $v0. Look at the instructions below for further hints.


### Initial Step: Create a Directory for This Lab and Copy Over the Files

After you log in, go into your <code>cs64</code> directory that you created last time. Then create a new directory for this lab: <code>lab5</code> and then go into that directory. Finally, copy over all of the files necessary for this week's tasks:

```bash
cp ~zmatni/public_html/cs64w20/labs/5/* .

chmod +x ./*
```

Note the use of the trailing <code>.</code> in the above command, which stipulates that the specified files should be copied into the current directory. Also note that you may have to change file permissions once you copy them over using the <code>chmod</code> command.

### Task 1: Conversion Program

You will write a MIPS assembly program that mimics this C++ code:

```cpp
int conv(int x, int y){
    int z = 0;
    for (int i = 0; i < 5; i++)
    {
        z = z + 2*x - y;
        if (x >= 3)
            y -= 1;
        x += 1;
    }
    return z;
}

int main(){
    int a = 5, b = 7;
    int c = conv(a, b);
    std::cout << c;
}
```

Given: main does not have any variables in $s registers.

A skeleton assembly program that you will complete to write your code is available to you in the **conversion.asm** file.

### Task 2: Print Array

You will write a MIPS assembly program that mimics this C++ code:

```cpp
void printA(int a[], int al){
    for (int i = 0; i < al; i++)
        std::cout << a[i] << "\n";
}

int main(){
    int arr[10] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    int alength = 10;
    std::cout << "The contents of the array are:\n";
    printA(arr, alength);
}
```

Given: main does not have any variables in $s registers.

A skeleton assembly program that you will complete to write your code is available to you in the **print_array.asm** file.

### Task 3: Nested Functions

You will write a MIPS assembly program that mimics this C++ code:

```cpp
int routineB(int r){
    return (r-5)*4;
}
int routineA(int x, int y){
    int s1 = 2*x + routineB(3*y);
    return routineB(s1 - 1);
}
int main(){
    int a = 5, b = 7;
    int s0 = routineA(a,b);
    std::cout << s0;
}
```

Given: The variable s0 in main must be placed in register $s0 and variable s1 in routineA() must be placed in register $s1.

Hint: Note that this is a nested function example - proceed with your knowledge of the MIPS Calling Convention.

A skeleton assembly program that you will complete to write your code is available to you in the **routines.asm** file.

## Turn in Everything Using Gradescope
You are going to turn in THREE files into Gradescope.
Navigate to the Lab assignment **lab05** on Gradescope and upload both files. *Every student must upload their own code*.

<hr>
<blockquote><font size="1">
Copyright 2020, Ziad Matni, CS Dept, UC Santa Barbara. Permission to copy for non-commercial, non-profit, educational purposes granted, provided appropriate credit is given;  all other rights reserved

