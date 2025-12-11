---
title: "Terminal Cheat Sheet"
date: 2025-12-11

---

Today I was learning *The Joy of React*, and I decided to create a simple Bash command cheat sheet.



## Terminal Symbols

When you open a terminal, you’ll see a string of characters called the **prompt**. It usually indicates your identity, current directory, or permissions (like the `#` in the image). The name “prompt” also suggests that the terminal is ready and waiting for your instructions.

![image-20251211123116200](/assets/images/image-20251211123116200.png)

In GitHub READMEs, you often see a `$` before a command. This indicates that it’s a terminal command, not regular code. For example:

```
$ npm install balabala
```

You might also encounter other symbols in the terminal, like `%`:

![image-20251211122717794](/assets/images/image-20251211122717794.png)

or arrows:

![image-20251211122908146](/assets/images/image-20251211122908146.png)

These symbols are mostly just hints. Some indicate user permissions (e.g., root vs normal user), but in general, they all signal that the terminal is ready to accept commands.

Personally, these mysterious symbols used to intimidate me—they looked like an alien language! When I was younger, seeing them would make me want to give up. Later, I read *Mindset* by Carol S. Dweck—which Josh also recommends—and realized that our brains can be trained. Even if it takes me ten minutes to understand a single term, it’s okay. Once you truly understand it and integrate it into your knowledge network, you’ll recognize it as naturally as your native language.



## Navigation

- These commands help you move between directories:
  - `pwd`: short for *print working directory*, shows your current working directory.
  - `ls`: short for *list*, prints the contents of the current directory.
  - `cd`: change directory, e.g., `cd dir`.
  - Common shortcuts: `~` = home directory, e.g., `cd ~/dir`; `..` = parent directory, e.g., `cd ../dir`. `.` refers to the current directory.
  - Auto-completion: Press `Tab` to complete file or folder names automatically. You don’t need to type the full name—just the first one or two letters (or even just one).



## Flags

Flags modify how a command behaves. For example, `-f` stands for *force*, so `rm -f` forces deletion. Usually, a single `-` is short-form, and `--` is long-form, but they do the same thing. For example:

```
# Both commands are equivalent
$ rm -f dir
$ rm --force dir

# Combining flags
$ rm -rf dir
```



## Multiple Commands

Commands are often repeated, or you may want to run several in sequence:

- Use the `Up` and `Down` arrow keys to cycle through previously executed commands.
- Switch to the previous directory using `cd -`. This `-` can also be used elsewhere, like switching Git branches.
- Combine multiple commands with `&&` to execute them sequentially, e.g., `command1 && command2`. This allows you to chain commands without waiting to type the next one manually.



## Multiple Sessions

Sometimes you want multiple sessions—either because one is busy or to keep commands organized:

- Open multiple tabs—usually one tab per project makes sense. (`File → New Tab`)
- Split a tab into multiple sessions (e.g., run the development server and monitor output at the same time): `File → Split Down/Right`. (Down is often better for vertical space.)



## Clearing the Terminal

If the terminal gets cluttered, you can clear it:

- `clear` clears the history.
- `Ctrl + L` also works on all operating systems, but only when the shell is ready.
- `Ctrl + Shift + K` (or `⌘ + K` on Mac) clears the window even if the shell is busy.



## Exiting

- Interrupt a running command: `Ctrl + C` (or `⌘ + C` on Mac).
- Exit a session (e.g., from Oh My Zsh back to default Zsh): `Ctrl + D`.
- If all else fails, close the terminal window.
- For text editors like `vim`/`vi`, you cannot exit with `Ctrl + C`. Press `Esc` first, then use `:q!` to force quit or `:wq` to save and quit.



## Important Note

Be careful with `rm`: it does not prompt for confirmation, and there is no recycle bin. Always double-check before running it.



## Other Tips

- `man`: short for *manual*, opens a command’s manual using `less` so it doesn’t flood the terminal. Example: `man ls`.
- Aliases: e.g., `alias hi='echo "Hello World!"'`, then typing `hi` executes the command.
- Open File Explorer: `explorer .` (may not always work on Windows).
- Open the current directory as a project in VS Code: `code .`.