# 01_os_and_distribution

## Goal of this chapter

In this chapter, you will examine the differences between the **OS**, the **Linux kernel**, and the **distribution** in a Linux environment.

In computer systems learning, the word "OS" appears very often.
However, when using Linux, you need to distinguish the following terms:

* OS
* Linux
* Linux kernel
* Distribution
* Version
* Architecture

In this chapter, you will not just memorize these as terms.
You will run commands in a real Linux environment and understand them by reading the displayed information.

---

## Learning flow

In this chapter, you will:

1. Check what an OS is
2. Check what the Linux kernel is
3. Check what a distribution is
4. Check what a shell is
5. Read `/etc/os-release` to check OS information
6. Use `uname` to check kernel information
7. Check the difference between `/etc/os-release` and `uname`
8. Think about the differences between AlmaLinux and Ubuntu
9. Run confirmation commands and organize system information
10. Explain the information in your own words

---

## 1. What is an OS?

OS stands for Operating System.

An OS is the basic software that sits between computer hardware and applications, and manages the whole computer.

For example, an OS manages:

* CPU
* Memory
* Storage
* Files
* Processes
* Users
* Network
* Input/output devices

Windows, macOS, and Linux are examples of operating systems.

Learning Linux is not only about memorizing commands.
It is also about observing how an OS manages a computer.

---

## 2. What is the Linux kernel?

Strictly speaking, the word Linux refers to the **Linux kernel**.

The kernel is the core part of the OS.
It manages hardware-near components and allows applications and commands to use the computer safely.

For example, the kernel is responsible for:

* Process management
* Memory management
* Filesystem management
* Device management
* Network communication management

What we usually call "Linux" is not only the kernel.
It is a combination of the kernel, commands, libraries, package management systems, configuration files, and more.

---

## 3. What is a distribution?

A **Linux distribution** is a package that combines the Linux kernel with various software and management tools in a usable form.

Typical distributions include:

* Ubuntu
* Debian
* AlmaLinux
* Rocky Linux
* Fedora
* Arch Linux

Even though they are all Linux, distributions have differences.

For example, package management commands may differ.

| Family | Examples | Package management |
| --- | --- | --- |
| Debian-based | Ubuntu, Debian | `apt` |
| Red Hat-based | AlmaLinux, Rocky Linux, Fedora | `dnf`, `yum` |

So when using Linux, it is important to check not only that it is Linux, but also **which distribution you are using**.

---

## 4. What is a shell?

When operating Linux, we often type commands in a terminal.

At that time, the program that receives user input, interprets it, and requests processing from the OS is called a **shell**.

The shell acts as an interface between the user and the OS.

```text
User
-> Shell
-> OS / Kernel
-> Hardware
```

For example, suppose you type the following command:

```bash
ls
```

The shell interprets the input `ls` and runs the corresponding program.
As a result, a list of files and directories in the current directory is displayed.

---

### Types of shells

Linux uses several kinds of shells.

Typical examples are:

| Shell | Description |
| --- | --- |
| `sh` | Basic Unix-like shell |
| `bash` | Representative shell used in many Linux environments |
| `zsh` | Shell with enhanced completion features |
| `fish` | Shell focused on usability |

In classes and learning materials, `bash` is often used.

You can check your current shell with:

```bash
echo $SHELL
```

Example output:

```text
/bin/bash
```

You can also check the currently running shell process with:

```bash
ps
```

Example output:

```text
	PID TTY          TIME CMD
 1234 pts/0    00:00:00 bash
 1250 pts/0    00:00:00 ps
```

In this example, you can see that `bash` is running as the shell.

---

### Shell and command input

The shell does more than just run commands.

It also provides features such as:

* Interpreting commands
* Handling variables
* Connecting commands with pipes `|`
* Redirecting output with `>` and `>>`
* Running shell scripts
* Managing command history

In other words, much of command-line operation in Linux is done through the shell.

---

### Relationship between OS, kernel, and shell

The relationship can be summarized as follows:

| Term | Role |
| --- | --- |
| Kernel | Core of the OS that manages hardware-near components |
| Distribution | Package of Linux kernel and various software |
| Shell | Program that receives user commands and requests processing from the OS |
| Terminal | Screen/application used to operate a shell |

An important point is that **terminal and shell are not the same**.

