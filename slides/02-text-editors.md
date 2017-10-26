class: center, middle

#Introduction to Text Editors

---

This lesson is to get you familiar with three different text editors: Nano, Emacs, and Vim.

--

Each has their own strengths, and you should pick one to be your primary editor. 

--

However you should also be somewhat familiar with the others, and know enough to open, edit, save and then quit.

--

Text editors may seem simple, but they are quite powerful underneath.

--

Unlike their GUI counterparts they can be used directly from the command line.

--

**Instructions**  
To follow along copy and paste `curl https://raw.githubusercontent.com/andrewquitadamo/bioinformatics-skills/master/data/02-text-editors/tale-of-two-cities.txt -O` into your terminal.

---

#Nano

Nano is the simplest text editor we will talk about.
It comes installed on many systems.

--

The filename will be at the top, and a small list of commands will be at the bottom.

--

The `^` character stands for the `Ctrl` key.

--

**Instructions**  
To start using Nano open up the command line and type:  
```
nano tale-of-two-cities.txt 
```  

---

##Moving Around

To start moving around the file, use the arrow keys.

--

To move down a page, use `Ctrl-V`.

--

To move up a page, use `Ctrl-Y`.

--

To go to the end of the line, use `Ctrl-E`.

--

To go to the beginning of the line, use `Ctrl-A`.

--

To go to the next line, use `Ctrl-N`.

--

To go to the previous line, use `Ctrl-P`.

--

**Instructions**  
Practice moving around the file 

---

##Editing

To start editing the file, just type.

--

In the upper right corner, Nano will now indicate the file has been modified.

--

**Instructions**  
Add some new text to `tale-of-two-cities.txt`

---

##Saving

To save the modified file use `Ctrl-O`. 

--

This will bring up a dialog with the filename. 

--

To save the file, hit enter.

--

**Instructions**  
Save your modifications to `tale-of-two-cities.txt`

---

##Copying, Cutting, and Pasting

To cut a line of text, use `Ctrl-K`.

--

To paste a line of text, use `Ctrl-U`.

--

To copy a line of text, use `Meta-^`, where `Meta` is the `Esc` key.

--

To highlight a portion of text for copying or cutting, use `Ctrl-^`.

--

**Instructions**  
Cut a line of text, and then paste it below the next line.  
Highlight the first half of a line, and paste it below the current line.

---

##Searching

To search for text, use `Ctrl-W`

--

