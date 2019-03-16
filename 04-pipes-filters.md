# Pipes and Filters
teaching: 25 /
exercises: 10  

#### Questions we'll answer:
- How can I combine existing commands to do new things?
---

Now that we know a few basic commands,
we can look at a powerful feature of the shell:
the ease with which it lets us combine existing programs in new ways.  

We'll start with a directory called `molecules`
that contains six files describing some simple organic molecules.
The `.pdb` extension indicates that these files are in Protein Data Bank format,
a simple text format that specifies the type and position of each atom in the molecule.  

Let's navigate to the molecules directory, which is a subdirectory of the data-shell directory
```sh
$ cd  # where does this take us?
$ cd Desktop/data-shell/  # use tab completion here, note that capitalization matters for Desktop
```
Let's look at the files in the molecules folder
~~~
$ ls molecules
~~~
The six files are printed
~~~
cubane.pdb    ethane.pdb    methane.pdb
octane.pdb    pentane.pdb   propane.pdb
~~~

Let's go into that directory with `cd` and run the command `wc *.pdb`.
`wc` is the "word count" command:
it counts the number of lines, words, and characters in files (from left to right, in that order).

We learned in the last lesson that 
the `*` in `*.pdb` matches zero or more characters,
so the shell turns `*.pdb` into a list of all `.pdb` files in the current directory:

~~~
$ cd molecules
$ wc *.pdb
~~~

The lines, words, and characters of each file are listed in columns,
so 'cubane.pdb' has 20 lines, 156 words, and 1158 characters
~~~
  20  156  1158  cubane.pdb
  12  84   622   ethane.pdb
   9  57   422   methane.pdb
  30  246  1828  octane.pdb
  21  165  1226  pentane.pdb
  15  111  825   propane.pdb
 107  819  6081  total
~~~


If we run `wc -l` instead of just `wc`,
the output shows only the number of lines per file:

~~~
$ wc -l *.pdb
~~~

~~~
  20  cubane.pdb
  12  ethane.pdb
   9  methane.pdb
  30  octane.pdb
  21  pentane.pdb
  15  propane.pdb
 107  total
~~~

We can also use `-w` to get only the number of words,
or `-c` to get only the number of characters.

Which of these files contains the fewest lines?
It's an easy question to answer when there are only six files,
but what if there were 6000?
Our first step toward a solution is to run a command that tells the shell to **redirect** the command's output
to a file instead of printing it to the screen.
> The greater than symbol tells the shell to **redirect**  
> The file we specify receives the output
> - If the file doesn't exist, the shell will create it
> - If the file does exist, it will be overwritten, so be sure you're using an accurate filename

We'll tell the shell to redirect the output into a file called 'lengths.txt'

Here's what to type on the command line:

~~~
$ wc -l *.pdb > lengths.txt
~~~

It doesn't look like anything happened. We can check for the file's existence by entering:

~~~
$ ls lengths.txt
~~~

~~~
lengths.txt
~~~


We can send the content of `lengths.txt` to the screen using `cat lengths.txt`.
`cat` stands for "concatenate":
it prints the contents of files one after another.
There's only one file in this case,
so `cat` just shows us what it contains:

~~~
$ cat lengths.txt
~~~

We see the number of lines for each file next to the filename
~~~
  20  cubane.pdb
  12  ethane.pdb
   9  methane.pdb
  30  octane.pdb
  21  pentane.pdb
  15  propane.pdb
 107  total
~~~


> ## Output Page by Page
>
> We'll continue to use `cat` in this lesson, for convenience and consistency,
> but it has the disadvantage that it always prints the whole file onto your screen.
> More useful in practice is the command `less`,
> which you use with `less lengths.txt`.
> This displays a screenful of the file, and then stops.
> You can go forward one screenful by pressing the spacebar,
> or back one by pressing `b`.  Press `q` to quit.


Now let's use the `sort` command to sort its contents.  

We will also use the `-n` flag to specify that the sort is
numerical instead of alphanumerical.
This does *not* change the file;
instead, it sends the sorted result to the screen:

~~~
$ sort -n lengths.txt
~~~

~~~
  9  methane.pdb
 12  ethane.pdb
 15  propane.pdb
 20  cubane.pdb
 21  pentane.pdb
 30  octane.pdb
