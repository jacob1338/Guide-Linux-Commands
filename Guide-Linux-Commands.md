# Introduction

**What is Unix philosophy?**

- write programs that do thing and do it well;
- write programs to work together;
- write programs to handle text streams, because that is a universal interface.

**What is a kernal?**

A kernel is a computer program that forms the core of an operating system and manages critical tasks like: 

- memory management
- task scheduling
- managing hardware

**What is Linux?**

While a kernel is a critical piece, it is NOT the same as an operating system. An engine is the essential "core" of a car, but you can't drive an engine on its own!

Today, the term "Linux" refers both to the kernel created by Linus Torvalds AND all the software that is part of the Linux ecosystem.

The Linux Kernel itself is not a full-blown operating system. When people talk about a Linux-based operating system, they are referring to *Linux distributions*. Typically, a *Linux distribution* bundles together the Linux kernel, GNU tools, documentation, a package manager, a window system, and desktop environment. There are nearly 1000 Linux distributions available. Some of the more popular ones includes Fedora, Ubuntu, Debian, and Slackware.

**What is a Shell?**

A shell is a computer interface to an operating system. Shells expose the OS’s services to human users or other programs. The shell takes our commands and gives them to the operating system to perform. It’s named a shell because it is the outer layer around the OS, like the shell around an oyster!

**What is Terminal?**

A terminal is a program that runs a shell. Originally, terminals were physical devices, but these days we work with software terminals.

**What is Bash?**

There are different shells, the most common one is Bash, there are others like: ZSH, Fish, Powershell.

On most Linux-based systems, the default shell program is Bash. There are many other shells, but Bash is currently the most popular.  Bash runs on pretty much every version of Unix and Unix-like systems.

Mac commands: command + space → spotlight search





# Basic Structure of Commands

**Command Case-sensitivity**:


- commands are case-sensitive;
- for Mac OS X, some commands are not case-sensitive, but it's safe to assume all are case-sensitive.

**Command Structure**:   `command [option]…[argument]…` …means one or more of the proceeding operands, so `[option]…` means we can pass one or more options to the command, `[argument]…` means we can pass one or more arguments.

- for options, case matters, such as **ncal -b** is not the same as **ncal -B**
- some commands require multiple arguments, such as`cp [option]…SOURCE DEST`in which two arguments (i.e. SOURCE and DEST) are required.
- long-form options use two dashes —, short-form options use one dash -, for example:

```bash
date -u
date --universal

sort file1 -r
sort file1 -reverse

sort file1 -u
sort file1 --unique

sort file1 -r
sort file1 --reverse --unique
```

Furthermore:

```bash

# Some commands can have either one or multiple arguments
cal july 1969 # july 1969 are two arguments
cal 2001 # 2001 is one argument

# We can combine multiple options
cal -h -3 

# We can collapse multiple options into short syntax
cal -h3 # it's the same as cal -h -3

# We can also collapse option and argument together
# The code below prints the current month as well as 2 months
# afterwards, 2 is the parameter of the option -A.
cal -A 2 
cal -A2

# Print the current month as well as 2 months before.
cal -B 2
cal -B2

# Print the current month as well as one month before and 
# one month after
cal -B1 -A1

# We can combine options and arguments
cal -B1 -A1 -hj july 2002
```


# Some Basic Commands
```bash
passwd # change password
clear # clear the screen
date # print the current date and time
ncal # new/vertical calendar, print the calendar for the current month
cal # traditional/horizontal calendar for the current month

# -h : turn off the highlighting of today's date
# -j: display calendar using Julian days (days are numbered starting
# from Jan 1st);
# -M: tell calendar to use Monday as the first day instead of Sunday;
# -M does not work in Mac OS X;
# -(digit): print the previous, present and next months
cal -h
cal -j 
cal -M 
cal -3

history # view entire history of commands typed
history | less # make the view more managable

# Re-run an earlier command if we have its line number 
# from the history.
!somenumber 
!37 # one example

echo $HISTFILESIZE # max size of commands stored, default 2000
echo $HISTSIZE # max size of commands in memory, default 1000
```


# Getting help

1. Find help from Man pages:

```bash
man command # read specific documentation about a command

man -k dog # search for the specified string in all man pages

# Display passwd in section 5 of manual page, instead of the default
# section 1.
man 5 passwd
```

Some shortcuts to navigate through the Man pages:

- type `h` for help and `q` for quit.;
- for long page, hit `space` bar or `f` for turning pages;
- hit `b` for back one page;
- hit `g` for going back to the first line of the file;
- hit `Enter` or `Down arrow` to scroll by one line;
- `/pattern` for searching forward in the file, `?pattern` for searching backward, `-I` ignore cases (i.e. case insensitive). To jump through the results, press `N` (forwards) and `Shift+N` (backwards).

