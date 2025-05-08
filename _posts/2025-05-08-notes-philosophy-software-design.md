---
layout: post
title:  "Notes on Philosophy of Software Design"
date:   2025-05-08 19:29:45 +0200
categories: notes books tech
---

## Intro

These are the notes from my reading of the book "Philosophy of Software Design" by John Ousterhout. 
The book presents a set of principles and ideas that can us design better software. I enjoyed reading the book and some of his comments on software design were useful for me.
I specially enjoyed the idea o shallow vs deep modules, and how any type of interface should be designed to be deeper.

Two quotes that I found specially interesting when approaching software engineering where:

> The most fundamental problem in computer science is problem decomposition: how to take a complex problem and divide it up into pieces that can be solved independently.

and

> However, there is quite a bit of scientific evidence that outstanding performance in many fields is related more to high-quality practice than innate ability (see, for example, Talent is Overrated by Geoff Colvin).


## Notes

**Page 3:**

> Incremental development means that software design is never done. Design happens continuously over the life of a system: developers should always be thinking about design issues. Incremental development also means continuous redesign.

**Page 5:**

> Complexity is anything related to the structure of a software system that makes it hard to understand and modify the system.

> Complexity can take many forms. For example, it might be hard to understand how a piece of code works; it might take a lot of effort to implement a small improvement, or it might not be clear which parts of the system must be modified to make the improvement; it might be difficult to fix one bug without introducing another. If a software system is hard to understand and modify, then it is complicated; if it is easy to understand and modify, then it is simple.

**Page 6:**

> Isolating complexity in a place where it will never be seen is almost as good as eliminating the complexity entirely.

> Complexity is more apparent to readers than writers. If you write a piece of code and it seems simple to you, but other people think it is complex, then it is complex.

> Your job as a developer is not just to create code that you can work with easily, but to create code that others can also work with easily.

**Page 7:**

> Change amplification: The first symptom of complexity is that a seemingly simple change requires code modifications in many different places.

> One of the goals of good design is to reduce the amount of code that is affected by each design decision, so design changes don’t require very many code modifications.

> Cognitive load: The second symptom of complexity is cognitive load, which refers to how much a developer needs to know in order to complete a task.

> A higher cognitive load means that developers have to spend more time learning the required information, and there is a greater risk of bugs because they have missed something important.

> Cognitive load arises in many ways, such as APIs with many methods, global variables, inconsistencies, and dependencies between modules.

> Sometimes an approach that requires more lines of code is actually simpler, because it reduces cognitive load.

**Page 8:**

> Unknown unknowns: The third symptom of complexity is that it is not obvious which pieces of code must be modified to complete a task, or what information a developer must have to carry out the task successfully.

> An unknown unknown means that there is something you need to know, but there is no way for you to find out what it is, or even whether there is an issue. You won’t find out about it until bugs appear after you make a change.


**Page: 9**
> One of the most important goals of good design is for a system to be obvious.

> Complexity is caused by two things: dependencies and obscurity.


**Page: 10**

> Dependencies are a fundamental part of software and can’t be completely eliminated. In fact, we intentionally introduce dependencies as part of the software design process. Every time you write a new class you create dependencies around the API for that class. However, one of the goals of software design is to reduce the number of dependencies and to make the dependencies that remain as simple and obvious as possible.

> The second cause of complexity is obscurity. Obscurity occurs when important information is not obvious. A simple example is a variable name that is so generic that it doesn’t carry much useful information (e.g., time). Or,

> In many cases, obscurity comes about because of inadequate documentation; Chapter 13 deals with this topic. However, obscurity is also a design issue. If a system has a clean and obvious design, then it will need less documentation. The need for extensive documentation is often a red flag that the design isn’t quite right. The best way to reduce obscurity is by simplifying the system design.


**Page: 12**

> The incremental nature of complexity makes it hard to control. It’s easy to convince yourself that a little bit of complexity introduced by your current change is no big deal. However, if every developer takes this approach for every change, complexity accumulates rapidly. Once complexity has accumulated, it is hard to eliminate, since fixing a single dependency or obscurity will not, by itself, make a big difference.


**Page: 13**

> Most programmers approach software development with a mindset I call tactical programming. In the tactical approach, your main focus is to get something working, such as a new feature or a bug fix.

> However, tactical programming makes it nearly impossible to produce a good system design.


**Page: 14**

> Before long, some of the complexities will start causing problems, and you will begin to wish you hadn’t taken those early shortcuts. But, you will tell yourself that it’s more important to get the next feature working than to go back and refactor existing code. Refactoring may help out in the long run, but it will definitely slow down the current task. So, you look for quick patches to work around any problems you encounter. This just creates more complexity, which then requires more patches. Pretty soon the code is a mess, but by this point things are so bad that it would take months of work to clean it up.

> The first step towards becoming a good software designer is to realize that working code isn’t enough. It’s not acceptable to introduce unnecessary complexities in order to finish your current task faster. The most important thing is the long-term structure of the system.


**Page: 15**

> Strategic programming requires an investment mindset. Rather than taking the fastest path to finish your current project, you must invest time to improve the design of the system.

> Some of the investments will be proactive. For example, it’s worth taking a little extra time to find a simple design for each new class; rather than implementing the first idea that comes to mind, try a couple of alternative designs and pick the cleanest one.

> Other investments will be reactive. No matter how much you invest up front, there will inevitably be mistakes in your design decisions. Over time, these mistakes will become obvious. When you discover a design problem, don’t just ignore it or patch around it; take a little extra time to fix it. If you program strategically, you will continually make small improvements to the system design.

> Thus, the best approach is to make lots of small investments on a continual basis. I suggest spending about 10–20% of your total development time on investments.


**Page: 18**

> Good design doesn’t come for free. It has to be something you invest in continually, so that small problems don’t accumulate into big ones. Fortunately, good design eventually pays for itself, and sooner than you might think.


> It’s crucial to be consistent in applying the strategic approach and to think of investment as something to do today, not tomorrow. When you get in a crunch it will be tempting to put off cleanups until after the crunch is over. However, this is a slippery slope; after the current crunch there will almost certainly be another one, and another after that. Once you start delaying design improvements, it’s easy for the delays to become permanent and for your culture to slip into the tactical approach. The longer you wait to address design problems, the bigger they become; the solutions become more intimidating, which makes it easy to put them off even more.


**Page: 19**

> Modules can take many forms, such as classes, subsystems, or services. In an ideal world, each module would be completely independent of the others: a developer could work in any of the modules without knowing anything about any of the other modules. In this world, the complexity of a system would be the complexity of its worst module.


> Unfortunately, this ideal is not achievable. Modules must work together by calling each others’s functions or methods. As a result, modules must know something about each other.

