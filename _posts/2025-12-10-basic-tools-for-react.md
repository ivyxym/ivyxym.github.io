---
title: "Comfortable Terminal on Windows (WSL + Hyper)"
date: 2025-12-10

---

Today I learned about several tools involved in the full lifecycle of developing a React application—tools that exist purely to make the workflow more efficient. This is one of the things I really love about *The Joy of React*: Josh completely puts aside the developer ego and the “default assumptions” often found in the English-speaking tech world. He even mentions tools like Chrome—which, for various reasons, may not be the most popular browser in some non-English-speaking countries—and Bash, which can be frustrating to use if your operating system is Windows.

I feel that many so-called beginner tutorials either focus too much on basic syntax without touching underlying principles or real-world issues, making them disconnected from reality and difficult to stay motivated with; or they fail to consider the beginner’s perspective altogether, presenting information in a way that’s hard to integrate into an existing knowledge network.
 But *The Joy of React* always shows up at the exact moment I need it. It reminds me not to feel discouraged and reassures me that certain syntax is not “obvious,” encouraging me to click through to a linked explanation when needed. I really love this course.



------



To launch a React application, simply opening `index.html` won’t work. Many optimizations—like bundling assets such as images—depend on the development server. So we need tools that allow us to control these features properly.



Below is an illustration showing the environment setup required to comfortably develop a React application:

In short, it involves installing WSL on Windows to act as a Linux environment, then connecting to it using a terminal application like Hyper, which provides a nicer UI, additional features, and a more convenient workflow. After that, we can use Bash or Zsh inside Hyper to interact with the WSL environment.

![Development Environment Overview](/assets/images/251210_pic1.jpg)



## Why install a Linux environment on Windows?

Linux is the standard environment in frontend development—and in most development domains. While you *can* accomplish many things on Windows, you may find that something solvable with a single command on Linux requires you to install multiple tools on Windows, only to end up with an error message that’s completely unreadable.

In China, Windows is unquestionably the dominant operating system for personal computers, and even many developers don’t use MacBooks. So setting up a Linux subsystem on Windows allows us to learn and work like Linux users—without getting lost in endless errors caused by the differences between the two systems.

For example, suppose a Bash script asks you to switch to a directory. On Windows, the path might be:

```
C:\Users\ivy\new file
```

But in Linux:

- spaces in folder names require quotes, and
- directory separators use `/` instead of `\`

This creates a difference in command format. You’d have to rewrite the Linux command to fit Windows, which is tedious.

That’s why we use WSL (Windows Subsystem for Linux), a Linux subsystem running inside Windows:

- **WSL 2** is the version currently in use. Compared with WSL 1, it includes a lightweight Linux kernel.
- Unlike running a Linux virtual machine through VMware or similar software, WSL doesn’t require a separate network environment, a full GUI, or heavy system resources.



## Why use a terminal application?

There are many terminals available:

- Windows PowerShell
- Windows Command Line
- Windows Terminal
- WSL’s built-in terminal

All of these work, and you should choose whatever feels comfortable. But more modern terminal applications provide conveniences like auto-completion, multiple panels, and improved usability.

Josh W. Comeau recommends two:

- Hyper
- VS Code’s integrated terminal

For example, Hyper connects to PowerShell by default. To switch it to WSL, change the setting to:

```
shell: 'C:\\Windows\\System32\\bash.exe'
```



## What are Bash and Zsh?

Shell languages define the syntax of the commands we write in terminals.

- **Bash** is the default shell language in Linux terminals. Setting `shell` to `bash.exe` means Bash is being used as the default.
- **Zsh** is extremely similar to Bash, but more user-friendly. To switch to Zsh, you can install it using:

```
apt-get install zsh
```