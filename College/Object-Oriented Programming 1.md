# *Object-Oriented Programming 1*

## Principles of OOP

### **Modularity**

Modularity is a way of breaking down a complex problem or system into smaller logical units (**modules**) that:

- Have a **clearly defined responsibility**.
- Can be **developed, tested, and changed independently**.
- Have **minimal interdependence**.

Benefits that modular program brings are: **Readability**, **Reusability**, Easier **Testing** & **Debugging**, **Scalability**.

In programming, modularity is achieved by **decomposition** through:

- Functions and procedures
- Classes and objects 
- Packages, modules, and namespaces

### **Encapsulation**

**Encapsulation** is a technique designed to prevent other parts of program or users to accidentally disturb and break modules functionality while using it or to rely on some informations and assumptions about its implemenation that might be changed.

It is achieved by using the principle of **information hiding** that says that every module should have clearly defined:

- **Interface**: Specification of elements (structures, types, operations) that other parts of program can see and rely on.
- **Implementation**: Intern parts (structure, behaviour) that other parts of program can't see and rely on assumptions about it.

In **C** it is usually done by spliting the module in one **header file (.h)** which makes interface, and one **(.c) file** that has implementation.

### **Classes**

A class, at its core, is an abstarction that groups together a **structure** (data) and **behaviours** (operations over that structure) into a single logical unit.

**Objects**, basically, are instances of the structure that holds data (**attributes**) of the given class. Each (non-static) function member (**method**) of that class is implemented as a regular function with added first hidden argument that points to the object invoking it.

Classes support encapsulation by defining which class members are **private**, which **protected**, and which are **public**.

Classes support concept of **constructors** (and **destructors**) which allow you to control how objects are initialized (destroyed). They are implemented as a class member function, with the same name as the function, which defines how object is initialized

### **Inheritance**

**Inheritance** is a mechanism designed to allow adding new features to a class without modifying it.

It is achieved through creating a new **child** class that *inherits* all features (*atributes, methods*) from original **parent** class, and then *specializing* or *extending* it by adding new features (*atrbiutes, methods*) that base class doesen't have.

Object of the derived class has built-in *subobject* of the base class, which is used in **Substitution rule** that says: wherever and whenever object of the base class is expected, a object of the derived class can be used.

When the object of the derived class is created, before executing its own constructor, the constructor of the base class is called first creating the subobject.

### **Polymorphism**

Principle of **polymorphism** is designed to allow changing the implementation of class behaviours (*methods*) so they can support newly added features.

It is achieved through defining class functions as **virtual** which allows derived classes of that class to redefine them and change its implementation.

For every class that has at least one virtual function, compiler generates a structure, table of virtual functions (**Virtual Table**) that holds pointers to implementations of virtual functions that correspond to that class.

Now in every object there is a pointer that points to a table of virtual functions (**Virtual Table Pointer**). Constructor initializes this pointer to point to a virtual table of a class that corresponds to that constructor.

So every call of virtual function is done by **dynamic binding**, by indirect access through virtual table pointer of that object, then pointer in virtual table to the function that corresponds to the virtual function of that class.

### **Generic class**

Concept of **generic classes** is designed to allow defining structures (classes) with arbitrary data types. Data types are given as parameters when declaring object.

They are just pure **automatization**. The effect is same as writing separate classes for each data type, these generic classes are different one from another, they are just generated on demand by compiler when used for the first time with concrete data types.

### **Abstraction**

**Abstraction** is a process where we ignore non-relevant details and behaviours of things, that are not important for solution, in order to simplify them enough so they become solvable and realizable.

Part of abstraction is also **generalization** where we ignore differences between things we need, in order to group them in generalized abstraction to achieve better simplification. We use **specialization** to define each things uniqueness that we need from them.

It is used as base tool, alongside decomposition, in a fight against **complex problem domains** that we try to solve, and in **modeling** real world phenomenons, systems and entities.

We use **classes** to represent abstractions from real world or logic concepts from problem domain, and its generalizations and specializations.

### **Model-based software engineering**

When we want to create classes whose behaviours depend a lot on objects current **state**, then the code could get pretty complex with a lot of branching to process every state and more susceptible to errors.