> For example, the arguments for a method create a dependency between the method and any code that invokes the method. If the required arguments change, all invocations of the method must be modified to conform to the new signature. Dependencies can take many other forms, and they can be quite subtle. The goal of modular design is to minimize the dependencies between modules.

> In order to manage dependencies, we think of each module in two parts: an interface and an implementation. The interface consists of everything that a developer working in a different module must know in order to use the given module.

> Typically, the interface describes what the module does but not how it does it.


**Page: 20**

> The implementation consists of the code that carries out the promises made by the interface.

> A developer should not need to understand the implementations of modules other than the one he or she is working in.

> The best modules are those whose interfaces are much simpler than their implementations. Such modules have two advantages. First, a simple interface minimizes the complexity that a module imposes on the rest of the system. Second, if a module is modified in a way that does not change its interface, then no other module will be affected by the modification. If a module’s interface is much simpler than its implementation, there will be many aspects of the module that can be changed without affecting other modules.

> The interface to a module contains two kinds of information: formal and informal. The formal parts of an interface are specified explicitly in the code, and some of these can be checked for correctness by the programming language.

**Page: 21**

> Each interface also includes informal elements. These are not specified in a way that can be understood or enforced by the programming language. The informal parts of an interface include its high-level behavior, such as the fact that a function deletes the file named by one of its arguments. If there are constraints on the usage of a class (perhaps one method must be called before another), these are also part of the class’s interface.


> The informal aspects of an interface can only be described using comments, and the programming language cannot ensure that the description is complete or accurate1.

> The term abstraction is closely related to the idea of modular design. An abstraction is a simplified view of an entity, which omits unimportant details.

> Abstractions are useful because they make it easier for us to think about and manipulate complex things.

> In modular programming, each module provides an abstraction in form of its interface. The interface presents a simplified view of the module’s functionality; the details of the implementation are unimportant from the standpoint of the module’s abstraction, so they are omitted from the interface.


**Page: 22**

> An abstraction can go wrong in two ways. First, it can include details that are not really important; when this happens, it makes the abstraction more complicated than necessary, which increases the cognitive load on developers using the abstraction. The second error is when an abstraction omits details that really are important. This results in obscurity: developers looking only at the abstraction will not have all the information they need to use the abstraction correctly. An abstraction that omits important details is a false abstraction: it might appear simple, but in reality it isn’t.

> The key to designing abstractions is to understand what is important, and to look for designs that minimize the amount of information that is important.


**Page: 23**

> Module depth is a way of thinking about cost versus benefit. The benefit provided by a module is its functionality. The cost of a module (in terms of system complexity) is its interface. A module’s interface represents the complexity that the module imposes on the rest of the system: the smaller and simpler the interface, the less complexity that it introduces.

> The best modules are those with the greatest benefit and the least cost. Interfaces are good, but more, or larger, interfaces are not necessarily better!


**Page: 25**

> On the other hand, a shallow module is one whose interface is relatively complex in comparison to the functionality that it provides. For example, a class that implements linked lists is shallow. It doesn’t take much code to manipulate a linked list (inserting or deleting an element takes only a few lines), so the linked list abstraction doesn’t hide very many details. The complexity of a linked list interface is nearly as great as the complexity of its implementation.

> Shallow classes are sometimes unavoidable, but they don’t provide help much in managing complexity.

> A shallow module is one whose interface is complicated relative to the functionality it provides. Shallow modules don’t help much in the battle against complexity, because the benefit they provide (not having to learn about how they work internally) is negated by the cost of learning and using their interfaces. Small modules tend to be shallow.


**Page: 28**

> but interfaces should be designed to make the common case as simple as possible

> If an interface has many features, but most developers only need to be aware of a few of them, the effective complexity of that interface is just the complexity of the commonly used features.


**Page: 29**

> The most important technique for achieving deep modules is information hiding. This technique was first described by David Parnas1. The basic idea is that each module should encapsulate a few pieces of knowledge, which represent design decisions. The knowledge is embedded in the module’s implementation but does not appear in its interface, so it is not visible to other modules.


**Page: 30**

> Information hiding reduces complexity in two ways. First, it simplifies the interface to a module. The interface reflects a simpler, more abstract view of the module’s functionality and hides the details; this reduces the cognitive load on developers who use the module.

> The best form of information hiding is when information is totally hidden within a module, so that it is irrelevant and invisible to users of the module. However, partial information hiding also has value. For example, if a particular feature or piece of information is only needed by a few of a class’s users, and it is accessed through separate methods so that it isn’t visible in the most common use cases, then that information is mostly hidden. Such information will create fewer dependencies than information that is visible to every user of the class.

> The opposite of information hiding is information leakage. Information leakage occurs when a design decision is reflected in multiple modules. This creates a dependency between the modules: any change to that design decision will require changes to all of the involved modules.


**Page: 31**

> However, information can be leaked even if it doesn’t appear in a module’s interface. Suppose two classes both have knowledge of a particular file format (perhaps one class reads files in that format and the other class writes them). Even if neither class exposes that information in its interface, they both depend on the file format: if the format changes, both classes will need to be modified. Back-door leakage like this is more pernicious than leakage through an interface, because it isn’t obvious.

> Information leakage occurs when the same knowledge is used in multiple places, such as two different classes that both understand the format of a particular type of file.

> One common cause of information leakage is a design style I call temporal decomposition. In temporal decomposition, the structure of a system corresponds to the time order in which operations will occur.


**Page: 32**

> It’s easy to fall into the trap of temporal decomposition, because the order in which operations must occur is often on your mind when you code. However, most design decisions manifest themselves at several different times over the life of the application; as a result, temporal decomposition often results in information leakage.

> When designing modules, focus on the knowledge that’s needed to perform each task, not the order in which tasks occur.

> temporal decomposition, execution order is reflected in the code structure: operations that happen at different times are in different methods or classes. If the same knowledge is used at different points in execution, it gets encoded in multiple places, resulting in information leakage.


**Page: 34**

> This example illustrates a general theme in software design: information hiding can often be improved by making a class slightly larger. One reason for doing this is to bring together all of the code related to a particular capability (such as parsing an HTTP request), so that the resulting class contains everything related to that capability. A second reason for increasing the size of a class is to raise the level of the interface; for example, rather than having separate methods for each of three steps of a computation, have a single method that performs the entire computation. This can result in a simpler interface. Both of these benefits apply in the example of the previous paragraph: combining the classes brings together all of the code related to parsing an HTTP request, and it replaces two externally-visible methods with one. The combined class is deeper than the original classes.

