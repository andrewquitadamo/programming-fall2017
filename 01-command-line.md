class: center, middle

#Introduction to the Command Line  

---

This lesson is to get you comfortable with the command line and give you an idea of what some of what it can do. 

--

Most of these commands have many more options, and are more powerful than the simple examples here.  

--

They are commands I've found useful, and is by no means an exhaustive list.  

--

**Instructions**  
To follow along copy and paste 
```
wget https://github.com/andrewquitadamo/bioinformatics-skills/archive/master.zip \
&& unzip master.zip && cd bioinformatics-skills-master/data/01-command-line/
``` 
into your terminal.
 
---

##Moving Around   

--

###pwd  
Prints path of current directory:  
```
pwd  
```  
--

**Instructions**  
Use `pwd` in your current directory.  
The results should look something like:  

```
/Users/andrewquitadamo/bioinf-ds/bioinformatics-skills-master/data/01-command-line
```  

---

###ls  
List contents of current directory:  
```
ls
```

--

List contents of current directory and size:  
```
ls -s
```  

--

List contents of current directory with permissions, size, and date modified:  
```
ls -l
```

--
  
List  contents of current directory sorted by date modified:  
```
ls -t
```  

--

Reverse the results:  
```
ls -r
```  

--

Show all files and directories, including hidden ones:  
```
ls -a
```  

---

###ls (cont.)

These options can be combined together. For example to list all the contents of a directory by time, in the long format, and reversed you would use `ls -altr`.  

--

**Instructions**  
Use `ls` in your current directory. 
The results should look like `SV_gene_sample SV_pos miRNA.tar.gz`.  

---

###mkdir
Creates new directory  
```
mkdir directory_name
```  

--

**Instructions**  
Use `mkdir` to create a new directory called `results`.  
Use `ls` to check your work.  

**Notes**  
Don't use spaces in your directory or file names.

---

###cd
Change directory:  
```
cd directory_name
```  

--

Move one directory up:  
```
cd ..
```  

--

Move to home directory:  
```
cd
```  

--

**Instructions**  
`cd` into `results`.  
Use `pwd` to check where you are.  
Then `cd ..` back up to the previous directory.

---

###Tab-completion
Tab completion is your friend. 

--

You can hit tab to fill in the rest of a command, filename or directory.  

--

**Instructions**  
Use tab completion to move into the `results` directory. 
Only type in `re` before hitting `tab`.

---

##Moving Files  

--

###cp  
Copy file to another directory:  
```
cp file directory
```  

--

Copy file to a new name:  
```
cp oldfile newfile
```  

--

**Instructions**  
Use `cp` to copy `SV_gene_sample` to `result`.  
Use `cp` to create a copy of `SV_gene_sample` called `SV.copy`.  
Use `ls` to check that the new files exist.

---

###mv  
Move file to another directory:  
```
mv filename directory
```  

--

Rename file:  
```
mv original_filename new_filename
```  

--

**Instructions**  
Use `mv` to rename `SV.copy` to `SV.new`.  
Use `mv` to move `SV.new` to `results`.  

---

###rm  
Remove file:  
```
rm file
```  

--

Remove directory:  
```
rm -r directory
```

--
  
**Instructions**  
`cd` into results and use `rm` to remove `SV.new`.

---

##Working with Files

--

###touch
Create new file:  
```
touch file
```  

--
**Instructions**  
Use `touch` to create a file called `empty_file`

---

###head  
Display first 10 lines of a file:  
```
head file
```  

--

Display first n lines of a file:  
```
head -n file
```  

--

**Instructions**  
Use `head` to display the first 20 lines of `SV_gene_sample`.

---

###>
Redirects the output of a command to a file.  
```
command > file
```
--

**Instructions**  
Redirect the output of the previous `head` command into a new file called `first_20_SV`.

---

###<  
Redirects the following as input for the command:  
```
head < file
```  

--

Can also be used to redirect a subshell evaluation to a command:  
```
head -n 2 <(ls)
```

---

###tail  
Display last 10 lines of a file:  
```
tail file
```  

--

Display last n lines of a file:  
```
tail -n file
```  

--

**Instructions**  
Use `tail` to print out the last 10 lines of `SV_gene_sample` and redirect the output to a new file called `last_10_SV`.

---

###cat  
Display contents of file:  
```
cat file
```  

--

Concatenate files:  
```
cat file1 file2
```  

--

**Instructions**  
Use `cat` to display `last_10_SV`.  
Use `cat` to combine `first_20_SV` and `last_10_SV`. Redirect the results to a new file called `SV_30`.

---

###| 
Pipe the output of a command to another command.  
```
command1 file | command2
```  

--

**Instructions**  
Use `head` and `tail -n 1` to get the tenth line of `SV_gene_sample`.

