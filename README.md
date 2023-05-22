SOLID Software Design Principles

issues that arise if Solid is not used

    -Code Fragility: tendency of the software to break in many places every time it changes
    -Code Rigidity: tendency for software to be difficult to change, even in simple ways. Every change causes a cascade of subsquent changes in dependent modules

Technical debt
    -The cost of prioritizing fast delivery over code quality for long periods of time.

Fast Delivery:
    -Easiest fix/change
    -Fast
    -Poorly written code

Quality Code:
    -More time-consuming
    -Adds a bit of complexity
    -Better maintainable

High technical debt can lead to increase in Cost Of Change over long time as well as increase in Response time

Technical debt will accumulates over time, but you can attempt to maintain it

Ways to control are by:
    -Write code
    -Refactor it to reduce the debt
    -Rinse and repeat

Solid principle and their benefits

The five SOLID principles are:
-Single responsibility principle
-Open closed principle
-Liskov substitution principle
-Interface segregation principle
-Dependency inversion principle

Benefits are:
    -It is easier to understand and reason about
    -Changes are faster and have a minimal risk level
    -Code is highly maintainable over long periods of time
    -Cost-effective

Solid is good for clean code, here are alternatives:
    -Constant refactoring
    -Design pattern
    -Unit testing (TDD)

Single responsibility principal
    -Every function, class, or module should have one and only one reason to change

Reasons for change:
    -Business logic
    -User interface
    -Persistence
    -Logging
    -Orchestration
    -Users

It is important to identify the reasons to change your components and then to be able to reduce them to a single one.


Why use it:
    -Makes code easier to understand, fix, and maintain
    -Less coupled and more resilient to change
    -Keep fragility and rigidity to very minimal levels
    -More testable design

Multiple reasons to change:
    -If statements
    -Switch statements
    -Monster methods
        -Method is doing more than it's intended purpose
    -God Classes
    -People
        -Different groups will use a code for different purposes or need more specialized for their needs

Danger of multiple responsibilities
    -More difficult to read and reason about
    -Decreasing in quality code due to testing difficulty
    -side effects
    -It can do its original goal, but accidentally do something else due to its other hidden code
    -Coupling: The level of interdependency between various software components

Key Takeaway: if Module A knows too much about Module B, changes to the internals of Module B may break functionality in Module A

Important to refactor responsibilities out to their respective specialized components
"We always want to design components that are self-contained, independent, and with a single and well-defined purpose"


Evolving Code with the Open Closed Principle (OCP)

OCP: classes, functions, and modules should be closed for modification but open for extension

Close for modification
    -Each new feature should not modify existing source code

Open for extension
    -A component should be extendable to make it behave a new way

Modifying existing source code can risk effecting subclasses

Risks are reduced if we implement new code in new class rather than an existing one

when to use OCP:
    -New features are easy to can be added easily with minimal cost
    -Minimize the risk of regression bugs
    -Enforces decoupling by isolating changes in specific components because every time you need to make an important change

Inheritance is used with closed principle without altering the source, but also causes coupling

Strategy pattern is similar to inheritance, but are extraction the interfaces and making classes from there
    -Original and new components are independent and can evolve on in their own respective way


Applying OCP to framework and API

API: a contract or agreement between different software components on how they should work together

A public framework or API is completely under your control
    -Clients cannot change existing code
    -The changes that you make to that framework can impact clients because they might use it in ways that you aren't aware of

A way to avoid such issues is by allowing the library open for extension
    -Providing interfaces that can be used as extension points

Best practices for changing API
    -Do not change public contracts
    -Expose abstractions to your customer and let them add new features on top of your framework
    -If a breaking change is inevitable, give your clients times to adapt



Applying Liskov Substitution Principle (LSP)

LSP:
    -If S is a subtype of T, then objects of type T in a program may be replaced with objects of type S without modifying the functionality or the correctness of the program
    -Any object of a type must be substitutable by objects of a derived type without altering the correctness of that program.

Relationships;
Is a:
Square is a type of rectangle
Is substitution by:
Is rectangle substituted by square

Violations of LSP: (Not being fully/properly substitution)
    -Empty method
    -Incorrect use of extension
    -Harden Precondition
    -Partial implemented interfaces
    -Type checking

Fixing incorrect relationships
    -Eliminate incorrect relationship between objects
    -Use "Tell, don't ask" principle to eliminate type checking and casting
    -Empty method
    -Fix by refactoring
    -Partial implemented interfaces
    -Breaking the interface into more specific interfaces
    -Type checking
    -"Tell, don't ask" principle

Applying LSP in a proactive way:
    -Make sure that a derived type can substitute its base type completely
    -Keep base class small
    -Keep interfaces lean

Modularizing Abstractions with the Interface Segregation Principle (ISP)
Interface segregation principle: Clients should not be forced to depend on methods that they do not use
    -"Interface" is not limited to java interface
Reinforces other principles

If we keep interfaces small, the classes that implement them have a higher chance to fully substitute that interface
If we have large interfaces with many methods, then there's a great chance that the derived types will not fully support all those methods

Benefits of ISP:
    -lean interfaces minimize dependencies on unused members and reduce code coupling
    -Code becomes more cohesive and focused
    -It reinforces the use of the SRP and LSP

By keeping interfaces small, we end up with a more decoupled system that is easier to change, maintain, and evolve over time

"Fat" interfaces:
    -May have many methods
    -Throws exceptions rather than implementation
    -Empty implementation
    -Low cohesion (purpose)
    -Misaligned, belong within other interface
    -Coupling
    -Issues can show not just in interfaces, but abstract classes as well

Refactoring code that depends on larger interfaces:

