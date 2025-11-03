#### Date: 3rd November 2025
# Introduction to Shell Scripting

## 1. What is a Shell?
A shell is a computer program that presents a command-line interface which 
allows you to control your computer using commands entered with a keyboard 
instead of controlling graphical user interfaces (GUIs) with a mouse/keyboard 
combination.

Popular shells include:
- **Bash (Bourne Again SHell):** The default for most Linux distributions.
- **Zsh (Z Shell):** Default for macOS, highly customizable.
- **Sh (Bourne Shell):** The original Unix shell.

## 2. Why Shell Scripting?
- **Automation:** Replace repetitive manual tasks with a single command.
- **Portability:** Scripts run on almost any Unix-like system.
- **Power:** Combine multiple commands and utilities to perform complex 
  operations.
- **Consistency:** Ensure tasks are performed the same way every time.

## 3. Basic Script Structure
Every script should start with a "shebang" line to tell the OS which 
interpreter to use:
```bash
#!/bin/bash
```

## 4. Variables
Variables are used to store information. No spaces around the `=` sign.
```bash
NAME="DevOps Engineer"
echo "Hello, $NAME"
```

## 5. User Input
Use the `read` command to get input from the user:
```bash
echo "Enter your name:"
read USERNAME
echo "Welcome $USERNAME"
```

## 6. Conditionals (If-Else)
Used to execute code based on certain conditions.
```bash
if [ "$NAME" == "Admin" ]; then
    echo "Access Granted"
else
    echo "Access Denied"
fi
```

## 7. Loops
Perform actions multiple times.
- **For Loop:**
```bash
for FILE in *.txt; do
    echo "Processing $FILE"
done
```
- **While Loop:**
```bash
COUNTER=0
while [ $COUNTER -lt 5 ]; do
    echo "Count: $COUNTER"
    ((COUNTER++))
done
```

## 8. Positional Parameters
Arguments passed to the script globally:
- `$0`: The name of the script.
- `$1`, `$2`: The first and second arguments.
- `$@`: All arguments as a list.
- `$#`: The number of arguments.

## 9. Functions
Organize code into reusable blocks:
```bash
greet() {
    echo "Hello from a function!"
}
greet
```

## 10. Exit Status
Every command returns an exit status (0 for success, non-zero for failure).
- Access it using `$?`.
```bash
mkdir my_dir
echo "Exit status was: $?"
```

## 11. Conclusion
Shell scripting is a fundamental skill for DevOps engineers. It enables 
automation of infrastructure setup, deployment processes, and system 
administration tasks, making "Infrastructure as Code" possible at a basic 
level.

---
*End of Notes*
