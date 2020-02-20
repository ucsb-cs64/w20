---
layout: lab
num: lab06
ready: true
desc: "MIPS Instructions & MIPS Calling Convention"
assigned: 2020-02-20 08:00:00.00-7
due: 2020-02-27 23:59:59.00-7
---

# Lab 6: MIPS Instructions & MIPS Calling Convention

**Due Thursday, February 27th at 11:59:59 PM**

This is a challenging lab, so plan accordingly.

## Goals for This Week

By the time you have completed this work, you should be able to:

<ul>
  <li>Understand how to use bitwise operations to decode a MIPS instruction</li>
  <li>Call a predefined function properly, using the MIPS calling convention</li>
  <li>Define your own functions, in accordance with the MIPS calling convention</li>
</ul>

**Provided files:**

[DecodeCode.c](/w20/lab/lab06/DecodeCode.c)

[DecodeCode.h](/w20/lab/lab06/DecodeCode.h)

[DecodeCodeTester.c](/w20/lab/lab06/DecodeCodeTester.c)

[DecodeMain.c](/w20/lab/lab06/DecodeMain.c)

[functions.asm](/w20/lab/lab06/functions.asm)

[functions_testing_stub.asm](/w20/lab/lab06/functions_testing_stub.asm)

[functions_tester.pl](/w20/lab/lab06/functions_tester.pl)

[iterative_max.asm](/w20/lab/lab06/iterative_max.asm)

[iterative_max_testing_stub.asm](/w20/lab/lab06/iterative_max_testing_stub.asm)

[iterative_max_tester.pl](/w20/lab/lab06/iterative_max_tester.pl)

**Documentation:**

[MIPS Reference Card](/w20/lab/documentation/MIPS_reference_card.pdf)

[SPIM Manual](/w20/lab/documentation/spim.pdf) 

[Grading Policies Regarding MIPS Assembly Instructions](/w20/lab/documentation/mips_instruction_policy.html)

[MIPS Calling Convention --- READ THIS!!](/w20/lab/documentation/callingconvention/calling_convention.html)


## Step by Step Instructions

  You will perform two tasks for this week, some with multiple steps.
  You may complete them in any order, though it is recommended to start with Task 1, as Task 2 assumes you already understand Task 1.
  The tasks are listed below:

<ul>
  <li>Task 1: Using Bitwise Operations in C/C++ to Decode a MIPS Instruction</li>
  <li>Task 2: Implement the <code>PrintReverse</code> Function (uses MIPS Calling Convention)</li>
  <li>Task 3: Implement the <code>IterativeMax</code> Function (uses MIPS Calling Convention)</li>
</ul>

  You may use any approved MIPS instructions or psuedoinstructions you want in order to implement these tasks.
  You may want to read the ***grading policies regarding MIPS assembly instructions*** (see Documentation above) for more information.

  Both of these tasks require you to follow the ***MIPS calling convention*** (again, see Documentation above).
  **Be sure to actually follow the calling convention; solutions which do not follow the MIPS calling convention will receive no credit!**

  The initial step below describes how to get the files you will need into the appropriate place.

### Initial Step: Create a Directory for This Lab and Copy Over the Files
After you log in, go into your <code>cs64</code> directory that you created last time. Then create a new directory for this lab called **lab6** and cd into that directory. Now copy over all of the files necessary for this week's tasks:

```bash
cp ~zmatni/public_html/cs64w20/labs/6/* .

chmod +x ./*
```

  Note the use of the trailing <code>.</code> in the above command, which stipulates that the specified files should be copied into the current directory. Also note that you may have to change file permissions once you copy them over using the <code>chmod</code> command.

### Task 1: Instruction Decoding

 Processor simulators are used to evaluate implementation ideas long before processors are fabricated.
 These simulators read in  compiled programs and execute them, performing the functions and reporting performance statistics for the theoretical processor. They are written in high-level languages such as C and C++.

 You are going to write one function in <code>DecodeCode.c</code> - a function that divides an instruction into its parts.
 An instruction is a single 32-bit value in which many smaller values have been packed together.
 The instruction format is in your textbook and on the MIPS Reference Card (and in your lecture notes).

 You do not need to read any of the text around it - all we care about is extracting fields <code>opcode</code>, <code>rs</code>, <code>rt</code>, <code>rd</code>, <code>immediate</code>, and <code>funct</code> (function code).
 Bit positions are expressed in an inclusive manner (e.g., bits 0 - 5 mean that all 6 bits are in the field).


 You can look at your code that you wrote in <code>RandomCode.c</code> - this will be very useful to you.
 Fill in the lines of code in <code>DecodeCode.c</code> that extract each set of bits.
 Be mindful of whether it wants the answer expressed as a signed integer or  an unsigned integer.