Solutions:
    -If it's your own code, you can split the interface yourself
    -If its external legacy code, must use design patterns like "Adapter"


Decoupling Components with the Dependency Inversion Principle (DIP)

DIP :High level modules should not rely on low level modules; both should depend on abstractions
    -Abstractions should not depend on details, details should depend on abstractions

High level modules
    -Written to solve real problems and use cases
    -They are more abstract and map to the business domain
    -What the software should do

Low level modules
    -contain implementations details that are required to execute the business policy
    -considered the internals of an application
    -How the software can do various tasks

Abstraction: Something that is not concrete
    -Something that we as developers cannot "new" up. In Java applications, we tend to model these abstractions using interfaces and abstract classes

Writing code that respects DIP
    -High and low level modules depend on the Abstraction and the abstraction does not rely on anything else and is independent

Dependency Injection (DI)
Dependency injection: allows for the creation of dependent objects outside of a class and passing them to the class

A better approach is to declare dependencies in the constructor of a class
Dependency injection helps in further decoupling components by reducing direct dependencies
Inversion of control principle complements dependency injection and addresses these challenges

Inversion of Control (IoC)

IoC: A design principle that delegates object creation, configuration, and lifecycle management to a container or framework
    -You don't "New" up objects
    -Control of object creation is inverted
    -It makes sense to use it for some objects in an application(services, data access, controller)

IoC
    -Makes it easy to switch between different implementations at runtime
    -Increased program modularity
    -Manage the lifecycle of objects and their configure

Spring beans: Objects used by your application that are managed by the Spring IoC container
    -They are created with the configuration that you supply for that container


Design Pattern: A solution to a problem in a context
    -A reusable and named solution to a recurring problem in a context

Decomposing the  Definition
    -Context
    -Problem
    -Solution

Important Aspects of Pattern
    -Recurring problem
    -Reusable solution
    -Name

Patterns are discovered, not created


OOP Building Blocks
-Abstraction
    -Essential details
    -Hiding complexity
-Encapsulation
    -Information hiding
    -Separate behavior that changes
-Inheritence
    -Inherit from another class
    -Methods
    -Properties
    -Avoid duplicated code
-Polymorphism
    -Subclass stands in for the superclass
    -Actual object type is decided at runtime

Other Principle
-Don't repeat yourself (DRY)
-Encapsulate what changes
-Favor composition over inheritence
-Programming to an interface, not an implementation

Principle Vs. Patterns
-You don't have to start with principle
-Principle: Low level knowledge
-Patterns: High level knowledge
    -Proven solutions

Pattern Classification
Purpose-
    -Creational
    -Behavioral
    -Structural

Scope-
    -Class
    -Object

Patterns capture expert knowledge

Well-designed Software
    -Flexible
    -Easy to maintain
    -Reusable

Design Patterns Benefits
    -Patterns are about reusability
    -Find the appropriate design
    -Find classes and interfaces
    -Determining object granularity
    -Communication and documentation
    -Shared vocabulary
    -Precise and complete

Problems with this Design
    -Violates the LSP
    -It's not flexible

Strategy Pattern
    -Defines a family of algorithms, encapsulate each one, and makes them interchangeable
    -Strategy lets the algorithm vary independently of clients that use it
    -Change a part of a system independently of all other parts
    -Swap out behavior at runtime

Strategy Pattern is a mix of:
    -Encapsulating what changes
    -Favoring composition over inheritence
    -Open-close principle
    -Programming to interfaces

Behavior Patterns you should know
    -Strategy and State
    -Command
    -Observer
    -Template method

A strategy is
    -Plan
    -Approach
    -Algorithm

Multiple strategies have
    -Same
    -Inputs
    -Outputs
    -Different
    -Implementation

Client
    -creates Command
    -delegates to Receiver
    -sets command Invoker
    -executes Command

Command method
    -Encapsulates requests in an object

Observer method
    -Notifies when the state of an object changes

Template method
    -Allows to redefine steps of an algorithm by subclasses

Abstract methods and Hooks
    -Abstract methods
        -Required
        -Steps that must be customized
    -Hooks
        -Optional
        -Abstract class may provide a default implementation

Creational patterns you should know
    -Singleton
    -Factory and Abstract Factory
    -Builder

Singleton's pattern
    -Ensures a class only has one instance, providing a global point of access

Factory method
    -Allows subclasses to decide which class to instantiate

Abstract Factory
    -Create hierarchies or families of related objects

Builder Pattern
    -Separate the construction of an object from its representation

Facade Pattern
    -Simplifies an interface to a subsystem, decoupling a client from it
    -May provide additional functionality

Decorator Pattern
    -Attach additional responsibilities to an object dynamically

Adapter Pattern
    -Convert the interface of a class into another interface clients expect
    -Bridge between Legacy code and new code

Proxy Pattern
    -Provides a surrogate for another object to control access to it

Common uses for Proxy
    -Remote calls
    -Security
    -Cache
    -Virtual

Exception: an unexpected event that occurs at runtime due to an error

Try/Catch Clause
    -form of handling exceptions (errors) to prevent crashes
    -used to provide a meaningful message in case of an error
    -can use multiple catchs to handle various forms of exceptions to handle each exception in its own respective manner
    -can use a single catch line with various exceptions to handle all exceptions in the same way

Finally Clause
    -Optional
    -Added at the end of catch and works similarly to the "else statement"
    -Will execute this clause regardless of if catch clause are executed or not

When handling exceptions, you can also use the superclass as a way to catch broader exceptions

All exceptions inherit from the Exception class

You can do this by adding the throws word to the methods header, and then specifying the Exception that will be thrown

Your method can initiate the throwing of an exception by using the word throw inside the method's body and instantiating an exception