107  total
~~~

We can put the sorted list of lines in another temporary file called `sorted-lengths.txt`
by putting `> sorted-lengths.txt` after the command.
> Tip: don't redirect to the same file, use a different filename

~~~
$ sort -n lengths.txt > sorted-lengths.txt
~~~

Once we've done that, we can run another command called `head` which prints the first 10 lines of a file (or files, if you're using a wildcard)  
to the output you specify (the default is the terminal, but we saw how you can print to a file using the redirect command)  

We're going to use `-n 1` with `head` to tell it that we only want the first line of the file;
`-n 20` would get the first 20 lines, and so on.

~~~
$ head -n 1 sorted-lengths.txt
~~~

Results in the first line of the file
~~~
  9  methane.pdb
~~~

> ### Side Note:
> there's a command called `tail` that will print the last 10 lines of the file or files  

## What Does `>>` Mean?

We have seen the use of **redirect** `>`, but there is a similar operator `>>` (double angles) which works slightly differently.  
It **redirects** AND **appends** to a file.  
Another new command is `echo`, which means what it sounds like - echoing information back to you.  
We can use the `echo` command to print text in the shell. It's a handy way to create customized output in your terminal.  
~~~
$ echo The echo command prints text
~~~

~~~
The echo command prints text
~~~

We know that using redirect will put the command's output into a file instead of printing it on the screen,so let's do that and look at what's in the file:
~~~
$ echo hello > test.txt
$ cat test.txt
$ hello
~~~ 

Now we'll use the **append** command to add to that file
~~~
$ echo goodbye >> test.txt
~~~

How do you view the contents of the file?
What do you see when you look at it?  

## New concept: Pipes
An advantage of the shell is the ability to run commands on the same line instead of separately. Kind of like nesting functions in math.  
A pipe is a temporary section of computer memory capable of linking two or more computer processors, increasing the overall efficiency of the computer.  
For example, we can run `sort` and `head` together:

~~~
$ sort -n lengths.txt | head -n 1
~~~

~~~
  9  methane.pdb
~~~

The vertical bar, `|`, between the two commands is called a **pipe**.
It tells the shell that we want to use
the output of the command on the left
as the input to the command on the right.
The computer might create a temporary file if it needs to,
or copy data from one program to the other in memory,
or something else entirely;
we don't have to know or care.

Nothing prevents us from chaining pipes consecutively.
That is, we can send the output of `wc` directly to `sort`,
and then the resulting output to `head`.
We first use a pipe to send the output of `wc` to `sort`:

~~~
$ wc -l *.pdb | sort -n
~~~

~~~
   9 methane.pdb
  12 ethane.pdb
  15 propane.pdb
  20 cubane.pdb
  21 pentane.pdb
  30 octane.pdb
 107 total
~~~

And now we send the output of this pipe, through another pipe, to `head`, and the full pipeline becomes:
> ### Tip
> Using the up arrow will scroll through your previous commands so you don't have to retype the whole thing here
~~~
$ wc -l *.pdb | sort -n | head -n 1
~~~


~~~
   9  methane.pdb
~~~


> ## Exercise 1
> ## Piping Commands Together
>
> In our current directory, we want to find the 3 files which have the least number of
> lines. Which command listed below would work?
>
> 1. `wc -l * > sort -n > head -n 3`
> 2. `wc -l * | sort -n | head -n 1-3`
> 3. `wc -l * | head -n 3 | sort -n`
> 4. `wc -l * | sort -n | head -n 3`
>
>
>
> > ## Solution
> > Option 4 is the solution.
> > The pipe character `|` is used to feed the standard output from one process to
> > the standard input of another.
> > `>` is used to redirect standard output to a file.
> > Try it in the `data-shell/molecules` directory!  
  

## Show .ppt slide: processes using the shell
Here's what actually happens behind the scenes when we create a pipe.
When a computer runs a program --- any program --- it creates a **process**
in memory to hold the program's software and its current state.  
Every process has an input channel called **standard input**.  

Every process also has a default output channel called **standard output**
(or "stdout").  