2. Three others: `type`, `which`, `help`

There are four types of Linux commands:

1. An executable program, usually stored in `/bin`, `/usr/bin`, or `/usr/local/bin`. These are compiled binary files (hence bin);
2. A built-in shell command. These commands are part of the shell (bash in our case);
3. A shell function;
4. An alias.

```bash
type command # tell us the type of a command

# To find the exact location of an executable
# This only works for executables, 
# not built-in shell commands or aliases.
which command

# For built-in shell commands, which very likely do not have 
# manual page documenation, use help:
help command # example: help cd
```

# Navigation

- Root Directory: the starting point for the file system, we call it the root, but its actual directory name is `/`.
- Home Directory: `/home` contains a home folder for each user on the system. For example, my home folder is located at `/home/user1`
- Shortcuts: `/` for root directory, `~` for home directory

```bash
# Linux: open the current directory
xdg-open . 

# Linux: open '/' directory (i.e. root directory) in the file viewer
xdg-open / 

# Linux: open '~' directory (i.e. home directory)
xdg-open ~ 

# Mac: open '/' directory in the file viewer
open / 
```


```bash
pwd # print working directory
ls # list all the contents in the current working directory
ls -m # list the contents separted by comma rather than space
ls /home/user1 # list the contents of a specific directory
ls / # list the contents of the root directory
ls ~ # list the contents of the user home directory

ls -l # print in long listing format
ls -a # list any hidden files that begin with .
ls -la # combine option -l and -a

# -h :print sizes lik 1K 2M with human-readable formats
# instead of bytes.
ls -lh 

ls -l --sort=time # sort by time
ls -l --sort=size # sort by size

cd <directory> # change directory
cd .. # move back up one level, 
# . refers to the current directory and .. refers to parent directory
cd ../.. # move back two levels
cd ~ # change directory to the user home directory
cd / # change directory to the root directory

 # relative path, if we are in the parent directory of Desktop
cd Desktop/Dogs

# relative path, assuming the current directory contains Dogs
cd Dogs 

# absolute path, which starts with '/' (i.e. root directory)
cd /home/jiesun/animals 

```

# Creating Files and Folders

```bash
touch <filename1> <filename2> <filename3>

# Create file cutepic not in current directory but one level back
touch ../cutepic 

# It's not recommended to have space in file name, but if we have to, 
# we need to use quotation mark
touch "my web"

file "my web"
 
# \ means to treat the letter behind as a normal text, 
# not as a symbol with significant meaning.
file my\ web

file <filename> # determine the file type

mkdir <foldername> # make directory name
mkdir ~/Games # make folder Games in the user home directory

# Make folder Mares in the directory of Horses, if the parent directory
# of Hourses does not exist, in the current directory, make one.
mkdir -p Horses/Mares 

```

Note: Naming a JPG file into .txt extension will not make the system think it’s a txt file (i.e. the system still thinks it’s a JPG file), however, it will make the application think it’s a txt file when we try to open the file automatically with a  system chosen default app. 

# Nano

Nano is a simple text editor that we can access right from the terminal. It’s far more accessible than other popular command-line editors like vim and emacs.

```bash
nano file
nano book.txt 
# start editing book.txt, if it does not exist, it will create one.
```

Shortcuts inside nano editor:
- `ctrl + X`: exit, 
- `ctrl + G`: get help,
- `ctrl + S`: save,
- `ctrl + O`: write out
- Use `ctrl-W` and then enter a search phrase to search FORWARD in the file from your current cursor location.
- To search and replace, use `ctrl+\ `and then enter the word you want to replace. Then enter the replacement and decide whether to replace specific matches or all matches.
- Spellchecking:  We can use spellchecking inside of Nano, but we have to enable it first in the Nano config file located at `/etc/nanorc`:

```bash
sudo nano /etc/nanorc
# then enable (i.e. remove comment mark #): set speller "aspell -x -c"
```

# Deleting, Copying & Moving

```bash
# There is no undo ore cycling bin to retrieve deleted files.
# They are gone!
rm <filename> 

rm -d <dirname> # Delete empty directory

# Delete directories and their contents recursively, use with care!
rm -r <dirname>

# -i means interatively, prompt before every removal
rm -ri <dirname>

# Delete empty directory
rmdir <dirname>

mv <source> <destination> # source can be a file or a directory
mv <source1 source2 source3> <directory>

# Move file cats in the current directory to the parent directory
mv cats ..

# Move file cats located in Cats in the current directory to MyCates
# located in the user home directory.
mv Cats/cats ~/MyCats/

# Rename
mv <current> <newname>

# Move DOBBY.txt to the user home directory and then rename it to
# Dobby.txt 
mv chicken.txt roosters.txt
mv DOBBY.txt ~/Dobby.txt 

cp <source> <destination> # Copy a file

# Copy the file moretodos in the current directory to be 
# renamed to file shopping in the user home directory
cp moretodos ~/shopping

# copy file1 file2 into the folder dir/
cp <source1 source2> <destination>
cp file1 file2 dir/

cp -r <source> <destination> # -r: copy directories recursively
```

