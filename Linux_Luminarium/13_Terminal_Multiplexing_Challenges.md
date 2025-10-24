# Terminal Multiplexing

<p>Ever had an SSH connection drop and lose all your work?
Ever wanted to run multiple terminals without opening a dozen windows?
Enter the world of terminal multiplexing!</p>

---

## Launching Screen
### Challenge Description
Launch the `screen` program to create a virtual terminal session and receive the flag.

### Concepts Learned
- **Screen Utility**: Creates multiple virtual terminal sessions within a single terminal window  
- **Session Management**: Allows running persistent processes independent of the main terminal  

### Steps to Get the Flag
1. **Launch screen**:  
   ```bash
   screen
   ```  
   This will start a new screen session and display the flag.

2. **Exit screen**:  
   - Type `exit` or press **Ctrl-D** to leave the screen session and return to your original shell.

**Note**  
- The flag will be displayed immediately upon entering the screen session  
- Screen sessions persist even if you disconnect, allowing long-running processes to continue  
- This introduces basic terminal multiplexing concepts

---

## Detaching and Attaching
### Challenge Description
Detach from a screen session, run `/challenge/run`, then reattach to see the flag.

### Concepts Learned
- **Detaching Screen**: Press Ctrl-A then d to detach from a screen session without stopping it.  
- **Reattaching Screen**: Use `screen -r` to reattach to a detached session.  
- **Background Processes**: Screen sessions run in the background even when detached.

### Steps to Get the Flag
1. **Launch screen**:  
   ```bash
   screen
   ```  
   This enters a new screen session.

2. **Detach from screen**:  
   - Press **Ctrl-A**, then **d** to detach.  
   - You should see `[detached from...]` and return to the original terminal.

3. **Run the challenge program**:  
   ```bash
   /challenge/run
   ```  
   This will send the flag to the detached screen session.

4. **Reattach to screen**:  
   ```bash
   screen -r
   ```  
   This will reattach to the session where the flag is displayed.

**Note**  
- Ensure you detach properly using Ctrl-A then d.  
- If you have multiple screen sessions, you might need to specify the session ID with `screen -r [session_id]`, but in this case, since there's only one, `screen -r` should suffice.

---

## Finding Sessions
To complete this challenge, you need to find which of the three screen sessions contains the flag. Here's how to do it:

### Steps:
1. **List all screen sessions**:
   ```bash
   screen -ls
   ```
   You should see output similar to:
   ```
   There are screens on:
           23847.mysession   (Detached)
           23851.goodwork    (Detached)
           23855.morework    (Detached)
   3 Sockets in /run/screen/S-hacker.
   ```

2. **Attach to the first session** (e.g., `mysession`):
   ```bash
   screen -r mysession
   ```
   If the flag is displayed in this session, note it down. If not, detach by pressing **Ctrl-A** followed by **d**.

3. **Attach to the second session** (e.g., `goodwork`):
   ```bash
   screen -r goodwork
   ```
   Again, check for the flag. If not found, detach with **Ctrl-A** then **d**.

4. **Attach to the third session** (e.g., `morework`):
   ```bash
   screen -r morework
   ```
   This session should contain the flag. Once you see it, you can detach or exit.

5. **After finding the flag, you can exit all sessions**. The flag will be displayed in one of the sessions.

### Note:
- The exact session names may vary, but the process remains the same.
- If you have trouble attaching, ensure you use the correct session name from the `screen -ls` output.
- This demonstrates how to manage multiple screen sessions and find specific content.

By following these steps, you will locate the flag in one of the screen sessions.



## Switching Windows
To complete this challenge, you need to attach to the screen session and switch to Window 1 to find the flag. Here's how:

### Steps:
1. **Attach to the screen session**:
   ```bash
   screen -r
   ```
   This will attach you to the existing screen session. You'll likely start in Window 0.

2. **Switch to Window 1**:
   - Press **Ctrl-A** followed by **1** (this jumps directly to Window 1).
   - Alternatively, you can use **Ctrl-A n** to go to the next window if Window 1 is next.

3. **View the flag**:
   - After switching to Window 1, the flag should be displayed.

4. **Detach from the session** (optional):
   - Press **Ctrl-A** followed by **d** to detach and return to your original terminal.

### Note:
- If there are multiple screen sessions, use `screen -ls` to list them and attach to the correct one with `screen -r [session_name]`.
- The flag will be visible in Window 1 once you switch to it.

By following these steps, you will retrieve the flag from Window 1 of the screen session.

---

### Detaching and Attaching (tmux)
To complete this challenge, follow these steps:

1. **Launch tmux** by running:
   ```bash
   tmux
   ```
   This will start a new tmux session.

2. **Detach from the tmux session** by pressing `Ctrl-B` followed by `d`. You will see a message like `[detached (from session 0)]` and return to your original shell.

3. **Run the challenge program**:
   ```bash
   /challenge/run
   ```
   This will send the flag to the detached tmux session.

4. **Reattach to the tmux session** to view the flag:
   ```bash
   tmux attach
   ```
   or simply:
   ```bash
   tmux a
   ```

After reattaching, the flag will be displayed in the tmux session. If you have multiple tmux sessions, you can list them with `tmux ls` and attach to a specific session with `tmux attach -t <session-name>`.

---

## Switching Windows (tmux)
To complete this challenge, you need to attach to the existing tmux session and switch to Window 0 to retrieve the flag. Here's how:

### Steps:
1. **Attach to the tmux session**:
   ```bash
   tmux a
   ```
   This will attach you to the existing tmux session. You might start in Window 1.

2. **Switch to Window 0**:
   - Press **Ctrl-B** followed by **0** (this jumps directly to Window 0).
   - Alternatively, you can use **Ctrl-B n** or **Ctrl-B p** to cycle through windows until you reach Window 0.

3. **View the flag**:
   - After switching to Window 0, the flag will be displayed.

4. **Detach from the session** (optional):
   - Press **Ctrl-B** followed by **d** to detach and return to your original terminal.

### Note:
- If there are multiple tmux sessions, use `tmux ls` to list them and attach to the correct one with `tmux a -t [session-name]`.
- The flag is specifically in Window 0, so ensure you switch to that window.

By following these steps, you will retrieve the flag from Window 0 of the tmux session.
