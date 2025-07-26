# CLI

### **General**

**What is a CLI?**  
A Command Line Interface is a text-based interface that allows users to interact with the operating system or software by typing commands into a console or terminal.

**What is a Shell?**  
A program that interprets the commands you type in the CLI and interacts with the operating system to execute them.

**Relation between CLI and Shell**  
CLI is the environment where you type commands. It passes commands to the shell that proceesses them, runs programs, and returns output to the CLI to display it.

**Examples**
- **Bash** and **zsh** are shells. You access them through a CLI like Terminal on Linux/macOS.
- **PowerShell** is both a shell and its own CLI on Windows.
- **Command Prompt (cmd.exe)** is a CLI running the cmd shell.

### **Command line Prompt**

**Prompt** is a symbol or message displayed by a shell indicating that it is ready to accept a command.  
It usually shows useful informations like username `\u`, hostname `\h`, current directory `\w` or git branch followed by prompt character (`$` in bash, `%` in zsh, `#` for root user in bash and zsh, `>` in cmd and PowerShell).

### **Command line structure**  

**Structure:** `command [options/flags] [arguments]`.
- **Command:** The program or built-in command you want to run (*what to do*).
- **Options/flags:** Modify how the command runs, often start with `-` or `--` (*how to do it*).
- **Arguments:** Inputs to the command (*on what to do it*).

### **Filesytem**  

**Paths:**  
- **Absolute path:** Full path from the root of the filesystem to the target file or directory.  
Starts with `/` in Unix, with drive letter `C:\` in Windows.
- **Relative path:** Path relative to your current working directory (CWD).  
Starts with the special path characters, or filename, or folder from CWD.

**Special path symbols:**  
`/` path separator (Unix), `\` path separator (Windows), `.` current directory, `..` parent directory, `~` home directory (Unix).

**Environment variables:**  
Windows: `%USERPROFILE%`, `%APPDATA%`, `%TEMP%`, `%ProgramFiles%`, `%SystemRoot%`, etc.  
Unix: `$HOME`, `$PATH`, `$PWD`, `$OLDPWD`, etc.  
You can add your own variables using shell's specific command.

**Command substitution** lets you use command output as a string in your filepath. Syntax: `$(command)`.

**Pattern matching symbols:**
- `*`: Any string (0+ chars), example `command *.txt`.
- `?`: Single character, example `command file?.txt`.

### **Redirection**

**Redirection** changes where input comes from or where output goes to. Output can be redirected to a file or a device. You can redirect them using operators.

By default:
- **stdin (standard input):** keyboard input.
- **stdout (standard output):** terminal screen output.
- **stderr (standard error):** error mesagges displayed on terminal screen.

**Syntax:** `command redirection_operator file/device`

**Redirection operators:** 
- `<`: Redirect stdin.
- `>`: Overwrite stdout.
- `>>`: Append stdout.
- `2>`: Redirect stderr.
- `2>>`: Append stderr.

### **Piping**

**Piping** (`|`) connects the output of one command directly as input to another command without intermediate files.  
Syntax: `command1 | command2`

### **Help**

**Help commands** are used to display guidance on how to use commands, their syntax, and available options.  
They are good for quick learning, troubleshooting, option discovery, etc.

## cmd

### **Commands**

**Create empty file:** `type nul > filename.extension`