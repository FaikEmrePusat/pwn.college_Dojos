# Comprehending Commands
<p>This module will expose you to some useful Linux commands that will serve you well for the rest of your journey here!
It is FAR from an exhaustive list, and we'll continue to expand this module, but this should be enough to get you started.</p>
<p>So, without further ado, let's learn some commands!</p>

## cat: not the pet, but the command!
### Challenge Description   
Read the `flag` file in your home directory using the `cat` command.

### Concepts Learned 
- **`cat` command**: Used to read and concatenate files.  
- **Home directory**: Your shell starts in `/home/hacker`, where the `flag` file is located.  

### Steps to Get the Flag
1. From your home directory (prompt: `hacker@dojo:~$`), run:  
   ```bash
   cat flag
   ```  
2. The contents of the `flag` file will be displayed, showing the flag.  

This demonstrates basic file reading with `cat` from the current directory.

---

## catting absolute paths
### Challenge Description 
Read the flag using `cat` with its absolute path `/flag`.

### Concepts Learned 
- **Absolute Path**: Access files directly from root (`/`) without relying on the current directory.  
- **`cat` command**: Reads file contents when provided with a path.  

### Steps to Get the Flag  
1. Run the command:  
   ```bash
   cat /flag
   ```  
2. The contents of the flag will be displayed.  

**Note**  
In pwn.college, the flag is always located at `/flag`, though it is not always directly accessible in other challenges.

---

## more catting practice


## grepping for a needle in a haystack

## comparing files

## listing files

## touching files

## removing files

## moving files

## hidden files

## An Epic Filesystem Quest

## making directories

## finding files

## Symbolic Links

## linking files