<ul>
 <li><code>funct</code>: bits 0-5 (unsigned)</li>
 <li><code>immediate</code>: bits 0-15 (signed)</li>
 <li><code>rd</code>: bits 11-15 (unsigned)</li>
 <li><code>rt</code>: bits 16-20 (unsigned)</li>
 <li><code>rs</code>: bits 21-25 (unsigned)</li>
 <li><code>opcode</code>: bits 26-31 (unsigned)</li>
</ul>


 I have provided three files, only one of which you will turn in. You are free to edit either <code>.c</code> file, but you may not change the <code>.h</code> file (for if you do, it will not compile when it gets turned in).

Once again, list the files you will be using:

```bash
ls Decode*
```

You should see three files: <code>DecodeCode.c</code>, <code>DecodeCode.h</code>, and <code>DecodeMain.c</code>.
To compile this code, you do the following:

```bash
gcc DecodeCode.c DecodeMain.c
```

Now you are ready to fill in the code!  Edit <code>DecodeCode.c</code>.

 Remember that you are only allowed to use bitwise operations to extract bits.
 You may not use multiplication or division.
 You may use an <code>if</code> statement for signed operations.

 Specifically for this portion, we have also provided <code>DecodeCodeTester.c</code>, which contains a small test suite which may be of interest to you.
 Instructions for compiling with the test suite, along with running it, are directly in <code>DecodeCodeTester.c</code>.
 In addition, <code>DecodeMain.c</code> contains code for testing with more tests; see <code>DecodeMain.c</code> for details.
 Note that this is **not** intended as a comprehensive test suite, but is instead there to make sure you are on the right track.
 You are encouraged to add your own tests to this suite.

## Task 2: Implement the <code>PrintReverse</code> Function

  For this task, you will implement the <code>PrintReverse</code> function in <code>functions.asm</code> using the MIPS calling convention.
  <code>PrintReverse</code> takes two arguments:

<ol>
  <li>The address of an array of word-long (four byte) signed integers, held in <code>$a0</code>.</li>
  <li>The length of the array as an unsigned integer, held in <code>$a1</code>.</li>
</ol>

  The function should print the provided array in reverse order.
  For example, if given:

<pre>1 2 3</pre>
...the function should print:
<pre>3 2 1</pre>

  In addition to printing out the elements in reverse order, you must call another **provided** function named <code>ConventionCheck</code> each time you print out an element.
  **Do not implement <code>ConventionCheck</code> youself, or modify it in any way.**
  On our end, we are going to use our own version of <code>ConventionCheck</code> while grading, so the only assumptions you can make about <code>ConventionCheck</code> are that it will follow the MIPS calling convention.

  While we provide an array in the file, your code should work on any arbitrary array.
  On our end, for testing purposes we will use different arrays, so your code should work with any other valid (non-empty) array.

The <code>main</code> function provided in <code>functions.asm</code> calls <code>PrintReverse</code> on your behalf, and it will display the contents of the array in non-reversed order **before and after** calling <code>PrintReverse</code>.

  Your output should have the format shown below.
  Note that the specific numbers used in the output differ from the numbers in your file; the important part is not what the absolute numbers are, but that the resulting output displays the numbers properly with respect to the particular input.
  The first two lines and the last line are generated by the <code>main</code> function, so you do not have to implement anything to print those portions out.
  The lines containing the words &ldquo;<code>Convention Check</code>&rdquo; are produced by the <code>ConventionCheck</code> function you must call after printing each input.

```
Current Array:
0 1 -1 5 32 6 -66 33 12 58 -4 64 
64
Convention Check
-4
Convention Check
58
Convention Check
12
Convention Check
33
Convention Check
-66
Convention Check
6
Convention Check
32
Convention Check
5
Convention Check
-1
Convention Check
1
Convention Check
0
Convention Check
0 1 -1 5 32 6 -66 33 12 58 -4 64
```

  Remember to follow the MIPS calling convention while implementing your <code>PrintReverse</code> function.
  Otherwise, the program may **crash hard**, and will receive **no credit**.



  **Hint:** Use &ldquo;<code>jal label</code>&rdquo; to call other functions, replacing <code>label</code> with the name of the function you want to call.
  For example, if you want to call the <code>ConventionCheck</code> function, then you ultimately need to use the following code snippet:

