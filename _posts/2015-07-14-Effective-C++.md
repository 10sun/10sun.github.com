---
layout : post
category : LearningNote
tags : [EffectiveC++, C++, Basis]
---
{% include JB/setup %}

**Introduction**

A short review of the terminology, the C++ vocabulary:
- *signature*: the parameters and return types of a function, revealed by each function's declaration.
- *explicit*: constructors declared explicit are usually preferable to non-explicit ones, because they prevent compilers from performing unexpected type conversions.

**Chapter 1**

- *Item 1*: view C++ as a federation of languages  
    + the primary sublanguages of C++:
        * C. C++ is still based on C deep down.
        * Object-Oriented: classes, encapsulation, inheritance, polymorphism, virtual functions (dynamic binding), etc.
        * Template C++: the generic programming part of C++.
        * The STL: standard template library.
- *Item 2*: prefer consts, enums, and inlines to #defines. This can be called "prefer compiler to preprocessor" as well.
    + *#define* doesn't respect scope. Once a macro is defined, it's in force for the rest of the compilation.
    + When replacing #define with constant, two special cases are worth mentioning:
        * Defining cosntant pointers.
        * To limit the scope of a constant to a class, make it a memer. To ensure there's at most one copy of the constant, make it a *static* member.
    + When you need the value of a class constant during compilation of the class, use "*the enum hack*". It takes the advantage of the fact that the values of an enumerated type can be used where ints are expected.
    + *For simple constants, prefer const objects or enums to #defines*.
    + *For function-like macros, prefer inline functions to #defines*.

<!--more-->

- *Item 3*: use *const* whenever possible.
    + The purpose of *const* om member functions is to identify which member functions may be invoked on *const* objects.
        * 1. Make the interface of a class easier to understand which functions may modify an object and which may not. 
        * 2. Make it possible to work with *const* objects.
    + Declearing something *const* helps compilers detect usage errors.
    + Compilers enforce bitwise constness, but you should program using conceptual constness.
    + When *const* and *non-const* member functions have essentially identical implementations, code duplication can be avoided by having the *non-const* version call the *const* version.
- *Item 4*: make sure that objects are initialized before they are used.
    + Always initialize the object before using it.
        * Make sure that all constructors initialize everything in the object.
        * The order in which an object's data is initialized is not fickle: base classes are initialized before derived classes, and within a class, data members are initialized in the order in which they are declared.
        * A translation unit is the source code giving rise to a single object file.
        * The relative order of initialization of non-local static objects defined in different translation units is undefined.
    + Manually initialize objects of built-in type.
    + Prefer use of the member initialization list to assignment inside the body of the constructor. List data members in the initialization list in the same order they are declared in the class.
    + Avoid initialization order problems across translation units by replacing non-local static objects with local static objects.

**Chapter 2**

- *Item 5*: Compilers may implicitly generate a class's default constructor, copy constructor, copy assignment operator, and destructor.
    + If you want to support assignment in a class containing a reference member, you must define the copy assignment operator yourself.
- *Item 6*: To disallow functionality automatically provided by compilers, declare the corresponding member functions *private* and give no implementations. Using a base class like *uncopyable* is one way to do this.
- *Item 7*: Declare virtual destructors in polymorphic base classes.
    + If a class has any virtual functions, it should have a virtual destructor.
    + Classes not designed to be base classes or not designed to be used polymorphically should not declare virtual destructors.
- *Item 8*: Destructors should never emit exceptions.
    + If functions called in a destructor may throw, the destructor should catch any exceptions, then swallow them or terminate the program.
- *Item 9*: Don't call virtual functions during construction or destruction, since such calls will never go to a more derived class than that of the currently executing constructor or destructor.
- *Item 10*: Assignment operators should return a reference to its left-hand argument. 
    + While defining your own assignment operators, the last line code should always be ''' return *this'''.
- *Item 11*: Make sure *operator=* is well-behaved when an object is assigned to itself.
    + Self-assignment problem is the result of aliasing: having more than one way to refer to an object.
    + The traditional way to prevent this error is to check for assignment to self via an identity test at the top of *operator=:*.
    + Techniques include: comparing address of source and target objects, careful statement ordering, and copy-and-swap.