> This method is shallow, and it exposes the internal representation used by the HTTPRequest class to store parameters. Any change to that representation will result in a change to the interface, which will require modifications to all callers. When implementations are modified, the changes often involve changes in the representation of key data structures (to improve performance, for example). Thus, it’s important to avoid exposing internal data structures as much as possible. This approach also makes more work for callers: a caller must first invoke getParams, then it must call another method to retrieve a specific parameter from the Map. Finally, callers must realize that they should not modify the Map returned by getParams, since that will affect the internal state of the HTTPRequest.


**Page: 36**

> Defaults illustrate the principle that interfaces should be designed to make the common case as simple as possible. They are also an example of partial information hiding: in the normal case, the caller need not be aware of the existence of the defaulted item. In the rare cases where a caller needs to override a default, it will have to know about the value, and it can invoke a special method to modify it.

> If the API for a commonly used feature forces users to learn about other features that are rarely used, this increases the cognitive load on users who don’t need the rarely used features.


**Page: 37**

> Try to design the private methods within a class so that each method encapsulates some information or capability and hides it from the rest of the class. In addition, try to minimize the number of places where each instance variable is used.

> if you can reduce the number of places where a variable is used, you will eliminate dependencies within the class and reduce its complexity.

> Information hiding and deep modules are closely related. If a module hides a lot of information, that tends to increase the amount of functionality provided by the module while also reducing its interface. This makes the module deeper. Conversely, if a module doesn’t hide much information, then either it doesn’t have much functionality, or it has a complex interface; either way, the module is shallow.


**Page: 38**

> Instead, think about the different pieces of knowledge that are needed to carry out the tasks of your application, and design each module to encapsulate one or a few of those pieces of knowledge. This will produce a clean and simple design with deep modules.


**Page: 40**

> In my experience, the sweet spot is to implement new modules in a somewhat general-purpose fashion. The phrase “somewhat general-purpose” means that the module’s functionality should reflect your current needs, but its interface should not. Instead, the interface should be general enough to support multiple uses. The interface should be easy to use for today’s needs without being tied specifically to them. The word “somewhat” is important: don’t get carried away and build something so general-purpose that it is difficult to use for your current needs.

> The most important (and perhaps surprising) benefit of the general-purpose approach is that it results in simpler and deeper interfaces than a special-purpose approach.


**Page: 41**

> This approach created information leakage between the user interface and the text class. Abstractions related to the user interface, such as the selection or the backspace key, were reflected in the text class; this increased the cognitive load for developers working on the text class. Each new user interface operation required a new method to be defined in the text class, so a developer working on the user interface was likely to end up working on the text class as well. One of the goals in class design is to allow each class to be developed independently, but the specialized approach tied the user interface and text classes together.


**Page: 43**

> The general-purpose approach provides a cleaner separation between the text and user interface classes, which results in better information hiding. The text class need not be aware of specifics of the user interface, such as how the backspace key is handled; these details are now encapsulated in the user interface class. New user interface features can be added without creating new supporting functions in the text class. The general-purpose interface also reduces cognitive load: a developer working on the user interface only needs to learn a few simple methods, which can be reused for a variety of purposes.


> One of the most important elements of software design is determining who needs to know what, and when. When the details are important, it is better to make them explicit and as obvious as possible, such as the revised implementation of the backspace operation. Hiding this information behind an interface just creates obscurity.


> What is the simplest interface that will cover all my current needs? If you reduce the number of methods in an API without reducing its overall capabilities, then you are probably creating more general-purpose methods.

> In how many situations will this method be used? If a method is designed for one particular use, such as the backspace method, that is a red flag that it may be too special-purpose. See if you can replace several special-purpose methods with a single general-purpose method.


**Page: 44**

> Is this API easy to use for my current needs? This question can help you to determine when you have gone too far in making an API simple and general-purpose. If you have to write a lot of additional code to use a class for your current purpose, that’s a red flag that the interface doesn’t provide the right functionality.

> Software systems are composed in layers, where higher layers use the facilities provided by lower layers. In a well-designed system, each layer provides a different abstraction from the layers above and below it; if you follow a single operation as it moves up and down through layers by invoking methods, the abstractions change with each method call.


**Page: 46**

> A pass-through method is one that does nothing except pass its arguments to another method, usually with the same API as the pass-through method. This typically indicates that there is not a clean division of responsibility between the classes.


**Page: 47**

> Pass-through methods make classes shallower: they increase the interface complexity of the class, which adds complexity, but they don’t increase the total functionality of the system.

> Pass-through methods indicate that there is confusion over the division of responsibility between classes.

> This is usually a bad idea: the interface to a piece of functionality should be in the same class that implements the functionality. When you see pass-through methods from one class to another, consider the two classes and ask yourself “Exactly which features and abstractions is each of these classes responsible for?” You will probably notice that there is an overlap in responsibility between the classes.

> The solution is to refactor the classes so that each class has a distinct and coherent set of responsibilities. Figure 7.1 illustrates several ways to do this. One approach, shown in Figure 7.1(b), is to expose the lower level class directly to the callers of the higher level class, removing all responsibility for the feature from the higher level class. Another approach is to redistribute the functionality between the classes, as in Figure 7.1(c). Finally, if the classes can’t be disentangled, the best solution may be to merge them as in Figure 7.1(d).

> One example where it’s useful for a method to call another method with the same signature is a dispatcher. A dispatcher is a method that uses its arguments to select one of several other methods to invoke; then it passes most or all of its arguments to the chosen method. The signature for the dispatcher is often the same as the signature for the methods that it calls. Even so, the dispatcher provides useful functionality: it chooses which of several other methods should carry out each task.


**Page: 49**

> The decorator design pattern (also known as a “wrapper”) is one that encourages API duplication across layers. A decorator object takes an existing object and extends its functionality; it provides an API similar or identical to the underlying object, and its methods invoke the methods of the underlying object.

> Could you add the new functionality directly to the underlying class, rather than creating a decorator class? This makes sense if the new functionality is relatively general-purpose, or if it is logically related to the underlying class, or if most uses of the underlying class will also use the new functionality.

> If the new functionality is specialized for a particular use case, would it make sense to merge it with the use case, rather than creating a separate class?

> Could you merge the new functionality with an existing decorator, rather than creating a new decorator? This would result in a single deeper decorator class rather than multiple shallow ones.

> Finally, ask yourself whether the new functionality really needs to wrap the existing functionality: could you implement it as a stand-alone class that is independent of the base class?


**Page: 50**

> Sometimes decorators make sense, but there is usually a better alternative.

> Another application of the “different layer, different abstraction” rule is that the interface of a class should normally be different from its implementation: the representations used internally should be different from the abstractions that appear in the interface. If the two have similar abstractions, then the class probably isn’t very deep.

> Another form of API duplication across layers is a pass-through variable, which is a variable that is passed down through a long chain of methods.


