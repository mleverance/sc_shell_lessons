# Introduction
In this section we're going to cover:
- How to move around on my computer
- How to see what files and directories I have
- How to specify the location of a file or directory on my computer
---

## Navigating Files and Directories

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
Here is an example file system similar to the file system on Mac OSX; it may look pretty different from yours.

![](./filesystem.svg)

- At the top is the *root directory;* the directory that holds everything else. We refer to it using a forward-slash character on its own; this is the leading slash we see when we type `pwd`.
- Inside that directory are several others. The `Users` directory is where user's personal files are stored.
- **Notice that there are two meanings of the forward slash:** When it appears at the front of a file or directory name, it refers to the root directory. When it appears *inside* a file path, it's just a separator between directory names.

Underneath `/Users`, we find one directory for each user with an account on this hypothetical machine.

![](./home-directories.svg)

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

> ## Listing Recursively and By Time
>
> The command `ls -R` lists the contents of directories recursively, i.e., lists
> their sub-directories, sub-sub-directories, and so on at each level. The command
> `ls -t` lists things by time of last change, with most recently changed files or
> directories first.
> In what order does `ls -R -t` display things? Hint: `ls -l` uses a long listing
> format to view timestamps.
>
> > ## Solution
> > The files/directories in each directory are sorted by time of last change.
> {: .solution}
{: .challenge}

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

If we want to work with files and folders inside `data-shell`, however, and we don't want to type `Desktop/data-shell` every time, it would be better if **we changed our current working directory to `data-shell`. The command to change locations is `cd` followed by a directory name to change our working directory. `cd` stands for "change directory", which is a bit misleading:
the command doesn't change the directory, it changes the shell's idea of what directory we are in.**

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

## Activity
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
> {: .solution}
{: .challenge}

# key points:
- "The file system is responsible for managing information on the disk."
- "Information is stored in files, which are stored in directories (folders)."
- "Directories can also store other directories, which forms a directory tree."
- "`cd path` changes the current working directory."
- "`ls path` prints a listing of a specific file or directory; `ls` on its own lists the current working directory."
- "`pwd` prints the user's current working directory."
- "`/` on its own is the root directory of the whole file system."
- "A relative path specifies a location starting from the current location."
- "An absolute path specifies a location from the root of the file system."
- "Directory names in a path are separated with `/` on Unix, but `\\` on Windows."
- "`..` means 'the directory above the current one'; `.` on its own means 'the current directory'."





# regular lesson begins




> ## Relative Path Resolution
>
> Using the filesystem diagram below, if `pwd` displays `/Users/thing`,
> what will `ls -F ../backup` display?
>
> 1.  `../backup: No such file or directory`
> 2.  `2012-12-01 2013-01-08 2013-01-27`
> 3.  `2012-12-01/ 2013-01-08/ 2013-01-27/`
> 4.  `original/ pnas_final/ pnas_sub/`
>
> ![File System for Challenge Questions](../fig/filesystem-challenge.svg)
>
> > ## Solution
> > 1. No: there *is* a directory `backup` in `/Users`.
> > 2. No: this is the content of `Users/thing/backup`,
> >    but with `..` we asked for one level further up.
> > 3. No: see previous explanation.
> > 4. Yes: `../backup/` refers to `/Users/backup/`.
> {: .solution}
{: .challenge}

> ## `ls` Reading Comprehension
>
> Assuming a directory structure as in the above Figure
> (File System for Challenge Questions), if `pwd` displays `/Users/backup`,
> and `-r` tells `ls` to display things in reverse order,
> what command will result in the following output:
>
> ~~~
> pnas_sub/ pnas_final/ original/
> ~~~
> {: .output}
>
> 1.  `ls pwd`
> 2.  `ls -r -F`
> 3.  `ls -r -F /Users/backup`
> 4.  Either #2 or #3 above, but not #1.
>
> > ## Solution
> >  1. No: `pwd` is not the name of a directory.
> >  2. Yes: `ls` without directory argument lists files and directories
> >     in the current directory.
> >  3. Yes: uses the absolute path explicitly.
> >  4. Correct: see explanations above.
> {: .solution}
{: .challenge}

### Nelle's Pipeline: Organizing Files

Knowing just this much about files and directories,
Nelle is ready to organize the files that the protein assay machine will create.
First,
she creates a directory called `north-pacific-gyre`
(to remind herself where the data came from).
Inside that,
she creates a directory called `2012-07-03`,
which is the date she started processing the samples.
She used to use names like `conference-paper` and `revised-results`,
but she found them hard to understand after a couple of years.
(The final straw was when she found herself creating
a directory called `revised-revised-results-3`.)

> ## Sorting Output
>
> Nelle names her directories "year-month-day",
> with leading zeroes for months and days,
> because the shell displays file and directory names in alphabetical order.
> If she used month names,
> December would come before July;
> if she didn't use leading zeroes,
> November ('11') would come before July ('7'). Similarly, putting the year first
> means that June 2012 will come before June 2013.
{: .callout}

Each of her physical samples is labelled according to her lab's convention
with a unique ten-character ID,
such as "NENE01729A".
This is what she used in her collection log
to record the location, time, depth, and other characteristics of the sample,
so she decides to use it as part of each data file's name.
Since the assay machine's output is plain text,
she will call her files `NENE01729A.txt`, `NENE01812A.txt`, and so on.
All 1520 files will go into the same directory.

Now in her current directory `data-shell`,
Nelle can see what files she has using the command:

~~~
$ ls north-pacific-gyre/2012-07-03/
~~~
{: .language-bash}

This is a lot to type,
but she can let the shell do most of the work through what is called **tab completion**.
If she types:

~~~
$ ls nor
~~~
{: .language-bash}

and then presses <kbd>Tab</kbd> (the tab key on her keyboard),
the shell automatically completes the directory name for her:

~~~
$ ls north-pacific-gyre/
~~~
{: .language-bash}

If she presses <kbd>Tab</kbd> again,
Bash will add `2012-07-03/` to the command,
since it's the only possible completion.
Pressing <kbd>Tab</kbd> again does nothing,
since there are 19 possibilities;
pressing <kbd>Tab</kbd> twice brings up a list of all the files,
and so on.
This is called **tab completion**,
and we will see it in many other tools as we go on.
