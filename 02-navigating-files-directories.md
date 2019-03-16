# Navigating Files and Directories

Questions we'll answer:
- How do I move around on my computer?
- How do I see what files and directories I have?
- How do I specify the location of a file or directory on my computer?
---

## Where are we?
**Before we can use the shell for what it's really powerful at--automating tasks and improving our productivity--we need to become comfortable with navigating and manipulating our file system in the shell.**

- The *file system* is the part of our operating system responsible for managing files and directories.
- Many of you may currently use a point-and-click file browser like Windows Explorer or Finder (on Mac).
- We'll see how the shell allows us to a lot of the same things (moving files, renaming files, creating folders).

**Let's open up the shell and get started.**

```sh
$ whoami
```

This command's output is the identifier for the current user, i.e., your username.
More specifically, when we type `whoami` at the shell:

1. The shell finds a program called `whoami` and runs it.
2. The shell displays the output from that program.
3. Then, the shell displays a new prompt so that we know it's ready for more input.

**The shell is a program that runs other programs, so the commands we type must be the names of existing programs.**

```sh
$ something
```

```sh
$ pwd
```

The command `pwd` stands for "print working directory" and it "prints" to the shell window the result of where we are on our file system.

**Since we just started the shell, by default, our current working directory is our home directory.**
To understand what a "home directory" is, let’s have a look at how the file system as a whole is organized.

> open shell-slides-for-workshop
> - show slide 1

- At the top is the *root directory;* the directory that holds everything else. We refer to it using a forward-slash character on its own; this is the leading slash we see when we type `pwd`.
- Inside that directory are several others. The `Users` directory is where user's personal files are stored.
- **Notice that there are two meanings of the forward slash:** When it appears at the front of a file or directory name, it refers to the root directory. When it appears *inside* a file path, it's just a separator between directory names.

Underneath `/Users`, we find one directory for each user with an account on this hypothetical machine.

Next, we'll see how to list the contents of our file system.

### Listing Files and Folders in a Directory

```sh
$ ls
```

The `ls` command stands for "listing;" it's a program that displays the contents of a directory.
By default, it prints the names of the files in the current directory in alphabetical order, arranged neatly into columns.

**Programs in the shell often take special options, also called flags, that change the output of the command.**
The `ls` command accepts a `-F` flag that highlights the names of directories, making it easier to distinguish them from files. It will display a slash immediately after each pathname that is a directory.

First let's move to our desktop

```sh
$ cd Desktop
```
then type this

```sh
$ ls -F
```

We can find out what other options the `ls` command accepts by typing:
Windows
```sh
$ ls --help
```
for Mac, the command is different and it means reading the manual. You'll type
```sh
$ man ls
```
- You'll see definitions of what each flag means, which is helpful when you want to refer back or find out what you might use
- Typing a space will page through the list, or use the arrows to move by line, and typing 'Q' will quit and return you to the prompt

> ## Unsupported command-line options
> If you try to use an option (flag) that is not supported, `ls` and other commands
> will usually print an error message 
> What happens if we type: ls -j


In addition to *options,* many commands we can use in the shell accept one or more *arguments.*
An argument to a command is some input, required or not, that the command will act on.
The `ls` command accepts as an argument the path to another directory.

```sh
$ ls -F Desktop
```

**Your output from this command should be a list of the files on your desktop and should include the folder data-shell. Take a moment to confirm that is the case.**

> ## Exploring more ls flags
>
> You can also use two flags at the same time. What does the command ls do when used with the -l flag? 
> What about if you use both the -l and the -h flag?
> Hint: man ls or ls --help for a list of all options
>
> > ## Solution
> > The -l flag makes ls use a long listing format, showing not only the file/directory names but also additional 
> > information such as the file size and the time of its last modification. If you use both the -h flag and the -l flag, 
> > this makes the file size “human readable”, i.e. displaying something like 5.3K instead of 5369.
> 

### Changing the Current Working Directory

**As we've seen, the bash shell is strongly dependent on the idea that our files are organized in a hierarchical file system.**
Organizing this this way, in a tree structure, allows us to keep track of our work.
While it's possible to put hundreds of files in our home directory, just as it's possible to pile hundreds of papers on our desk, it's not the best strategy if we ever hope to find something in particular.

Let's take a look at the contents of the `data-shell` folder.

```sh
$ ls -F Desktop/data-shell
```

**Note that we've provided the path to a directory that is contained inside another directory inside our current directory.**
We can provide arbitrarily long file paths to arbitrarily deep files and folders on our system, as long as they are accurate.

If we want to work with files and folders inside `data-shell`, and we don't want to type `Desktop/data-shell` every time, it would be better if we changed our current working directory to `data-shell`. The command to change locations is `cd` followed by a directory name. `cd` stands for "change directory", which is a bit misleading:
the command doesn't change the directory, it changes the shell's idea of what directory we are in.

