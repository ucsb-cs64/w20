---
layout: lab
num: lab02
ready: true
desc: "Binary Arithmetic, Bitwise Operators, and MIPS"
assigned: 2020-01-16 09:00:00.00-7
due: 2020-01-21 23:59:59.00-7
---
<div markdown='1'>

<h1>Lab 2: Binary Arithmetic, Bitwise Operators, and MIPS</h1>
<hr>
<p>Due Tuesday, January 21st at 11:59:59 PM</p>

<h2>Goals for This Week</h2>
<p>By the time you have completed this work, you should be able to:</p>
<ul>
 <li>Perform bitwise operations</li>
 <li>Know <i>when</i> and <i>how</i> you use bitwise operators in high-level code</li>
 <li>Get an introduction to MIPS and the <a href="http://spimsimulator.sourceforge.net/">SPIM simulator</a></li>
</ul>

**Provided files:**
<ul>
 <li><a href="{{'/lab/lab02/lab02.pdf' | relative_url }}"><code>lab02.pdf</code></a></li>
 <li><a href="{{'/lab/lab02/RandomCode.h' | relative_url }}"><code>RandomCode.h</code></a></li>
 <li><a href="{{'/lab/lab02/RandomCode.c' | relative_url }}"><code>RandomCode.c</code></a></li>
 <li><a href="{{'/lab/lab02/RandomMain.c' | relative_url }}"><code>RandomMain.c</code></a></li>
 <li><a href="{{'/lab/lab02/RandomCodeTester.c' | relative_url }}"><code>RandomCodeTester.c</code></a></li>
 <li><a href="{{'/lab/lab02/mipsdemo.asm' | relative_url }}"><code>mipsdemo.asm</code></a></li>
</ul>

**Documentation:**
<ul>
 <li><a href="{{'/lab/lab02/documentation/spim.pdf' | relative_url }}">SPIM Manual</a></li>
</ul>

<hr>
<h2>Step by Step Instructions</h2>
<p>
 The initial step below describes how to get the files you will need into the appropriate place.
 These files are used for all the different tasks.
</p>

<h3>Initial Step: Create a Directory for This Lab and Copy Over the Files</h3>
<p>After you log in, go into your <code>cs64</code> directory that you created last time:</p>
```
cd cs64
```

<p>Then create a new directory for this lab: <code>lab2</code>:</p>
```
mkdir lab2
```

<p>Then go into that directory.</p>
<p>Now copy over all of the files necessary for this week's tasks (there are 6 in total): </p>
```
cp ~zmatni/public_html/cs64w20/labs/2/* .
```

<p>
UNIX NOTES: Note the use of the asterix (*) as glob/macro, which specifies that all files of a given form should be chosen (e.g. <code>ls *c</code> will list all files that end in 'c'). Also note the use of the trailing <code>.</code> at the end of the above command, which stipulates that the specified files should be copied into the current directory.
</p>

<p>
You may need to change permissions on the files you just copied over (sometimes students have said that copying files over from other users only results in files that are read-only and thus not editable). You can do that with the UNIX command (done inside your lab2 subdirectory):
</p>

```
chmod 664 *
```

<p>You have THREE (3) main tasks and each has it's sub-tasks or problems. They are as follows: </p>
* Do the 27 problems in the lab02.pdf file. Submit your PDF file with solutions to Gradescope.
* Do the Bitwise Operations in C/C++ problems described below. Submit your solution code (as a .c file) to Gradescope (autograder).
* Do the intro to MIPS exercise described below.

<h2>Task 1: Binary Addition and Bit-Level Operations</h2>
<p>This task entails answering a series of questions focused on bit-level operations.</p>
<p>Open the file <a href="{{'/lab/lab02/lab02.pdf' | relative_url }}">lab02.pdf</a> and answer the questions, just as with Lab 1.</p>

<h2>Task 2: Bitwise Operations in C/C++</h2>
<p>In this task, you will write some high-level language code using C/C++ bitwise logic operations.</p>

<h3>Step 1: Familiarizing Yourself With the Files and Compilation Process</h3>
<p>
 There should be three files in your directory starting with the word <code>Random</code>.
 List just those files:
</p>

```
ls Random*
```

<p>
 Those three files contain a single program.
 If you have not taken CS24 before, you might not know how this works.
 <code>RandomCode.h</code> contains the *prototypes* for the functions you are going to implement.
 <code>RandomCode.c</code> contains the *definitions* or implementations of those functions.
 That is where you are going to add your code.
 I have also provided a handy test file with which you can test your code.
 This is <code>RandomMain.c</code>.
</p>

