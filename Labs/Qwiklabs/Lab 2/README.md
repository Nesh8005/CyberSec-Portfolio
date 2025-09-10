# Lab 2: Examine Input/Output in the Linux Shell

## Overview
In this lab, I explored **input and output in the Linux Bash shell** using the `echo`, `expr`, and `clear` commands. These commands demonstrate how a shell accepts input, returns output, performs calculations, and manages the workspace.  

This activity built foundational skills in communicating with the Linux operating system through the shell.

---

## Scenario
As a **security professional**, it’s important to understand how to interact with the operating system through the shell.  

In this scenario, I practiced:  
1. Using `echo` to display strings as output.  
2. Using `expr` to perform basic mathematical calculations.  
3. Using `clear` to clean the Bash shell screen.  
4. Exploring additional input/output operations.  

---

## Tasks and Commands

### Task 1: Generate Output with the echo Command
```bash
# Output a simple string
echo hello

# Output with quotation marks
echo "hello"

# Output a custom name
echo "YourName"
```
Expected output:
```nginx
hello
hello
YourName
```


### Task 2: Generate Output with the expr Command
```bash
# Subtraction: Calculate false positives
expr 32 - 8
# Output: 24

# Multiplication: Yearly login attempts
expr 3500 \* 12
# Output: 42000
```


### Task 3: Clear the Bash Shell
```bash
clear
```
Effect: The screen is cleared, and the prompt returns to the top-left of the shell window.


### Key Learnings

echo is used to generate output and display text in the shell.

expr performs basic integer arithmetic operations (+, -, *, /).

clear helps maintain a clutter-free workspace in the shell.

Input (commands) and output (results) form the foundation of shell interaction.

### Conclusion

 This lab provided hands-on practice with basic Linux Bash commands for input and output. Understanding these core concepts is essential before progressing to more advanced shell operations.

#### I now feel more confident in:

1. Generating text output with echo

2. Performing integer calculations with expr

3. Managing the shell environment using clear