<pre>
jal ConventionCheck
</pre>

  In order to test your code, you may use the provided <code>functions_tester.pl</code> script on <code>csil</code>, like so:

<pre>
./functions_tester.pl
</pre>


## Task 3: Implement the <code>IterativeMax</code> Function

  In this task, you will implement the <code>IterativeMax</code> function in <code>iterative_max.asm</code> using the MIPS calling convention.
  <code>IterativeMax</code> take two arguments:

<ol>
  <li>The address of an array of word-long (four byte) signed integers, held in <code>$a0</code>.</li>
  <li>The length of the array as an unsigned integer, held in <code>$a1</code>.</li>
</ol>

  The main purpose of the function is to determine which element of the provided array is the largest (i.e., the maximum element in the array).
  This is achieved by going through the array one element at a time.
  On each element, the function should do the following, in order:

<ol>
  <li>Print out the current element of the array</li>
  <li>
    Determine what the new maximal element of the array is so far.
    For example, if the old maximum was <code>5</code> and <code>7</code> was just observed in the array, then the maximum should be set to <code>7</code>.
  </li>
  <li>Print out the new maximum element of the array so far (after setting the new maximum in the previous step)</li>
  <li>Call the <code>ConventionCheck</code> function, to help make sure the proper MIPS calling convention is being followed</li>
</ol>

  **Do not implement <code>ConventionCheck</code> youself, or modify it in any way.**
  On our end, we are going to use our own version of <code>ConventionCheck</code> while grading, so the only assumptions you can make about <code>ConventionCheck</code> are that it will follow the MIPS calling convention.


  While we provide an array in the file, your code should work on any arbitrary array.
  On our end, for testing purposes we will use different arrays, so your code should work with any other valid (non-empty) array.

The <code>main</code> function provided in <code>iterative_max.asm</code> calls <code>IterativeMax</code> on your behalf, and it will display the contents of the array in non-reversed order **before and after** calling <code>IterativeMax</code>.

  Your output should have the format shown below.
  Note that the specific numbers used in the output differ from the numbers in your file; the important part is not what the absolute numbers are, but that the resulting output displays the numbers properly with respect to the particular input.
  The first two lines and the last line are generated by the <code>main</code> function, so you do not have to implement anything to print those portions out.
  The lines containing the words &ldquo;<code>Convention Check</code>&rdquo; are produced by the <code>ConventionCheck</code> function you must call after printing each input.

```
Current Array:
0 1 -1 5 32 6 -66 33 12 58 -4 64 
0
0
Convention Check
1
1
Convention Check
-1
1
Convention Check
5
5
Convention Check
32
32
Convention Check
6
32
Convention Check
-66
32
Convention Check
33
33
Convention Check
12
33
Convention Check
58
58
Convention Check
-4
58
Convention Check
64
64
Convention Check
0 1 -1 5 32 6 -66 33 12 58 -4 64
```

  Remember to follow the MIPS calling convention while implementing your <code>IterativeMax</code> function. Otherwise, the program may **crash hard**, and will receive **no credit**.

  You may assume that the provided array will always be non-empty. That is, it is guaranteed that the provided array will always contain at least one element.

  Some **hints** follow, which you may or may not find useful:

<ul>
  <li>
    One way of initializing things is to set the initial maximum to the first element of the array, and then iterate over the array starting from the second element.
    However, this would require some extra steps in order to get the same output as above.
    As such, a simpler strategy may be to set the initial value to the most negative possible signed integer, and start iterating from the first element.
    As the array is guaranteed to contain at least one element, this is safe; the only way this most negative possible signed integer could be returned is if the array contains only this element.
  </li>
  <li>
    
 Use &ldquo;<code>jal label</code>&rdquo; to call other functions, replacing <code>label</code> with the name of the function you want to call.
 For example, if you want to call the <code>ConventionCheck</code> function, then you ultimately need to use the following code snippet:
    
<pre>
jal ConventionCheck
</pre>
  </li>
</ul>
  
 In order to test your code, you may use the provided <code>iterative_max_tester.pl</code> script on <code>csil</code>, like so:

<pre>
./iterative_max_tester.pl
</pre>

## Turn in Everything Using Gradescope

You are going to turn in THREE files into Gradescope.
Navigate to the Lab assignment **lab06** on Gradescope and upload both files. *Every student must upload their own code*.


<hr>
<blockquote><font size="1">
Copyright 2020, Ziad Matni, CS Dept, UC Santa Barbara. Permission to copy for non-commercial, non-profit, educational purposes granted, provided appropriate credit is given;  all other rights reserved
</font></blockquote>