**Page: 51**

> Pass-through variables add complexity because they force all of the intermediate methods to be aware of their existence, even though the methods have no use for the variables. Furthermore, if a new variable comes into existence (for example, a system is initially built without support for certificates, but you later decide to add that support), you may have to modify a large number of interfaces and methods to pass the variable through all of the relevant paths.

> Eliminating pass-through variables can be challenging. One approach is to see if there is already an object shared between the topmost and bottommost methods.

> The solution I use most often is to introduce a context object as in Figure 7.2(d). A context stores all of the application’s global state (anything that would otherwise be a pass-through variable or global variable). Most applications have multiple variables in their global state, representing things such as configuration options, shared subsystems, and performance counters. There is one context object per instance of the system. The context allows multiple instances of the system to coexist in a single process, each with its own context.

> Unfortunately, the context will probably be needed in many places, so it can potentially become a pass-through variable. To reduce the number of methods that must be aware of it, a reference to the context can be saved in most of the system’s major objects. In the example of Figure 7.2(d), the class containing m3 stores a reference to the context as an instance variable in its objects. When a new object is created, the creating method retrieves the context reference from its object and passes it to the constructor for the new object. With this approach, the context is available everywhere, but it only appears as an explicit argument in constructors.


**Page: 54**

> Contexts are far from an ideal solution. The variables stored in a context have most of the disadvantages of global variables; for example, it may not be obvious why a particular variable is present, or where it is used. Without discipline, a context can turn into a huge grab-bag of data that creates nonobvious dependencies throughout the system. Contexts may also create thread-safety issues; the best way to avoid problems is for variables in a context to be immutable. Unfortunately, I haven’t found a better solution than contexts.

> The “different layer, different abstraction” rule is just an application of this idea: if different layers have the same abstraction, such as pass-through methods or decorators, then there’s a good chance that they haven’t provided enough benefit to compensate for the additional infrastructure they represent. Similarly, pass-through arguments require each of several methods to be aware of their existence (which adds to complexity) without contributing additional functionality.


**Page: 55**

> it is more important for a module to have a simple interface than a simple implementation.


**Page: 56**

> Configuration parameters are an example of moving complexity upwards instead of down. Rather than determining a particular behavior internally, a class can export a few parameters that control its behavior, such as the size of a cache or the number of times to retry a request before giving up.


**Page: 57**

> When you do create configuration parameters, see if you can compute reasonable defaults automatically, so users will only need to provide values under exceptional conditions.

> Pulling complexity down makes the most sense if (a) the complexity being pulled down is closely related to the class’s existing functionality, (b) pulling the complexity down will result in many simplifications elsewhere in the application, and (c) pulling the complexity down simplifies the class’s interface. Remember that the goal is to minimize overall system complexity.


**Page: 61**

> When two or more modules are combined into a single module, it may be possible to define an interface for the new module that is simpler or easier to use than the original interfaces.

> If you find the same pattern of code repeated over and over, see if you can reorganize the code to eliminate the repetition. One approach is to factor the repeated code out into a separate method and replace the repeated code snippets with calls to the method. This approach is most effective if the repeated code snippet is long and the replacement method has a simple signature. If the snippet is only one or two lines long, there may not be much benefit in replacing it with a method call. If the snippet interacts in complex ways with its environment (such as by accessing numerous local variables), then the replacement method might require a complex signature (such as many pass-by-reference arguments), which would reduce its value.


**Page: 64**

> In general, the lower layers of a system tend to be more general-purpose and the upper layers more special-purpose. For example, the topmost layer of an application consists of features totally specific to that application.

> When you encounter a class that includes both general-purpose and special-purpose features for the same abstraction, see if the class can be separated into two classes, one containing the general-purpose features, and the other layered on top of it to provide the special-purpose features.


**Page: 65**

> Red Flag: Special-General Mixture This red flag occurs when a general-purpose mechanism also contains code specialized for a particular use of that mechanism. This makes the mechanism more complicated and creates information leakage between the mechanism and the particular use case: future modifications to the use case are likely to require changes to the underlying mechanism as well.


**Page: 70**

> However, length by itself is rarely a good reason for splitting up a method. In general, developers tend to break up methods too much. Splitting up a method introduces additional interfaces, which add to complexity. It also separates the pieces of the original method, which makes the code harder to read if the pieces are actually related. You shouldn’t break up a method unless it makes the overall system simpler; I’ll discuss how this might happen below.


**Page: 71**

> When designing methods, the most important goal is to provide clean and simple abstractions. Each method should do one thing and do it completely. The method should have a clean and simple interface, so that users don’t need to have much information in their heads in order to use it correctly. The method should be deep: its interface should be much simpler than its implementation. If a method has all of these properties, then it probably doesn’t matter whether it is long or not.

> Splitting up a method only makes sense if it results in cleaner abstractions, overall. There are two ways to do this, which are diagrammed in Figure 9.3. The best way is by factoring out a subtask into a separate method, as shown in Figure 9.3(b). The subdivision results in a child method containing the subtask and a parent method containing the remainder of the original method; the parent invokes the child. The interface of the new parent method is the same as the original method. This form of subdivision makes sense if there is a subtask that is cleanly separable from the rest of the original method, which means (a) someone reading the child method doesn’t need to know anything about the parent method and (b) someone reading the parent method doesn’t need to understand the implementation of the child method. Typically this means that the child method is relatively general-purpose: it could conceivably be used by other methods besides the parent.


**Page: 72**

> There are also situations where a system can be made simpler by joining methods together. For example, joining methods might replace two shallow methods with one deeper method; it might eliminate duplication of code; it might eliminate dependencies between the original methods, or intermediate data structures; it might result in better encapsulation, so that knowledge that was previously present in multiple places is now isolated in a single place; or it might result in a simpler interface, as discussed in Section 9.2.


**Page: 76**

> Exception handling code is inherently more difficult to write than normal-case code. An exception disrupts the normal flow of the code; it usually means that something didn’t work as expected. When an exception occurs, the programmer can deal with it in two ways, each of which can be complicated. The first approach is to move forward and complete the work in progress in spite of the exception. For example, if a network packet is lost, it can be resent; if data is corrupted, perhaps it can be recovered from a redundant copy. The second approach is to abort the operation in progress and report the exception upwards. However, aborting can be complicated because the exception may have occurred at a point where system state is inconsistent (a data structure might have been partially initialized); the exception handling code must restore consistency, such as by unwinding any changes made before the exception occurred. Furthermore, exception handling code creates opportunities for more exceptions. Consider the case of resending a lost network packet. Perhaps the packet wasn’t actually lost, but was simply delayed. In this case, resending the packet will result in duplicate packets arriving at the peer; this introduces a new exceptional condition that the peer must handle.

