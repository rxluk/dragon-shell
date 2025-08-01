---
title: 'Users and Permissions in Linux'
description: >
  Understand how user creation, groups, and file read, write, and execute permissions work in Linux.
date: '2025-08-01T14:30:00-03:00'
draft: false
tags:
  - linux
  - permissions
categories:
  - docs
authors:
  - luk
cover:
  image: pattern.png
---

Managing users and permissions in Linux is essential to keeping the system secure and organized, especially in multi-user environments or servers.

Let’s explore the fundamental commands and concepts for handling user accounts, groups, and permissions in Linux.

---

## 👥 User Management

### `adduser` / `useradd` - Create users

```bash
adduser username             # creates a user with an interactive assistant
useradd username             # more direct method
```

### `passwd` - Set or change user password

```bash
passwd username              # sets or changes the user's password
```

### `deluser` / `userdel` - Remove users

```bash
deluser username
userdel username
userdel -r username          # also removes the home directory
```

---

## 👪 Group Management

### `addgroup` / `groupadd` - Create groups

```bash
addgroup groupname
groupadd groupname
```

### `usermod` - Add user to a group

```bash
usermod -aG group username    # adds user without removing from other groups
```

### `groups` - View user's groups

```bash
groups                        # shows current user's groups
groups username               # shows groups for another user
```

---

## 🔐 File Permissions

In Linux, files and directories have permissions defined for:

- **User (owner)**
- **Group**
- **Others**

### Check permissions with `ls -l`

```bash
ls -l file.txt
```

Example output:

```
-rw-r--r-- 1 luk users 1024 Aug 1 08:00 file.txt
```

Meaning:

- `rw-` = owner can read and write
- `r--` = group can only read
- `r--` = others can only read

---

## 🛠 Changing Permissions

### `chmod` - Change permissions

```bash
chmod 755 script.sh          # rwxr-xr-x
chmod u+x file.sh            # adds execute permission for the owner
chmod -R 644 *.txt           # recursively applies permission
```

Quick reference:
- `r` = 4 (read)
- `w` = 2 (write)
- `x` = 1 (execute)

---

## 👤 Changing Owner and Group

### `chown` - Change file owner

```bash
chown user file.txt
chown user:group file.txt
```

### `chgrp` - Change only the group

```bash
chgrp group file.txt
```

---

## 🔒 Special Permissions (Advanced)

### Sticky Bit

Prevents users from deleting others' files in shared directories (like `/tmp`):

```bash
chmod +t /directory
```

### Setuid and Setgid

Allows executables to run with the owner's or group's permissions:

```bash
chmod u+s binary      # setuid
chmod g+s folder      # setgid
```

---

## 🔍 Check UID, GID, and File Details

```bash
id                      # shows UID, GID and groups
stat file.txt           # complete file information
```

---

Managing users and permissions is a core skill in Linux system administration — and a fundamental part of offensive security: an attacker needs to know how to escalate privileges, and a defender needs to know how to prevent it.

---
