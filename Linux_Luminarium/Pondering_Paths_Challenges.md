# Pondering Paths
<p>This module will teach you the basics of Linux file paths!</p>
<p>The Linux filesystem is a "tree".
That is, it has a root (written as <code>/</code>).
The root of the filesystem is a directory, and every directory can contain other directories and files.
You refer to files and directories by their <em>path</em>.
A path from the root of the filesystem starts with <code>/</code> (that is, the root of the filesystem), and describes the set of directories that must be descended into to find the file.
Every piece of the path is demarcated with another <code>/</code>.</p>
<p>Armed with this knowledge, go forth and tackle the challenges below.</p>

---

## The Root
### Challenge Description 
Execute the `pwn` program located at the root directory (`/`) using its absolute path to retrieve the flag.

### Concepts Learned 
- **Absolute Path**: Specify the full path from root (`/`) to access files/programs.  
- **Command-Line Execution**: Run programs directly by providing their absolute path in the terminal.  

### Steps to Get the Flag
1. Launch the terminal in the challenge environment.  
2. Run the command:  
   ```bash
   /pwn
   ```  
3. The program outputs the flag.  

---

## Program and absolute paths
### Challenge Description
The challenge program (`run`) is located in the `/challenge` directory. To execute it, you must use its absolute path: `/challenge/run`.

### Concepts Learned
- **Absolute Path with Subdirectories**: Accessing files located in nested directories using the full path from root.

### Steps to Get the Flag
1. Open the terminal.
2. Run the program using its absolute path:
   ```bash
   /challenge/run
   ```
3. The program will output the flag.

---

## Position thy self
### Challenge Description
Execute the `/challenge/run` program from a specified directory using the `cd` command to change your current working directory first.

### Concepts Learned
- **Current Working Directory**: Each process (including your shell) operates within a specific directory context
- **cd Command**: Changes the shell's current working directory when given a path argument
- **Path Navigation**: Using absolute or relative paths to move through the filesystem

### Steps to Get the Flag
1. The challenge will specify a target directory to navigate to
2. Use the cd command with the provided path:
   ```bash
   cd /specified/directory
   ```
3. Verify your location (notice how the prompt changes to show current path)
4. Execute the challenge program using its absolute path:
   ```bash
   /challenge/run
   ```
5. The program will output the flag when run from the correct directory

---

## Position elsewhere
### Concepts Learned
Execute `/challenge/run` from a specified directory using the `cd` command.

### Concepts Learned
- **cd command**: Changes current working directory
- **Working directory**: Each process operates within a specific directory context
- **Path navigation**: Moving through filesystem hierarchy

### Steps to Get the Flag
1. Navigate to the specified directory:
   ```bash
   cd /target/directory
   ```
2. Verify location (prompt shows current path)
3. Execute the program:
   ```bash
   /challenge/run
   ```
4. Program outputs flag when run from correct directory

---

## Position yet elsewhere
### Concepts Learned
Run `/challenge/run` from a specified directory using `cd` to change your working directory.

### Concepts Learned
- **`cd` command**: Changes current directory
- **Working directory**: Processes operate within a directory context
- **Path navigation**: Moving through filesystem hierarchy

### Steps to Get the Flag 
1. Change to specified directory:
   ```bash
   cd /given/path
   ```
2. Confirm location (prompt shows current path)
3. Execute program:
   ```bash
   /challenge/run
   ```

*Note: The `~` in your prompt represents your home directory and changes as you navigate.*

---

## implicit relative paths, from /

## explicit relative paths, from /

## implicit relative path

## home sweet home
