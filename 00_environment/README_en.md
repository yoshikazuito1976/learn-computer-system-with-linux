# 00_environment

## Goal of this chapter

In this chapter, you will learn how to check your current Linux environment.

Before operating a computer system, it is important to observe your current situation:

- Where am I?
- Which user am I using?
- What kind of OS am I running?
- What is the name of this machine?
- How long has this system been running?

In Linux, many types of system information are displayed as text.
The goal of this chapter is to read that text information and explain your environment in your own words.

---

## Learning flow

In this chapter, you will:

1. Check the current directory
2. Check the current user
3. Check the hostname
4. Check the OS information
5. Check the kernel information
6. Check the current date and time
7. Check the system uptime
8. Explain the environment in your own words

---

## 1. Check the current directory

First, check which directory you are currently in.

```bash
pwd
```

`pwd` stands for “print working directory”.
It displays the directory where you are currently working.

**Example output**

```text
/home/siwuser/learn-computer-system-with-linux
```

From this result, you can understand where you are working in the filesystem.

---

## 2. Check the current user

Next, check which user you are using.

```bash
whoami
```

**Example output**

```text
siwuser
```

In Linux, different users may have different permissions.
Therefore, it is important to know which user you are currently using.

---

## 3. Check the hostname

Check the name of the computer you are operating.

```bash
hostname
```

**Example output**

```text
localhost.localdomain
```

A hostname is the name used to identify a computer, especially on a network.

---

## 4. Check the OS information

There are many Linux distributions, such as Ubuntu, AlmaLinux, Debian, and Rocky Linux.

You can check the OS information with the following command:

```bash
cat /etc/os-release
```

**Example output**

```text
NAME="AlmaLinux"
VERSION="9.5 (Teal Serval)"
ID="almalinux"
VERSION_ID="9.5"
```

You can read the Linux distribution name and version from this file.

**Important items to check**

- `NAME`
- `VERSION`
- `ID`
- `VERSION_ID`

---

## 5. Check the kernel information

The kernel is the core part of the operating system.

You can check kernel-related information with this command:

```bash
uname -a
```

**Example output**

```text
Linux localhost.localdomain 5.14.0-503.el9.x86_64 #1 SMP PREEMPT_DYNAMIC x86_64 GNU/Linux
```

From this output, you can find information such as:

- OS type
- Hostname
- Kernel version
- CPU architecture

`/etc/os-release` shows information about the Linux distribution.
`uname -a` shows information closer to the kernel.

---

## 6. Check the current date and time

Check the current date and time.

```bash
date
```

**Example output**

```text
Sat May 30 15:20:00 JST 2026
```

Time information is important in system administration.
For example, when reading logs, you need to know when an event happened.

---

## 7. Check the system uptime

Check how long the system has been running.

```bash
uptime
```

**Example output**

```text
15:20:10 up 2 hours, 15 minutes, 1 user, load average: 0.00, 0.01, 0.05
```

From this output, you can check:

- Current time
- How long the system has been running
- Number of logged-in users
- System load average

---

## Run all commands together

Try running all the commands together.

```bash
pwd
whoami
hostname
cat /etc/os-release
uname -a
date
uptime
```

Read each result and check the following points:

- Which directory am I in?
- Which user am I using?
- What is the hostname?
- What is the OS name and version?
- What is the kernel version?
- Is the current time correct?
- How long has the system been running?

---

## Think about it

Answer the following questions in your own words.

1. What information can you check with `pwd`?
2. What information can you check with `whoami`?
3. What kind of information is written in `/etc/os-release`?
4. What is the difference between `uname -a` and `/etc/os-release`?
5. Why is it important to check the date, time, and uptime when managing a server?

---

## Key point of this chapter

In Linux, you can observe the state of a system by using commands.

The important thing is not only to memorize command names.

You also need to read the text output of commands and explain what it means.

Learning computer systems starts with observation.