# Terminal Shortcuts

- up arrow:  cycle through previous commands;
- down arrow: go down to more recent commands;
- `ctrl + l`: clear
- `ctrl + a`: move the cursor to the beginning of the line
- `ctrl + e`: move the cursor to the end of the line
- `ctrl + f`: move the cursor forward one character at a time
- `ctrl + b`: move the cursor backwards one character at a time
- `alt + f`: move the cursor forward one word
- `alt + b`: move the cursor backwards one word
- `ctrl + t`: swap the current character under the cursor with the one preceding it
- `alt + t`: swap the current word under the cursor with the one preceding it
- `ctrl + k`: kill the text from the current cursor location until the end of the line
- `ctrl + u`: kill the text from the current cursor location to the beginning of the line
- `alt + d`: kill the text from the current cursor location through the end of the word
- `ctrl + d`: kill the letter under the current cursor
- `ctrl + w` or `alt + delete`: kill the text from the current cursor through the beginning of the word
- `ctrl + y`: retrieve the most recently killed text
- `ctrl + r`: search the history after using history command
- `ctrl + c`: terminate the current command

# Basic Working with Files

```bash
# Concatenate and print the contents of the files
# -b option numbers nonempty otuput lines
# -n option numbers all output lines
cat <filename>
cat <file1> <file2> # concatenate the contents and output them

# Display the contents of a file, one page at a time
less <filename>
less -I <filename> # search with case insensitive
less -N <filename> # turn on line numbers

# Concatenate and print files reverse. It prints each line of a file, 
# starting with the last file.
tac <filename>
tac ~/.bash_history

# Print the contents of a file, reversing the order of each line.
rev <filename>

# Print a portion of a file, by default, it prints the first 10 
# lines of a file.
head <filename>
head -n 21 <filename> # print 21 lines instead of 10 lines.
head -21 <filename>

# Print the last 10 lines of a file.
tail <filename>
tail -n 21 <filename> # print 21 lines instead of 10 lines.
tail -21 <filename>

tail -f syslog # Following the updates of the syslog file

# Count the words, lines, or bytes in files.
# -l option to limit the output to be the number of lines;
# -w option to limit the output to the number of words.
# -c tells the number of bytes;
# -m tells the number of characters;
wc <filename>
wc -l <filename>
wc -w <filename>
wc -c <filename>
wc -m <filename>

# Output the sorted contents of a file (it does not 
# change the file itself) alphabetically.
sort <filename>
sort -r <filename> # in reverse order
sort -n <filename> # treat as numeric values rather than letters.
sort -u <filename> # output only sorted unique values.

sort <filename> -k 2 # sort by the second column
sort <filename> -nk2
```

# Redirection Data Stream

“Redirection” describes the ways we can alter the source of standard input, and the destinations for standard output and standard error.

```bash
# Write output to a file,
# that file will be completely overwritten if it already existed.
command > filename 
ls -l /usr/bin > list.txt
sort -k5n list.txt > sorted_list.txt

# Append new content to the end of the file
command >> filename
date >> cal.txt # append current time to cal.txt

# Pass the contents of a file to standard input
command < filename
cat < chickens.txt # print the contents in chicken.txt
sort < cal.txt # sort the contents in cal.txt
# Note: for cat and sort, with no File, read standad input 
# (i.e. keyboard).

# Use cat to read in the contents of original.txt and then
# redirect the output to a file called output.txt
cat < original.txt > output.txt
cat < cats.txt >> output.txt # append cats.txt to output.txt

# cat nonexistenfile will yield error, and we redirect this
# standard error to file called error.txt
# standard input's descriptor is 0, standard output is 1
# standard error's descriptor is 2
cat nonexistenfile 2> errorlog.txt
sort cts.txt 2> errorlog.txt 
# cts.txt did not exist, so it will write error to error.txt
cat nonexistenfile 2>>log erro.text # append error to file content

# Concatenate dog and cat files and write to animals2,
# and if there is error, append error message to errorlog
cat dog.txt cat.txt > animals2 2>> errorlog.txt

# If we redirect both standard output and error to the same file
ls docs > output.txt 2>&1 # same as below
ls docs > output.txt 2> output.txt 

# New version of bash supports &> for redirecting both standard output
# and error to the same file
ls docs &> output.txt # write/overwrite
ls doc &>> otuput.txt # append

# Note: Order Matters! Always redirect standard error after standard 
# output if you want to redirect both.

# Combine contents of three files into one new file
cat angela-survey.txt nico-survey.txt juan-survey.txt > all-species.txt

# Sort the uniques
sort --unique all-species.txt > sorted-animals.txt
date >> sorted-animals.txt # append the current date
# append the text "Green Anaconda"
echo "Green Anaconda" >> sorted.animal.txt 
ughh 2>> sorted-animals.txt # append error message
```

