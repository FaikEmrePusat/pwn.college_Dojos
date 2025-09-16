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

## Position elsewhere

## Position yet elsewhere

## implicit relative paths, from /

## explicit relative paths, from /

## implicit relative path

## home sweet home
