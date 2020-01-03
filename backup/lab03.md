---
layout: lab
num: lab03
ready: true
desc: "Basic MIPS Assembly Programming"
assigned: 2019-10-16 14:00:00.00-7
due: 2019-10-23 23:59:59.00-7
---
<div markdown='1'>
<h1>Lab 3: Basic MIPS Assembly Programming</h1>
<hr>
<p>Due Wednesday, October 23rd at 11:59:59 PM</p>

<h2>Goals for This Week</h2>
<p>By the time you have completed this work, you should be able to use basic arithmetic and standard I/O calls in MIPS assembly.</p>

<b>Provided files:</b>
<ul>
  <li><a href="{{'/lab/lab03/Arithmetic.asm' | relative_url }}"><code>Arithmetic.asm</code></a></li>
  <li><a href="{{'/lab/lab03/hello.asm' | relative_url }}"><code>hello.asm</code></a></li>
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
  <li>Task 1: Basic arithmetic calculations with I/O calls.</li>
  <li>Task 2: Hello World program with I/O calls.</li>
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
<p>Then create a new directory for this lab: <code>lab3</code>:</p>
<pre>
mkdir lab3
</pre>
<p>Then go into that directory.</p>
<p>Now copy over all of the files necessary for this week's tasks:</p>
<pre>
cp ~zmatni/public_html/cs64f19/labs/3/hello.asm ~zmatni/public_html/cs64f19/labs/3/Arithmetic.asm .
</pre>
<p>
  Note the use of the trailing <code>.</code> in the above command, which stipulates that the specified files should be copied into the current directory.
</p>


<h2>Task 1: Arithmetic Exercise</h2>
<p>
  You will write an assembly program that will prompt the user for 3 inputs (let's abstractly call them
  a, b, and c) without a leading string. It will then calculate the value of:  <code>2*(a - b) + 3*c</code>.</p>
<p>
  You can ONLY use the <code>mult</code> instruction ONCE!
  (You will lose half the points for this task if you do not follow this rule).
</p>
<p>
  A sample run of this program will look like this, with user input in <b>bold</b>. Please note that when the answer is given, there is NO expectation of a new line:
</p>
<pre>
<b>4</b>
<b>-5</b>
<b>7</b>
39
</pre>
<p>
  You should write your program in the provided <code>Arithmetic.asm</code> template file.
  You may assume that the user can use signed integers as inputs, but that no multiplication will lead to overflow.
  You do not actually have to check for that.
</p>

  
<h2>Task 2: Hello World</h2>
<p>
  You will write a type of Hello World program that will also get an integer input from the user and prints out two lines with newline characters at the end of each of them. A sample run of this program will look like this, with user input in <b>bold</b>:
</p>
<pre>
Choose an integer number between 0 and 1000:
<b>42</b>
Hello World!
User chose 42. Truly a wise choice.
</pre>
<p>
  Your code should be written in the provided <code>hello.asm</code> template file.
  Be sure that your output matches <i>exactly</i> with the output above. Note where the new lines are and where they are not.
  (The last line DOES have a new line at the end of it).
</p>
<p>
  Assume that the user will put in an integer between 0 and 1000. *You don't have to check for it.*
</p>
<b>Clues:</b>
<p>
  Remember what syscall codes you have to use for std input, std output for either 
  integers and strings, and program exit. When printing out strings, remember that you have
  to first define them under the <code>.data</code> directive.
</p>

<p>
  <b>Test both your programs extensively (we certainly will) before you turn them in!</b>
</p>

<h2>Turn in Everything Using Gradescope</h2>
You are going to turn in TWO things into Gradescope: the 2 files: `arithmetic.asm` and `hello.asm` files.
Navigate to the Lab assignment **lab03** on Gradescope and upload both files. *Every student must upload their own code*.

</div>
<hr>
<blockquote>
<p><font size="1">
Copyright 2019, Ziad Matni, CS Dept, UC Santa Barbara. Permission to copy for non-commercial, non-profit, educational purposes granted, provided appropriate credit is given;  all other rights reserved
</font></p> 
</blockquote>
