---
title: "A Simple Git Quick Start"
date: 2025-12-15

---



When I first started learning programming, I had already heard of the famous Git. After all, if you know GitHub, you probably know Git as well. But for a long time, I wasn’t really *using* Git properly. There were two main reasons.

First, when you’re only building small toy projects, Git doesn’t feel strictly necessary. Second—and more importantly—Git felt intimidating to me. Its concepts and architecture aren’t actually that hard, but GitHub hosts the source code of some of the most advanced open-source projects in the industry. Back when I barely understood anything about the tech world, a single page full of unfamiliar terms was enough to scare me away.

Now that I’m finally treating Git as a real tool, I can honestly say: it’s incredibly convenient.

------

## A Simple Example: Syncing Local Code with a Remote Repository

Over the weekend, I built my first React project—a Wordle clone from *The Joy of React* course.

### Step 1: Fork the starter repository

I started by visiting Josh W. Comeau’s starter repository:
https://github.com/joy-of-react/project-wordle

This repository contains some initial code that I could build on. By clicking the **Fork** button in the top-right corner, I created my own copy of the project in my GitHub account. Under the repository title, it now shows *forked from joy-of-react/project-wordle*.

------

### Step 2: Clone the repository to my local machine

Next, I opened my terminal and cloned my forked repository so I could work on it locally.

First, I navigated to the directory where I wanted to store the project. For example, if I want the project to live at:

```
~/projects/joy-of-react/project-wordle
```

I should first switch to:

```
~/projects/joy-of-react
```

because `git clone` will download the project into a new folder named after the repository.

The command looks like this:

```
$ git clone https://github.com/[USERNAME]/[REPOSITORY NAME].git
```

------

### Step 3: Choose a branch

If you’re just working on a small personal project, it’s totally fine to work directly on the `main` branch. If you’re collaborating with others—or experimenting with features you’re not sure about—it’s better to create a new branch.

In my case, I stayed on `main`, which is the default branch, so no extra steps were needed.

------

### Step 4: Modify the code

I made changes to the code locally.

------

### Step 5: Stage the changes

```
$ git add .
```

This adds all modified files to the staging area.

------

### Step 6: Commit the changes

```
$ git commit -m "[YOUR COMMIT MESSAGE]"
```

This creates a snapshot of your changes with a short description.

------

### Step 7: Push local changes to GitHub

```
$ git push origin main
```

This synchronizes your local code with the remote repository on GitHub.

The first time you push, GitHub may require authentication using SSH. Below is how I set that up.

------

## Pushing Code with SSH

This step verifies that you are the owner of the GitHub account—and it’s much more secure than using a password.

### 1. Generate an SSH key locally

First, check whether you already have an `.ssh` directory:

```
$ ls ~/.ssh
```

If it doesn’t exist, create it:

```
$ mkdir ~/.ssh
```

Generate a new SSH key using the Ed25519 algorithm:

```
$ ssh-keygen -t ed25519 -C "your_email@example.com"
```

When prompted for the file path, press **Enter** to use the default location (`~/.ssh/id_ed25519`).

Then enter and confirm a passphrase (this helps you avoid typing your password repeatedly).

To view your public key:

```
$ cat ~/.ssh/id_ed25519.pub
```

Copy the entire output.

------

### 2. Add the SSH key to GitHub

Go to GitHub → **Settings** → **SSH and GPG keys** → **New SSH key**.

Paste the public key into the **Key** field, give it a title, and click **Add SSH key**.

Now GitHub can verify your identity.

------

### 3. Configure the local repository

Navigate to your project directory and check existing remotes:

```
$ cd [PATH TO PROJECT] && git remote -v
```

If `origin` already exists and uses an HTTPS URL (as it does after cloning), replace it with the SSH version:

```
$ git remote set-url origin git@github.com:[USERNAME]/[REPOSITORY NAME].git
```

If `origin` doesn’t exist yet, you can add it directly:

```
$ git remote add origin git@github.com:[USERNAME]/[REPOSITORY NAME].git
```

------

### 4. Test the SSH connection

```
$ ssh -T git@github.com
```

Type `yes` if prompted.
If you see:

> *Hi USERNAME! You've successfully authenticated, but GitHub does not provide shell access.*

then everything is set up correctly.