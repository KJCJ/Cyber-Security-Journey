# My Cyber Cheatsheet

## 🧭 0. Navigation & Getting Unlost
* **`cd <folder>`** 
  * **Anatomy:** `cd` (Tool) + `<folder>` (Target)
  * **Example:** `cd C:\cyber` or `cd $Home`
* **`Get-Help <command>`**
  * **Anatomy:** `Get-Help` (Tool) + `<command>` (Target)
  * **Example:** `Get-Help cd`

## 🧱 1. The Basics: How to Build a Command
A command is usually made of three parts:
`[The Tool] [The Options/Flags] [The Target]`

## 📁 2. Navigation & Folders (Windows PowerShell)
* **`cd <folder>`**
  * **Anatomy:** `cd` (Tool) + `<folder>` (Target)
  * **Example:** `cd C:\cyber`
  * **Why:** Move into a specific folder.
* **`cd ..`**
  * **Anatomy:** `cd` (Tool) + `..` (Flag meaning "up one level")
* **`ls <optional_path>`**
  * **Anatomy:** `ls` (Tool) + `<optional_path>` (Target)
  * **Example:** `ls` (lists current folder) or `ls C:\cyber` (lists that folder)
* **`mkdir <new_folder_name>`**
  * **Anatomy:** `mkdir` (Tool) + `<new_folder_name>` (Target)
  * **Example:** `mkdir projects`

## 🔍 3. Finding Files
* **`find <path> -type <type> -size <size>`**
  * **Anatomy:** `find` (Tool) + `<path>` (Target) + `-type` (Flag) + `<type>` (Input) + `-size` (Flag) + `<size>` (Input)
  * **Example:** `find . -type f -size 1033c`
  * **Why:** Search a path for files that match specific rules. (`f` means file, `c` means bytes).

## 🛠️ 4. VS Code Commands
* **`code <folder_or_file>`**
  * **Anatomy:** `code` (Tool) + `<folder_or_file>` (Target)
  * **Example 1:** `code .` (Opens the *current* folder using the dot `.` shortcut)
  * **Example 2:** `code C:\cyber\progress.md` (Opens a specific file)
  * **Example 3:** `code C:\cyber` (Opens a specific folder)

## 🎮 5. OverTheWire: Bandit Commands
* **`ssh <username>@<server> -p <port>`**
  * **Anatomy:** `ssh` (Tool) + `<username>` (Target) + `@` (Connector) + `<server>` (Target) + `-p` (Flag) + `<port>` (Input)
  * **Example:** `ssh bandit0@bandit.labs.overthewire.org -p 2220`
* **`cat <filename>`**
  * **Anatomy:** `cat` (Tool) + `<filename>` (Target)
  * **Example:** `cat readme` or `cat ./-file2`
  * **Trick:** If the filename starts with a dash, use `./` before it to tell the tool "this is a file, not a flag."
* **`ls -a`**
  * **Anatomy:** `ls` (Tool) + `-a` (Flag for "all")
  * **Why:** Shows hidden files (files that start with a dot).
* **`exit`**
  * **Anatomy:** `exit` (Tool)
  * **Why:** Disconnects you from the SSH session.