The terminal is the screen for typing and displaying text.
The shell is the command interpreter running inside it.

```text
Terminal
-> A screen for operating the shell

Shell
-> A program that interprets and executes commands
```

Understanding this distinction helps you describe Linux operation more accurately.

---

## 5. Check OS information

In Linux, you can check OS and distribution information in `/etc/os-release`.

```bash
cat /etc/os-release
```

Example output:

```text
NAME="AlmaLinux"
VERSION="9.5 (Teal Serval)"
ID="almalinux"
VERSION_ID="9.5"
PLATFORM_ID="platform:el9"
PRETTY_NAME="AlmaLinux 9.5 (Teal Serval)"
```

Key items to check:

| Item | Meaning |
| --- | --- |
| `NAME` | Distribution name |
| `VERSION` | Version name |
| `ID` | Internal identifier used by the system |
| `VERSION_ID` | Version number |
| `PRETTY_NAME` | Human-readable display name |

From this, you can identify the type of Linux you are using.

---

## 6. Check kernel information

Next, check kernel information.

```bash
uname -a
```

Example output:

```text
Linux localhost.localdomain 5.14.0-503.el9.x86_64 #1 SMP PREEMPT_DYNAMIC x86_64 GNU/Linux
```

This result includes information such as:

| Information | Meaning |
| --- | --- |
| `Linux` | Kernel name |
| `localhost.localdomain` | Hostname |
| `5.14.0-503.el9.x86_64` | Kernel version |
| `x86_64` | CPU architecture |
| `GNU/Linux` | Information indicating OS type |

If you want a shorter check, you can also use:

```bash
uname -r
```

This shows only the kernel version.

```bash
uname -m
```

This shows the machine architecture.

---

## 7. Difference between `/etc/os-release` and `uname`

Both `/etc/os-release` and `uname` are used to check system information.
However, the type of information they show is different.

| Command / file | What it shows |
| --- | --- |
| `cat /etc/os-release` | Distribution information |
| `uname -a` | Kernel information |
| `uname -r` | Kernel version |
| `uname -m` | CPU architecture |

In short:

```text
/etc/os-release
-> Check which Linux distribution it is

uname
-> Check which kernel it is running on
```

Understanding this difference helps you use the word "Linux" more accurately.

---

## 8. Think about the differences between AlmaLinux and Ubuntu

AlmaLinux and Ubuntu are both Linux distributions.
However, they differ in family and common use cases.

| Item | AlmaLinux | Ubuntu |
| --- | --- | --- |
| Family | Red Hat-based | Debian-based |
| Package management | `dnf` | `apt` |
| Common use cases | Servers, enterprise systems | Servers, desktops, learning environments |
| Configuration style | Red Hat-style conventions | Debian-style conventions |

Even within Linux, commands and configuration methods may differ depending on the environment.

So when reading tutorials or web articles, you should pay attention to:

* Which distribution the explanation assumes
* Whether the same commands work in your environment
* Whether the package manager is `apt` or `dnf`
* Whether configuration file locations are the same

---

## 9. Try running commands

Run the following commands and check the results.

```bash
cat /etc/os-release
uname -a
uname -r
uname -m
hostnamectl
```

With `hostnamectl`, you can also check OS, kernel, and architecture information together.

---

## 10. Observation notes

Based on the command outputs, fill in the table below.

| Item | Your environment |
| --- | --- |
| Distribution name | |
| Version | |
| ID | |
| Kernel version | |
| Architecture | |
| Hostname | |
| Package management command | |

---

## Think about it

Answer the following questions in your own words.

1. What kind of software is an OS, and what does it manage?
2. What is the Linux kernel?
3. What is a Linux distribution?
4. What can you check with `/etc/os-release`?
5. What can you check with `uname -a`?
6. What are the differences between AlmaLinux and Ubuntu?
7. Why is it necessary to consider distribution differences when reading web articles and learning materials?

---

## Key point of this chapter

When using Linux, it is important not to judge the environment with only the single word "Linux."

Even within Linux, the distribution, version, kernel, and package management method can differ.

The key is to observe your own environment first, and be able to explain what OS, distribution, and kernel you are working on.

In computer systems learning, it is not enough to memorize terms.
It is important to build the ability to read information from a real environment.