---

###column
Can be used to nicely display tabular files:  
```
column -t filename
```  
--

```
head filename | column -t
```  

--

**Instructions**  
Use column to view `SV_gene_sample`.

---

###cut
Use cut to extract columns from tabular files.  

Get second column from a file:
```
cut -f 2 file1
```

--

Get first to fouth columns:
```
cut -f 1-4 file1
```  

--

**Instructions**  
Use `cut` to get the first column of `SV_gene_sample`.

---

###sort  
Sort a file by lines:  
```
sort file1
```  

--

Sort a file numerically:  
```
sort -n file1
```  

--

Sort a file in reverse:  
```
sort -r file1
```  

--

**Instructions**  
Use `cut` and `sort` in combination to sort the first column of `SV_gene_sample`.

---

###uniq  
*Requires input to be sorted first  

Filter out repeated lines:  
```
uniq file1
```  

--

Count the occurences:  
```
uniq -c file1
```  

--

**Instructions**  
Use `cut`, `sort`, and `uniq` to only get the unique values form the first column.  
Add the `-c` flag to count the number of occurences of each value.

---

###grep  
Display all the instances of a pattern:  
```
grep 'pattern' file
```  

--

Count the lines that contain a pattern:  
```
grep -c 'pattern' file
```  

--

**Instructions**  
Use `grep` to find all instances of "YL_CN_MSL_117" in `SV_gene_sample`.
Use `grep` to find all `DUP`s in `SV_gene_sample`.

---

###sed  
Print i-j lines of a file:  
```
sed -n i,jp file
```   

--

Delete first line of a file:  
```
sed 1d file1
```  

--

Delete i-j lines of a file:  
```
sed i,jd file1
```  

--

Replace pattern in file:  
```
sed 's/find/replace/g' file1
```  

--

**Instructions**  
Use `sed` to remove the header of `SV_gene_file`.   
Use `sed` to replace all tabs (`\t`) with commas in `SV_gene_file`.  

---

###join
Combine files based on common fields:  
```
join -1 1 -2 1 file1 file2
```  

The common fields have to be in sorted order.  

--

**Instructions**  
Use join to combine `SV_gene_sample` and `SV_pos`. 
You will need to use sort and redirection to get the files in sorted order first.

---
##Working Remotely  

--

###ssh  
Log into a server:  
```
ssh username@server.address
```
  
--

Example:
```
ssh username@viper.urc.uncc.edu
```  

---

###scp  
Download files from a server:  
```
scp username@server.address:/path/to/file /desired/location/on_local_machine
```  
Upload files to a server:  
```
scp /local/path/to/file/ username@server.address:/desired/location
```  

---

###wget
Download file:  
```
wget ftp://url/path/to/file
```  

--
**Instructions**
Use `wget` to download the chromosome Y FASTA file from `ftp://hgdownload.cse.ucsc.edu/goldenPath/hg19/chromosomes/chrY.fa.gz` 

---

##Miscellaneous  

--

###tar
Unzip a tar.gz file:  
```
tar xvfz archive_name.tar.gz
```  

--

Unzip a .gz file:  
```
gunzip archive_name.gz
```  

--

**Instruction**  
Use `tar` to decompress `miRNA_gene.tar.gz`.  
Use `gunzip` to decompress `chrY.fa.gz`.  

---

###less
Interactive viewing of files:  
```
less filename
```  

--

You can move around using the keyboard.  
`f` go forward one screen.  
`b` go backward one screen.  
`h` display the help.  
`g` go to the beginning.  
`G` go to the end.  
`/searchterm` search for searchterm.  
`n` next search result.  

--

**Instructions**  
Use `less` to inspect `chrY.fa`.  

---

###diff
Display the differences between files:  
```
diff file1 file2
```  

--

**Instrucions**  
Use `diff` to find the changes between `SV_30` and `SV_gene_sample`.  

---

###history
Display your command line history:
```
history
```

--

You can set the number of lines you want to keep by using `export HISTSIZE=2000`

---

###Ctrl-r
Allows you to search back through your history:  
```
ctrl-r searchterm
```  

--

You can hit `ctrl-r` again to cycle back through your history.

--

**Instructions**  
Use `ctrl-r` to find the `sed` commands that you used.  

---

###chmod
Allow user, group and others to read, write and execute:  
```
chmod 777 file
```  

--

Allow user to read, write and execute, group and others to read and execute:  
```
chmod 0755 file
```  

---

###man  
Get the manual page for a command:  
```
man command
```  
 
--

**Instructions**  
Use `man` to look up the manpage for the `ls` command. 

---

###Resources
[GNU Coreutils Cheatsheet](http://www.catonmat.net/download/gnu-coreutils-cheat-sheet.pdf)  