- *Item 12*: Copying functions should be sure to copy all of an object's data members and all of its base class parts (invoke appropriate base class copy assignment operators).
    + Don't try to implement one of the copying functions in terms of the other. Put common functionality in a third function that both call.

**Chapter 3**

- *Item 13*: A resource is something that once you are done using it, you need to return to the system. 
    + To prevent resource leaks, use Resource Acquisition Is Initialization (RAII) objects that acquire resources in their constructors and release them in their destructors.
    + Two commonly useful RAII classes: *tr1::shared_ptr*, and *auto_ptr*/*unique_ptr*. *tr1::shared_ptr* is usually the better choice. Copying an *auto_ptr* sets it to null.
- *Item 14*: Copying an RAII object entails copying the resource it manages. So the copying behavior of the resource determines the copying behavior of the RAII object.
    + Common RAII class copying behaviors are disallowing copying and performing reference counting, but other behaviors are possible.
- *Item 15*: API often require access to raw resources, so each RAII class should offer a way to get at the resource it manages.
    + There are two ways: explicit conversion (much safer) or implicit conversion (more convenient but also more error proned).
- *Item 16*: Use the same form in corresponding uses of *new* and *delete*.
    + This item is arisen by a simple question: does the pointer being deleted point to a single object or to an array of objects?
    + Using brackets in the use of *delete*, *delete* assumes an array is pointed to. Otherwise, it assumes that a single object is pointed to.
    + Simple rule: if you use [] in a new expression, you must use [] in the corresponding *delete* expression. If you don't use [] in a new expression, don't use [] in the matching *delete* expression.
- *Item 17*: Store *new*-defined objects in smart pointers in standalone statements. Failure to do so may lead to subtle resource leaks when exceptions are thrown.

**Chapter 4**

- *Item 18*: Make interfaces easy to use correctly and hard to use incorrectly.
    + Ways to facilitate correct use: consistency in interfaces and behavioral compatibility with built-in types.
    + Ways to prevent errors: creating new types, restricting operations on types, constraining object values, and eliminating client resource management responsibilities.
    + *tr1::shared_prt* supports custom deleters. This prevents the cross-DLL problem.
- *Item 19*: Treat class design as type design.
- *Item 20*: Prefer pass-by-reference-to-const to pass-by-value.
    + HOWEVER, for built-in types and STL iterator and function object types, pass-by-value is usually appropriate.
- *Item 21*: Don't try to return a reference when you must return an object.
    + Never return a pointer or reference to a local stack object.
    + Never return a pointer or reference to a heap-allocated object.
    + Never return a pointer or reference to a local static object if there is a chance that more than one such object will be needed.
- *Item 22*: Declare data members private. Data members should be private.
    + *protected* is no more encapsulated than *public*.
- *Item 23*: Prefer non-member, non-friend functions to member functions
    + Object-oriented principles dictate that *data should be as encapsulated as possible*. Because encapsulation should be put in the first place: encapsulation afords us the flexibility to change things in a way that affects only a limited number of clients.
    + The reason for doing so is to increase encapsulation, packaging flexibility, and functional extensibility.
- *Item 24*: Declare non-member functions when type conversions should apply to all parameters.
    + Provide a *swap* member function when *std::swap* would be inefficient for your type. Make sure your *swap* doesn't throw exceptions.
    + If you offer a member *swap*, also offer a non-member *swap* that calls the member. For classes, specialize *std::swap* too.
    + When calling *swap*, employ a *using* declaration for *std::swap*, then call *swap* without namespace qualification.
    + Never try to add something completely new to *std*.

**Chapter 5**

- *Item 26*: Postpone variable definitions as long as possible.
    + When defining a variable of a type with a constructor and destructor, there is a cost associated with unused variables, so you want to avoid them whenever you can.
    + Not only should you postpone a variable's definition until right before you have to use the variable, you should also try to postpone the definition until you have initialization arguments for it.
    + It increases program clarity and improves program efficiency.
- *Item 27*: Minimize casting.
    + C++ offers 4 new cast forms:
        * *const_cast*: used to cast away the constness of objects.
        * *dynamic_cast*: used to perform "safe downcasting". i.e. to determine whether an object is of a particular type in an inheritance hierarchy.
        * *reinterpret_cast*: intended for low-level casts that yield implementation-dependent results.
        * *static_cast*: used to force implicit conversions.
    + Avoid casts whenever practical, especially *dynamic_casts* in performance-sensitive code.
    + When casting is necessary, try to hide it inside a function.
    + Prefer C++ style casts to old-style casts.
- *Item 28*: Avoid returning *handles* to object internals.
    + References, pointers, and iterators are all *handles* (ways to get at other objects).
    + Returning a handle to an object's internals always runs the risk of compromising an object's encapsulation.
    + Avoid returning *handles* to object internals increases encapsulation, helps *const* member functions act *const*, and minimizes the creation of dangling handles.
- *Item 29*: Strive for exception-safe code.
    + Exception-safe functions leak no resources and allow no data structures to become corrupted, even when exceptions are thrown.
    + Three types of guarantees offered by exception-safe functions
        * Basic guarantee: if an exception is thrown, everything in the program remains in a valid state.
        * Strong guarantee: if an exception is thrown, the state of the program is unchanged.
        * Nothrow guarantee: never to throw exceptions.
    + One principle strategy for the strong guarantee is the "copy and swap" strategy.It is an excellent way to make all-or-nothing changes to an object's state. However it doesn't guarantee that the overall function is strongly exception-safe.
    + A function can usually offer a guarantee no stronger than the weakest guarantee of the functions it calls.
- *Item 30*: Understand the ins and outs of inlining.
    + The idea behind an inline function is to replace each call of the function with its code body.
    + *inline* is a request to compilers, not a command. This request can be given implicitly or explicitly.
        * The implicit way is to define a function insed a class definition.
        * The explicit way is to precede a function's definition with the  *inline* keyword.
    + calls to virtual functions defy inlining.
    + limit most inlining to small, frequently called functions.
    + don't declare function template *inline* just because they appear in header files.
- *Item 31*: minimize compilation dependencies between files.
    + The key to the separation of interface and implementation is the replacement of dependencies on *definitions* with dependencies on *declarations*.
    + Two approaches based on the idea are Handle classes and Interface classes.
    + Avoid using objects when object references and pointers will do.
    + Depend on class declarations instead of class definitions whenever you can.
    + Provide separate header files for declarations and definitions.
    + Library header files should exist in full and declaration-only forms.

**Chapter 6**

- *Item 32*: Make sure public inheritance models *is-a*.
    + Public inheritance means "is-a". Everything that applies to base classes must also apply to derived classes, because every derived class object is a base class object.
- *Item 33*: Avoid hiding inherited names.
    + Names in derived classes hide names in base classes. Under public inheritance, this is never desirable.
    + To make hidden names visible again, employ *using* declarations or forwarding functions.
- *Item 34*: Differentiate between inheritance of interface and inheritance of implementation.
    + The purpose of declaring a *pure virtual* function is to have derived classes inherit a function *interface only*.
    + The purpose of declaring a *simple virtual* function is to have derived classes inherit a *function interface as well as a default implementation*.
    + The purpose of declaring a *non-virtual* function is to have derived classes inherit a function interface as well as a mandatory implementation.
- *Item 35*: consider alternatives to virtual functions.
    + *non-virtual interface (NVI) idiom*: it is the basic design, which has clients call private virtual functions indirectly through public non-virtual member functions.
    + Several alternatives to virtual functions:
        * The template method pattern via the Non-Virtual Interface idiom.
        * Replace virtual functions with function pointer data members, a stripped-down manifestation of the Strategy design pattern.
        * The strategy pattern via *tr1::function*. Allow you use of any callable entity with a signature compatible with what you need.
        * Replace virtual functions in one hierarchy with virtual functions in another hierarchy. This is the conventional implementation of the Strategy design pattern.
    + A disadvantage of moving functionality from a member function to a function outside the class is that the non-member function lacks access to the class's non-public members.
    + *tr1::function* objects act like generalized function pointers. Such objects support all callable entities compatible with a given target signature.
- *Item 36*: Never redefine an inherited non-virtual function.
- *Item 37*: Never redefine a function's inherited default parameter value.
    + Static binding is also called early binding, while dynamic binding is called late binding.
    + Default parameter values are statically bound, while virtual functions, the only functions you should be overridding, are dynamically bound.
- *Item 38*: *Composition* is the relationship between types that arises when objects of one type contain objects of another type. It is also called *layering*, *containment*, *aggregation*, and *embedding*.
    + Composition means either *has-a*, or *is-implemented-in-terms-of*.    
    + In the application domain, composition means has-a. In the implementation domain, it means is-implemented-in-terms-of.
- *Item 39*: Use private inheritance judiciously.
    + Private inheritance means is-implemented-in-terms of. It is usually inferior to composition. 
    + Private inheritance can enable the empty base optimization.
    + Private inheritance means that the implementation only should be inherited, but the interfaces should be ignored. It is just a technique.
- *Item 40*: Use multiple inheritance judiciously.
    + Multiple inheritance is more complex than single inheritance. It can lead to new ambiguity issues, and to the need for virtual inheritance.
    + Virtual inheritance imposes in size, speed, and complexity of initialization and assignment. It's most practical when virtual bases have no data.
    + Multiple inheritance has legitimite uses. One scenario involves combining public inheritance from an inteerface class iwht private inheritance from a class that helps with implementation.


**Chapter 7**

Generic programming: the ability to write code that is independent of the types of objects being manipulated.

- *Item 41*: Understand implicit interfaces and compile-time polymorphism.
    + Both classes and templates support interfaces and polymorphism.
    + For classes, interfaces are explicit and centered on function signatures. Polymorphism occurs at runtime through virtual functions.
    + For template parameters, interfaces are implicit and based on valid expressions. Polymorphism occurs during compilation through template instantiation and function overloading resolution.
- *Item 42*: Understand the two meanings of typename.
    + *dependent names*: names in a template that are dependent on a template parameter are called dependent names. When a dependent name is nested inside a class, it is called *nested dependent name*.
    + Anytime you refer to a nested dependent type name in a template, you must immediately precede it by the word *typename*.
    + When declaring template parameters, *class* and *typename* are interchangeable.
    + Use *typename* to identify nested dependent type names, except in base class lists or as a base class identifier in a member initialization list.
- *Item 43*: Know how to access names in templatized base classes.
    + In derived class templates, refer to names in base class templates via a *this->* prefix, via *using* declarations, or via an explicit base class qualification.
- *Item 44*: Factor parameter-independent code out of templates.
    + Template generates multiple classes and 
- *Item 45*:
- *Item 46*:
- *Item 47*: Use *traites* classes for information about types.
    + *traits* allow you to get information about a type during compilation. They are implemented using templates and template specializations.
    + How to use a traits class:
        * Create a set of overloaded worker functions or function templates, that differ in a traits parameter. Implement each function in accord with the traits information passed.
        * Create a "master" function or function template that calls the workers, passing information provided by a trait class.
- *Item 48*: Be aware of template metaprogramming.
    + *Template metaprogramming (TMP)* is the process of writing template based C++ programs that execute during compilation.
    + TMP has two great strengths: 1. it makes some things easy that would otherwise be hard or impossible. 2. they shift work from runtime to compile-time.
    + TMP enables earlier error detection and higher runtime performance.
    + TMP can be used to generate custom code based on combinations of policy choices and it can also be used to avoid generating code inappropriate for particular types.

**Chapter 8**

- *Item 49*: Understand the behavior of the new-handler.
    + *set_new_handler* allows you to specify a function to be called when memory allocation requests cannot be satisfied.
    + *curiously recurring template pattern (CRTP)*
    + Nothrow *new* is of limited utility, because it applies only to memory allocation; subsequent constructor calls may still throw exceptions.
- *Item 50*: Understand when it makes sense to replace new and delete.
    + Three of the most common reasons to replace compiler-provided versions of *operater new* or *operator delete*.
        * To detect usage errors.
        * To improve efficiency.
        * To collect usage statistics.
    + Some other reasons:
        * To increase the speed of allocation and deallocation.
        * To reduce the space overhead of default memory management.
        * To compensate for suboptimal alignment in the default allocator.
        * To cluster related objects near one another.
        * To obtain unconventional behavior.
- *Item 51*: Adhere to convention when writing *new* and *delete*.
    + *operator new* should contain the following:
        * an infinite loop trying to allocate memory.
        * it should call the new-handler if it can't satisfy a memory request.
        * it should handle requests for zero bytes.
        * class specific versions should handle requests for larger blocks than expected.
    + *operator delete* should do nothing if passed a pointer that is null. Class specific versions should handle blocks that are larger than expected.
- *Item 52*: Write placement *delete* if you write placement *new*.
    + When an *operator new* function takes extra parameters (other than the mandatory *size_t* argument), that function is known as *placement version of new*.
    + If an *operator new* with extra parameters isn't matched by an *operator delete* with the same extra parameters, no *operator delete* will be called if a memory allocation by the *new* needs to be undone.
    + Placement *delete* is only called if an exception arises from a constructor call that's coupled to a placement *new*.
    + Applying *delete* to a pointer never yields to a placement version of *delete*.
    + When you write a placement version of *operator new*, be sure to write the corresponding placement version of *operator delete*.
    + When you declare placement versions of *new* and *delete*, be sure not to unintentionally hide the normal versions of those functions.

**Chapter 9**

- *Item 53*: Pay attention to compiler warnings.
    + Take compiler warnings seriously, and strive to compile warning-free at the maximum warning level supported by your compilers.
    + Don't become dependent on compiler warnings.
- *Item 54*: Familiarize yourself with the standard library, including TR1.
    + The major parts of the standard C++ libraries specified by C++98:
        * The *Standard Template Library (STL)*: containers, iterators, algorithms, function objects, and various container and function object adapters.
        * *Iostreams*.
        * Support for *internationalization*.
        * Support for *numeric processing*: templates for complex numbers (*complex*) and arrays of pure values (*valarray*).
        * An *exception hierarchy*: the base class *exception*, its derived classes *logic_error* and *runtime_error*, and other classes derived from these two.
        * *C89's standard library*.
    + TR1 (technical release 1) specifies 14 new components. All are in the namespace *std::tr1::*.
        * the *Smart pointers*: *tr1::shared_ptr* and *tr1::weak_ptr*.
        * *tr1::function*: it makes it possible to represent any callable entity whose signature is consistent with a target signature.
        * *tr1::bind*: a second generation binding facility.
        * *Hash tables*: it is used to implement sets, multisets, maps and multimaps.
        * *Regular expressions*.
        * *Tuples*: a nifty generalization of the pair template that's already in the standard library.
        * *tr1::array*. The site of a *tr1::array* is fixed during compilation and the object uses no dynamic memory.
        * *tr1::mem_fn*: a syntactically uniform way of adapting member function pointers.
        * *tr1::reference_wrapper*: a facility to make references act a bit more like objects. It makes it possible to create containers that act as if they hold references.
        * *Random number generation*.
        * *Mathematical special functions*: Laguerre polynomials, Bessel functions, complete elliptic integrals, and many more.
        * *C99 compatibility extensions*.
        * *Type traits*: a set of traits classes to provide compile-time information about types.
        * *tr1::result_of*: a template to deduce the return types of function calls.
- *Item 55*: Familiarize yourself with Boost.
    + Boost is a community and website for the development of free, open source, peer-reviewed C++ libraries. 
    + Boost offers implementations of many TR1 components, but it also offers many other libraries too.
        * *string and text processing*, *containers*, *function objects and higher-order programming*, *generic programming*, *template metaprogramming (TMP)*, *math and numerics*, *correctness and testing*, *data structures*, *inter-language support*, *memory*, and *miscellaneous*.