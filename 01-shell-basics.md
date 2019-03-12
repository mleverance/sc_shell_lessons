# The Unix Shell

## Background

At a high level, computers do four things:

- Run programs,
- Store data,
- Communicate with each other, and
- Interact with us.

They can do the last of these in many different ways, including direct brain-computer interfaces and speech recognition, using systems such as Alexa or Google Home.
While such hardware interfaces are becoming more commonplace, most interaction is still done using screens, mice, touchpads and keyboards.
Although most modern desktop operating systems communicate with their human users by means of windows, icons and pointers, these software technologies didn’t become widespread until the 1980s.
Before this time, most people used *line printers.*
These devices only allowed input and output of the letters, numbers, and punctuation found on a standard keyboard, so programming languages and software interfaces had to be designed around that constraint.

**Let's introduce two terms.**
Command line interface(CLI) and graphical user interface (GUI)
- *command-line interface,* or CLI is an interface that developed from keyboard inputs
>The heart of a CLI is a *read-evaluate-print loop,* or REPL: when the user types a command and then presses the Enter (or Return) key, the computer reads it, executes it, and prints its output in the shell window.
The user then types another command, and so on until the user logs off.
The shell is a **command-line interface** which is useful for complex, purpose-specific things.
It uses a simple vocabulary of commands that are typed in by the user.
- *graphical user interface,* or GUI, which has windows, icons and pointers.
They are easy to learn and fantastic for simple tasks where "click" translates into "do the thing I want". It relies on wanting a simple set of things, and having programs that can do those things.

### The Shell
The Shell is a program which runs other programs rather than doing calculations itself.
The most popular Unix shell is Bash, (the Bourne Again SHell ---  
it's derived from a shell written by Stephen Bourne).
Bash is the default shell on most modern implementations of Unix
and in most packages that provide Unix-like tools for Windows.

## Is CLI difficult to use?

It's a different model of interacting than a GUI, and that
will take some effort to learn. A GUI presents you with choices and you select one. With a **command line interface** (CLI) the choices are combinations
of commands and parameters, more like words in a language than buttons on a screen. They aren't presented to you so you must learn a few, like learning some vocabulary in a new language. But a small
number of commands gets you a long way, and we'll cover those essential few today.

### Activity
- Where are some places you'll encounter a command line interface?
Using the etherpad, take a minute to enter answers for these:
- Advantages/disadvantages of CLI
  - advantages are its high action-to-keystroke ratio, its support for automating repetitive tasks, and its capacity to access networked machines
  - disadvantages are its primarily textual nature and how cryptic its commands and operation can be
- Advantages/disadvantages of GUI


### Flexibility and automation

The grammar of a shell allows you to combine existing tools into powerful
pipelines and handle large volumes of data automatically. Sequences of
commands can be written into a *script*, improving the reproducibility of
workflows and allowing you to repeat them easily.

In addition, the command line is often the easiest way to interact with remote machines and supercomputers.
Familiarity with the shell is near essential to run a variety of specialized tools and resources
including high-performance computing systems.


### What does it look like?

Let's take a look at the shell window looks like:

~~~
SHOW MY SHELL WINDOW
~~~

The first line shows what's called a **prompt**,
indicating that the shell is waiting for input.
- Your shell will have different text for your prompt; it includes useful information about who and where
you are.
- Your prompt ends with $
- When you type commands, you *don't type the prompt*, only the commands that follow it.

# Files
You need to download some files to follow this lesson:
- open your shell (also called terminal and command line)
  - on Mac, go to Applications - Utilities - terminal
  - on Windows, you should have Git for Windows downloaded
    - go to Start menu, find Git Bash, and open

## What to type
- go to etherpad
- copy
git clone https://github.com/mleverance/uark-swc-files.git

cd Desktop
  git clone https://github.com/mleverance/uark-swc-files.git

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