# Pipes

```bash
# Stream from command1 to command2
command1 | command2

date | rev # reverse the output of current date
ls /usr/bin/ | less # print less version of bin directory
ls /usr/bin/ > list.txt # output the result to list.txt

# Count the word of commands qin bin directory
# -a: all including hidden files, -1: one file per line
ls /usr/bin/ -1a | wc
ls /usr/bin/ -1a | wc > count.txt # output the count to list.txt

nano msf # create and write a file
cat msf | tr s S # tr translates each s into a S
cat msf | tr -d s # delete every s

# Delete every letter and every space in data.txt
cat data.txt | tr -d [:alpah:] | tr -d [:blank:] 

# tr translates each lower-case letter to a upper-case letter
cat msf | tr a-z A-Z 

# Feed a file to head, which cuts it down to the first 7 lines,
# then passes it to tail, outputs the last 5 lines of that "chunk".
# -n prints the line number for each line.
cat file1 -n | head -7 | tail -5

# ls -lh lists all the files in the current directory;
# sort -r reverses the order, -h means human readable, 
# -k sorts via a key, 
# 5 means the 5th column, which contains file size info.
# The piple below outputs the top 3 biggest files
ls -lh | sort -rhk 5 | head -3

# Concatenate three files and then count the words, 
# and then outputs the number.
cat file1 file2 file3 | wc -w > list.txt
```


```bash
# The tee program reads standard input and copies it to both
# standard output and a file. So the output of command1 is
# copied to file.txt and in the same time flows into command2.
command1 | tee file.txt | command2

# Concatenate three files and output the file to files.txt,
# and then print the word counts of the concatenated file.
cat file1 file2 file3 | tee files.txt | wc -w
```

```bash
# Count the number of Pokemon files in the PokeDex/ folder.
ls ./PokeDex | wc -l  
# Create a new file called all-pokemon.txt in the PokemonExercise
# folder that contains the LOWERCASED name of every single Pokemon file
# in the directory, sorted in numerical order!
ls ./PokeDex | tr A-Z a-z | sort -n > all-pokemon.txt
#  Using the command-line, print out lines 16-18.
cat all-pokemon.txt | head -18 | tail -3

# Using a single pipeline: 
# output the first 151 lines of the all-pokemon.txt;
# remove all digits 0-9 from the lines (using `tr` )
# sort the now number-less lines alphabetically
# store the new result in a file called new.txt
cat all-pokemon.txt | head -151 | tr -d [:digit:] | sort > new.txt
```

Different between redirection and piping:

- `>` connects a command to some file,
- `|` connects a command to another command.

# Expansion

## Pathname Expansion

The asterisk ( * ) character represents zero or more characters in a filename. For example:
- `ls *.html` will match any files that end with .html like index.html and navbar.html
- `cat blue*` will match any files that start with "blue" like "blue.html" or "bluesteel.js"

The question mark ( ? ) character represents any single character.
- `ls app.??` will match any files named "app" that end with two character file extensions like "app.js" or "app.py" but NOT "app.css"
- `ls pic?.png` will match pic1.png, pic2.png, pic3.png, but also picA.png, or picx.png.

Inside of square brackets ([ ]) we can specify a range of characters to match. Note: it only represents one single character.
- `ls pic[123].png` (or `ls pic[1-3].png`) will only match pic1.png, pic2.png, and pic3.png, not pic123.png
- `ls file[0-9]` will match file1, file2, file3, up to file9
- `ls [A-F]*` will match any files that begin with a capital A, B, C, D, E, or F

Inside of square brackets ([ ]) we can specify a range of characters to NOT match, using a caret ( ^ ).
- `ls [^a]*` will match any files that do NOT start with "a"
- `ls [^0-9]*` will match any files that do NOT start with a numeric digit (0-9)

## Brace Expansion

Basically, it will generate multiple strings for us based on a pattern. We provide a set of strings inside of curly braces ({ }), as well as optional surrounding prefixes and suffixes.  For example, `touch page{1,2,3}.txt` will generate three new files: page1.txt, page2.txt, and page3.txt.

