# Hello Hackers
<div>

<p>This module will teach you the VERY basics of interacting with the command line!
The <em>command</em> line lets you execute <em>commands</em>.
When you launch a terminal, it will execute a command line "shell", which will look like this:</p>
<pre><code class="language-console hljs shell">hacker@dojo:~$
</code></pre>
<p>This is called the "prompt", and it's prompting you to enter a command.
Let's take a look at what's going on here:</p>
<ul>
<li>The <code>hacker</code> in the prompt is the <em>username</em> of the current user.
In the pwn.college DOJO environment, this is "hacker".</li>
<li>In the example above, the <code>dojo</code> part of the prompt is the <em>hostname</em> of the machine the shell is on (this reminder can be useful if you are a system administrator who deals with many machines on a daily basis, for example).
In the example above, the hostname is <code>dojo</code>, but in pwn.college, it will be derived from the name of the challenge you're attempting.</li>
<li>We will cover what <code>~</code> means later :-)</li>
<li>The <code>$</code> at the end of the prompt signifies that <code>hacker</code> is not an administrative user.
In much later modules in pwn.college, when you learn to use exploits to become the administrative user, you will see the prompt signify that by printing <code>#</code> instead of <code>$</code>, and you'll know that you've won!</li>
</ul>
<p>Anyways, the prompt awaits your command.
Move on to the first challenge to learn how to actually execute commands!</p>

</div>

---

## Intro to Commands

In this challenge, you will learn to use the `whoami` command in the terminal.  

- `whoami`: displays the current username.  
- **Case-sensitive** — `whoami` is correct, but `Whoami` is not.  

When typed correctly, the command runs and the shell will show the prompt again.


### How to Capture the Flag

Simply type **`hello`** into the terminal and run it:

- `hello` → works and gives the flag.  
- `Hello`, `HELLO`, etc. → invalid.

---

## Intro to Arguments

In this challenge, commands are structured with the **first word** being the **command** and the **subsequent words** being its **arguments**.

For example, when you type `echo Hello` in the terminal:
*   `echo` is the **command**.
*   `Hello` is the **argument**.

The `echo` command simply prints its arguments as output.

To retrieve the flag, you must use the `hello` command with a single argument: `hackers`.

**The correct command to execute is:**
```
hello hackers
```

---

## Command History

When working in the terminal, typing every command from scratch can become tedious. To help with this, the shell saves a history of every command you execute.

You can navigate through this list of previously run commands by using the **Up Arrow (↑)** and **Down Arrow (↓)** keys.

In this challenge, the flag was saved into this history. Press the **Up Arrow Key** to scroll through your past commands until you find it.

This is also a fundamental skill for efficient terminal use, allowing you to quickly recall and re-run commands without retyping them.


