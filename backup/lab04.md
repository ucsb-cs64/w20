---
layout: lab
num: lab04
ready: true
desc: "MIPS Assembly Programming using Branching, Loops, and Memory Access"
assigned: 2019-10-23 14:00:00.00-7
due: 2019-10-30 23:59:59.00-7
---
<div markdown='1'>

<h1>Lab 4: MIPS Assembly Programming using Branching and Loops </h1>
<hr>
<p>Due Wednesday, October 30th at 11:59:59 PM</p>

<h2>Goals for This Week</h2>
<p>By the time you have completed this work, you should be able to:</p>
<ul>
  <li>Use basic arithmetic and control instructions in MIPS assembly</li>
  <li>Write simple loops in MIPS assembly</li>
  <li>Write more complex loops in MIPS assembly</li>
  <li>Write MIPS assembly code that accesses CPU memory</li>
</ul>

<p>
**This is a long lab and can prove to be challenging! We recommend that you work with a partner** (this is optional, of course, and everyone should still submit their own work.)
</p>

<b>Provided files:</b>
<ul>
  <li><a href="{{'/lab/lab04/MedianNumbers.asm' | relative_url }}"><code>MedianNumbers.asm</code></a></li>
  <li><a href="{{'/lab/lab04/factorial.asm' | relative_url }}"><code>factorial.asm</code></a></li>
  <li><a href="{{'/lab/lab04/swap_array.asm' | relative_url }}"><code>swap_array.asm</code></a></li>
</ul>

<b>Documentation:</b>
<ul>
  <li><a href="{{'/lab/documentation/MIPS_reference_card.pdf' | relative_url }}">MIPS Reference Card</a></li>
  <li><a href="{{'/lab/documentation/spim.pdf' | relative_url }}">SPIM Manual</a></li>
  <li><a href="{{'/lab/documentation/mips_instruction_policy.html' | relative_url }}">Grading Policies Regarding MIPS Assembly Instructions</a></li>
</ul>

<hr>
<h2>Step by Step Instructions</h2>
<p>
  There are three tasks that you need to complete for this week, some with multiple steps.
  Strictly speaking, you may complete them in any order, though for this lab it is recommended to go in order.
  The tasks are listed below:
</p>

<ul>
  <li>Task 1: Control Operations</li>
  <li>Task 2: Basic Loops</li>
  <li>Task 3: Intermediate Loops using Memory Access</li>
</ul>

<p>
  You may use any MIPS instructions or psuedoinstructions you want in order to implement these tasks.
  However, you will be somewhat restricted on exams.
  You may want to read the <a href="{{'/lab/documentation/mips_instruction_policy.html' | relative_url }}">grading policies regarding MIPS assembly instructions</a> for more information.
</p>

<p>
  The initial step below describes how to get the files you will need into the appropriate place.
  These files are used for all the different tasks.
</p>

<h3>Initial Step: Create a Directory for This Lab and Copy Over the Files</h3>
<p>After you log in, go into your <code>cs64</code> directory that you created last time:</p>
<pre>
cd cs64
</pre>
<p>Then create a new directory for this lab: <code>lab4</code>:</p>
<pre>
mkdir lab4
</pre>
<p>Then go into that directory.</p>
<p>Now copy over all of the files necessary for this week's tasks:</p>
<pre>
cp ~zmatni/public_html/cs64f19/labs/4/MedianNumbers.asm ~zmatni/public_html/cs64f19/labs/4/factorial.asm ~zmatni/public_html/cs64f19/labs/4/swap_array.asm .
</pre>
<p>
  Note the use of the trailing <code>.</code> in the above command, which stipulates that the specified files should be copied into the current directory.
</p>
  
<h2>Task 1: Control Operations</h2>
<p>
  This task requires you to use branches in MIPS assembly.
  To this end, you will write a MIPS program which will ask the user for three numbers and then print out the median.
  A sample run of this program will look like this, with user input in <b>bold</b>:
</p>
<pre>
Enter the next number:
<b>3</b>
Enter the next number:
<b>5</b>
Enter the next number:
<b>-13</b>
Median: 3
</pre>
<p>
  Your code should be written in the provided <code>MedianNumbers.asm</code> template file.
  Be sure that your output matches <i>exactly</i> with the output above.
</p>
<p>
  Note that you do not need to use a complex sorting algorithm because you are only comparing exactly 3 numbers, not some arbitrary number of numbers.
  A good development strategy here is to write a small program in C/C++ that will behave the same way as the program above, and to test it out.
  From there, it can be ported to assembly, which should be simpler than directly writing in assembly (considering that you are just starting to write in assembly).
  Try to write as simple of C/C++ code as possible, as ultimately any complexity in C/C++ will almost certainly translate to complexity in assembly.