```bash
# Generate ten .txt files
echo {Mon,Tue,Wed,Thu,Fri}_{AM,PM}_Planner.txt}
echo Journal_{1..365} # generate 365 strings
mkdir Journal_{1..365} # create 365 folders

# -p means make parent directories as needed
# The code below generates 5 folders in each folder 
# there will be 3 sub-folders
mkdir -p {Mon,Tue,Wed,Thu,Fri}/{Breakfast,Lunch,Dinner}

echo {2..10..2} # interval is 2, output: 2 4 6 8 10
echo {x,y{1..5},z} # output: x y1 y2 y3 y4 y5 z
```

## Arithmetic Expansion

The shell will perform arithmetic via expansion using the $((expression)) syntax. inside the parentheses, we can right arithmetic expressions using: `+ - * / ** %`.  The shell only performs integer arithmetic, so the result is always a whole number

```bash
echo 10+3 # treat 10+3 as string
echo $((10+3)) # print 13
echo $((10/3)) # print 3
echo $((10%3)) # print 1
```

## Double Quoting vs Single Quoting

Large whitespace is ignored because the shell performs something called word splitting. `echo look    at       me` will print `look at me`.  If we wrap text in double quotes, the shell will respect our spacing and will ignore special characters except for dollar sign `$` , backslash`\`, and backtick `. 

Use Single Quotes to suppress all forms of substitution.

```bash
echo "today is ...   $(date)" # output current date value
echo 'today is ...   $(date)' # output: today is ...   $(date)
```

## Command Substitution

We can use the $(command) syntax to display the output of another command. 

```bash
# print "today is Thu 01 May 2021 03:10:31 PM PDT"
echo "today is $(date)" 

echo today `date`
echo Hello $(whoami) # print "Hello username"
```

## Escaping

To prevent expansion or substitution for specific characters, we can prefix them with a single backslash.

```bash
echo "$5.00" # print .00
echo "\$5.00" # print $5.00
```

## Examples

```bash
# Print out the current date using the format *month-day-year*, 
# like **09-19-21**
date +"%m-%d-%y"

touch todos-$(date +"%m-%d-%y").txt 
# the resulting file: todos-06-28-22.txt.

# List out all the files that end with the number 9 
ls *[9]

# List out all the filenames where the second to last character is 1
ls *1?

# List out all the files that start with afternoon 
# and then end with the number 7
ls afternoon*7

# Make a new folder called Mornings, and move all the files 
# that start with morning inside of it
mkdir Mornings
mv mornings* Mornings

# Make a folder of 4 subfolders with 2 sub-sub-folders
mkdir -p Year/{Winter,Spring,Summer,Fall}/{Yard,House} 
# -p make parent dir.
ls -R Year # look recursively inside the directory

# Create 2 files in each sub-sub-sub directory
touch Year/{Winter,Spring,Summer,Fall}/{Yard,House}/{todos.txt,done.txt}

```

# Finding Things

The `locate` command performs a search of pathnames across our machine that match a given substring and then prints out any matching names. It is nice and speedy because it uses a pre-generated database file rather than searching the entire machine. Note that the database updates periodically.

```bash
sudo apt install mlocate # install locate
locate Planner/Mon # search by path
locate /bin/less???

# Some files deleted can still be matched and printed by using locate 
# because the database may not be updated.For that situation, you can 
# first run the code below to update the database,
sudo updatedb # update the pre-generated database

# or use option -e, which prints entries that actually exist 
# at the time locate is run.
# -i option tells locate to ignore casing;
# -l or --limit limits the number of entries that locate retrieves;

locate Planner -il10 # case insentive, and limiting to 10 entries
```

Unlike locate, find does not use a database file. By default, `find` on its own will list every single file and directory nested in our current working directory. We can also provide a specific folder `find friends/` would print all files and directories inside the friends directory (including nested folders)

```bash
find -type f # limit the search to files
find -type d # limit the search to directories

# -name: match filenames and directories
# -iname for a case insensitive search

# Find all files that end in the .txt extension
find ~/Desktop -name "*.txt" 

find ~ -type f -name "*.txt"ls 
find ~ -name "Desk*" # match Desktop folder
find ~ -iname "chick"
find ~ -iname "*chick*"

find -size +1G # find all files larger than 1 gigabyte
find -size -50M # find all files under 50 megabytes
find -size 20k # find all files that are exactly 20 kilobytes

find -user alex # match files and directories that belong to a user
```

## Timestamps

- mtime (modification time): when a file was last modified, i.e. contents changed.
- ctime (change time): when a file was last changed, it not only includes contents changed, but also includes renaming a file, moving it or altering permissions.
- atime (access time): when a file is read by an application or a command like cat.