> Secondary exceptions occurring during recovery are often more subtle and complex than the primary exceptions. If an exception is handled by aborting the operation in progress, then this must be reported to the caller as another exception. To prevent an unending cascade of exceptions, the developer must eventually find a way to handle exceptions without introducing more exceptions.


**Page: 77**

> (one of my favorite sayings: “code that hasn’t been executed doesn’t work”).

> A recent study found that more than 90% of catastrophic failures in distributed data-intensive systems were caused by incorrect error handling1. When exception handling code fails, it’s difficult to debug the problem, since it occurs so infrequently.

**Page: 78**

> Programmers exacerbate the problems related to exception handling by defining unnecessary exceptions. Most programmers are taught that it’s important to detect and report errors; they often interpret this to mean “the more errors detected, the better.” This leads to an over-defensive style where anything that looks even a bit suspicious is rejected with an exception, which results in a proliferation of unnecessary exceptions that increase the complexity of the system.

> It’s tempting to use exceptions to avoid dealing with difficult situations: rather than figuring out a clean way to handle it, just throw an exception and punt the problem to the caller.

> However, if you are having trouble figuring out what to do for the particular situation, there’s a good chance that the caller won’t know what to do either. Generating an exception in a situation like this just passes the problem to someone else and adds to the system’s complexity.

> The exceptions thrown by a class are part of its interface; classes with lots of exceptions have complex interfaces, and they are shallower than classes with fewer exceptions.


**Page: 79**

> Throwing exceptions is easy; handling them is hard. Thus, the complexity of exceptions comes from the exception handling code. The best way to reduce the complexity damage caused by exception handling is to reduce the number of places where exceptions have to be handled. The


**Page: 81**

> When I argue for defining errors out of existence, people sometimes counter that throwing errors will catch bugs; if errors are defined out of existence, won’t that result in buggier software? Perhaps this is why the Java developers decided that substring should throw exceptions. The error-ful approach may catch some bugs, but it also increases complexity, which results in other bugs. In the error-ful approach, developers must write additional code to avoid or ignore the errors, and this increases the likelihood of bugs; or, they may forget to write the additional code, in which case unexpected errors may be thrown at runtime. In contrast, defining errors out of existence simplifies APIs and it reduces the amount of code that must be written. Overall, the best way to reduce bugs is to make software simpler.

> The second technique for reducing the number of places where exceptions must be handled is exception masking. With this approach, an exceptional condition is detected and handled at a low level in the system, so that higher levels of software need not be aware of the condition.

> Exception masking doesn’t work in all situations, but it is a powerful tool in the situations where it works. It results in deeper classes, since it reduces the class’s interface (fewer exceptions for users to be aware of) and adds functionality in the form of the code that masks the exception. Exception masking is an example of pulling complexity downward.


**Page: 82**

> The third technique for reducing complexity related to exceptions is exception aggregation. The idea behind exception aggregation is to handle many exceptions with a single piece of code; rather than writing distinct handlers for many individual exceptions, handle them all in one place with a single handler.


**Page: 85**

> This example illustrates a generally-useful design pattern for exception handling. If a system processes a series of requests, it’s useful to define an exception that aborts the current request, cleans up the system’s state, and continues with the next request. The exception is caught in a single place near the top of the system’s request-handling loop. This exception can be thrown at any point in the processing of a request to abort the request; different subclasses of the exception can be defined for different conditions. Exceptions of this type should be clearly distinguished from exceptions that are fatal to the entire system.


> Exception aggregation works best if an exception propagates several levels up the stack before it is handled; this allows more exceptions from more methods to be handled in the same place. This is the opposite of exception masking: masking usually works best if an exception is handled in a low-level method.

> RAMCloud does not have separate recovery mechanisms for each different kind of error. Instead, RAMCloud “promotes” many smaller errors into larger ones. RAMCloud could, in principle, handle a corrupted object by restoring that one object from a backup copy. However, it doesn’t do this. Instead, if it discovers a corrupted object it crashes the server containing the object. RAMCloud uses this approach because crash recovery is quite complex and this approach minimized the number of different recovery mechanisms that had to be created. Creating a recovery mechanism for crashed servers was unavoidable, so RAMCloud uses the same mechanism for other kinds of recovery as well. This reduced the amount of code that had to be written, and it also meant that server crash recovery gets invoked more often. As a result, bugs in recovery are more likely to be discovered and fixed.


**Page: 86**

> One way of thinking about exception aggregation is that it replaces several special-purpose mechanisms, each tailored for a particular situation, with a single general-purpose mechanism that can handle multiple situations.


**Page: 87**

> For the same reason that it makes sense to define errors out of existence, it also makes sense to define other special cases out of existence. Special cases can result in code that is riddled with if statements, which make the code hard to understand and lead to bugs. Thus, special cases should be eliminated wherever possible. The best way to do this is by designing the normal case in a way that automatically handles the special cases without any extra code.


**Page: 88**

> Defining away exceptions, or masking them inside a module, only makes sense if the exception information isn’t needed outside the module. This was true for the examples in this chapter, such the Tcl unset command and the Java substring method; in the rare situations where a caller cares about the special cases detected by the exceptions, there are other ways for it to get this information.

> With exceptions, as with many other areas in software design, you must determine what is important and what is not important. Things that are not important should be hidden, and the more of them the better. But when something is important, it must be exposed.


**Page: 90**

> Special cases of any form make code harder to understand and increase the likelihood of bugs.

> The best way to do this is by redefining semantics to eliminate error conditions.

**Page: 91**

> Designing software is hard, so it’s unlikely that your first thoughts about how to structure a module or system will produce the best design. You’ll end up with a much better result if you consider multiple options for each major design decision: design it twice.


**Page: 92**

> Does one alternative have a simpler interface than another? In the text example, all of the text interfaces are relatively simple. Is one interface more general-purpose than another? Does one interface enable a more efficient implementation than another? In the text example, the character-oriented approach is likely to be significantly slower than the others, because it requires a separate call into the text module for each character.

> Sometimes none of the alternatives is particularly attractive; when this happens, see if you can come up with additional schemes. Use the problems you identified with the original alternatives to drive the new design(s).

> The design-it-twice principle can be applied at many levels in a system.

> Designing it twice does not need to take a lot of extra time. For a smaller module such as a class, you may not need more than an hour or two to consider alternatives.


**Page: 94**

> For larger modules you’ll spend more time in the initial design explorations, but the implementation will also take longer, and the benefits of a better design will also be higher.

> The design-it-twice approach not only improves your designs, but it also improves your design skills. The process of devising and comparing multiple approaches will teach you about the factors that make designs better or worse. Over time, this will make it easier for you to rule out bad designs and hone in on really great ones.