<p>
 The way this works is that after the usual #include files, there is a line:
</p>

```
#include "RandomCode.h"
```

<p>
 This tells <code>RandomMain.c</code> to read in <code>RandomCode.h</code> for the function prototypes.
 This allows us to compile them separately. To compile them, do the following:
</p>

```
gcc RandomCode.c RandomMain.c
```

Another way you could do this is:

```
gcc Random*.c
```

<h3>Step 2: Implementing Bit-Level Manipulation Routines</h3>

<p>**You will only be turning in <code>RandomCode.c</code>** - we are going to provide the <code>.h</code> file and any test files for our test cases. I have provided the main so that you can test your files individually. Make sure you **do not edit <code>RandomCode.h</code>**. If you edit that file, then your solution will not work with our test cases.
</p>

<p>
 Your assignment is to look at the functions in <code>RandomCode.c</code> and fill in the several lines necessary for each one.
 Each one should perform a series of bitwise operations (usually just one) on an integer, and return the resulting integer.
 The functions are roughly ordered easiest to hardest.
 The idea is to take  what you understand about bitwise operations and apply it to high-level code.
</p>

<p>You should use **only** bitwise operations, **except** for the following functions where you may also use <code>if</code>:</p>

<ul>
 <li><code>ifBit7is0</code></li>
 <li><code>ifBit3is1</code></li>
 <li><code>signedBits0through5</code></li>
 <li><code>signedBits6through9</code></li>
</ul>

<p>
 For the <code>if</code> functions, you may need to utilize the fact that in C, &ldquo;true&rdquo; is non-zero and &ldquo;false&rdquo; is zero.
 So this means that if you want to return true, you can return any number other than 0.
 For the functions that return signed results, be sure that sign extension is performed!
</p>

<p>
 Here is a little sample to see how it might look.
 This does not match the main code provided for you - this is for illustrative purposes in the description only.
</p>

<table border="1">
 <tr><th>Function</th><th>Input</th><th>Output</th></tr>
 <tr><td><code>multiplyBy8</code></td><td><code>7</code></td><td><code>56</code></td></tr>
 <tr><td><code>setBit6to1</code></td><td><code>0x01</code></td><td><code>0x41</code></td></tr>
 <tr><td><code>setBit3to0</code></td><td><code>0xffff</code></td><td><code>0xfff7</code></td></tr>
 <tr><td><code>flipBit5</code></td><td><code>0x01</code></td><td><code>0x21</code></td></tr>
 <tr><td><code>ifBit7is0</code></td><td><code>0x77</code></td><td><code>nonzero</code></td></tr>
 <tr><td><code>ifBit3is1</code></td><td><code>0x77</code></td><td><code>0</code></td></tr>
 <tr><td><code>unsignedBits0through5</code></td><td><code>0x335</code></td><td><code>0x35</code></td></tr>
 <tr><td><code>unsignedBits6through9</code></td><td><code>0x3b4</code></td><td><code>0xe</code></td></tr>
 <tr><td><code>signedBits0through5</code></td><td><code>0x3fa</code></td><td><code>0xfffffffa</code></td></tr>
 <tr><td><code>signedBits6through9</code></td><td><code>0xcf7</code></td><td><code>0x03</code></td></tr>
 <tr><td><code>signedBits0through5</code></td><td><code>0x38f</code></td><td><code>0xf</code></td></tr>
 <tr><td><code>signedBits6through9</code></td><td><code>0x38f</code></td><td><code>0xfffffffe</code></td></tr>
 <tr><td><code>setBits4through9</code></td><td>(<code>0xffffffff</code>, <code>0x23</code>)</td><td><code>0xfffffe3f</code></td></tr>
</table>

<p>
 The function that needs the most explanation is <code>setBits4through9</code>.
 You can think of this as replacing bits 4-9 (inclusive) with the second input's lowest bits.
 Leave the rest of the input's bits unchanged.
</p>

<p>
 Any extracted bits should be returned in the lowest bits of the return value.
 For example, in <code>unsignedBits6through9</code>, if bits <code>0110</code> were extracted from the value, then <code>0110</code> with 28 leading zeros should be returned (we are working with 32-bit integers).
</p>

<p>
 Specifically for this portion, we have also provided <code>RandomCodeTester.c</code>, which contains a small test suite which may be of interest to you.
 Instructions for compiling with the test suite, along with running it, are directly in <code>RandomCodeTester.c</code>.
 Note that this is **not** intended as a comprehensive test suite, but is instead there to make sure you are on the right track.
 You are encouraged to add your own tests to this suite.
</p>