The shell is actually just another program.
Under normal circumstances,
whatever we type on the keyboard is sent to the shell on its standard input,
and whatever it produces on standard output is displayed on our screen.
When we tell the shell to run a program,
it creates a new process
and temporarily sends whatever we type on our keyboard to that process's standard input,
and whatever the process sends to standard output to the screen.

Instead of creating enormous programs that try to do many different things,
Unix programmers created lots of simple tools that each do one job well,
and that work well with each other.
This programming model is called "pipes and filters".
We've already seen pipes;
a **filter** is a program like `wc` or `sort`
that transforms a stream of input into a stream of output.
Almost all of the standard Unix tools can work this way:
unless told to do otherwise,
they read from standard input,
do something with what they've read,
and write to standard output.  

> ## Exercise 2
> ## Pipe Reading Comprehension
>
> A file called `animals.txt` (in the `data-shell/data` folder) contains the following data:
>
> ~~~
> 2012-11-05,deer
> 2012-11-05,rabbit
> 2012-11-05,raccoon
> 2012-11-06,rabbit
> 2012-11-06,deer
> 2012-11-06,fox
> 2012-11-07,rabbit
> 2012-11-07,bear
> ~~~
> 
>
> What text passes through each of the pipes and the final redirect in the pipeline below?
>
> ~~~
> $ cat animals.txt | head -n 5 | tail -n 3 | sort -r > final.txt
> ~~~
> 
> Hint: build the pipeline up one command at a time to test your understanding
> > ## Solution
> > The `head` command extracts the first 5 lines from `animals.txt`.
> > Then, the last 3 lines are extracted from the previous 5 by using the `tail` command.
> > With the `sort -r` command those 3 lines are sorted in reverse order and finally,
> > the output is redirected to a file `final.txt`.
> > The content of this file can be checked by executing `cat final.txt`.
> > The file should contain the following lines:
> > ```
> > 2012-11-06,rabbit
> > 2012-11-06,deer
> > 2012-11-05,raccoon
> > ```

# Key points
review pipes & filters slide


## EXERCISE IF TIME
### Nelle's Pipeline: Checking Files

Nelle has run her samples through the assay machines
and created 17 files in the `north-pacific-gyre/2012-07-03` directory described earlier.
As a quick sanity check, starting from her home directory, Nelle types:

~~~
$ cd north-pacific-gyre/2012-07-03
$ wc -l *.txt
~~~

The output is 18 lines that look like this:

~~~
300 NENE01729A.txt
300 NENE01729B.txt
300 NENE01736A.txt
300 NENE01751A.txt
300 NENE01751B.txt
300 NENE01812A.txt
... ...
~~~


Now she types this:

~~~
$ wc -l *.txt | sort -n | head -n 5
~~~


~~~
 240 NENE02018B.txt
 300 NENE01729A.txt
 300 NENE01729B.txt
 300 NENE01736A.txt
 300 NENE01751A.txt
~~~


Whoops: one of the files is 60 lines shorter than the others.
When she goes back and checks it,
she sees that she did that assay at 8:00 on a Monday morning --- someone
was probably in using the machine on the weekend,
and she forgot to reset it.
Before re-running that sample,
she checks to see if any files have too much data:

~~~
$ wc -l *.txt | sort -n | tail -n 5
~~~


~~~
 300 NENE02040B.txt
 300 NENE02040Z.txt
 300 NENE02043A.txt
 300 NENE02043B.txt
5040 total
~~~


Those numbers look good --- but what's that 'Z' doing there in the third-to-last line?
All of her samples should be marked 'A' or 'B';
by convention,
her lab uses 'Z' to indicate samples with missing information.
To find others like it, she does this:

~~~
$ ls *Z.txt
~~

~~~
NENE01971Z.txt    NENE02040Z.txt
~~~


Sure enough,
when she checks the log on her laptop,
there's no depth recorded for either of those samples.
Since it's too late to get the information any other way,
she must exclude those two files from her analysis.
She could just delete them using `rm`,
but there are actually some analyses she might do later where depth doesn't matter,
so instead, she'll just be careful later on to select files using the wildcard expression `*[AB].txt`.
As always,
the `*` matches any number of characters;
the expression `[AB]` matches either an 'A' or a 'B',
so this matches all the valid data files she has.
