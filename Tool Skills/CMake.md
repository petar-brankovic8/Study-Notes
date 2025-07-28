# **CMake**

### **Important commands**

`cmake_minimum_required(VERSION x.y)`  
Ensures CMake version is compatible.

`project(ProjectName [LANGUAGES ...])`  
Defines the project name.

`add_executable(name file1 file2 ...)`  
Creates an executable.

`add_library(name [STATIC|SHARED] file1 file2 ...)`  
Creates an library.  
If STATIC or SHARED is not specified, the default is value of global variable `BUILD_SHARED_LIBS`.

`add_subdirectory(<directory>)`  
Include another CMake file located in a subdirectory.

### **Target commands**

**Executable** or **library** is a *target*.

`target_include_directories(<target> [PRIVATE|PUBLIC|INTERFACE] <directory1> <directory2> ...)`  
Tells compiler in which include directories to look for header files that target uses.

`target_link_libraries(<target> [PRIVATE|PUBLIC|INTERFACE] <library1> <library2> ...)`  
Tells compiler which libraries to link to the target.

`target_compile_features(target [PRIVATE|PUBLIC|INTERFACE] <feature1> <feature2> ...)`  
Specifying which language features does a target need. For example, it uses features from C++17, and it forces that compiler supports those features.

### **Forcing C standard**

`set(CMAKE_C_STANDARD <number>)`  
`set(CMAKE_CXX_STANDARD <number>)`  
Use this standard if possible. (Example: number = 17 for C++17).

`set(CMAKE_C_STANDARD_REQUIRED ON)`  
`set(CMAKE_CXX_STANDARD_REQUIRED ON)`  
Force to use this standard, fail otherwise.

`set(CMAKE_C_EXTENSIONS OFF)`  
`set(CMAKE_CXX_EXTENSIONS OFF)`  
Disables compiler specific extensions.

### **Variables**

`set(VAR_NAME value)`  
Defining variables.

`${VAR_NAME}`  
Accessing variables.

Only variable type is string, but additionally they can be interpreted as Booleans or lists.
- **Boolean** is interpreted as `TRUE` only if the string is equal to `1, ON, YES, TRUE or Y` (case-insensitive).  
Every other string value is treated as `FALSE`.
- **List** is stored as `"string1;string2;...;stringN"` and is interpreted and expanded as `string1 string2 ... stringN`.

### **List commands**

`list(APPEND <list> <element1> <element2> ...)`  
Adds elements to list.

`list(REMOVE_ITEM <list> <element1> <element2> ...)`  
Removes elements from list.

`list(INSERT <list> <index> <element1> <element2> ...)`  
Inserts elements at index position in list.

`list(LENGTH <list> <variable>)`  
Checking list length by assigning it to a variable.

`file(GLOB <list> "src/*.cpp")`  
Automatically gather files matching a pattern in to the list (All .cpp files in src/ in this example).

`file(GLOB_RECURSE <list> "src/*.cpp")`  
Finds all files recursively (All .cpp in /src and subdirectories).

`foreach(<variable> ${<list>})`  
____`command(${<variable>})`  
`endforeach()`  
Iterating over a list by accessing every element through `${<variable>}`.

### **Global variables**

`CMAKE_PROJECT_NAME` - Name of top-level project.

`PROJECT_NAME` - Name of the project in current subdirectory.

`CMAKE_SOURCE_DIR` - Root source directory of the top-level CMakeLists.txt.

`CMAKE_CURRENT_SOURCE_DIR` - Source directory of the current CMakeLists.txt.