<p>
 **IMPORTANT:** ***You may NOT use if, for, while instructions, nor create recursive functions, nor use arrays.***
</p>


<h2>Task 3: SPIM Tutorial</h2>
This will be a task that you do on the computer, but will NOT be writing anything up about it for THIS assignment. The purpose of this exercise is to familiarize you with SPIM and MIPS assembly language.

SPIM is a program that ***simualtes*** the MIPS CPU assembler. We don't have to buy a MIPS chipset or computer board in order to learn assembly language! We just have to simulate the hardware via software!

<h3>Step 1: Get SPIM</h3>
If you are on one of the CSIL lab machines, the SPIM simulator program should be available (you can make sure by typing <code>which spim</code> at a UNIX prompt, which will tell you where it's installed.

However, you may want to install SPIM on your home machine as well. In order to do so, you will want to go to the developer's page <a href="http://spimsimulator.sourceforge.net">HERE</a> and follow directions to download the software (it's not a big piece of software, won't take long to download, and is relatively straight-forward to install). The way we will be using SPIM is via the UNIX command line. We will develop our programs in a text file (with the .asm suffix) and then run them on SPIM as such:

```
spim -f filename.asm
```

Check out the sample program we have <a href="{{'/lab/lab02/mipsdemo.asm' | relative_url }}">here</a> called **mipsdemo.asm**. Start by viewing the program (either on a web browser or using a text editor like **emacs** or **vim**). It might not make much sense! That's ok, however, because we will become very familiar with this sort of programming in class!

Run the program like this from the UNIX prompt (once you've installed SPIM, of course):

```
spim -f mipsdemo.asm
```

**What do you see happening? How different would a program like this written in C++ or Java or Python look?!**

Keep in mind that you are learning not only a new language, but a new way of thinking, along with a new tool (SPIM).
Most of all, you have been doing this for only very recently - if this feels difficult, it is because it *is* difficult.
If you want to read more, or just have more potentially helpful information in your grasp, the links below may be of some assistance:

<ul>
 <li>
   For understanding the MIPS instructions themselves, it may be helpful to consult the MIPS reference card in the front of the textbook.
   A digital copy is also available <a href="{{'/lab/documentation/MIPS_reference_card.pdf' | relative_url }}">here</a>. We will become very familiar with this document in class over the next couple of weeks.
 </li>
 <li>For further understanding of how the <code>syscall</code> instruction works in SPIM, see <a href="https://www.doc.ic.ac.uk/lab/secondyear/spim/node8.html">this page</a>.</li>
 <li>For a detailed amount of information regarding SPIM, particularly the terminal interface, you may want to consult <a href="{{'/lab/documentation/spim.pdf' | relative_url }}">this manual</a>.</li>
</ul>

<h2>Turn in Everything Using Gradescope</h2>
You are going to turn in TWO things into Gradescope: the exercises in the PDF file *AND* the C/C++ program you wrote.

<h3>The lab02.pdf file:</h3>
**If you partnered with someone (it's OPTIONAL - and NO MORE THAN TWO people can work on one assignment together), record the email address they are using for the class at the top of the assignment. EACH person needs to submit their own assignment!**

Your assignment file is a PDF with the questions and blank spaces for the answers. The easiest way to proceed is to (a) print the original PDF, (b) write your answers on the paper ***USING DARK INK*** (so it shows up in a scan), (c) scan your print outs into a NEW PDF file (you can still give it the same name), and finally, (d) upload/submit the NEW PDF file to Gradescope. It should go without saying that neatness counts: if your scan is unreadable or your handwriting is very
bad, your assignment may not get graded (i.e. you'd get a zero score).

If you have software that allows you to directly edit a PDF file, you can use that instead of steps (a), (b), and (c) above. This is not usually software we have for students to use, so if you want to go this route, you may have to purchase this PDF-editing software yourself. Again, this is OPTIONAL. It's perfectly fine to go the print-then-scan route described above.

Your final step will be to go to Gradescope, select the <b>lab02</b> entry, and upload/submit your NEW PDF. Please call your submitted PDF file **lab02.pdf**.

<h3>The program RandomCode.c</h3>
Once you're done with writing your functions, navigate to the Lab assignment **lab02 - Code** on Gradescope and upload your `RandomCode.c` file. *Every student must upload their own code*.

**That's all for this assignment!**

</div>

<hr>
<blockquote>
<p><font size="1">
Copyright 2020, Ziad Matni, CS Dept, UC Santa Barbara. Permission to copy for non-commercial, non-profit, educational purposes granted, provided appropriate credit is given;  all other rights reserved
</font></p> 
</blockquote>