**Page: 96**

> there is still a significant amount of design information that can’t be represented in code. For example, only a small part of a class’s interface, such as the signatures of its methods, can be specified formally in the code. The informal aspects of an interface, such as a high-level description of what each method does or the meaning of its result, can only be described in comments.

> if you write code with the expectation that users will read method implementations, you will try to make each method as short as possible, so that it’s easy to read. If the method does anything nontrivial, you will break it up into several smaller methods. This will result in a large number of shallow methods. Furthermore, it doesn’t really make the code easier to read: in order to understand the behavior of the top-level method, readers will probably need to understand the behaviors of the nested methods. For large systems it isn’t practical for users to read the code to learn the behavior.


**Page: 97**

> Comments allow us to capture the additional information that callers need, thereby completing the simplified view while hiding implementation details.

> Furthermore, many of the most important comments are those related to abstractions, such as the top-level documentation for classes and methods.


**Page: 98**

> The overall idea behind comments is to capture information that was in the mind of the designer but couldn’t be represented in the code.


**Page: 100**

> Chapter 2 described three ways in which complexity manifests itself in software systems: Change amplification: a seemingly simple change requires code modifications in many places. Cognitive load: in order to make a change, the developer must accumulate a large amount of information. Unknown unknowns: it is unclear what code needs to be modified, or what information must be considered in order to make those modifications.

> Documentation can reduce cognitive load by providing developers with the information they need to make changes and by making it easy for developers to ignore information that is irrelevant.

> Documentation can also reduce the unknown unknowns by clarifying the structure of the system, so that it is clear what information and code is relevant for any given change.


**Page: 101**

> The guiding principle for comments is that comments should describe things that aren’t obvious from the code.


**Page: 102**

> Developers should be able to understand the abstraction provided by a module without reading any code other than its externally visible declarations.

> The first step in writing comments is to decide on conventions for commenting, such as what you will comment and the format you will use for comments.

> Interface: a comment block that immediately precedes the declaration of a module such as a class, data structure, function, or method. The comment describe’s the module’s interface. For a class, the comment describes the overall abstraction provided by the class. For a method or function, the comment describes its overall behavior, its arguments and return value, if any, any side effects or exceptions that it generates, and any other requirements the caller must satisfy before invoking the method. Data structure member: a comment next to the declaration of a field in a data structure, such as an instance variable or static variable for a class.


**Page: 103**

> Unfortunately, many comments are not particularly helpful. The most common reason is that the comments repeat the code: all of the information in the comment can easily be deduced from the code next to the comment.


**Page: 104**

> Red Flag: Comment Repeats Code If the information in a comment is already obvious from the code next to the comment, then the comment isn’t helpful. One example of this is when the comment uses the same words that make up the name of the thing it is describing.


**Page: 105**

> Comments augment the code by providing information at a different level of detail.

> Some comments provide information at a lower, more detailed, level than the code; these comments add precision by clarifying the exact meaning of the code. Other comments provide information at a higher, more abstract, level than the code; these comments offer intuition, such as the reasoning behind the code, or a simpler and more abstract way of thinking about the code.

> Comments at the same level as the code are likely to repeat the code.

**Page: 106**

> Comments can fill in missing details such as: What are the units for this variable? Are the boundary conditions inclusive or exclusive? If a null value is permitted, what does it imply? If a variable refers to a resource that must eventually be freed or closed, who is responsible for freeing or closing it? Are there certain properties that are always true for the variable (invariants), such as “this list always contains at least one entry”?


**Page: 107**

> When documenting a variable, think nouns, not verbs. In other words, focus on what the variable represents, not how it is manipulated.

> These comments are written at a higher level than the code. They omit details and help the reader to understand the overall intent and structure of the code. This approach is commonly used for comments inside methods, and for interface comments.

**Page: 108**

> The original comment didn’t describe the overall intent of the code, so it’s hard for a reader to decide whether the code is behaving correctly.

> Higher-level comments are more difficult to write than lower-level comments because you must think about the code in a different way. Ask yourself: What is this code trying to do? What is the simplest thing you can say that explains everything in the code? What is the most important thing about this code?

> Engineers tend to be very detail-oriented. We love details and are good at managing lots of them; this is essential for being a good engineer. But, great software designers can also step back from the details and think about a system at a higher level. This means deciding which aspects of the system are most important, and being able to ignore the low-level details and think about the system only in terms of its most fundamental characteristics.


**Page: 109**

> Comments of the form “how we get here” are very useful for helping people to understand code.


**Page: 110**

> If you want code that presents good abstractions, you must document those abstractions with comments.

> If interface comments must also describe the implementation, then the class or method is shallow.

> The interface comment for a method includes both higher-level information for abstraction and lower-level details for precision: The comment usually starts with a sentence or two describing the behavior of the method as perceived by callers; this is the higher-level abstraction. The comment must describe each argument and the return value (if any). These comments must be very precise, and must describe any constraints on argument values as well as dependencies between arguments. If the method has any side effects, these must be documented in the interface comment. A side effect is any consequence of the method that affects the future behavior of the system but is not part of the result. For example, if the method adds a value to an internal data structure, which can be retrieved by future method calls, this is a side effect; writing to the file system is also a side effect. A method’s interface comment must describe any exceptions that can emanate from the method. If there are any preconditions that must be satisfied before a method is invoked, these must be described (perhaps some other method must be invoked first; for a binary search method, the list being searched must be sorted). It is a good idea to minimize preconditions, but any that remain must be documented.

**Page: 114**

> Red Flag: Implementation Documentation Contaminates Interface This red flag occurs when interface documentation, such as that for a method, describes implementation details that aren’t needed in order to use the thing being documented.


**Page: 116**

> The main goal of implementation comments is to help readers understand what the code is doing (not how it does it).


**Page: 120**

> If your code is undergoing review and a reviewer tells you that something is not obvious, don’t argue with them; if a reader thinks it’s not obvious, then it’s not obvious. Instead of arguing, try to understand what they found confusing and see if you can clarify that, either with better comments or better code.


**Page: 122**

> When considering a particular name, ask yourself: “If someone sees this name in isolation, without seeing its declaration, its documentation, or any code that uses the name, how closely will they be able to guess what the name refers to? Is there some other name that will paint a clearer picture?”


**Page: 123**

> Names are a form of abstraction: they provide a simplified way of thinking about a more complex underlying entity. Like other forms of abstraction, the best names are those that focus attention on what is most important about the underlying entity while omitting details that are less important.

> The most common problem with names is that they are too generic or vague; as a result, it’s hard for readers to tell what the name refers to;

> The name should provide information about what the result actually is, such as mergedLine or totalChars.

