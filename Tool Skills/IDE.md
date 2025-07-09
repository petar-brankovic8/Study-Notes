# IDE's

## General knoweldge

### **What is an IDE?**  
**IDE** (Integrated Development Environment) is a software that brings together:
- Text editor (syntax highlighting, error checking, code completion)
- Build system (compile + link + run code)
- Debugger (run code step by step to fix bugs)
- Project/file management tools
- Version control (Git)
- Plugins or extensions (tools like terminal)

### **Debuggers**  

**Breakpoints** are used to pause code execution at any line to inspect program state. Exception breakpoints pause when a specific exception or error occurs.

**Step controls** are used to execute code line by line.
- **Step Over:** Run the next line without entering functions.
- **Step Into:** Enter a functiono call to debug inside it.
- **Step Out:** Exit the current function and return to the caller.

**Variable watch panels** or hovering over variables is used to see current values, types, memory addresses.

**Call stack view** shows the hierarchy of function calls leating to the current line, helps trace where an unexpected value originated.

### **Refactoring tools**

**Rename tool** instead of manual find-and-replace to avoid renaming unintended matches that are not variables, functions or classes.

**Extract method/function tool** is used to create function with parameters matching used variables from selected code block, and replaces the code block with a call to the new function.

**Replace inline variable/function tool** is used to replace a temporary variable or function with its assigned expression everywhere. Simplifies code if variable adds no readability benefit.

**Change signature / function parameters tool** is used to add, remove, or reorder function parameters, automatically updating all function calls in the project. For example adding a new parameter with defaul    t value will update all existing calls safely.

**Move/Pull members up or down tool** is used to move a method or property to a parent class (pull up) or child class (push down) when restructuring class hiearchies.

**Safe delete tool** for deleting classes, functions, or variables if they are unused.

### **Productivity tools**

**Multi-Cursor editing** Alt + Click (or Ctrl + Click) in most IDEs.

**Regex search and replace** is used to create patterns that match strings you need to find in your project. Regex = Regular Expressions.

**Task runners** are used to automate repetitive workflowes.

**Code snippets** are used to create custom code templates.

**Testing tools:**
- **Unit tests:** Test invdividual functions or classes in isolation.
- **Integration tests:** Test combined components to ensure they work together properly.
- **End-to-End (E2E) tests:** Simulate user workflow to test full application behaviour.

## VS Code