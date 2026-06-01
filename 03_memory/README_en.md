# 03 Observing Memory

## Goal of this chapter

In this chapter, you will observe the memory state on Linux and understand how computers use memory when running programs.

In the previous chapter, you learned about CPU and processes.

Processes are executed by the CPU. However, a process does not run solely on the CPU.

When a program is executed, the program itself and the data being processed are placed on memory.

In other words, to understand processes, you also need to understand memory.

---

## Keywords

- Memory
- RAM
- Process
- Used Memory
- Free Memory
- Buffer
- Cache
- Swap
- `/proc/meminfo`

---

## What is Memory?

Memory is a temporary workspace for the computer.

If storage is "a place to save long-term," then memory is "a place to put what you're using now."

For example, when you start an application, the program is loaded from storage and expanded into memory.

The CPU processes instructions and data that are on memory.

---

## First, Let's Observe

On Linux, you can check the memory state with commands.

```bash
free -h
```

The `free` command displays the memory usage of the entire system.

When you add the `-h` option, it is displayed in human-readable units.

---

## How to Read the free Command

When you run `free -h`, items like the following are displayed:

```text
              total        used        free      shared  buff/cache   available
Mem:          7.6Gi       1.2Gi       4.8Gi       100Mi       1.6Gi       6.0Gi
Swap:         2.0Gi          0B       2.0Gi
```

The points to watch are as follows:

| Item | Meaning |
|---|---|
| total | Total amount of memory |
| used | Amount of memory in use |
| free | Amount of memory immediately available |
| buff/cache | Amount of memory used as buffers and caches |
| available | Amount of memory considered practically available |
| swap | Auxiliary area used when memory is insufficient |

---

## The Difference Between free and available

It is a bit risky to judge whether there is enough memory by looking at the `free` value alone.

On Linux, free memory is effectively utilized as a cache.

Therefore, even if `free` appears small, there may actually be memory remaining that can be reused as needed.

This is where `available` becomes important.

`available` represents the amount of memory that a new program can potentially use in the current state.

When checking memory availability, pay attention to not just `free`, but also `available`.

---

## Viewing More Detailed Memory Information

On Linux, memory information can also be checked as a text file.

```bash
cat /proc/meminfo
```

`/proc/meminfo` displays detailed information about memory.

For example, it contains items like the following:

```text
MemTotal
MemFree
MemAvailable
Buffers
Cached
SwapTotal
SwapFree
```

On Linux, you can check the state of the system from virtual files under `/proc`.

This is an important concept for learning Linux.

---

## Viewing Memory Usage per Process

Memory is used by running processes.

Let's check which processes use the most memory.

```bash
ps aux --sort=-%mem | head
```

This command displays processes with high memory usage from the top.

Looking at the `%MEM` column, you can see how much memory that process is using.

---

## Observing in Real-Time with top

The `top` command allows you to check CPU and memory usage in real-time.

```bash
top
```

On the `top` screen, memory information for the entire system is displayed at the top.

You can also check the CPU usage and memory usage of each process.

When exiting, press `q`.

---

## Memory and Swap

Swap is a mechanism that temporarily uses part of storage as a replacement for memory when memory is insufficient.

However, since storage is slower than memory, when swap is used extensively, the system's performance may become slow.

With `free -h`, you can also check swap usage.

```bash
free -h
```

Pay attention to the `Swap` row.

---

## Let's Observe

Run the following commands and observe the results.

```bash
free -h
```

```bash
cat /proc/meminfo | head
```

```bash
ps aux --sort=-%mem | head
```

```bash
top
```

---

## Missions

### Mission 1: Check the Memory Capacity of Your Environment

Run `free -h` and check the total amount of memory in your environment.

Items to check:

- total
- used
- free
- available

---

### Mission 2: Explain the Difference Between free and available

Explain the difference between `free` and `available` in your own words.

Example:

```text
free is the amount of memory immediately available, and available is the amount of memory that can potentially be used if needed.
```

---

### Mission 3: Observe /proc/meminfo

Run the following command:

```bash
cat /proc/meminfo | head
```

From the displayed items, select three that seem to have understandable meanings and explain them.

---

### Mission 4: Find Processes Using a Lot of Memory

Run the following command:

```bash
ps aux --sort=-%mem | head
```

From the displayed processes, identify those with high memory usage.

Items to check:

- USER
- PID
- %MEM
- COMMAND

---

### Mission 5: Think About the Relationship Between CPU and Memory

Complete the following sentence:

```text
A process is executed by the CPU, but the running program and data are placed on ________.
```

---

## Think About It

Think about the following questions in your own words:

1. What is the difference between memory and storage?
2. Why is memory used when a program is executed?
3. Why do you need to check `available` instead of just `free`?
4. Why does the system become slow when swap is used too much?

---

## Summary

Memory is a temporary workspace for the computer.

Processes are executed by the CPU, but the running program and data are placed on memory.

On Linux, you can observe the state of memory using commands like `free`, `top`, `ps`, and `/proc/meminfo`.

When looking at memory, rather than just memorizing numbers,

- What is using memory?
- How much headroom is there?
- How are processes and memory related?

It is important to observe these aspects.

In the next chapter, you will learn about storage and filesystems in contrast to memory.