```sh
cd Desktop
cd data-shell
cd data
```

Now where are we?
How can we find out?

```sh
pwd
ls -F
```

We now know how to go down the directory tree, but how do we go up?

```sh
cd data-shell
```
But we get an error!  Why is this?  

With our methods so far, `cd` can only see sub-directories inside your current directory.  There are
different ways to see directories above your current location; we'll start with the simplest.  

There is a shortcut in the shell to move up one directory level that looks like this:

~~~
$ cd ..
~~~

The `..` symbol is a special directory name meaning "the directory containing the current working directory."
We also call this the *parent* of the current working directory.

If we run `pwd` after running `cd ..`, we're back in `/Users/*yourname*/Desktop/data-shell`:

The special directory `..` doesn't usually show up when we run `ls`.  If we want
to display it, we can give `ls` the `-a` flag:

```sh
ls -F -a
```

The `-a` option stands for "show all" and it can be used to see hidden files and folders.

It also displays another special directory that's just called `.`, which means "the current working directory". 


### Relative versus Absolute File Paths

**So far, we've seen three commands for navigating our file system. What do they mean?**

- `pwd`
- `ls`
- `cd`

Let's explore these commands further.
What happens if you type `cd` on its own, without specifying a directory?

```sh
$ cd
```

How can you check what happened?

```sh
$ pwd
```
cd without an argument returns you to the home directory, which helps if you're lost in your filesystem

Let's go back to the `data` directory we were in before.
Last time, we used three commands to ge there.
Let's string those three file paths together so that we only have to type `cd` once.

```sh
$ cd Desktop/data-shell/data
```
Check that we’ve moved to the right place by running pwd 

**So far, when specifying directory names, we've been using relative paths.**
A relative path is a file path that is relative to the current working directory.
That is, when we use a relative path with a command like `ls` or `cd`, the program tries to find that location based on our current location in the file system.

It's also possible to specify an *absolute path* to a directory by specifying its entire path from the root directory, which is indicated by the leading slash.
Note that absolute paths are what is printed out by the `pwd` program.

```sh
$ pwd
$ cd /home/arthur/Desktop/data-shell
$ cd ~/Desktop/data-shell
```
### A note on tab completion
You can save time by typing the first letter or letters of a directory (or file, if you want a file from a directory) and then press tab to autocomplete the directory or file name

from the data-shell folder
```sh
$ cd no (press tab)
> displays the two names that begin with 'no'
> we want the north-pacific-gyre directory
> how do we know it's a directory? (ends in slash) 
> retype with more letters this time
$ cd nor (press tab)
> now it autocompletes to north-pacific-gyre directory
```

## Activity
We'll do a couple activities using the etherpad to reinforce what we've just learned.  
> ## Exercise 1
> ## Absolute vs Relative Paths
>
> Starting from `/Users/amanda/data/`,
> which of the following commands could Amanda use to navigate to her home directory,
> which is `/Users/amanda`?
>
> 1. `cd .`
> 2. `cd /`
> 3. `cd /home/amanda`
> 4. `cd ../..`
> 5. `cd ~`
> 6. `cd home`
> 7. `cd ~/data/..`
> 8. `cd`
> 9. `cd ..`
>
> > ## Solution
> > 1. No: `.` stands for the current directory.
> > 2. No: `/` stands for the root directory.
> > 3. No: Amanda's home directory is `/Users/amanda`.
> > 4. No: this goes up two levels, i.e. ends in `/Users`.
> > 5. Yes: `~` stands for the user's home directory, in this case `/Users/amanda`.
> > 6. No: this would navigate into a directory `home` in the current directory if it exists.
> > 7. Yes: unnecessarily complicated, but correct.
> > 8. Yes: shortcut to go back to the user's home directory.
> > 9. Yes: goes up one level.
> 
> ## Exercise 2
> ## Relative Path Resolution
>
> Using the filesystem diagram http://swcarpentry.github.io/shell-novice/fig/filesystem-challenge.svg, if `pwd` displays `/Users/thing`,
> what will `ls -F ../backup` display?
>
> 1.  `../backup: No such file or directory`
> 2.  `2012-12-01 2013-01-08 2013-01-27`
> 3.  `2012-12-01/ 2013-01-08/ 2013-01-27/`
> 4.  `original/ pnas_final/ pnas_sub/`
>
>
> > ## Solution
> > 1. No: there *is* a directory `backup` in `/Users`.
> > 2. No: this is the content of `Users/thing/backup`,
> >    but with `..` we asked for one level further up.
> > 3. No: see previous explanation.
> > 4. Yes: `../backup/` refers to `/Users/backup/`.

# key points:
- show slide 2