> Red Flag: Vague Name 
> If a variable or method name is broad enough to refer to many different things, then it doesn’t convey much information to the developer and the underlying entity is more likely to be misused.

**Page: 125**

> The process of choosing good names can improve your design by identifying weaknesses.

> If it’s hard to find a simple name for a variable or method that creates a clear image of the underlying object, that’s a hint that the underlying object may not have a clean design.

**Page: 126**

> The second important property of good names is consistency. In any program there are certain variables that are used over and over again.

> Consistency has three requirements: first, always use the common name for the given purpose; second, never use the common name for anything other than the given purpose; third, make sure that the purpose is narrow enough that all variables with the name have the same behavior.


**Page: 128**

> Gerrand makes one comment that I agree with: “The greater the distance between a name’s declaration and its uses, the longer the name should be.” The earlier discussion about using loop variables named i and j is an example of this rule.

> Choosing good names is an example of the investment mindset discussed in Chapter 3: if you take a little extra time up front to select good names, it will be easier for you to work on the code in the future.

**Page: 129**

> documentation. The best time to write comments is at the beginning of the process, as you write the code. Writing the comments first makes documentation part of the design process. Not only does this produce better documentation, but it also produces better designs and it makes the process of writing documentation more enjoyable.

**Page: 130**

> Even if you do have the self-discipline to go back and write the comments (and don’t fool yourself: you probably don’t), the comments won’t be very good. By this time in the process, you have checked out mentally.

> I use a different approach to writing comments, where I write the comments at the very beginning: For a new class, I start by writing the class interface comment. Next, I write interface comments and signatures for the most important public methods, but I leave the method bodies empty. I iterate a bit over these comments until the basic structure feels about right. At this point I write declarations and comments for the most important class instance variables in the class. Finally, I fill in the bodies of the methods, adding implementation comments as needed. While writing method bodies, I usually discover the need for additional methods and instance variables. For each new method I write the interface comment before the body of the method; for instance variables I fill in the comment at the same time that I write the variable declaration.


**Page: 131**

> Comments serve as a canary in the coal mine of complexity. If a method or variable requires a long comment, it is a red flag that you don’t have a good abstraction. Remember from Chapter 4 that classes should be deep: the best classes have very simple interfaces yet implement powerful functions. The best way to judge the complexity of an interface is from the comments that describe it. If the interface comment for a method provides all the information needed to use the method and is also short and simple, that indicates that the method has a simple interface.

> Red Flag: Hard to Describe The comment that describes a method or variable should be simple and yet complete. If you find it difficult to write such a comment, that’s an indicator that there may be a problem with the design of the thing you are describing.

**Page: 132**

> If you are programming strategically, where your main goal is a great design rather than just writing code that works, then writing comments should be fun, since that’s how you identify the best designs.


**Page: 135**

> The tactical approach very quickly leads to a messy system design. If you want to have a system that is easy to maintain and enhance, then “working” isn’t a high enough standard; you have to prioritize design and think strategically. This idea also applies when you are modifying existing code.


**Page: 136**

> If you want to maintain a clean design for a system, you must take a strategic approach when modifying existing code. Ideally, when you have finished with each change, the system will have the structure it would have had if you had designed it from the start with that change in mind.

> Whenever you modify any code, try to find a way to improve the system design at least a little bit in the process. If you’re not making the design better, you are probably making it worse.

> Every development organization should plan to spend a small fraction of its total effort on cleanup and refactoring; this work will pay for itself over the long run.


**Page: 137**

> The best way to ensure that comments get updated is to position them close to the code they describe, so developers will see them when they change the code. The farther a comment is from its associated code, the less likely it is that it will be updated properly.

> When writing implementation comments, don’t put all the comments for an entire method at the top of the method. Spread them out, pushing each comment down to the narrowest scope that includes all of the code referred to by the comment.

**Page: 138**

> When writing a commit message, ask yourself whether developers will need to use that information in the future. If so, then document this information in the code.


**Page: 139**

> If information is already documented someplace outside your program, don’t repeat the documentation inside the program; just reference the external documentation.


**Page: 140**

> One good way to make sure documentation stays up to date is to take a few minutes before committing a change to your revision control system to scan over all the changes for that commit; make sure that each change is properly reflected in the documentation. These pre-commit scans will also detect several other problems, such as accidentally leaving debugging code in the system or failing to fix TODO items.

> One final thought on maintaining documentation: comments are easier to maintain if they are higher-level and more abstract than the code. These comments do not reflect the details of the code, so they will not be affected by minor code changes; only changes in overall behavior will affect these comments.


**Page: 141**

> Consistency is a powerful tool for reducing the complexity of a system and making its behavior more obvious. If a system is consistent, it means that similar things are done in similar ways, and dissimilar things are done in different ways. Consistency creates cognitive leverage: once you have learned how something is done in one place, you can use that knowledge to immediately understand other places that use the same approach. If a system is not implemented in a consistent fashion, developers must learn about each situation separately. This will take more time.

> Consistency allows developers to work more quickly with fewer mistakes.

**Page: 142**

> Interfaces. An interface with multiple implementations is another example of consistency. Once you understand one implementation of the interface, any other implementation becomes easier to understand because you already know the features it will have to provide.

> Invariants. An invariant is a property of a variable or structure that is always true. For example, a data structure storing lines of text might enforce an invariant that each line is terminated by a newline character. Invariants reduce the number of special cases that must be considered in code and make it easier to reason about the code’s behavior.


**Page: 143**

> When in Rome ... The most important convention of all is that every developer should follow the old adage “When in Rome, do as the Romans do.” When working in a new file, look around to see how the existing code is structured. Are all public variables and methods declared before private ones? Are the methods in alphabetical order? Do variables use “camel case,” as in firstServerName, or “snake case,” as in first_server_name? When you see anything that looks like it might possibly be a convention, follow it. When making a design decision, ask yourself if it’s likely that a similar decision was made elsewhere in the project; if so, find an existing example and use the same approach in your new code.


**Page: 143**

> Don’t change existing conventions. Resist the urge to “improve” on existing conventions. Having a “better idea” is not a sufficient excuse to introduce inconsistencies.

**Page: 144**

> Consistency is another example of the investment mindset. It will take a bit of extra work to ensure consistency: work to decide on conventions, work to create automated checkers, work to look for similar situations to mimic in new code, and work in code reviews to educate the team. The return on this investment is that your code will be more obvious. Developers will be able to understand the code’s behavior more quickly and accurately, and this will allow them to work faster, with fewer bugs.


**Page: 145**

