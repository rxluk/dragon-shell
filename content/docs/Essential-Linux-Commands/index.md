---
title: "Essential Linux commands"
description: >
  Essential Linux terminal commands for anyone who wants to master the shell.
date: '2025-08-01T08:30:00-03:00'
draft: false
tags:
  - linux
  - shell
  - terminal
categories:
  - docs
authors:
  - luk
cover:
  image: pattern.png
---

The terminal is one of the most powerful tools in Linux. If you're beginning your journey as a hacker, sysadmin, or developer, understanding the basics of the shell is essential.

In this post, we'll explore the main commands and how to use them in practice.

---

## 📁 Navigating Between Directories

### `ls` - List files and directories

```bash
ls              # list files
ls -l           # long listing format
ls -a           # show hidden files
ls -lh          # human-readable sizes
ls -la          # detailed + hidden files
```

### `cd` - Change directory

```bash
cd /path/to/folder
cd ..           # go up one level
cd ~            # go to home directory
```

---

## 🗂 Copying, Moving, and Deleting Files

### `cp` - Copy files

```bash
cp source.txt destination/
cp -r folder/ /destination/     # recursive copy
```

### `mv` - Move or rename files

```bash
mv file.txt /destination/
mv oldname.txt newname.txt
```

### `rm` - Remove files and folders

```bash
rm file.txt
rm -r folder/                   # recursive removal
rm -rf /                       # ⚠️ deletes everything, use with extreme caution
```

---

## 📊 Disk Space

### `df` - Show disk usage

```bash
df -h                          # human-readable format
```

### `du` - Show file/folder size

```bash
du -sh *                       # size of all items in current directory
```

---

## 📥 Download Files

### `wget` - Download from a URL

```bash
wget https://site.com/file.zip
```

---

## 🔍 Searching Content

### `grep` - Search for patterns in files

```bash
grep "text" file.txt
grep -i "word" file.txt        # case-insensitive search
grep -r "word" /path           # recursive search
grep -n "error" log.txt        # show line number
grep -v "string" file.txt      # exclude lines containing string
```

---

## 🧪 Regular Expressions with `grep`

```bash
grep "^root" /etc/passwd        # lines starting with 'root'
grep "[0-9]" file.txt           # lines with numbers
grep -E "error|fail" log.txt    # error OR fail
```

---

## ✂️ Cut Columns or Characters

### `cut` - Slice text from lines

```bash
cut -d ':' -f1 /etc/passwd      # show first column using ':' delimiter
cut -c 1-5 file.txt             # show characters 1 to 5
```

---

## 📢 Display Messages or Variables

### `echo` - Print to terminal

```bash
echo "Hello, world!"
echo $USER
echo "User: $USER, Directory: $PWD"
```

### Redirection with `>` and `>>`

```bash
echo "new line" > file.txt     # overwrite file
echo "another line" >> file.txt # append to file
```

---

## 🧠 Pro Tip: Combine Commands

You can use pipes (`|`) to chain commands together:

```bash
cat file.txt | grep "error" | cut -d ' ' -f2
```

---

Mastering and practicing these commands is an essential step for any hacker, Linux enthusiast, or even developer. Keep practicing, writing your own scripts, and exploring more options!