</p>
<p>
  Run your own tests on this program BEFORE submitting it. *hint*: Try every concievable position for the middle number, in other words, try entering 1, 2, 3 (ans: 2), then 2, 1, 3 (ans: also 2), then 3, 1, 2, then 3, 2, 1, etc... Try it with all sorts of numbers: positives, negatives, zeros.
</p>

<h2>Task 2: Basic Loops</h2>
<p>
  This task requires you to write a basic loop in MIPS assembly.
  To this end, you will implement the <a href="https://en.wikipedia.org/wiki/Factorial">factorial function</a> iteratively (i.e., <b>without</b> using recursion), which will take as an input some number gathered from the user.
  C++ code showing how to do this is shown below:
</p>

```cpp
    int n, fn=1;
    cout << "Enter the number:\n";
    cin >> n;
    for (int x = 2; x <= n; x++) {
        fn = fn * x; }
    cout << "Factorial is:\n" << fn << "\n";
```

<p>
  A sample run of the program on input <code>1</code> is shown below, with user input in <b>bold</b>:
</p>
<pre>
Enter the number:
<b>1</b>
Factorial is:
1
</pre>
<p>
  A second run of this program on input <code>0</code> is shown below, with user input in <b>bold</b>:
</p>
<pre>
Enter the number:
<b>0</b>
Factorial is:
1
</pre>
<p>
  A third run of this program on input <code>5</code> is shown below, with user input in <b>bold</b>:
</p>
<pre>
Enter the number:
<b>5</b>
Factorial is:
120
</pre>
<p>
  You should write your program in the provided <code>factorial.asm</code> template file.
</p>
<p>
  For any credit, your solution's output <b>must</b> match the above output <i>exactly</i>. While you may write your own algorithm to do this, it must be <b>iterative</b>; that is, you may <b>not</b> use recursion. <b>IF YOU USE RECURSION, YOU WILL GET A ZERO ON THIS PART OF THE ASSIGNMENT!</b>
  You may assume that the user will only input non-negative numbers, and that no multiplication will lead to overflow.
  You will be working only with unsigned integers for this task. 
  </p>
  <p>
  As with the previous task, run your own tests on this program BEFORE submitting it. 
</p>

<h2>Task 3: Loops with Memory Access</h2>
<p>
  In this task, you will swap values around from within an array.
  In order to allow us to produce different test cases, the main code is separate from your code.
  We will supply a different main file depending on what we want the initial values to be.
</p>

<h3>Step 0: A Note About <code>add</code>/<code>addi</code> versus <code>addu</code>/<code>addiu</code></h3>
<p>
  Recall that <code>add</code>/<code>addi</code> will raise a processor-level exception (for the purposes of this class, a fatal error) in the event that the addition sets the overflow bit.
  In contrast, <code>addu</code>/<code>addiu</code> (where “<code>u</code>” is short for “unsigned”) will still set the overflow bit, but they will ignore its value.
  The behavior of <code>add</code>/<code>addi</code> makes sense if we are dealing with signed numbers in two’s complement, and the behavior of <code>addu</code>/<code>addiu</code> makes sense if we are dealing with unsigned numbers, which do not have a concept of overflow (that is, it’s impossible to get a result of an incorrect sign in a context where everything is implicitly either zero or positive).
</p>
<p>
  The above distinction is important when dealing with memory.
  Memory addresses are inherently unsigned; there is no such thing as a negative address.
  As such, when you manipulate memory addresses (as you would need to do in order to translate <code>myArray[x]</code> to MIPS assembly), you should be using <code>addu</code>/<code>addiu</code>, <b>not</b> <code>add</code>/<code>addi</code>.
  The signed variants (<code>add</code>/<code>addi</code>) will often produce the same result, but if we start dealing with very large addresses, then suddenly the processor might experience an overflow error in a nonsensical context.
</p>
<p>
  It is quite possible, and even common, to need to have <i>both</i> the signed and unsigned variants of <code>add</code> in the same program.
  For example, consider the following snippet of C-like code, where semantically we should provide an error if signed integer overflow occurs:
</p>

```cpp
int* arr = ...; // initialize arr to some valid value
int temp = arr[x] + arr[y];
```

