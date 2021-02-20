---
layout: post
title: Linux Useful Commands - ls, grep, pipe, ps, for, sleep,head, tail
categories: [Linux, Useful Commands]
tags: [Linux,Linux Terminal,pipe,bash,grep,ls,symlinks,ps,linux process status,inline shell script,sleep,for,shell script,inline bash script,head,tail]
mermaid: true 
---

## ls - List information about the FILEs

### Useful ls options
-l
: long listing format

-L
: show info about symbolic links reference

-1
: lined format

-a
: show hidden files

-h
: human friendly output format for sizes and more

-S
: sort by file size (directories would come first)

-t
: sort by modification time

-r
: reverse output order

-p
: append `/` indicator to directories

-F
:  append indicator (one of `*/=>@|`) to entries


###  ls -F and output prefixes meaning

|                   Prefix or Postfix                   |                                Meaning                                |
|:--------------------------------------|:--------------------------------------------------------------------|
|`/`                      | directories                                     |
|`@`                      | symbolic links                                     |
|`|`                      | FIFOs                                     |
|`=`                      | sockect                                     |
|`*`                      | executable files                                     |


### ls - Examples

show directories with a starting slash:
```bash
ls -p 
```
grep those not starting with slash:
```bash
grep -v /
```

list **only files** (not directories):
```bash
ls -p | grep -v /
```

piping to head command to show last **most recently modified file or directory**:
```bash
ls -t | head -1
```
piping to head command to **show largest file**:
```bash
ls -l -h -S | head -1
```

## Piping to grep

In many scenarios we can use grep to do more work on output.

find -F usage in help of ls command:
```bash
ls --help | grep F
```
find vscode process information in process status( ps)
```bash
ps a | grep 'vscode' 
```

cpu usage of vscode:
```bash
ps au | grep 'vscode' | awk '{print $3}'
```
`$3` grabs the 3rd column of output

use first 5 most cpu consuming processes:
```bash
ps -Ao user,uid,comm,pid,pcpu,tty --sort=-pcpu | head -n 6
```
or only:
```bash
ps -A --sort=-pcpu | head -n 6
```

get pid and name **most cpu consuming process**:
```bash
ps -A --sort=-pcpu | head -n +2 | awk '{if(NR>1)print $1"  "$4}'
```

get pid and name **most cpu consuming proccess continuously** with delays in between:
```bash
for i in {1..10}; do ps -Ao pcpu,comm --sort=-pcpu | head -n 2; sleep 5s; done;
```