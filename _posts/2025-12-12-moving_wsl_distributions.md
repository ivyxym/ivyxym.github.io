---
title: "Moving WSL Distributions from C: to D: Drive - Rethinking the Linux Subsystem Workflow on Windows"
date: 2025-12-12

---



If you’re using Windows and installed your WSL Ubuntu distribution through the Microsoft Store—or used another installation method without specifying a custom path—your Ubuntu installation is most likely stored on the C drive. If your computer has multiple drives, your C drive may not have much free space.

One of the main reasons we install WSL is that Windows, as a non-UNIX system, can cause various issues during development. As a result, WSL tends to hold many environment configurations and dependencies, which can take up significant disk space. That’s why it’s a good idea to move WSL off the C drive and onto a drive with more room.

A couple of days ago, when I first installed WSL, I didn’t think about this. But the issues I encountered during the migration process unexpectedly helped me understand WSL better. Here are some notes from that experience.



------



## Migrating WSL

Let’s say I want to move my WSL installation from the C drive to the D drive.

### 1. Export the existing WSL distribution to the D drive

We know that after enabling the WSL feature, we still need to install distributions on top of it. In my case, I only installed Ubuntu. So, in Windows Terminal, I export it like this:

```
$ wsl --export Ubuntu D:\ubuntu_backup.tar
```

To see all installed distributions:

```
$ wsl --list --verbose
```

### 2. Unregister the Ubuntu instance on the C drive

This removes all its data, so make sure the export succeeded:

```
$ wsl --unregister Ubuntu
```

### 3. Re-import Ubuntu into the new location on the D drive

```
$ wsl --import Ubuntu D:\WSL\Ubuntu D:\ubuntu_backup.tar
```

And that completes the migration.



------



## Setting Up Hyper for Easier Use

If you use Hyper as your terminal, and your `Preferences` file is configured like this:

```
shell: 'C:\\Windows\\System32\\wsl.exe',
shellArgs: [],
```

then you don’t need to change anything.
`wsl.exe` is not tied to a specific distribution—it manages **all** WSL distributions. So it will automatically find your Ubuntu installation even if it’s on the D drive.

Some tutorials suggest using `'C:\\Windows\\System32\\bash.exe'`, but according to documentation (and confirmed by AI tools), `bash.exe` is for WSL 1 and is now considered *legacy*. It may be removed in the future. It also assumes only one distribution exists, while `wsl.exe` handles multiple distributions properly.

However, if your Hyper setup points to a **specific** distribution, for example:

```
shell: 'C:\\Users\\[YOUR USERNAME]\\AppData\\Local\\Microsoft\\WindowsApps\\CanonicalGroupLimited.UbuntuonWindows_XXXX\\ubuntu.exe'
```

then you’ll need to update the path, since it won’t automatically track your new installation location.



------



## Which Distribution Does Hyper Open?

If Hyper launches `wsl.exe`, which distribution does it open when you have more than one installed?

When you run:

```
$ wsl --list --verbose
```

You’ll see one distribution marked with a `*` — that one is the **default distribution**, and `wsl.exe` will open it by default.

If you want to switch distributions inside Windows Terminal, you can use the `-d` flag:

```
$ wsl -d Debian
```



------



## Understanding Paths

There are two types of paths you need to distinguish:

### 1. `/mnt/c/Users/[YOUR NAME]`

This is actually your **Windows user directory** on the C drive.
The `/mnt` prefix means “mounted”—WSL mounts Windows drives instead of accessing them directly. Windows and WSL don’t exist in the same filesystem, so you can’t simply `cd` into the C drive without going through `/mnt`.

### 2. `/home/[YOUR NAME]`

This is the **home directory inside the current WSL distribution**.


Software installed on Windows isn’t necessarily accessible from inside WSL. For example, installing Node.js on Windows doesn’t make it available in WSL. Since our goal is to avoid Windows-related inconsistencies during development, we should rely heavily on WSL and avoid installing development tools directly through Windows GUI installers.