The solution that classic OOP languages do not support, is modeling objects behaviour using **state machines** and generating code from that model (***model-based software engineering***).

### **Threads**

If we have behaviours that need to execute parallelly, creating elementary steps for each of them and cycling between them in infinite while loop can create huge unnecessary complexity, so we implement behaviour of active objects as **threads**.

Each thread has its own sequence of instructions (***control flow***), that includes its own automatic variables and call stack. Operating system regulates thread parallel processing.

### **Software architecture characteristics**

**Bad** software characteristics:
- **Rigidity**: Parts of software are too much mutually dependent, so they become hard to change. Every change in one part requires changes in other parts.
- **Fragility**: Caused by a lot of intertwining, problems in one part causes a lot of problems in other parts - **domino effect**.
- **Immobility**: Parts of one app are hard to use in another, because of huge interdependency with other parts.

So software with **good** characteristics is:
- **Flexible**: Easy to maintain (*modify & extend*).
- **Robust**: Resistant to changes, they dont affect its correctness.
- **Portable & Reusable**: Parts are easily implemented in another app.

And it is achieved by:
- Clear, simple, correct, understandable and flexible **architecture**.
- Real **abstractions** and good **distribution of responsibility**.
- **Modularity** and **Encapsulation**
- **Weak interdependency** between parts (*abstraction, modules*), simple **interfaces**.

### **Distribution of responsibility**

Good distribution of responsibility among abstractions, classes, modules is achieved by grouping elements of software (*data, functionalities*) by principle of **strong cohesion & loose coupling**:
- Elements inside the same class or module should be strongly and tightly interconnected (***cohesion***).
- Elements of different classes and modules should ideally just know interfaces of each other, not their internal details (***loose coupling***).

It is similar to the **single responsibility principle**: Classes should have limited responsibility, so there would exist only one reason for their modification.

One of the ways to achieve better software characteristics is by using **localization of design decisions** by keeping each design decision in one place, not scattering it throughout the program. 

### **Algorithmic decomposition**

In the center of attention of algorithmic decomposition is the task that needs to be done, for which we define **procedure** for its execution.

Initially the procedure is divided in **steps**, of high level of granularity and abstraction. Then every step is divided in more smaller steps until we reach lowest levels of granularity, the one where we can express it with elemental construct of programming language we use.

When to **decompose**:
- **Too much code**: When implementation of procedure has too much code, it becomes hard to read, follow and understand. General rule: If it has more than 15-20 lines of code you should think of decomposing it more.
- **Too much nesting**: When there is too much branching (*if-then-else*) or loops (*for, while*). General rule: It isn't good to have more then 2 levels of nesting, becomes hard to read and understand.
- **Reusable parts**: When some parts of implementation of one operation are used in other operations, to avoid code duplication. *Copy-paste* is a very bad practise in programming because it leads to a lot of errors and mistakes.

Procedures are also product of **abstraction**, where for every step we care only about its interface, we delay their implementation and details for later.

In OOP algorithmic decomposition also has an important role, but not central anymore like in procedural programming, so it is one of main elements in **object decomposition**. 

We still use it for decomposing procedures, but for every step, we define an **agent** (*abstraction, class*) that is responsible for its execution.

When we decompose a method (*operation*) of some class in to steps, we can **delegate responsibility** of those steps to some other class, or we can keep them and implement in the current class as **helper** methods.

These helper methods should usually be protected, as they probably aren't part of interface, but could probably be used in implementation of other operations in derived classes. If we make them virtual and allow polymorphism, then we can change their implementation and behaviour of original operation in base class which can be useful sometimes. These virtual helper functions are called **hook** methods.

### **Relations and dependencies between classes**

Our class (**client**), in order to fulfill its responsibility, often wants to use services (*operations*) of other classes (**servers**).

To do that, client has to have a structural **link** with server. In OOP, it is achieved by having pointer/reference to the object of the class we want use.

Links between classes don't have to be used only for calling operations. It can represent a simple connection between objects, to define that they are in conceptual **relation**, which can be used as data.

Instead of letting object-client create the needed objects-server by himself, the practise shows that it's better to let someone who uses the class, from outside, **inject dependency** by passing as the object-server that the client uses, as argument in constructor, setter, or method directly.

### **Class encapsulation**

