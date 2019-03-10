---
title: "Introducing the Shell"
teaching: 5
exercises: 0
questions:
- "What is a command shell and why would I use one?"
objectives:
- "Explain how the shell relates to the keyboard, the screen, the operating system, and users' programs."
- "Explain when and why command-line interfaces should be used instead of graphical interfaces."
keypoints:
- "Explain the steps in the shell's read-run-print cycle."
- "Most commands take flags (options) which begin with a `-`."
- "Identify the actual command, flags, and filenames in a command-line call."
- "Explain the steps in the shell's read-run-print cycle."
- "Demonstrate the use of tab completion and explain its advantages."
keypoints:
- "A shell is a program whose primary purpose is to read commands and run other programs."
- "The shell's main advantages are its high action-to-keystroke ratio, its support for automating repetitive tasks, and its capacity to access networked machines."
- "The shell's main disadvantages are its primarily textual nature and how cryptic its commands and operation can be."
---
### Background
Before we discuss specifics about the shell, let's review four things computers do:

-   run programs
-   store data
-   communicate with each other
-   interact with us

The last item, interaction with us, happens in different ways
- keyboard & mouse
- touchscreen interfaces
- speech recognition

We're familiar with **graphical user interfaces** (GUI): windows, icons and pointers.
They are easy to learn and fantastic for simple tasks where "click" translates into "do the thing I want". 
But this magic relies on 
wanting a simple set of things, and having programs that can do those things.

The shell is a **command-line interface** which is useful for complex, purpose-specific things. 
It uses a simple vocabulary of commands that are typed in by the user.

The heart of a command-line interface is a **read-evaluate-print loop** (REPL). When you type a command 
and press <kbd>Return</kbd> (also known as <kbd>Enter</kbd>) the shell
reads your command,
evaluates (or "executes") it,
prints the output of your command on the screen, and waits for you to enter another command.
 
### The Shell
The Shell is a program which runs other programs rather than doing calculations itself.
The most popular Unix shell is Bash, (the Bourne Again SHell ---  
it's derived from a shell written by Stephen Bourne).
Bash is the default shell on most modern implementations of Unix
and in most packages that provide Unix-like tools for Windows.

### Is it difficult?

It is a different model of interacting than a GUI, and that 
will take some effort - and some time - to learn. A GUI 
presents you with choices and you select one. With a **command line interface** (CLI) the choices are combinations 
of commands and parameters, more like words in a language than buttons on a screen. They
are not presented to you so
you must learn a few, like learning some vocabulary in a new language. But a small 
number of commands gets you a long way, and we'll cover those essential few today.

### Flexibility and automation 

The grammar of a shell allows you to combine existing tools into powerful
pipelines and handle large volumes of data automatically. Sequences of
commands can be written into a *script*, improving the reproducibility of 
workflows and allowing you to repeat them easily.

In addition, the command line is often the easiest way to interact with remote machines and supercomputers.
Familiarity with the shell is near essential to run a variety of specialized tools and resources
including high-performance computing systems.
As clusters and cloud computing systems become more popular for scientific data crunching,
being able to interact with the shell is becoming a necessary skill.
We can build on the command-line skills covered here
to tackle a wide range of scientific questions and computational challenges.


### What does it look like?

A typical shell window looks like:

~~~
SHOW MY SHELL WINDOW
~~~

The first line shows what's called a **prompt**, 
indicating that the shell is waiting for input.
- Your shell will have different text for your prompt; it includes useful information about who and where 
you are.
- Your prompt ends with $
- When you type commands, you *don't type the prompt*, only the commands that follow it.

You can change your prompt to a $ only by typing 
~~~
PS1='$ '
~~~

The part that you type,
`ls -F /` in the second line of the example,
typically has the following structure: a **command**,
some **flags** (also called **options** or **switches**) and an **argument**.
Flags start with a single dash (`-`) or two dashes (`--`), and change the behaviour of a command.
Arguments tell the command what to operate on (e.g. files and directories).
Sometimes flags and arguments are referred to as parameters.
A command can be called with more than one flag and more than one argument: but a
command doesn't always require an argument or a flag.

In the second line of the example above, our **command** is `ls`, with a **flag** `-F` and an
**argument** `/`. Each part is separated by spaces: if you omit the space 
between `ls` and `-F` the shell will look for a command called `ls-F`, which 
doesn't exist. Also, capitalization matters: `LS` is different from `ls`. 

Next we see the output that our command produced. In this case it is a listing 
of files and folders in a location called `/` - we'll cover what all these mean 
later today. Those using a macOS might recognize the output in this example.

Finally, the shell again prints the prompt and waits for you to type the next 
command.



Open a shell window and try executing `ls -F /` for yourself (don't forget that spaces
and capitalization are important!). You can change the prompt too, if you like.


> ## Command not found 
> If the shell can't find a program whose name is the command you typed, it 
> will print an error message like:
> 
> ~~~
> $ ls-F
> ~~~
> {: .language-bash}
> ~~~
> -bash: ls-F: command not found
> ~~~
> {: .output}
> 
> Usually this means that you have mis-typed the command - in this case we omitted
> the space between `ls` and `-F`. 
{: .callout}