> If code is obvious, it means that someone can read the code quickly, without much thought, and their first guesses about the behavior or meaning of the code will be correct. If code is obvious, a reader doesn’t need to spend much time or effort to gather all the information they need to work with the code. If code is not obvious, then a reader must expend a lot of time and energy to understand it. Not only does this reduce their efficiency, but it also increases the likelihood of misunderstanding and bugs. Obvious code needs fewer comments than nonobvious code.

> “Obvious” is in the mind of the reader: it’s easier to notice that someone else’s code is nonobvious than to see problems with your own code. Thus, the best way to determine the obviousness of code is through code reviews. If someone reading your code says it’s not obvious, then it’s not obvious, no matter how clear it may seem to you.


**Page: 148**

> Event-driven programming makes it hard to follow the flow of control. The event handler functions are never invoked directly; they are invoked indirectly by the event module, typically using a function pointer or interface. Even if you find the point of invocation in the event module, it still isn’t possible to tell which specific function will be invoked: this will depend on which handlers were registered at runtime. Because of this, it’s hard to reason about event-driven code or convince yourself that it works. To compensate for this obscurity, use the interface comment for each handler function to indicate when it is invoked, as in this example:

> Red Flag: Nonobvious Code
> If the meaning and behavior of code cannot be understood with a quick reading, it is a red flag. Often this means that there is important information that is not immediately clear to someone reading the code.

**Page: 149**

> Generic containers. Many languages provide generic classes for grouping two or more items into a single object, such as Pair in Java or std::pair in C++. These classes are tempting because they make it easy to pass around several objects with a single variable. One of the most common uses is to return multiple values from a method, as in this Java example: return new Pair<Integer, Boolean>(currentTerm, false); Unfortunately, generic containers result in nonobvious code because the grouped elements have generic names that obscure their meaning. In the example above, the caller must reference the two returned values with result.getKey() and result.getValue(), which give no clue about the actual meaning of the values.

> software should be designed for ease of reading, not ease of writing.

**Page: 150**

> To make code obvious, you must ensure that readers always have the information they need to understand it. You can do this in three ways. The best way is to reduce the amount of information that is needed, using design techniques such as abstraction and eliminating special cases. Second, you can take advantage of information that readers have already acquired in other contexts (for example, by following conventions and conforming to expectations) so readers don’t have to learn new information for your code. Third, you can present the important information to them in the code, using techniques such as good names and strategic comments.

**Page: 152**
 
> Another way of thinking about this is in terms of depth: the more different implementations there are of an interface, the deeper the interface becomes. In order for an interface to have many implementations, it must capture the essential features of all the underlying implementations while steering clear of the details that differ between the implementations; this notion is at the heart of abstraction.

> However, implementation inheritance creates dependencies between the parent class and each of its subclasses. Class instance variables in the parent class are often accessed by both the parent and child classes; this results in information leakage between the classes in the inheritance hierarchy and makes it hard to modify one class in the hierarchy without looking at the others.

> Thus, implementation inheritance should be used with caution. Before using implementation inheritance, consider whether an approach based on composition can provide the same benefits. For instance, it may be possible to use small helper classes to implement the shared functionality. Rather than inheriting functions from a parent, the original classes can each build upon the features of the helper classes.


**Page: 153**

> One of the most important elements of agile development is the notion that development should be incremental and iterative. In the agile approach, a software system is developed in a series of iterations, each of which adds and evaluates a few new features; each iteration includes design, test, and customer input. In general, this is similar to the incremental approach advocated here.


**Page: 154**

> Developing incrementally is generally a good idea, but the increments of development should be abstractions, not features. It’s fine to put off all thoughts about a particular abstraction until it’s needed by a feature. Once you need the abstraction, invest the time to design it cleanly; follow the advice of Chapter 6 and make it somewhat general-purpose.


**Page: 155**

> The problem with test-driven development is that it focuses attention on getting specific features working, rather than finding the best design.

> As mentioned in Section 19.2, the units of development should be abstractions, not features. Once you discover the need for an abstraction, don’t create the abstraction in pieces over time; design it all at once (or at least enough to provide a reasonably comprehensive set of core functions). This is more likely to produce a clean design whose pieces fit together well.


**Page: 156**

> Design patterns represent an alternative to design: rather than designing a new mechanism from scratch, just apply a well-known design pattern. For the most part, this is good: design patterns arose because they solve common problems, and because they are generally agreed to provide clean solutions. If a design pattern works well in a particular situation, it will probably be hard for you to come up with a different approach that is better. The greatest risk with design patterns is over-application. Not every problem can be solved cleanly with an existing design pattern; don’t try to force a problem into a design pattern when a custom approach will be cleaner.

> Using design patterns doesn’t automatically improve a software system; it only does so if the design patterns fit.

> Although it may make sense to use getters and setters if you must expose instance variables, it’s better not to expose instance variables in the first place. Exposed instance variables mean that part of the class’s implementation is visible externally, which violates the idea of information hiding and increases the complexity of the class’s interface.


**Page: 159**

> The best approach is something between these extremes, where you use basic knowledge of performance to choose design alternatives that are “naturally efficient” yet also clean and simple. The key is to develop an awareness of which operations are fundamentally expensive.


**Page: 160**

> The best way to learn which things are expensive is to run micro-benchmarks (small programs that measure the cost of a single operation in isolation).

> Once you have a general sense for what is expensive and what is cheap, you can use that information to choose cheap operations whenever possible.

> If the only way to improve efficiency is by adding complexity, then the choice is more difficult. If the more efficient design adds only a small amount of complexity, and if the complexity is hidden, so it doesn’t affect any interfaces, then it may be worthwhile (but beware: complexity is incremental). If the faster design adds a lot of implementation complexity, or if it results in more complicated interfaces, then it may be better to start off with the simpler approach and optimize later if performance turns out to be a problem.


**Page: 161**

>Before making any changes, measure the system’s existing behavior. This serves two purposes. First, the measurements will identify the places where performance tuning will have the biggest impact. It isn’t sufficient just to measure the top-level system performance. This may tell you that the system is too slow, but it won’t tell you why. You’ll need to measure deeper to identify in detail the factors that contribute to overall performance; the goal is to identify a small number of very specific places where the system is currently spending a lot of time, and where you have ideas for improvement. The second purpose of the measurements is to provide a baseline, so that you can re-measure performance after making your changes to ensure that performance actually improved. If the changes didn’t make a measurable difference in performance, then back them out (unless they made the system simpler). There’s no point in retaining complexity unless it provides a significant speedup.


**Page: 162**

> If you can identify a fundamental fix, then you can implement it using the design techniques discussed in previous chapters.

> The key idea is to design the code around the critical path.

**Page: 163**

> One of the most important things that happens in this process is to remove special cases from the critical path. When code is slow, it’s often because it must handle a variety of situations, and the code gets structured to simplify the handling of all the different cases.