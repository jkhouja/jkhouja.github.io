---
title: "VIM cheatsheet"
tableofcontents: true
math: true
---


```text
'\' is the default <leader> in vim.  
```

## Basics
#### Saving and Exiting
```text
:w   Save
:wq  Save and quit
:q   Quit
:q!  Quit without Saving
```

#### Managing Buffers
```text
:e filename                Edit a file in a new buffer
:ls    List opened buffers
:b [chars]+ tab  switch to buffer
:bnext (or :bn)            go to next buffer
:bprev (of :bp)            go to previous buffer
:bd                        delete a buffer (close a file)
```

#### Splitting windows
```text
:sp filename            Open a file in a new horizontally split window
:vs filename            Open a file in a new vertically split window
ctrl+ws                 Split windows horizontally
ctrl+wv                 Split windows vertically
ctrl+ww                 switch between windows
ctrl+wq                 Quit a window
```

#### Modes
```text
Esc        Normal Mode
i          Insert Mode 
I          Insert Mode from in Visual Mode
v          Visual Mode
Shft + v   Visual Line Mode
Ctrl + v   Visual Block Mode | 
R          Replace Mode
```


#### Basic commands
```text
ctrl + L                  Refresh screen
u      Undo
Ctrl-r Redo
/      Search (See search section)
.      Repeat previous command
q:     Open Commands history window
q?     Open commands history window and search
```
## Navigation 
### Insert Mode
```text
Shift + arrow keys   Move one word in direction of arrow
```

### Command Mode
```text
h   move one character left
l   move one character right
j   move one row down
k   move one row up

w   move to beginning of next word
b   move to beginning of previous word
e   move to end of word

W   move to beginning of next word after a whitespace
B   move to beginning of previous word before a whitespace
E   move to end of word before a whitespace

0   move to beginning of line
$   move to end of line

gg  move to first line
G   move to last line
nG  move to n'th line of file (where n is a number)

Ctrl-B  page up
Ctrl-F  page down
Ctrl-D  move half-page down
Ctrl-U  move half-page up

Ctrl-o  jump to last cursor position
Ctrl-i  jump to next cursor position

*   next word under cursor
#   previous word under cursor
%   jump to matching bracket { } [ ] ( )
```

## Editing 

```text
Normal Mode

r[char]         Replace char under cursor with [char]
y + [direction] Copy + direction
d + [direction] Cut + direction
dd              Cut whole line
p               Paste after cursor
P               Paste before cursor

N + [command]   Repeat command N times
30i- Esc        Insert 30 dashes in a line (as a separator)

Editing in Visual Mode

1.Select text
2.Apply command [key] [Use I to insert chars before cursor and a after the cursor]
3.Esc #sometimes needed

y   yank (copy) marked text
d   delete marked text
~   switch case
```

### Cut and Paste
```text
yy - yank (copy) a line
2yy - yank 2 lines
yw - yank word
y$ - yank to end of line
p - put (paste) the clipboard after cursor
P - put (paste) before cursor
dd - delete (cut) a line
dw - delete (cut) the current word
x - delete (cut) current character
```

### Paste Mode
This mode is to paste from other applications without experiencing unexpected behaviors:
```text
    :set paste
    :set nopaste
```

### Insert Mode - Inserting/Appending text
```text
i - start insert mode at cursor
I - insert at the beginning of the line
a - append after the cursor
A - append at the end of the line
o - open (append) blank line below current line (no need to press return)
O - open blank line above current line
```

## Search / replace


### Searching and Replacing

```text         
/pattern                  search for pattern
?pattern                  search backward for pattern
n                         repeat search in same direction
N                         repeat search in opposite direction
:%s/[text1]/[text2]/gci   
                          % global search and not by line
                          g (global and not by column/block)
                          c (ask for confirmation)
                          I or i (case sensitive|insesitive)
```

### Regex:
```text
^ starts with
$ ends with
., *, \, [, ], ^, $  metacharacters.
\                    escape character
+, ?, \|, {, }, (,)  must be escaped to use their special function.
\t    tab
\d    digit
\.    . (period)
\s    whitespace
\n    new line when searching and null byte when replacing
\r    new line when replacing
\{#}  for repeating # times
\@=   Positive lookahead
\@!   Negative lookahead
\@<=  Positive lookbehind
\@<!  Negative lookbehind
```

## Useful things

### Formatting
```text
:%!column -t -s $'\t'     Format tsv / csv file nicely using tab as a separator. -s is for separator and $'\t' is for tab.

:%!python -m json.tool    Format JSON by passing the buffer into the command
```

### View subset of buffer
```text
:g/pattern                Only displays part of the buffer that matches the pattern
:g/pattern/command        Applies command to matching part of the patter
:g!/pattern               Parts that do NOT match pattern.  Same as :v/pattern
```


### Copying to clipboard of Mac OSX
```text
:w !pbcopy     Copy Only selection to clipboard
:%w !pbcopy    Whole file 
:r !pbpaste    paste from the clipboard 
```

### Rename multiple_matches

```text
after selecting text and hitting enter:
cgn
write replacement in visual mode then [esc]
.  #to reapply change for next match
n  #to skip next match
```

### Python syntax checker

```text
Jedi plugin is useful for code navigation
Add to follwoing to the vimrc:

let g:jedi#goto_definitions_command = "<leader>gg"
:SyntasticCheck "to run syntastic
```