<p>
  In the above snippet of code, we would need the unsigned variants of <code>add</code> (that is, <code>addu</code>/<code>addiu</code>) in order to grab both <code>arr[x]</code> and <code>arr[y]</code>.
  However, in order to perform the addition itself (that is, <code>+</code>), we need to use the signed variant of <code>add</code> (that is, <code>add</code>/<code>addi</code>).
  To help clarify this, keep in mind that <code>arr[x]</code> is shorthand for <code>*(arr + x)</code>, where <code>arr</code> is a pointer (it holds a memory address).
  As such, <code>arr + x</code> is adding together items of types <code>int*</code> (a pointer) and <code>x</code> (an unsigned integer), which denotes the calculation of a new memory address.
  As this is a calculation for a memory address, and memory addresses are unsigned, we use <code>addu</code>/<code>addiu</code>.
  However, for the addition that takes place in the original code (that is, <code>arr[x] <b>+</b> arr[y]</code>), this is adding together two values of type <code>int</code>, a signed integer.
  As such, in this case, we are dealing with signed integer arithmetic, hence we use <code>add</code>/<code>addi</code> for this addition.
</p>


<h3>Step 1: Familiarize Yourself With the Code</h3>
<p>
  Open the file <code>swap_array.asm</code>.
  In the <code>.data</code> section, a number of prompts have been defined, along with an array named <code>myArray</code> which you will modify the contents of.
  In the <code>.text</code> section, some code for running tests is in place, along with a function stub named <code>doSwap</code>, which you will define.
  We have not fully discussed functions yet, and so this might be a little confusing. Do not worry about function implementation for this exercise since the 'hooks' have been placed for you. **All** you have to do is write the code. We will go into much more detail with function implementations in the following week in lecture.

  The restrictions are that you may only use registers <code>$v0 - $v1</code>, <code>$t0 - $t7</code>, and <code>$a0 - $a3</code>.
  Additionally, the last line of each function may not be removed (which is always <code>jr $ra</code>).
</p>

<h3>Step 2: Implement <code>doSwap</code></h3>
<p>
  Now look at the stub for <code>doSwap</code>, which contains a snippet of C/C++ code in the comments which you must implement.
  This snippet is duplicated below for convenience:
</p>

```cpp
unsigned int x = 0;
unsigned int y = 8;

while (x != 4) {
  int temp = myArray[x];
  myArray[x] = myArray[y];
  myArray[y] = temp;
  x++;
  y--;
}
```

<p>
  Your assembly code must do the same thing as the above C/C++ code.
  <b>Make sure your code does not depend on initial values.</b>
  While you may assume that <code>myArray</code> will always contain exactly 9 elements, you can make no assumptions regarding what values these are.
  Remember that the program we run it on will have different global declarations.
</p>

<p>
  In addition, keep in mind that the point made regarding the practical distinction between <code>add</code>/<code>addi</code> and <code>addu</code>/<code>addiu</code> in the previous section is relevant for this task. 
  Correct implementations <b>must</b> utilize <b>both</b> forms, and in the proper manner (that is, <code>addu</code>/<code>addiu</code> for memory addresses and other unsigned things, and <code>add</code>/<code>addi</code> for signed values).
</p>

<p>
  For testing, the code in <code>main</code> will ultimately use your <code>doSwap</code> implementation, and it features a built-in correctness check.
  If you would like to test on other array contents, feel free to change the values of <code>myArray</code> (keeping sure to keep it exactly 9 elements long).
  If you do change the values in <code>myArray</code>, be sure to also change the corresponding values in <code>expectedMyArray</code>, which holds what the result should be.
  When it comes to your implementation, do <b>not</b> simply programmatically copy the values in <code>expectedMyArray</code> into <code>myArray</code>; while this will appear to work on your end, on our end the values in <code>expectedMyArray</code> will not sync up with <code>myArray</code> as it does in your code, so this would end up always giving the wrong result on our end.
</p>

<p>
  While we provide an array in the file, **your code should work on any arbitrary array.** 
  On our end, for testing purposes we may use different arrays, so your code should work with any other valid (non-empty) array.
</p>


<h2>Turn in Everything Using Gradescope</h2>
You are going to turn in THREE (3) things into Gradescope: the 3 completed .asm files.
Navigate to the Lab assignment **lab04** on Gradescope and upload both files. *Every student must upload their own code*.

</div>
<hr>
<blockquote>
<p><font size="1">
Copyright 2019, Ziad Matni, CS Dept, UC Santa Barbara. Permission to copy for non-commercial, non-profit, educational purposes granted, provided appropriate credit is given;  all other rights reserved
</font></p> 
</blockquote>
