# Data Manipulation

<p>You've learned to pipe data, specify input, and so on.
Let's start putting things together!
In this module, you'll learn a number of commands for manipulating data that will help you achieve great results on the shell.</p>

---

## Translating characters
### Challenge Description
Use the `tr` command to reverse the case-swapping performed by `/challenge/run` and recover the original flag.

### Concepts Learned
- **`tr` command**: Translates or deletes characters from standard input  
- **Case Swapping**: The program outputs the flag with inverted case (uppercase ↔ lowercase)  
- **Character Sets**: Using character ranges in `tr` to perform case conversion  

### Steps to Get the Flag
1. Run `/challenge/run` and pipe its output to `tr` to swap the case:  
   ```bash
   /challenge/run | tr 'a-zA-Z' 'A-Za-z'
   ```  
   This command will:  
   - Convert lowercase letters to uppercase  
   - Convert uppercase letters to lowercase  
   - Effectively reverse the case-swapping done by the program  

2. The corrected flag will be displayed in the terminal.

**Note**  
- The character sets `'a-zA-Z'` and `'A-Za-z'` define the mapping for translation  
- All non-alphabetic characters (like numbers, symbols, braces) remain unchanged  
- This demonstrates how `tr` can be used for character-level text transformation

## Deleting characters
### Challenge Description
Remove the decoy characters '^' and '%' from the output of `/challenge/run` using `tr -d` to reveal the flag.

### Concepts Learned
- **`tr -d` command**: Deletes specified characters from the input stream.  
- **Character Deletion**: Useful for filtering out unwanted characters from command output.  

### Steps to Get the Flag
1. Run the following command to delete '^' and '%' from the output:  
   ```bash
   /challenge/run | tr -d '^%'
   ```  
2. The cleaned output will display the flag without the decoy characters.

This demonstrates how `tr -d` can be used to remove specific characters from text streams.

---

## Deleting newlines
### Challenge Description
Remove newline characters from the output of `/challenge/run` using `tr -d` to reveal the flag in a single line.

### Concepts Learned
- **`tr -d` command**: Deletes specified characters from the input stream.  
- **Newline Character**: Represented as `\n`, which must be escaped and quoted for proper interpretation by the shell and `tr`.  

### Steps to Get the Flag
1. Run the following command to delete all newline characters:  
   ```bash
   /challenge/run | tr -d "\n"
   ```  
2. The output will be the flag without any newlines, displayed as a continuous string.

This demonstrates how to use `tr` to remove control characters like newlines from text streams.

---

## Extracting the first lines with head
### Challenge Description
Use `head` to capture the first 7 lines of output from `/challenge/pwn` and pipe them to `/challenge/college` to receive the flag.

### Concepts Learned
- **`head` command**: Extracts the first few lines from input (default 10 lines).  
- **`-n` option**: Specifies the number of lines to display.  
- **Piping**: Connecting multiple commands to process data sequentially.  

### Steps to Get the Flag
1. Run the composite command with two pipes:  
   ```bash
   /challenge/pwn | head -n 7 | /challenge/college
   ```  
   This will:  
   - Execute `/challenge/pwn` and generate output.  
   - Use `head -n 7` to retain only the first 7 lines.  
   - Pipe those 7 lines to `/challenge/college`, which will process them and output the flag.  

2. The flag will be displayed directly in the terminal after execution.

---

## Extracting specific sections of text
### Challenge Description
Extract the flag characters from the output of `/challenge/run` using `cut` to select the appropriate column and then use `tr` to remove newlines, forming the complete flag.

### Concepts Learned
- **`cut` command**: Extracts specific columns from text-based input using a delimiter.  
- **`tr` command**: Removes specified characters, such as newlines, to concatenate output.  
- **Piping**: Combines multiple commands to process data sequentially.  

### Steps to Get the Flag
1. Run the following command to extract the flag characters (assuming they are in the second column) and join them into a single line:  
   ```bash
   /challenge/run | cut -d " " -f 2 | tr -d "\n"
   ```  
   - `cut -d " " -f 2` specifies a space as the delimiter and selects the second field from each line.  
   - `tr -d "\n"` deletes all newline characters, combining the extracted characters into a continuous string.  

2. If the flag characters are in a different column, adjust the `-f` value accordingly (e.g., `-f 1` for the first column, `-f 3` for the third).  

This command efficiently processes the output to reveal the flag by isolating the relevant data and formatting it correctly.

---

## Sorting data
### Challenge Description
Retrieve the real flag from `/challenge/flags.txt` by sorting the file alphabetically and extracting the last line, where the real flag is located.

### Concepts Learned
- **`sort` command**: Orders lines alphabetically by default.  
- **`tail` command**: Extracts the last few lines from input (using `-n 1` for the last line).  

### Steps to Get the Flag
1. Run the following command to sort the file and get the last line:  
   ```bash
   sort /challenge/flags.txt | tail -n 1
   ```  
   This will output the real flag.

2. Alternatively, you can use `sort -r` to reverse the sort and get the first line, but the above method is straightforward for this challenge.

This demonstrates how to combine `sort` and `tail` to filter data based on sorted order.
