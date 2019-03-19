from: https://pad.carpentries.org/2019-03-18-UNT

The Unix Shell

To shorten your terminal prompt type: PS1="$ "

ls : list files and directories
ls -F : list files and differentiate directories with a slash at the end
pwd : path of working directory
ls --help : gives a listing of help for the command
man ls : opens a manual page for documentation on the command (may not work on Windows; search for the manual page on the internet)
cd : change directory (with no arguments takes you to your home directory)
cd ~/Desktop : change to Desktop directory
[TAB] : Use the tab key to auto complete matching names when typing a command, a.k.a. tab completion
cd .. :  change directory up one level
clear :  clear previous output from the screen
ls -a : lists hidden directories too (those starting with a dot)
mkdir:  make a directory
rmdir: remove a directory
nano draft.txt : open a file called draft.txt in the nano text editor
touch my_file.txt : create a file called my_file.txt without opening the file in a text editor
mv : move a file or directory or rename (mv thesis/old_name.txt thesis/new_name.txt)
cp : copy
rm -r : remove recursively (to delete a directory)
* : wildcard character to match 1 or more characters (ls *.txt : matches any files in the directory with a .txt extension)
? : wildcard character that matches a single character
wc : word count; can tell you things like line counts, word counts, character counts
wc -l *.pdb : number of lines in files with extension pdb
wc -c *.pdb: number of characters in files with extension pdb
> : use this character to redirect output to a file instead of the screen (wc -l *.pdb > lengths.txt); the file is created and will overwrite a file if the name already exists
cat : concatenate; prints contents of file to the screen (or wherever you direct the output)
sort : sort the input
head: output the first lines (head -n 5 sorted-lengths.txt  : prints the first 5 lines)
tail: output the last lines (tail -n 5 : prints the last 5 lines)
| (vertical line): pipe sends output of one command into the input of the next command
wc -l *.pdb | sort -n | head -n 1 : use pipes to send the output of one command to be the input of the next command; this example gives the line counts of all the .pdb files, sorts them, and takes the first one (basically it shows us which of these files is shortest)
uniq : removes consecutive duplicate lines (only duplicates that are right next to each other)
cut : removes sections from the lines of a file
cut -d, -f 2 animals.txt : tells the cut command the delimeter for sections is a comma, and that we only want to print out the second field from each line
bash : run a bash script (bash middle.sh)
# : indicates comments follow
history : outputs your commandline history
! : run a command from the history, so, for example, if you wanted to rerun line 730 from the history, you would use "!730"
A "script" is just a file containing the same commands you would run from the command line, but it can be run with "bash" so you don't have to type them in yourself.
