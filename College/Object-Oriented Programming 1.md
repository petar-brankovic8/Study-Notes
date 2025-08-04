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

**Objects**, basically, are instances of structure that holds data (**attributes**) of the given class. Each (non-static) function member (**method**) of that class is implemented as a regular function with added first hidden argument that points to the object invoking it.

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

When we want to create classes whose behaviours depends a lot on objects current **state**, then the code could get pretty complex with a lot of branching to process every state and more susceptible to errors.

The solution that classic OOP languages do not support, is modeling objects behaviour using **state machines** and generating code from that model (***model-based software engineering***).

### **Threads**

If we have behaviours that need to execute parallelly, creating elementary steps for each of them and cycling between them in infinite while loop can create huge unnecessary complexity, so we implement behaviour of active objects as **threads**.

Each thread has its own sequence of instructions (***control flow***), that includes its own automatic variables and call stack.

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

### **krejzi niga**

refactoring if implementation gets more complex

localization of design decisions

algorithmically decomposed compononets assign to classes as their responsibilities often called scenarios or mechanisms

helper and hook functions/methods

clients, servers, links, associatoins, dependecy injection

public, protected, private order

data members always private, make getters and setters  
all interface operations always public
helper and hook function are protected

friend function and friend class

static class members, initialization and use vs global objects

static class functions vs global functions

generalization/specialization

open-closed principle

final

apstracting shared properties and forming general interface for clients  
the less you know the better  
dependency inversion principle  
generalization + polymorphism = reduction in branching

abstract classes

defining polymorph operation in abstarct class

upcast and downcast

mixin class
interface segregation

generalization set

reclassifying  
diamond problem

virtual base class

java interface

exception handling

## **C++**

Copy constructor
Operator overloading
Assignment operator

virual/override

pure abstract classes in c++

downcast

try/catch