To search and replace, use `Ctrl-\`

--

**Instructions**  
Search for 'season' in `tale-of-two-cities.txt`

---

##Getting Help

Use `Ctrl-G` to view the help screen.

--

**Instructions**  
Take a look at the other commands you can use in Nano.

---

##Quitting

To exit use `Ctrl-X`. 

--

Nano will ask you if you want to save your file, if you have unsaved changes.

--

**Instructions**  
Exit out of Nano

---

#Emacs

Emacs is a powerful text editor that also provide various other utilities.

--

Some operating systems come with Emacs, others do not. 

--

`C` stands for `Ctrl`

--

`M` stands for `Meta`, which is usually `Alt`

--

**Instructions**  
To start using Emacs, type `emacs tale-of-two-cities.txt`

---

##Moving Around

You can use the arrow keys to move around.

--

To move down a screen, use `C-v`

--

To move up a screen, use `M-v`

--

To move down one line, use `C-n`

--

To move up one line, use `C-p`

--

To move to the end of the line, use `C-e`

--

To move to the beginning of the line, use `C-a`

--

**Instructions**  
Practice moving around the file

---

##Editing

Just like Nano, all you have to do is start typing.

--

**Instructions**  
Add some new text to `tale-of-two-cities.txt`

---

##Saving

To save your changes, use `C-x C-s`

--

**Instructions**  
Save your changes to `tale-of-two-cities.txt`

---

##Copying, Cutting, and Pasting

To cut a line of text use `C-k`

--

To paste a line of text use `C-y`

--

To highlight a portion of text, hit `C-space` and then move to the end of the section you want to highlight.

--

To cut a portion of text use `C-w`

--

To copy a protion of highlighted text use `M-w`

--

**Instructions**  
Practice cutting and pasting lines.  
Practice highlighting sections and copying them.

---

##Undoing Changes

To undo a command use `C-x u`

---

##Searching

To search, use `C-s`. This is the forward search.

--

`C-r` is the reverse search, and will search from where you are upwards.

--

You can hit `C-s` or `C-r` multiple times to cycle through the results.

--

**Instructions**  
Search for 'epoch' in the file

---

##Getting Help

Use `C-h C-h` to open up the helps screen

--

**Instructions**  
Open up the help menu, and take a look around.

---

##Quitting

To quit, use `C-x C-c`. 

--

Emacs will ask you if you want to save any unsaved changes.

--

**Instructions**  
Exit out of Emacs

---

#Vim

Vim is a powerful text editor. 

--

Vim comes installed on pretty much everything. 

--

If you have a smart toaster, it probably has Vim on it.

--

**Instructions**  
To start using Vim type `vim tale-of-two-cities.txt`

---

##Moving Around

You can move around with the arrow keys.  

--

However you can use `h`,`j`,`k`,`l` to move left, down, up, and right respectively.

--

To move to the beginning of the file use `gg`

--

To move to the end of the file use `G` 

--

To move to the end of a line, use `$`

--

To move to the beginning of the line, use `0`

--

To move to the next word, use `w`

--

To move back a word, use `b`

--

**Instructions**  
Move around the file using the commands. Try to not use the arrow keys. 

---

##Editing

Vim has a special mode for editing. To enter it, hit `i`, which stands for interactive mode.

--

In the interactive mode you can't use your commands for moving around.

--

To exit interactive mode, hit the `Esc` key. This will bring you to the command mode.

--

**Instructions**  
Enter interactive mode and edit some text.  
Remember to exit out of interactive mode when you are done.

---

##Saving

To save enter command mode (`Esc`) and type `:w`

--

**Instructions**  
Save your changes

---

##Copying, Cutting, and Pasting

`dd` cuts the current line.

--

`p` pastes text below the current line.

--

`P` pastes text above the current line.

--

`yy` copies the current line.

--

**Instructions**  
Practice copying, cutting and pasting lines of text

---

##Combining Commands with Numbers

You can repeat a command N times by using `Ncommand`.

--

For example to move up 10 lines you could use `10k`, or to delete 15 lines you could use `15dd`.

--

**Instructions**  
Try to copy 5 lines of text and paste them above the current lines.

---

##Undoing Changes

To undo your last edit, go to the command mode (hit `Esc`) and type `u`.

---

##Searching

To start searching enter command mode (`Esc`), and type `/searchterm`.

--

Hit `n` to go to the next result or `N` to go to the previous result.

--

**Instructions**  
Search for 'was' and cycle through the results.

---

##Getting Help

Use `:h` or `:help` to open up the help screen. 

--

**Instructions**  
Open up the help screen and see what is available.

---

##Quitting

Use `:q` to quit. Vim won't quit if you have unsaved changes. Use `:q!` to force quitting without saving.

--

To save and quit use `:wq`

--

**Instructions**  
Exit out of Vim

---

##Resources
I highly recommend you choose either Vim or Emacs and learn how to use it well.  
They are very useful and have many tricks to help make you very productive.  

* [Vim Tutorial and Introduction](http://danielmiessler.com/study/vim/)  
* [Learn to Speak Vim](http://yanpritzker.com/2011/12/16/learn-to-speak-vim-verbs-nouns-and-modifiers/)  
* [Series of Articles on Learning Vim](http://benmccormick.org/tag/learning-vim-in-2014/)  
* [Intermediate Vim Tips](http://ideasintosoftware.com/vim-productivity-tips/)  
* [How to Boost Your Vim Productivity](http://sheerun.net/2014/03/21/how-to-boost-your-vim-productivity/)  
* [Everything You Need To Know About Vim](https://github.com/mhinz/vim-galore)  
* [Absolute Beginners Guide to Emacs](http://www.jesshamrick.com/2012/09/10/absolute-beginners-guide-to-emacs/)  
* [Emacs Tutor](http://tuhdo.github.io/emacs-tutor.html)  
* [Emacs Tour](http://www.gnu.org/software/emacs/tour/)  