The order of declaring class members, for increased readability:
1. **Public**: Interface, only what is needed by the most users.
2. **Protected**: Specific interface, for priviliged users.
3. **Private**: Implementation, it should be hidden, only for the designers of the class.

Recommended distribution of class members:
- **Public**: Only methods (*operations*) that are part of interface.
- **Protected**:
    - Getters & Setters that are not part of interface, but are needed for derived classes to access data members.
    - Helper and hook methods, because they are often needed in child classes.
- **Private**: All data members exclusively, so their access can be more easily controlled and manipulated. If access is needed make getters & setters. 

If we want to store data that is not property of a single object, but a class as a whole, instead of defining it globally available which would break encapsulation, we define it as **static data member**. There exists only one instance for every static data member, shared between all objects of that class.

Similarly, if there are services requested from a class as whole, not concrete objects, we can define **static member function**, and they do not have pointer to the object that is invoking them.

### **Hiearchical decomposition**

**Hiearchical decomposition** is another element of object decomposition and it implies creating hiearchy of classes connected with relation of inheritance. It uses generalization and specialization as base tool.

To avoid modifying existing parts of software, which is usually the main source of rigidity and domino effects, we use **open-closed principle**. Every class/module should be closed for changes, but open for extensions and redefining which is usually achieved with inheritance and polymorphism.

Because of this all operations should be defined by default **virtual**, and to remove possibilites of error and improve readability, a keyword **override** to imply that the function is being redefined.

In special cases some virtual operations should be closed for redefining and some classes should be closed for inheriting, and that is done by declaring them **final**.

Base motive for **generalization** is that some other part of software (client) wants to observe and use instances of different specialized classes as if they are the same, through generalized interface, not making difference between them.

**Abstract class** is a generalized class that won't have it's own direct instances, only indirect, because it doesen't have its own implementation of operations that need to be polymorphed. Using them we make software more loosely coupled, and clients of the class more indenpended and flexible (*the less you know, the better*). Generalization and polymorphism drastically reduce the amount of conditional branching.

Operations that yet need to be polymorphed are called **abstract operations**, and they give only specification of service (declaration), no implementation (definition).

By using **implict conversion** (*without explicit request*) you can convert pointer/reference of derived class to a pointer/reference of its base class (**upcast**). This conversion allows objects of derived class to be accessed as instances of base, generalized class.

Opposite conversion (**downcast**) isn't always safe because compiler can't check if the object of the base class is also object of the derived class, and by so it can cause runtime error.

We can also create **mixin** classes that are not meant to be used as a standalone classes, but as an functionality interface for other classes (clinets) to inherit.

By splitting one big class in to a smaller single class that inherits more mixin classes we can avoid having properties and behaviours for all different contexts in one interface, which would make it large and hard to read and understand. This principle of creating mixin classes for every context is called **interface segregation**.

### **exception handling**


## **C++**

### **Objects**

Because C++ wants to treat class objects as similliar as possible as instances of built-in types, it makes generalization of term **object**.

On C++, *object* is a **region of storage**, part of memory, that has:
- **Size**: That can be determined using operator sizeof (in units of sizeof(char)).
- **Alignment**: Most CPUs work faster when data is stored at memory addresses that are multiples of their size. A type's alignment is the number of bytes  its address should be a multiple of that can be determined using operator alignof.
- **Storage duration**: Automatic, Static, Dynamic, or Thread-local.
- **Lifetime**: Can be determined by its storage duration or its *temporary*, how long does it exist during runtime.
- **Type**: Can be a class type (class, struct, or union) or built-in type.
- **Value**: That can also be undetermined.
- **Name (*optional*)**: Identifier in program that is referencing that object.

**Variable** is an object or reference that has its identifier and scope lifetime. It has to be declared before used.

**Objects** are made by:
- **Definitions**: Special type of declaration that has an effect of creating an object.
- **new**: Operator.
- **throw**: Operator.
- **Temporary**: When there is a special request for creating temporary object.

**Declaration** is a statement that introduces identifier in to a program. Every identifier must be declared before use.

### **Types**

**Types** limit set of operations that are allowed for their entities and give semantics (*meaning*) to the sequences of bits that those entities represent.

