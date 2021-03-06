# The Unix Shell

## Background

At a high level, computers do four things:

- Run programs,
- Store data,
- Communicate with each other, and
- Interact with us.

They can do the last of these in many different ways, including direct brain-computer interfaces and speech recognition, using systems such as Alexa or Google Home.  
These interfaces are becoming more commonplace, most interaction is still done using screens, mice, touchpads and keyboards.  

**Let's introduce two terms.**

Command line interface(CLI) and graphical user interface (GUI)

- *command-line interface,* or CLI is an interface that developed from keyboard inputs
>The heart of a CLI is a *read-evaluate-print loop,* or REPL: when the user types a command and then presses the Enter (or Return) key, the computer reads it, executes it, and prints its output in the shell window.
The user then types another command, and so on until the user logs off.  
The shell is a **command-line interface** which is useful for complex, purpose-specific things.  
It uses a simple vocabulary of commands that are typed in by the user.  

- *graphical user interface,* or GUI, which has windows, icons and pointers.  
> They are easy to learn and fantastic for simple tasks where "click" translates into "do the thing I want".  
It relies on wanting a simple set of things, and having programs that can do those things, like click farms set up to click on paid advertising links.

### The Shell
The Shell is a program which runs other programs rather than doing calculations itself.
The most popular Unix shell is Bash, (the Bourne Again SHell ---  
it's derived from a shell written by Stephen Bourne).
Bash is the default shell on most modern implementations of Unix and in most packages that provide Unix-like tools for Windows.

### You might be wondering... Is CLI difficult to use?
If you haven't used the shell before, it may seem clunky and unrelatable at first.  
It will take some effort to learn because it's a different way of interacting with the computer than what you're most likely used to.  
With a GUI you get set choices and you select one.  
With a **command line interface** (CLI) the choices are combinations of commands and parameters, and because they aren't presented to you, you have to learn a few, like learning vocabulary in a new language.  
But the plus is that a small number of commands gets you a long way, and we'll cover those essential few today.
> Some places you might see a CLI are webserver, remote computer, copying/moving large files, high performance computing or cluster computing 

### Why use the shell?
The power of the shell is combining existing tools into powerful
pipelines and handling large volumes of data automatically. Sequences of
commands can be written into a *script*, improving the reproducibility of
workflows and allowing you to repeat them easily.  
If you can run a script that saves you days of computational work, it's a better choice.

### Activity
Talk with a neighbor and take two minutes with the etherpad to enter answers for these:
If someone else has already written what you were going to enter in the etherpad, you can put a + next to it

- **Advantages/disadvantages of CLI**  
- **Advantages/disadvantages of GUI**

- CLI
  - advantages are its high action-to-keystroke ratio, its support for automating repetitive tasks, and its capacity to access networked machines
  - disadvantages are its primarily textual nature and how cryptic its commands and operation can be
- GUI
  - don't have to learn commands, choices easy to see
  - stuck with interface design, limited to clicking to select


### What does it look like?

Here's what the shell window looks like:

~~~
SHOW MY SHELL WINDOW
~~~

The first line shows what's called a **prompt**, indicating that the shell is waiting for input.
- Your shell will have different text for your prompt; it includes information about who and where
you are.
- The prompt ends with a dollar sign ($)
- When you type commands, you *don't type the prompt*, only the commands that follow it.

# Files
You'll need to download some files to use in this lesson.  
I'm going to explain according to your OS.  
Linux users
- open Bash from the applications menu or search bar
Mac users
- go to Applications - Utilities - terminal
Windows users, you should have Git for Windows downloaded. I'm on Windows so you can follow what I'm doing:
- go to your desktop
- right click
- select Git Bash Here
- a terminal window will open
    
 #### Sticky check: 
 If you need help, put up a yellow sticky and a helper will come by


## File download
Everyone:
- at your prompt, type `cd Desktop`
  - if you get a message like mine that says "no such file or directory", that is OK
- now type `pwd`
  - you should see a string printed that ends with Desktop
  - if you don't, put up a yellow sticky so a helper can assist
We're ready to download files now
- go to the etherpad line ___ and copy the following
- git clone https://github.com/mleverance/uark-swc-files.git
  - Windows users: if you copy and then right click in your shell window, it will paste the information for you
  - Mac/Linux: you can copy/paste
Press enter/return, you'll see the files load, and the cursor is back at the prompt
- look at your desktop
- there is now a folder there called uark-swc-files
- the commands you enter in the shell are a different way of creating files, and we're going to talk about that more next

### Sticky check
Put up your blue sticky if you see the uark-swc-files folder on your desktop

> if you're having trouble with git, follow this link to download the zip file
> https://swcarpentry.github.io/shell-novice/data/data-shell.zip
