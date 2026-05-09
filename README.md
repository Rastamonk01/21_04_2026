# 21_04_2026 - Python & JavaScript Debugging Lab
Practice 21-04-2026 - I just chanced your README.md file

![Python](https://img.shields.io/badge/Python-3.x-blue?style=for-the-badge&logo=python&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-Debugger-yellow?style=for-the-badge&logo=javascript&logoColor=black)
![VS Code](https://img.shields.io/badge/VS_Code-Debugger-007ACC?style=for-the-badge&logo=visualstudiocode&logoColor=white)
![Status](https://img.shields.io/badge/Status-Complete-success?style=for-the-badge)

---

## Scenario

Imagine you are a developer learning to diagnose code behaviour by pausing execution and inspecting the exact state of your program at any point in time. Rather than relying on guesswork or reading through every line, you are asked to use two industry-standard debugging tools - the VS Code Python debugger for your backend script and the Chrome DevTools Sources panel for your frontend JavaScript - to step through your code line by line and observe variable values as they change in real time.

---

## What the Lab Does

This lab runs through two parallel debugging sessions across 8 steps:

1. Creates `app.py` - a Python script that prints directly, defines a `greet()` function, calls it, and prints the return value
2. Creates `index.html` - a web page with an `<h1>` heading and an embedded JavaScript block that mirrors the Python structure using `console.log()` and a `greet()` function
3. Sets a breakpoint in VS Code on the `def greet():` line of `app.py` and launches the Python debugger
4. Steps through `app.py` line by line, observing the Variables panel populate with `result = 'Hello, class!'` as execution moves through the function call
5. Opens `index.html` via Live Server at `127.0.0.1:5500` in Chrome
6. Opens Chrome DevTools and navigates to the Sources panel
7. Sets a breakpoint on `console.log("hello class")` at line 12 of `index.html` and pauses execution
8. Steps through the JavaScript, watching the Scope panel show the `result` variable resolve to `"hello from greet function"` and the Console display both log outputs

---

## File Structure

```
21_04_2026/
├── app.py        ← Python script (debug with VS Code Run and Debug)
├── index.html    ← HTML + JavaScript page (debug with Chrome DevTools)
├── notes.txt     ← CLI commands and class workflow reference
└── README.md
```

---

## Code Overview

### `app.py`

```python
print("Hello, World!")

def greet():
    return "Hello, class!"

result = greet()

print(result)
```

### `index.html` - JavaScript block

```javascript
console.log("hello class")

function greet() {
  return "hello from greet function"
}

let result = greet()
console.log(result)
```

Both files follow the same logical pattern: a direct output statement, a named function that returns a string, a variable that captures the function's return value, and a second output statement that prints that variable.

---

## Debugging Tools Used

### 1. VS Code - Python Debugger (Run and Debug panel)
**Definition:** The VS Code Run and Debug panel is a built-in debugger that pauses Python execution at breakpoints, steps through code one line at a time, and displays all live variable values in the Variables and Call Stack panels.  
**Why I used it:** Used to pause `app.py` at line 3 (`def greet():`) and then step forward to line 6 (`result = greet()`) and line 8 (`print(result)`), confirming at each step that `result` held the value `'Hello, class!'` as the function return flowed back into the calling scope.

---

### 2. Breakpoints
**Definition:** A breakpoint is a marker placed on a specific line of code that tells the debugger to pause execution just before that line runs, freezing the program's state so it can be inspected.  
**Why I used it:** Set a red dot breakpoint on line 3 of `app.py` in VS Code and on line 12 of `index.html` in Chrome DevTools. Breakpoints are what make stepping through code possible - without them the program would run to completion before anything could be observed.

---

### 3. Step Over / Step Into
**Definition:** Step Over (`F10`) executes the current line and moves to the next without entering any called functions. Step Into (`F11`) follows execution inside a function call.  
**Why I used it:** Used Step Over in both VS Code and Chrome DevTools to advance through each line sequentially, watching the Variables and Scope panels update after each step - confirming that `greet()` returned its value correctly and that `result` was assigned before `print()` was called.

---

### 4. Variables Panel (VS Code)
**Definition:** The Variables panel in VS Code's Run and Debug view displays all variables currently in scope - Locals, function variables, and Globals - and updates their values live as execution steps forward.  
**Why I used it:** At line 6, the Variables panel showed `result` as unassigned. After stepping to line 8, it updated to `result = 'Hello, class!'` - providing visual proof that the function call and assignment completed successfully before the `print()` ran.

---

### 5. Chrome DevTools - Sources Panel
**Definition:** The Sources panel in Chrome DevTools is a full JavaScript debugger built into the browser. It displays the source code of any loaded file, supports breakpoints, and shows live scope and call stack information.  
**Why I used it:** Used to debug the JavaScript inside `index.html`. With the debugger paused at line 12 (`console.log("hello class")`), the Scope panel confirmed that `result` was `<value unavailable>` at that early point, then updated to `"hello from greet function"` after stepping past the `greet()` call on line 18.

---

### 6. Console (Chrome DevTools)
**Definition:** The Console tab in Chrome DevTools displays all output from `console.log()` statements, errors, and warnings generated by the page's JavaScript, along with the line number each output came from.  
**Why I used it:** After stepping through the full JavaScript execution, the Console confirmed both expected outputs appeared in order: `hello class` from line 12 and `hello from greet function` from line 19 - verifying the script ran completely and correctly.

---

### 7. Live Server
**Definition:** Live Server is a VS Code extension that serves local HTML files over `http://127.0.0.1:5500`, allowing them to be opened in a real browser with hot-reload on save.  
**Why I used it:** `index.html` must be served over HTTP (not opened as a local file) for Chrome DevTools to fully attach its debugger and display source maps correctly. Live Server provides that local HTTP environment without any server configuration.

---

## CLI Commands Used

### 8. `pwd`
**Definition:** Prints the absolute path of the current working directory to the terminal.  
**Why I used it:** Used at the start of the session to confirm the exact location in the file system before creating project files, preventing scripts and HTML from being saved in the wrong directory.

---

### 9. `ls`
**Definition:** Lists all files and directories in the current working directory.  
**Why I used it:** Used to verify that `app.py`, `index.html`, and `notes.txt` were present in the project folder after creation, and again after changes to confirm nothing was accidentally deleted or misnamed.

---

### 10. `mkdir`
**Definition:** Creates a new directory with the name specified as the argument.  
**Why I used it:** Used to create the `21_04_2026` project folder in the `SingleA` workspace directory, giving the session a clean, date-labelled location for all lab files.

---

### 11. `cd`
**Definition:** Changes the current working directory to the path provided.  
**Why I used it:** Used to navigate into the newly created project folder so that all subsequent file creation and terminal commands ran in the correct context.

---

## Debugger Concepts Summary

| Concept | Tool | Purpose |
|---|---|---|
| Breakpoint | VS Code / Chrome DevTools | Pause execution at a specific line to inspect state |
| Step Over | VS Code / Chrome DevTools | Advance one line at a time without entering functions |
| Variables panel | VS Code | Display all in-scope variables and their live values |
| Call Stack | VS Code / Chrome DevTools | Show the chain of function calls leading to the current line |
| Scope panel | Chrome DevTools | Display Script-level and Global variables for JavaScript |
| Console | Chrome DevTools | Confirm `console.log()` output and line-number attribution |

---

## CLI Commands Summary

| Command | Purpose |
|---|---|
| `pwd` | Print current working directory |
| `ls` | List files and directories |
| `mkdir` | Create a new directory |
| `cd` | Change into a directory |

---

## Screenshots

| Screenshot | Description |
|---|---|
| `python_debugger.jpg` | VS Code Run and Debug panel - breakpoint hit on `def greet()` at line 3, execution paused on line 6 (`result = greet()`), terminal showing `Hello, World!` and `Hello, class!` output |
| `python_debugger_2.jpg` | VS Code debugger stepped to line 8 - Variables panel showing `(return) greet = 'Hello, class!'` and `result = 'Hello, class!'` confirming successful function return |
| `web_debugger.jpg` | Chrome DevTools Sources panel - breakpoint set on line 12 (`console.log("hello class")`), execution paused, Scope panel showing `result: <value unavailable>` at that early point |
| `web_debugger_2.jpg` | Chrome DevTools after stepping through - Console showing both outputs (`hello class` at line 12, `hello from greet function` at line 19), Scope confirming `result` resolved correctly |

---

## Git Workflow Used

```bash
git status
git add .
git commit -m "Add app.py, index.html, notes.txt and README for debugging lab"
git push
```