**Fundamental types:**
- void
- std::nullptr_t
- arithmetic types
    - floating-point types
        - float, double, long double
    - integral types
        - bool
        - character types
            - char, signed char, unsigned char
            - char16_t, char32_t, wchar_t
        - signed integer types
            - short int, int, long int, long long int
        - unsigned integer types
            - unsigned short int, unsigned int, unsigned long int, unsigned long long int

**Compound types:**
- reference types
    - lvalue reference types
        - to objects types
        - to function types
    - rvalue reference types
        - to object types
        - to function types
- pointer types
    - to objects
    - to functions
- pointer-to-member types
    - to data members
    - to function members
- array types
- function types
- enumeration types
- class types
    - non-union types: struct, class
    - union types

For all types, except functions and references, there is a **cv-qualified** version: **const**, **volatile**, and **const volatile**.

For every type and category, in standard library, there is a corresponding template struct `is_....<T>` with data member `value` that in compile-time results in true or false depending on that if the template argument is a member of given type category.

Specificator **decltype** determines the type of given entity or expression given inside of brackets in compile-time. This can be used for defining types that are hard to determine what they are or that depend on type of other entities, typically in templates.

You can declare your own **identificator** for the type by:
- Declaring class.
- Declaring enumeration (enum).
- *typedef* declaration.
- *using* declaration.

A **typedef** declaration has exactly the same form as a variable declaration, except you replace the variable name with the typedef name. Something like this `typedef ExistingType NewName;` or `typedef ReturnType (*NewName)(ArgType1, ArgType2, ...);`.

Syntax for **using** is much simpler: `using NewName = ExistingType;`. It can also work with templates like `template<typename T> using NewName = ExistingTemplateClass<T>;` and invoke it with `NewName<Type> objectName;`.

*typedef* and *using* are mainly used for **localization of design decisions**, giving more meaning and semantics to declared objects with a **meaningful type name**, or just for shortening **complex types**.

### **Conversions**

**Conversion** is transforming value of one type to a value of other type.

Conversion can be **implict**, which means it is done automatically by the compiler in the places that it is needed, which are:
- **Function argument**: When Type1 is passed as an argument, but the corresponding parameter is of Type2.
- **Function return**: When the function has declared return Type2, but command *return* has Type1.
- **Operator operand**: When the operand of the operator is Type1, but Type2 is expected.
- **Object initialization**: When initializing new object of Type2, with Type1.
- **Switch argument**: When Type1 is used in switch it will convert it to integral Type2.
- In **if**, **for**, **do**, **while**: If Type1 isn't bool, it is converted to it (Type2 is bool).

Allowed implicit conversion, that don't give compile error:
- **Bool**:
    - Zero value (for arithmetic types), null value for pointers and nullptr convert to false
    - Everything else converts to true.
- **Integral promotion**:
    - Arithmetic operations do not take values smaller than int, so all char, short, and bool types convert to int operand.
- **Int**:
    - Any integral type can implicitly convert to any other integral type. If destination type can accept whole range of values of source type, value is saved, if not than value can be lost.
- **Floating-point**:
    - Any floating-point type can be implicitly converted to any other floating-point type with potential value or precision loss.
    - Any floating-point type can be implicitly converted to any other integral type with potential cutting.
    - Any integral type can be implicitly converted to any floating-point type with potential value loss if that value can't be precisely represented in floating-point.
- **Enum**:
    - Promotes to int via integer promotion.
    - Scoped enum doesen't impilictly convert, needs cast.
- **Pointers**:
    - void* -> T*, T* -> void*.
    - Derived* -> Base* (Base* -> Derived* not implicit, needs cast).
- **Const Pointers**:
    - Implicit conversion from pointer to non-const type T to pointer to const type T is allowed (ncT* -> cT*).
    - cT* -> ncT* not implicit, needs cast (not recommended, can cause undefined behaviour).
- **Array**
    - Array-to-pointer decay: Array T[] in expressions decays to pointer T*.

Implicit conversions can be done **transitively**, meaning compiler can process whole array of successive implict conversion, with limitation that it must have maximum one user-defined conversion.



