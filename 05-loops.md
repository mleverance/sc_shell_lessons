# Loops
teaching: 40 / 
exercises: 10  
Questions we'll answer:
- "How can I perform the same actions on many different files?"
---

**Loops** are key to productivity improvements through automation as they allow us to execute
commands repeatedly. Similar to wildcards and tab completion, using loops also reduces the
amount of typing (and typing mistakes).   

Let's navigate to the `creatures` directory. There are only two example files in this directory,
but the principles apply to many many more files at once.
```sh
$ cd
$ cd Desktop/data-shell/creatures
$ ls
$ basilisk.dat unicorn.dat
```
We're going to modify these files in the future, so we want to save a version of the original files, naming the copies
`original-basilisk.dat` and `original-unicorn.dat`.

Let's try the `cp` copy command.  
When we used it previously, we gave the command `cp` and entered the file name first and then the new file name the original is copied to, so we'll do the same thing here.  
~~~
$ cp basilisk.dat unicorn.dat original-*.dat
~~~

Uh oh, this doesn't work and we get an error:
~~~
cp: target `original-*.dat' is not a directory
~~~


This problem arises when `cp` receives more than two inputs. When this happens, it
expects the last input to be a directory where it can copy all the files it was passed.
So it expected `original-*.dat` to be the directory.  
Since there is no directory with that name in the `creatures` directory we get an error.

Instead, we can use a **loop**
to do some operation once for each thing in a list.
Here's a simple example that displays the first three lines of each file in turn:

~~~
$ for filename in basilisk.dat unicorn.dat
> do
>    head -n 3 $filename	
> done
~~~

~~~
COMMON NAME: basilisk
CLASSIFICATION: basiliscus vulgaris
UPDATED: 1745-05-02
COMMON NAME: unicorn
CLASSIFICATION: equus monoceros
UPDATED: 1738-11-24
~~~

> ## Let's break this down
> ### Prompt
> The shell prompt changes from `$` to `>` and back again as we were
> typing in our loop. The second prompt, `>`, is different to remind
> us that we haven't finished typing a complete command yet. 

> ### Indentation of code within a for loop
> It's common practice to indent the line(s) of code within a for loop.
> It makes the code easier to read -- it is not required for the loop to run.

When the shell sees the keyword `for`,
it knows to repeat a command (or group of commands) once for each item in a list.
Each time the loop runs (called an iteration), an item in the list is assigned in sequence to
the **variable**, and the commands inside the loop are executed, before moving on to 
the next item in the list.
Inside the loop,
we call for the variable's value by putting `$` in front of it.
The `$` tells the shell interpreter to treat
the **variable** as a variable name and substitute its value in its place,
rather than treat it as text or an external command. 

In this example, the list is two filenames: `basilisk.dat` and `unicorn.dat`.
Each time the loop iterates, it will assign a file name to the variable `filename`
and run the `head` command.
The first time through the loop,
`$filename` is `basilisk.dat`. 
The interpreter runs the command `head` on `basilisk.dat`, 
and then prints the 
first three lines of `basilisk.dat`.
For the second iteration, `$filename` becomes 
`unicorn.dat`. This time, the shell runs `head` on `unicorn.dat`
and prints the first three lines of `unicorn.dat`. 
Since the list was only two items, the shell exits the `for` loop.

> ## Same Symbols, Different Meanings
>
> Here we see `>` being used a shell prompt, whereas `>` is also
> used to redirect output.
> Similarly, `$` is used as a shell prompt, but, as we saw earlier,
> it is also used to ask the shell to get the value of a variable.
>
> If the *shell* prints `>` or `$` then it expects you to type something,
> and the symbol is a prompt.
>
> If *you* type `>` or `$` yourself, it is an instruction from you that
> the shell should redirect output or get the value of a variable.

We called the variable in this loop `filename`
to make its purpose clearer to human readers.
The shell itself doesn't care what the variable is called;
Programs are only useful if people can understand them.

> ## Exercise 1
> ## Variables in Loops
>
> This exercise refers to the `data-shell/molecules` directory.  
> 
> `ls` gives the following output:
>
> cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
>
> What is the output of the following code?
>
> $ for datafile in *.pdb
> > do
> >    ls *.pdb
> > done
>
>
>
> > ## Solution
> > The first code block gives the same output on each iteration through
> > the loop.
> > Bash expands the wildcard `*.pdb` within the loop body (as well as
> > before the loop starts) to match all files ending in `.pdb`
> > and then lists them using `ls`.
> > The expanded loop would look like this:
> > ```
> > $ for datafile in cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
> > > do
> > >	ls cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
> > > done
> > ```
> > 
> >
> > ```
> > cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
> > cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
> > cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
> > cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
> > cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
> > cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
> > ```

> ## Limiting Sets of Files
>
> What would be the output of running the following loop in the `data-shell/molecules` directory?
>
> ~~~
> $ for filename in c*
> > do
> >    ls $filename 
> > done
> ~~~
> 
>
> 1.  No files are listed.
> 2.  All files are listed.
> 3.  Only `cubane.pdb`, `octane.pdb` and `pentane.pdb` are listed.
> 4.  Only `cubane.pdb` is listed.
>
> > ## Solution
> > 4 is the correct answer. `*` matches zero or more characters, so any file name starting with 
> > the letter c, followed by zero or more other characters will be matched.
> >


Let's continue with our example in the `data-shell/creatures` directory.
Here's a slightly more complicated loop:

~~~
$ for filename in *.dat
> do
>     echo $filename
>     head -n 100 $filename | tail -n 20
> done
~~~

Reminder: 
> If *you* type `>` or `$` yourself, it is an instruction from you that
> the shell should redirect output or get the value of a variable.


The shell starts by expanding `*.dat` to create the list of files it will process.
The **loop body**
then executes two commands for each of those files.
The first, `echo`, just prints its command-line arguments to standard output.
For example:

~~~
$ echo hello there
~~~

prints:

~~~
hello there
~~~

In this case,
since the shell expands `$filename` to be the name of a file,
`echo $filename` just prints the name of the file.
Note that we can't write this as:

~~~
$ for filename in *.dat
> do
>     $filename
>     head -n 100 $filename | tail -n 20
> done
~~~

because then the first time through the loop,
when `$filename` expanded to `basilisk.dat`, the shell would try to run `basilisk.dat` as a program.  

Finally, the pipe of `head` and `tail` selects lines 81-100
from whatever file is being processed (assuming the file has at least 100 lines).  
The output of the command `head` on the left of the pipe is used as the input to the command of `tail` on the right.  
The first 100 lines are selected, and then the last 20 lines of those first 100 are printed for each file.

> ## Pro tip
> If you use Spaces in Names
>
> Spaces are used to separate the elements of the list
> that we are going to loop over. 
> If one of those elements
> contains a space character, we need to surround it with
> quotes, and do the same thing to our loop variable.


Going back to our original file copying problem,
we can solve it using this loop:

~~~
$ for filename in *.dat
> do
>     echo cp $filename original-$filename
> done
~~~


This loop runs the `cp` command once for each filename.
The first time, when `$filename` expands to `basilisk.dat`,
the shell executes:

~~~
cp basilisk.dat original-basilisk.dat
~~~

The second time, the command is:

~~~
cp unicorn.dat original-unicorn.dat
~~~

Since the `cp` command does not normally produce any output, it's hard to check 
that the loop is doing the correct thing. By prefixing the command with `echo` 
it is possible to see each command as it _would_ be executed.  

> ## Those Who Know History Can Choose to Repeat It
>
> Another way to repeat previous work is to use the `history` command to
> get a list of the last few hundred commands that have been executed. 
> Try it
> ~~~
> $ history
> ~~~
>
> Now try it with a pipe
> ~~~
> $ history | tail -n 5
> ~~~
> 
> Save your history to a file!
> $ history >> my_history.txt


> ## Exercise 2
> ## Nested Loops
> 
> Navigate to the `data-shell/molecules` directory.
> 
> Suppose we want to set up a directory structure to organize
> some experiments measuring reaction rate constants with different compounds
> *and* different temperatures.  
>
> Take a few minutes to work through this nested loop, and check the results in the directory when it's finished.
>
> ~~~
> $ for species in cubane ethane methane
> > do
> >     for temperature in 25 30 37 40
> >     do
> >         mkdir $species-$temperature
> >     done
> > done
> ~~~
> 
>
> > ## Solution
> > We have a nested loop, i.e. contained within another loop, so for each species
> > in the outer loop, the inner loop (the nested loop) iterates over the list of
> > temperatures, and creates a new directory for each combination.
> >
> > Try running the code for yourself to see which directories are created!