```bash
# show atime-access time rather than m time for each file/directory
ls -lu 

# show ctime-change time rather than m time for each file/directory
ls -lc 

ls -l # by default show creation time

# Use 1 week ago instead of current time stamp to create the file
touch last_week -d "1 week ago" 

# Find files modified exactly 30 mintues ago
# +30: greater than 30
# -30: less than 30
find -mmin 30 

find -amin -1 # find files accessed less than 1 mintue ago

# Find files accessed more than 1*24 hours ago, any fractional part
# is ignored, the bode below find file accessed at least 2 days ago.
find -atime +1
```

## Logical Operations

Logical Operations: `-and`, `-or`, `-not`

```bash
find -type -f -not -name "*.html" # find files except html files
find ~ -iname "*chick*" -or -iname "*kitty*"

# Find files changed less than 60 minutes ago which are not .log files.
find -cmin -60 -not -name "*.log"
find -cmin -60 ! -name "*.log" # ! is same as -not

find ~ ! -empty # find files that are not empty
```

## User-Defined Actions

```bash
# {} are for the current pathname (each match);
# Semicolon is required to dicate the end of the command.
# We need to wrap the {} and ; in quotes because they have special
# meanings otherwise
find -exec command {}; 

# Find empty files in the user home directory
find ~ -type f -empty
# If we want to run ls -l for every file listed above:
find ~ -type f -empty -exec ls -l '{}' ';'

# -ok prompts to ask for every single match: y or n
find ~ -type f -empty -ok rm '{}' ';'

# Find all files that end with .html and then create a copy of each one
# using cp command. Each copy ends with "_COPY", such as "index.html_COPY"
find ~ -type f -name "*.html" -exec cp '{}' '{}_COPY' ';'

```

Difference between` -exec` and `xargs` commands: -exec command is executed separately for every single element while xargs command builds up the input into a bundle that will be provided as an argument to the next command.

```bash
find -empty | ls 
# this will not work because ls does not take standard input

# List every empty file with details, ls -ls runs mutliple times 
# for each element.
find -empty -exec ls -l '{}' ';' 

echo f1 f2 | mkdir # this will not work

# This will make 2 empty directories: f1 and f2
echo f1 f2 | xargs mkdir 

# List every empty file with details, ls -ls runs only one time 
# for the bundled input from previous command.
find -empty | xargs ls 

# Find 4 individual chapter files and then pass them to the cat
# command, which outputs the combined contents to a file 
# called fullbook.txt
find -name "chapter[1-4].txt" | xargs cat > fullbook.txt
```

## Examples

```bash
# Using find (and another command), count the number of case files 
# that include  "closed", in lowercase, in their name.
find . -name "*closed*" | wc -l

# Find the open cases that have a 1,3,5,7, or 9 as the last digit 
# in their case number.
find . -iname "*[13579]_open*" | wc -l

# Find the one case file that is larger than 150k and is closed.
find -size +150k -iname "*closed*"

# Find the one case that has been modified more recently 
# than the yesterday.txt file.
find -newer yesterday.txt
```

# grep

This command searches for patterns in each file’s content, it will print each line that matches a pattern we provide.

Note: `find` will search in filenames while `grep` will search in files or in text.

```bash
grep pattern file # by default, the pattern is case sensitive
grep pattern file -i # -i means case insensitive

# -w matches words, rather than fragments located inside of 
# other words.
grep -w "cat" book.txt

# -r preforms a recursive search, which includes all files 
# under a directory, subdirectories and their files and so on.
# If we do not specify a directory, it will default to our current
# working directory.
grep -r "chicken" 
grep -ri "parm[ae]san" MealDiary/

# Search for patter in each file
# -i means ignore case
# -c means output a count of matching lines for each input file
grep "myself" file1.txt -ic

# -A prints a number of lines after the matching line
# -B prints a number of lines before the matching line
# -C prints a number of lines output context
grep "grass" file1.txt -iB1 # -B1 prints one line before the match.

# prints one line before and one line after
grep "grass" file1.txt -i -A1 -B1 
grep "grass" file1.txt -i -C1 # same as -A1 -B1

# -n prints the line number for the matching line
grep "6" file1.txt -wn 

grep "wagon" file1.txt -m2 # stop reading after 2 matching lines
```

## Regex (Regular Expression)