**Explicit** conversion are dony by:
- **const_cast**: For removing cv-qualification (or adding, but that can be done implicitly). Most common for pointers and references.
- **static_cast**: Allows some more conversions by compiler, that are less safe than implicit ones. Usually for numeric conversions where range is known safe, for upcasts (from derived* -> base*), for void pointers (void* -> T*), and for calling explicit constructors or conversion operators explicitly.
- **dynamic_cast**: Used for conversion in hierarchy classes, for downcasting, upcasting, and sidecasting by checking its virtual functions (so it has to have at least one), and return null for pointers and exception for references if it is unvalid.
- **reinterpret_cast**: Can be used for almost all types, except removing cv-qualification, but it doesent change value in any way, it just interprets it in different way, corresponding to given type. Very unsafe and rarely needed.
- **C-type cast**: It tries to use all explicit conversions, except dynamic_cast. Not recommended for use, hard to understand and debug. Syntax: `(new_type)expression`.

### Type specifications

**Char** has representation and allignment that can be processed fastest on the given system. It can be signed char or unsigned char (depending on system). They are always 1 byte, but byte size can vary in systems (99% is 8 bits).

**Int** has minimal size of 16 bits, though on modern  32-bit and 64-bit systems its almost guarnateed that it has minimum size of 32 bits.

**Float** is usually 32 bit floating-point rational number with 8 bits for exponent and 23 bits for mantissa.  
**Double** is usually 64 bit with 11 bits for exponent and 52 for mantissa.  
**Long double** is usually 80 bits.

**Enum** can explicitly define its underlying integral type that is used for storing values of enumerators (default is int, or first integral type that can hold whole range of values), with condition that it must be able to hold all values. Syntax: `enum EnumName : UnderlyingType {...};`

**Array** of base class objects is a bad practise to use. If array of objects of derived class is used to initialize it (*rule of supstitution*), and object of derived class has bigger size, then there will be undefined behaviour and program would not be able to detect a mistake. To avoid it, use array of pointers to objects of base class.

**Struct** are a class type, and should be used only when we need to represent some very simple abstracted data structures, by rule used in implementation of some other structures or abstractions. Struct then by rule have only data members and eventually constructors, rarely some simple operations or destructors. In every other case, classes should be used.

### **Literals**

**Bool**: `True`, `False`. 

**Char**: `'a'`, `u8'a'` (UTF-8), `u'a'` (UCS-2), `U'a'` (UCS-4), `L'a'` ("wide" char), `'AB'` (when literal has 2+ chars, it represents int value depending on implementation).  

**Char escape sequences**: `\'` (quote), `\"` (double quote), `\\` (backlash), `\n` (newline), `\t` (horizontal tab), `\nnn` (sign given with 1 byte code with three octal digits nnn, most used one '\0' for string end), `\xnn` (sign with 1 byte code with two hexadecimal digits nn).

**Int**: `123` (decimal), `0123` (octal), `0x123` (hexadecimal), `0b101` (binary), `123u` (unsigned), `123l` (long), `123ll` (long long), ``123`000`000`` (with apostrophes, helps for reading).

**Double**: `1.23` (decimal), `0x1.23` (hexadecimal), `1.23e-4` (with exponent), `1.23p-4` (hexadecimal exponent), `1.23f` (float), `1.23l` (long double), ``1.200`003`` (with apostrophes).

**String**: `"abc"`, `L/u8/u/U"abc"` (same as char coding), `"abc" "def"` (after preprocessing it will merge them).

---

inline function - multiple definitions - for headers

global / static data member vs local static   
thread_local

smart pointers

initializer list


Copy constructor
Operator overloading
Assignment operator

virtual/override

friend functions and classes

pure abstract classes in c++

dynamic downcast

virtual base class
generalization set
diamond problem

try/catch

const & mutable methods

user defined conversions  
conversion operator  
specificator explicit  
=delete specificator 

user defined literals
constexpr

foward class declaration

auto return type for templates

local class

inheritance function overloading, use using Base::

for (range)

placement new, std::nothrow

using Base::Base, for constructor inheritance

delegating constructor

=default 

implicit defaultly created  
default constructor  
copy constructor  
operator=

virtual destructor

move constructor  
move assignment

rvalue method calling

enumerator class

constexpr constructor

non-member operator overloading, implicit conversion

operator usage

operator new & delete