> `.` : matches any single character;
> `^` : matches the start of a line;
> `$` : matches the end of a line;
> `[abc]` : matches any character in the set;
> `[^abc]` : matches any char not in set;
> `[A-Z]` : matches characters in a range;
> `*`  : repeat previous expression 0 or more times;
> `\`: escape meta-characters;



```bash
grep "p...." file1.txt -w # find words with exact 5 characters
grep "^I" file1.txt -w # find I in the beginning of the line.
grep "$)" file1.txt -w # find ) at the end of the line.
```

## egrep

It’s the same as `grep -E`, i.e. Extended Regular Expressions. In basic regular expressions, the meta-characters` ? + { | ( )` lose their special meaning, so use `\?`, `\+`, `\{`, `\|`,` \(` and `\)` instead, or use `-E` option

```bash
# ? means optinal
# The command means find either bird or birds
grep "birds?" -wE file1.txt

grep "[aeiou]{2}" -E file1.txt # find 2 vows next to each other
grep "[aeiou]{2,4}" -E file1.txt # match vows in a range from 2 to 4
```

## Piping to grep

```bash
# ps -aux will otuput a huge list of all processes running on our
# machine. We pipe that data to grep, and then filter it down to only
# processes that include "hermione"
ps -aux | grep hermione
ps -aux | grep "sound" -i # find processes relating to sound
man grep | grep "count" -i # match "count" in the man page of grep

# grep -l shows the file names of the matches, -n shows line numbers
find ~ -name "*.txt" ! -empty -type f -exec grep -nl "indigo" '{}' ';'

# -I suppresses some info, process a binary file as if it did not
# contain matching data.
grep ~ -rE "https?:\/\/(?:www\.|(?!www))[a-zA-Z0-9][a-zA-Z0-9-]+[a-zA-Z0-9]\.[^\s]{2,}|www\.[a-zA-Z0-9][a-zA-Z0-9-]+[a-zA-Z0-9]\.[^\s]{2,}|https?:\/\/(?:www\.|(?!www))[a-zA-Z0-9]+\.[^\s]{2,}|www\.[a-zA-Z0-9]+\.[^\s]{2,}" -I
```

# Permission

```bash
whoami # print user name
```

File Attributes: `drwxr-xr-x`  or `-rw-rw-r—`
- Note that the file attribute is composed of ten letters, the first letter denotes the file type (either -, d, b, c or l), the last nine letters can be divided into three chunks, each has three letters (either r, w, x or -, and in order).
- first letter (-: regular file, d: directory, b: block special files, c: character special file, l: symbolic link)



## Altering Permissions

Change the permissions of a file/directory, we use `chmod mode file`

First, we specify the “who” using the following values:
- `u` : user (the owner of the file)
- `g` : group (members of the group the file belongs to)
- `o` : others
- `a` : all of the above

Next, we tell `chmod` “what” we are doing using the following characters:
- `-` (minus sign) removes the permission
- `+` (plus sign) grants the permission
- `=` (equals sign) set a permission and removes others

Finally, the “which” values are:
- `r` : the read permission;
- `w` : the write permission;
- `x` : the execute permission.

```bash
chmod g+w file.txt # g: group, +: add, w: write
chmod a-w file.txt # g: all, +: remove, w: write
chmod a=r file.txt # a: all, =: set permission, r: read

# 7(rwx) for owner, 5(r-x) for group, 5(r-x) for world
chmod 755 file.txt
```



```bash
# Create a new login for the username;
# We need to enter username's password;
# To leave the session, type exit.
su - username 

# Change the user, but stay in the current working directory.
su username
```

## Super Root User

Even if the root user is locked by default, we can still run specific commands as the root user by using the `sudo` command. Individual users are granted an “allowed” list of commands they can run as the super user.

```bash
sudo -l # see the permitted commands for the particular user

sudo apt update # update the ubuntu system
sudo cat /etc/sudoers

# Find the time limit for using sudo without typing password
man sudo | grep minutes -C2

```

## Change Ownership

```bash
chown newowner file.txt # make newowner the owner of file.txt

# if user do not have permission, use root user power
sudo chown newowner file.txt 

chown :newgroup file.txt # make newgroup the group of file.txt

chown newowner:newgroup file.txt 
# change user and group in the same time
# you may need root user power, if so, use sudo
```

## Groups

```bash
groups # show what groups
groups username # show which groups the user is in

sudo addgroup groupname # create a new group
sudo adduser user group # add user to group
```

# Environment

```bash
printenv # view the enviornment variables
printenv | less
printenv | grep USER # find user info
```

Parameter expansion: if we write out the name of an environment variable prefixed with a dollar sign ($), the shell will replace it with the actual value. For example, `echo $USER` results in the USER variable’s value.

```bash
echo $USER # parameter expansion
```

## Startup Files

When we log in, the shell reads information from startup files. First, the shell reads from global config files that effect the environment for all users. Then, the shell reads startup files for specific users. The specific files the shell reads from depends on the type of session: login vs. non-login shell sessions

For login sessions:

- `/etc/profile` - global config for all users
- `~/.bash_profile` - user's personal config file
- `~/.bash_login` - read if bash_profile isn't found
- `~/.profile` - used if previous two aren't found

For non-login sessions (typical session when you launch the terminal via the GUI):

- `etc/bash.bashrc` - global config for all users
- `~/.bashrc` - specific settings for each user. This is where we can define our own settings and configuration.

Defining variables: to define a variable, use the syntax `variable=value.`Since built-in variable are upper-cased, so it’s a common convention to lowercase custom variables to prevent confusion.

```bash
# Define shell variable, which only exists in the current shell session
color = 'purple' 

export color = 'purple' # define enviornment variable

```

Define our own commands using alias keyword.

[What are your favorite bash aliases? | DigitalOcean](https://www.digitalocean.com/community/questions/what-are-your-favorite-bash-aliases)

(https://www.cyberciti.biz/tips/bash-aliases-mac-centos-linux-unix.html)

```bash
# -a: all, -l: long listing format, 
# -F: --classify, append indicator to entries
alias ll='ls -alF' 
type ll
which ll # show where it is

# The defined alias only exists in the current session

# If we want the alias to work across sessions, make edits in ~./bashrc
# The .bashrc file is a script that's executed when a user logs in. 
# The file itself contains a series of configurations for the terminal
# session.
nano ~/.bashrc

# get the top process eating cup
alias pscpu='ps auxf | sort -nr -k3'
alias pscup='ps auxf | sort -nr -k3 | head -10'

# We can put all self-defined alias in a separate file
cd ~
nano .bash_aliases
```

# Writing a Basic Script

```bash
nano hi # create a script named hi

####################################################################
# '#!/' is called the shebang, it tells which interpreter the OS 
# should use; After the shebang, we need to include the path to the
# Bash binary.  This is not Bash specific. If we wanted to write a
# python script, we would include the path to the python binary.

#!/bin/bash
echo "Hello there, $USER"
echo "Today is $(date)"
echo "last ran hi at $(date)" >> hi.log
####################################################################

# One way to execute hi
bash hi # if in the directory of hi
bash ~/hi # if not, provide complete path

# Another way to excute hi
echo $PATH # find path variable, directories separated by :
# Path Variable: a list of directories where the shell looks to
# try and find a program.

mkdir ~/bin # create a directory inside user home directory
mv hi bin/

# in Ubuntu, system automatically add $HOME/bin to path variable
less .profile 
source .profile # read and execute the content of the file
echo $PATH # now ~/bin is added to the path variable
# If you do not see #HOME/bin is added to the path variable, then
# you can add PATH="$HOME/$bin:PATH" to ~/.bashrc, 
# then source ~/.bashrc

# The reason permission denied is because hi is still not executable 
ls ~/bin/ -l 
chmod a+x ~/bin/hi # add x permission to all

which hi # find the location
```

```bash
# If we want to create and run a python script from terminal

which python3 # find the location
cd ~/bin # go to the bin of the user home directory

# One way to create and execute a python script
nano pyhi # or nano pyhi.py
###########################
print("Hellow there from Python")
###########################
python3 pyhi # or python3 pyhi.py

# Another way
nano pyhi # or nano pyhi.py
###########################
#!/usr/bin/python3
print("Hellow there from Python")
###########################
chmod a+x pyhi # or chmod a+x pyhi.py
pyhi # or pyhi.py

```

# Cron

The cron service allows us to schedule commands to run at regular intervals.

To set up a cron job, we need to edit the crontab configuration file. Rather than edit the files directly, it’s best to use `crontab -e` command.

When we use `crontab -e`, the change we make take effect immediately. 

[Crontab.guru - The cron schedule expression editor](https://crontab.guru/)

![CronSyntax](G:\My Drive\Github_jacob1338\Guide-Linux-Commands\Private\Private-Guide-Linux-Commands-Screenshots\CronSyntax.JPG)

![CronCharacters](G:\My Drive\Github_jacob1338\Guide-Linux-Commands\Private\Private-Guide-Linux-Commands-Screenshots\CronCharacters.JPG)


```bash
crontab -e # open the file to introduce tasks to be run by cron

#########################################################

# if error, also output error message to time.log
* * * * * command >> ~/time.log 2>&1 

# Run a job at minute 30, every hour (i.e. clock shows x:30)
30 * * * * command

# Run a job everyday at midnight
0 0 * * * command

# Rn a job at midnight every weekday
0 0 * * 1-5 command

# Run a job every 5 mintues
*/5 * * * * command

# Run a job every monday in April at 6:30AM
30 6 * 4 1 command
#########################################################
```