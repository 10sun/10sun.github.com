---
layout : post
category : LearningNote
tags : [C++Primer, Basis]
---
{% include JB/setup %}

**Chapter 2: Variables and Basic Types**


- Primitive Built-in Types
    + Integral Types: arithmetic types representing integers, characters and boolean values.
        * a byte = 8 bits, a word = 4 bytes = 32 bits.
        * when the assigned value exceeds the range which a data type can hold, the compiler will let the assigned value modulo the max range value.
    + Floating-point Types: *float (32 bits), double (64 bits), long double (96 or 128 bits)*
- Literal Constants: 
    + Literal: we can only speak of it in terms of its value
    + Constant: it cannot be changed.
    + 3 ways of notations for *integral literals*: decimal, octal, or hexadecimal.
        * Suffix: by adding a suffix, we can force the type of a literal integer constant to be type *long (L)* or *unsigned (u)* or *unsigned long (UL)*.
    + *floating-point literals*: 2 ways of notations: decimal (L), or scientific (E, or e).
    + *Boolean and Character Literals*:
        * boolean: true, or false
        * character: '' + character.
    
| signed | unsigned | boolean | 
|--------|:---------:|--------:|
|both postive and negative numbers | only valus greater than 0 | true or false |
| sign bit = 1, value < 0 | | |
| sign bit = 0, value >= 0| | |

<!--more-->

- constructor:
    + default constructor: constructor with no arguments, usually called when there is no specific initializer available.


**Chapter 3: Library Types**

- Library *string* type
    + *string* supports variable-length character strings
    + common ways to initialize a string
    
    ```c++
    std::string s1;              // Default constructor; s1 is the empty string
    std::string s2(s1);          // initialize s2 as a copy of s1
    std::string s3("value");     // initialize s3 as a copy of the string literal
    std::string s4(n, "c");      // initialize s4 with n copies of the character 'c'
    ```

    + reading and writing of *string*('>>' & '<<') always discard the whitespace(space).
    + '*getline*' reads the entire line, but discard the newline sign('\n').
    + operations defined for *string*
    + when mixing strings and string literals, at least one operand to each '+' operator must be of *string* type
    
    ``` c++
    string.empty()          // returns true if string is empty; otherwise false.
    string.size()           // returns number of characters in the string
    string[n]               // access the n+1 th element in the string. string index starts from 0 to string.size()-1
    s1 + s2                 // concatenats s1 and s2
    s1 = s2                 // replace characters in s1 by a copy of s2
    s1 == s2                // returns trun if v1 and v2 are equal, otherwise false
    !=, <, <=, >, >=        // comparison between strings
    ```

**Chapter 4: Arrays and Pointers**

- Array
    + *initialization*
    + *operation*

- Pointer
    + *pointer* is a compound type, pointing to an object of some other type. It offers indirect access to the object to which it points.
    + It can point to an object, instead of a single element in an array.
    + "*" is the pointer operator, "&" is the *address-of* operator.
    + 4 way to initialize/assign:
        * constant expression with value 0
        * address of an object of an appropriate type
        * address on past the end of another object
        * another valid pointer of the same type
    + *Difference between Pointers and References*
        * Reference is another name (alias) to the object, however pointer is just an indirective access of the object. 
        * Once initialized, reference is fixed to one object. However, reference can be changed to different addresses of different objects.
    + When you define a const object, you must initialize the const object. However, the const pointer doesn't have to be initialized.

- C-Style character strings
    + strcpy: copy entire strings
    + strncpy: copy an assigned number of strings

**Chapter 5: Expressions**

- Definitions:
    + *Expression* is composed of one or more operands that are combined by operators. 
    + *unary* and *binary* operators. 
        * unary operators have the highest precedence.
    + *overflow*: a situation whereby the calculated result size exceeds that which can be defined by the data type.
    + *relational and logical* operators return values of *bool*.
        * *logical* operator treats the operands as conditions. If the value is 0, then the result of logical operator is *false*. Otherwise, it is *true*.
        * *short circuite evaluation*: evalute the left operands first. If the left operands can not determine the condition, it will evaluate the rest operands.
    + *Bitwise* operators: take operands of integral type. These operators treat their operands as a collection of bits, providing operations to test and set individual bit.
        * it is strongly recommended to use *unsigned int* while using bitwise operators.
        * *bitset* operations are more direct, easier to read, easier to write and more likely to be used correctly.
        * *I/O operators '>>' & '<<'* are left associative.
        * *shift operators '>>' & '<<'* have middel-level precedence. LOWER that *arithmetic* operators, but HIGHER than *relational, assignment, conditional* operators.
    + *assignment* operators: left-hand operands of assignment operators must be *nonconst* lvalues.
        * assignment operator is right-associative.
        * compound operators: *a op= b* is essentially equal to *a = a op b*. The left-hand operand is only evaluated once.
    + *incremental '++' & decremental '--'* operators: they provide a shorthand for adding or subtracting 1 from an object.
        * *prefix operators* yield a *changed result/value* and also a *changed operand*.
        * *postfix operators* yield an *unchanged result/value* but *changed operand*.
        * mostly, we use prefix operators.
        * *postfix operators* have higher precedence than *dereference '*'* operator.
    + *Arrow '->'* operator: 
        (*p).foo  // dereference p to get an object, and then fetch its member named foo.
        p->foo    // equavilant way to fetch the foo from the object to which p points.
    + *conditional operator*: the only ternary operator in c++.
        cond ? expression1 (true) : expression2 (false);
    + *sizeof* operator: returns the size of defined data type in bytes.
    + When in doubt, parenthesize expressions to force the grouping that the logic of your program requires.
    + If you change the value of an operand, don't use that operand elsewhere in the same statement.

**Chapter 6: Statements**

- Definitions:
    + Null statement: empty statement ends with a semicolon. It is useful when the language requires a statement but the programmer's logic doesn't.
    + Block: a compound statement, a sequence of statements surrounded by a pair of curly braces. A block is a scope.

- Notes:
    + dangling else problem: it occurs when a statement contains more if clauses than else clauses. It can be resolved by *matching the else with the last occuring unmatached if*.
    + *switch*: a deeply nested *if ... else ...*. 
        * It is usually to end the case label statement with "break", except the following case: you want to excute the same statement under multiple cases.
        * It is also necessary to always add *"default"* case label at the end of the switch block.
        * always **constant** for the case labels, **no variables** for the case labels.
    + *while*: expression in *while(condition)* will be converted into bool after being executed.
        * a *return* or *break* can help avoiding the endless loop.
    + *for*: it is a must to initialize the condition variable.
    + *do while*: 
        * The statement block *do* will firstly be executed, then the condition in *while* will be evaluated.
        * it ends with an *semicolon ;* at the end, after *while*.
        * it is not allowed to declare a new variable in the *while(condition)*.
    + *try catch*
    + *preprocessor*: *-D* is the compile flage for preprocessor information.


**Chapter 7: Functions**

- Definitions:
    + *Function*: Functions are named units of computation and are essential to structuring even modest programs. it is a programmer-defined operation. It is represented by a name and a set of operand types. 
        * The operands, *parameters*, are specified in a *comma-separated* list enclosed in parentheses.
        * *function body*: Actions that the function performs, specified in a block.
        * *return type*: every function has an associated return type.
    + *call operator*: a pair of parentheses.
    + *arguments*: the value used to initialize a parameter is the corresponding argument passed in the call. They might be variables, literal constants, or expressions.
    + *recursive function*: function that calls itself directly or indirectly.

- Notes:
    + a variable local to a function may not use the same name as the name of any of the function's parameters.
    + *Nonreference parameters* are the local *copies* of the corresponding argument. Changes are made to the local copy. Once the function terminates, the local values are gone. 
    + *Reference parameters* refer directly to the objects to which they are bound rather than to copies of those objects. It directly works on the variables instead of the local copies.
        * In C++, it is safer and more natural to use reference parameters.
        * When the only reason to make a parameter a reference is to avoid copying the argument, the parameter should be *const* reference.
    + *Vector parameters*: in practice, C++ program tend to pass containers by passing iterators to the elements we want to pass.
    + *Array parameters*: 
        * for nonreference parameter: when we pass the array, the argument is a pointer to the first element in the array.
        * for reference parameter: the compiler passes the reference to the array itself. The array size is part of the parameter and argument types.
    + *Return*: return statement terminates the functin that is currently executing and returns control to the functin that called the now-terminated function.
        * *void*: no return values.
        * return a value: the type of returned value should be declared in the function declaaration.
        * *NEVER return a reference to a local variable*. 
        * *NEVER return a pointer to a local object*.
        * a *recursive* function must always define a stopping condition. (ex 7.20)
    + Function prototype: return type, function name, and parameter list.
        * function declarations go in header files.
        * default argument: the value that is expected to be used most of the time.
        * While using a function, if some of the parameters already have default values, arguments for them are not needed.
        * A parameter can have its default argument specified only once in a file.
        * Default arguments ordinarily should be specified with the declaration for the function and placed in an appropriate header.
        * Parameters with default arguments should be *behind* the parameters without default arguments.
    + The *Scope* of a name is the part of the program's text in which that name is known.
    + The *lifetime* of an object is the time during the program's execution that the object exists.
    + *automatic objects*: only exist while a function is executing. They are created and destroyed on each call to a function.
    + *static local objects*: guaranteed to be initialized no later than the first time that program execution passes through the object's definition.
        * local *statics* will not be destroyed when the function ends.
        * local *statics* continue to exist and hold their values across calls to the function.
    + *Inline Function*: optimize small, straight-line functions that are called frequently.
        * *inline* is only a request to the compiler. The compiler may choose to ignore the request.
        * When calling a function is slower than evaluating the equivalent expression, we use *inline*.
        * *inline functions* should be *defined* in *header* files.
        * whenever an *inline* function is added or changed in the header file, every source file that uses the header file must be recompiled.
    + *Class Member Functions*:
        * function prototype must be defined within the class body, while the body of the function may be defined within the class itself, or outside the class body.
        * A member function that is defined inside the class is implicitly treated as an *inline* function.
        * A member function may access the private members of its class.
        * *this*: implicit parameter for each member function.
            - When a member function is called, the *this* parameter is initialized with the address of the object on which the function was invoked.
            - *const member functions*: *const* modifies the type of the implicit *this* parameter. *this* will return a *const* object.
        * Member functions defined outside the class definition must indicate that they are members of the class *class::member_function*.
        * *constructor*: data members are initialized through the constructor.
            - constructor is a special member function that is distinguished from other member funtions by having the same name as its class. It has no return type.
            - *default constructor*: takes no arguments. It says what happens when we define an object but do not supply an explicit initializer.
            - *constructor initializer list*: the colon and the following text up to the open curly is the constructor initializer list. It specifies the initial values for one or more data members of the class. They are separated by **commas**.
            - *explicit*: a keyword to prevent implicit conversion. *explicit* is only for constructor! Prefixing the *explicit* keyword to the constructor prevents the comipler from using that constructor for implicit conversions.
    + *Overloaded Functions*: two functions in the same scope are overloaded if they have the same name but different parameter lists.
        * Functions cannot be overloaded based only on differences in the return type.
        * declarations for every version of an overloaded function must appear in the same scope.
        * In C++, name lookup happens before type checking.
        * Function *overload resolution*: a function call is associated with a specific function from a set of overloaded functions.
        * For nonreference parameters, *const* and non-const are the same parameters. It's illegal to add *const* in front of the params to overload the function.
        * *Three Steps in Overload Resolution*
            - *Candidate Functions*: identify the set of overloaded functions considered for the call. The functions in this set are called candidate functions.
            - *Determining the viable functions*: Select the functions from the set of candidate functions that can be called with the arguments specified in the call. These selected functions are called *viable functions*.
                + The same number of parameters
                + The type of each argument must match or be convertible to the type of its corresponding parameter.
            - *Finding the best match, if any*: The closer the types of the arguments and parameter are to each other, the better the match.
                + The rank for conversions:
                    * Exact match
                    * Match through a promotion
                    * Match through a standard conversion
                    * Match through a class-type conversion
        * When using overloaded functions with *enum* parameters: Two enumeration types may behave quite differently during function overload resolution, depending on the value of their enumeration constants.
        * Whether a parameter is *const* only matters when the parameter is a reference or pointer.
    + *Pointers to Functions*: a function pointer is a pointer that denotes a unction rather than an object.
        * A function's type is determined by its *return type* and its *parameter list*.
        * use *Typedefs* to simplify function pointer definitions.
        * initializing a function pointer to zero indicates that the pointer does not point to any function.
        * Only pointers that have been initialized or assigned to refer to a function can be safely used to call a function.
        * A function parameter can be a function pointer.
        * A function can return a pointer to function. 
   
**Chapter 8: The IO Library**

- Definitions:
    + *base class*: a class that is the parent of another class. The base class defines the interface that a derived class inherits.
    + *derived class*: a class that shares the interface with its parent class.
    + *condition states*: A set of condition state members that indicate whether a given IO object is in a usable state, or has encountered a particular kind of error.
- Notes:
    + The standard IO types are defined in three separate headers:
        * *iostream*: the types used to read and write to a console.
        * *fstream*: the types used to read and write named files.
        * *sstream*: the types used to read and write in-memory strings.
        * each type of *fstream* and *sstream* is derived from a corresponding type defined in the *iostream* header.
        * Because of the inheritance, we can pass an object of a derived type to that function, which takes a reference to a base-class type.
        * No copy of Assign for IO objects.
        * If we need to pass or return an IO object, it must be passed or returned as a pointer or reference.
    + To assure that the stream is loaded successfully, use *if* or *while* to test the state of the stream.
    + Each IO stream objects contains a condition state member that is managed through the *setstate* and *clear* operations. (*ex 8.3 & 8.4*)
        * *badbit*: a system level failure. Not possible to continue using a stream after such an error.
        * *failbit*: set after a recoverable error. 
        * *eofbit*: set when an end-of-file is encountered-
        * The state of the stream is revealed by the *bad*, *fail*, *eof* and *good* operations.
        * *clear*: put the stream back in its valid state. Called after we have remedied whatever problem occurred, and we want to set the stream to valid state.
        * *setstate*: turns on the specified condition to indicate that a problem occurred. It leaves existing state variables unchanged except that it adds the additional indicated state(s).
        * *rdstate*: returns an *iostate* value that corresponds to the entire current condition state of the stream.
    + Managing a buffer:
        * conditions causing the buffer flushed:
            - program completes normally.
            - at some indeterminate time, the buffer becomes full, in which case it will be flushed before writing to the next value.
            - using a manipulator: *endl*. It writes a newline and flushes the buffer.
            - use *unitbuf* manipulator to set the stream's internal state to empty the buffer after each output operation. Empty every output.
            - *tie* the output stream to an input stream. The output buffer is flushed whenever the associated input stream is read. *The library ties cout to cin*.
                + To break existing tie,  we pass in an argument of 0. (cin.tie(0)).
        * Buffers are not flushed if the program crashes. Thus we should use *endl* when writing output.
    + File Input and Output:
        * Supplying a file name as an initializer to an *ifstream* or *ofstream* object has the effect of opening the specified file.
        * If defining a stream object without a specified name, we need to use the call function of the stream object to bind the stream to a file specified by the filename.
        * Standard IO library uses *C-style* character strings rather than C++ strings to refer to file names. We can use *c_str* member of *string* class to obtain a C-style string.
        * *close* a file stream before associate it with a different file.
        * If we reuse a file stream to read or write more than one file, we must *clear* the stream before using it to read from another file.
        * File modes: integral constants to set one or more modes when we open a given file.
            - *out, trunc, app* only for *ofstream* or *fstream*
            - *in* only for *ifstream* or *fstream*
            - *ate, binary* can be used for both: *ate* only affects at the opening of the file; *binary* mode processes the file as a sequence of bytes.
            - *fstream* can both read and write its associated file.
    + String streams
        * *istringstream, ostringstream, stringstream*
        * *sstream* must be included. 

**Chapter 9 Sequential Containers**

- Definitions:
    + *Container*: a template type that holds a collection of objects of a specified type.
    + *adaptors*: container adaptor adapts an underlying container type by defining a new interface in terms of the operations provided by the original type. *stack*, *queue* and *priority_queue*.
    + *sequantial container*: a type that holds an *ordered* collection of objects of a single type. Elements in a sequential container are accessed by position.
    + *iterator*: a type whose operations support navigating among the elements of a container and examining values in the container.
    + *iterator range*: denoted by a pair of iterators that refer to two elements, or to one past the last element, in the same container.
    + *Adaptor*: adaptor is a general concept in the library.Essentially, an adaptor is a mechanism for making one thing act like another.

- Notes:
    + 3 types of *sequential containers*: vector, list and deque.
    + Most commonly used container constructor is the default constructor, which provides the best run-time performance and easier access.
    + 3 ways to initialize a sequential container:
        * Initialize a container as a copy of another container
        * initialize as a copy of a range of elements
        * allocate and initialize a specified number of elements (*only valid for sequential container, not for associative container*)
    + **It is always necessary to check the validity of the iterator or the iterator range.**
    + *vector* & *deque* allow random access to their elements by iterator/position, therefore it is possible to perform relational operators and arithmetic.
        * *capacity*: how many it could hold before new space must be allocated.
        * *size*: the number of elements in the vector.
    + *begin* & *end* refer to the first and one-past-the-end in the container respectively.
    + all sequential containers support "*push_back( )*" to add element at the end of current containers. However, *list* and *deque* also support "*push_front( )*".
    + Container elements are **copies**. Read/write on them have no effect on the values from which are copied.
    + Don't cache the iterator returned from *end*. Inserting or deleting elements in a deque or vector will invalidate the cached iterator.
    + *front( )* & *back( )* return reference to the first and last element in the container respectively, instead of iterator to these elements.
    + *pop_front* & *pop_back* remove the first and last elements in the container respectively.
    + Generally speaking, unless there is a good reason to prefer another container, *vector* is usually the right one to use.
    + Rules of thumb for selecting approriate container to use:
        * Random access to elements: *vector* or *deque*.
        * Need to insert or delete elements in the middle of the container: *list*.
        * Need to insert ot delete elements at the front and the back, but not in the middel: *deque*.
    + *containers cannot be used to store iostream, for the reason that all elements of a container should support assignment and copy. However, iostream doesn't support assignment or copy.*
    + When not certain which container to use, write the code so that it uses only operations common to both *vectors* and *lists*： use iterators, not subscripts, and avoid random access to elements.
    + *additional ways to construct strings*:
        * *string s(cp, n)*: create *s* as a copy of *n* characters from array pointed by *cp*.
        * *string s(s2, pos2)*: create *s* as a copy of characters in the string *s2* startomg at omdex *pos2*.
        * *string s(s2, pos2, len2)*: create *s* as a copy of *len2* characters from *s2* starting at index *pos2*.
    + *string* class provides 6 search functions, all returning a *string::size* type value that is the index of where the match occured, or a special value named *string::npos* if there is no match.
        * *find* functions are case sensitive.
        * *s1.compare(s2)* functions have following results: 
            - negative: s1 is less than s2.
            - positive: s1 is larger than s2.
            - 0: s1 is equal to s2. 
    + The iterators of *list* don't support arithmetic computation or certain relationship operators.

**Chapter 10 Associative Container**

- Definitions:
    + *Associative container*: a type that holds a collection of objects that supports efficient lookup by key.
    + *pair*: a type that holds two data values. It is a template type, defined in *utility* header.
    + *map*: a map is a collection of key-value pairs, often referred to as an *associative array*. It is associative in that values are associated with a particular key rather than being fetched by position in the array.
    + *set*: a collection of keys.
    + *value_type*: the type of the element stored in a container.
    + * operator: The dereference operator when applied to a *map, set, multimap*, or *multimap* iterator yields a *value_type*.
- Notes:
    + *Associative containers use the key to order and access elements. The use of a key distinguishes them from the sequential containers, in which elements are accessed positionally.*
    + *pair*: The members of a pair are *public*, respectively named as *first* and *second*. The members can be accessed using the dot operator notation.
    + *associative container*:
        * associative containers cannot be defined from a size, since there would be no way to know what values to give the keys.
        * *type*: a pair representing the types of the keys and associated values.
        * elements are ordered by *key*. When we iterate across an associative container, we are guaranteed that the elements are accessed in key order, irrespective of the order in which the elements were placed in the container.
    + *map*: indicate both the key and value type when defining a map object.
        * The key type should support the "<" operator.
        * We can change the value, but not the key member of the pair.
        * dereferencing the iterator yields a pair object in which *first* member holds the *const* key and *second* member holds the value.
        * **Using index that is not already present adds an element with that index to the map. That means if a new element appears, the map will initialize the associated value by default constructor.** This sometimes can be a side effect.
        * map iterator returns a *value_type*, which is a pair consisting of a *const key_type* and *mapped_type*. While subscript operator returns a value of type *mapped_type*.
        * when using *insert()*, a pair of the map *value_type* should be passed as an argument.
        * *m.count(k)*: returns the number of occurences of *k* within *m*. It can be used to determine whether a key is in the map.
        * *m.find(k)*: returns an iterator to the element indexed by *k*, if there is one, or returns an off-the-end iterator if the key is not present. It retrieves an element without adding it.
    + *set*: most useful when we simply want to know whether a value is present.
        * *set* does not provide a subscript operator, and does not define *mapped_type*.
        * There can only be one element with a given key in a *set*.
        * To fetch an element from a set, use *set.find()*.
    + *multimap* & *multiset*: multimap and multiset allow multiple instances of a key.
        * when a multimap or multiset has multiple instances of a given key, those instances will be adjacent elements within the container.
        * *lower_bound* and *upper_bound*: these two are associative container operations. They take a key ad return an iterator.
            - *lower_bound*: returns the iterator referring to the first instance of the key.
            - *upper_bound*: returns the iterator referring to just after the last instance.
            - If the key is not in the *multimap* or *multiset*, *lower_bound* and *upper_bound* will return the same iterator, indicating that there is no such element in the container. Moreover, they will return an iterator referring to the point at which the key can be inserted without disrupting the order within the container.
        * *m.equal_range(key)*: it returns a pair of iterators. If the key is present, then the first iterator refers to the first instance of the key and the second iterator refers to one past the last instance of the key. If no matching element found, both the first and second iterator refer to the position where this key could be inserted.
    + Knowing what operations we need to provide can help us see what data structures we'll need and how we might implement those actions.

**Chapter 11 Generic Algorithms**

- Definitions:
    + *inserter*: an inserter is an iterator adaptor that takes a container and yields an iterator that inserts elements into the specified container.
        * There are three kinds of inserters:
            - *back_inserter*: it creates an iterator that uses *push_ack*.
            - *front_inserter*: it uses *push_front*.
                + We can only use *front_inserter* only if the container has a push_front operation.
            - *inserter*: it uses *insert*. Its second argument is an iterator indicating the position ahead of which insertion should begin.
- Notes:
    + Generic algorithms are type independent. They achieve their type independence by operating in terms of iterators. 
    + Iterators can be categorized by the operations that they support: *input, output, forward, bidirectional* and *random access*.

**Chapter 12 Classes**

- Definitions:
    + *class*: C++ mechanism for defining our own abstract data types. Classes may have data, function or type members. A class defines a new type and a new scope.
    + *Data abstraction*: The ability to define both data and function members. Data abstaction is a programming technique that relies on the separation of interface and implementation. Fundamental to object-oriented and generic programming.
    + *Encapsulation*: The ability to protect class members from general access. It is a term that describes the technique of combining lower-level elements to form a new higher-level entity. It hides the implementation details of a type. In C++, it is enforced by preventing general user access to the *private* parts of a class.
    + *Mutuable*: a mutable data member is a member that is *never const*, even when it is a member of a *const* object.
    + *constructors*: special member functions that control how objects of the class are initialized.
    + *const member function*: a member function that may not change an object's odinary (i.e. neither *static* nor *mutable*) data members.
    + *friend*: the friend mechanism allows a class to grant access to its nonpublic members to specified functions or classes. The keyword *friend* may only appear within a class definition.
    + *static* member: a static member exists independently of any object of its calss; each static member is an object associated with the class, not with the objects of that class.
        * A static member function has no *this* parameter. It may directly access the static members of its class but may not directly use the nonstatic members.
- Notes:
    + Classes are the most fundamental features in C++. It allows us to define new types that are tailored to our own applications, making our programs shorter and easier to modify.
    + Member functions define the interface to the class. The class is encapsultated by making the data and functions used by the implementation of a class *private*.
    + Name lookup in Class member definitions:
        * Class members follow normal block-scope name lookup.
        * after function scope, look in class scope.
        * after class scope, look in the surrounding scope.
        * names are resolved where they appear within the file.
    + Constructors should initialize every data member. IT should use a constructor initializer list to initialize the data member.
    + *Constructor Initializer*: members of a class type that do not have a default constructor and members that are *const* or reference types must be initialized in the constructor initializer regardless of type.
    + The order in which members are initialized is the order in which the members are defined.
    + *static members*:
        * the name of a static member is in the scope of the class, avoiding name collisions with members of other classes or global objects.
        * Encapsulation can be enforced.
        * static members must be defined exactly once outside the class body. They are not initialized through the class constructors but instead should be initialized when they are defined.
        * Only integral *const static* members can be initialized within the class body. However, the data member should still be defined outside the class definition.

**Chapter 13 Copy Control**

- Definitions:
    + *copy constructor*: The constructor that takes a signal parameter, a (usually const) reference to an object of the class type itself, is called the copy constructor.
    + *assignment operator*: define what it means to assign one object of a class type to another of the same type. It must be a member of its class and should return a reference to its object.
    + *destructor*: special member function that cleans up an object when the object goes out of scope or is deleted.
- Notes:
    + For classes consisting of pointer members, it is always worth paying attention to the "copy-control" functions: *copy constructor, assignment operator, destructor*.
        * if a class does not define one or more of these operations, the compiler will define them automatically. The synthesized operations perform memberwise initialization, assignment, or destruction.
        * Unlike the copy constructor and assignment operator, the synthesized destructor is created and run regardless of wether the class defines its own destructor. The synthesized destructor is run after the class-defined destructor, if there is one, completes.
    + Classes that allocate memory or other resources almost always require that the class defines the copy-control members to manage the allocated resource.
    + *copy constructor*: used to explicitly or implicitly initialize one object from another of the same type, or to copy an object to pass it as an argument to a function.
    + *use count*: programming technique used in copy-control members. A separate class is created that points to the shared object and manages the use count.
    + *value semantics*: the copy-control behavior of classes that mimic the way arithmetic types are copied.

**Chapter 14 Overloaded Operations and Conversations**

- Definitions:
    + Overloaded operators are functions with special names: the keyword *operator* followed by the symbol for the operator being defined.
    + *Binders:* a *binder* is a function adaptor that converts a binary function object into a unary function object by binding one of the operands to a given value. It binds an operand of a psecified function object.
    + *Negators:* a *negator* is a function adaptor that reverses the truth value of a predicate function object.
    + *conversion operator*: a conversion operator defines conversion that converts a value of a class type to a value of some other type. It is declared in the class body by specifying the keyword *operator* followed by the type that is the target type of the conversion. *operator type()*
- Notes:
    + Overloaded operators: no additional operators can be defined for the built-in data types.
        * precedence and associativity of operators are fixed, regardless of the type of the operands.
        * default arguments for the overloaded operators are illegal, except for *operator ()*, the function call operator.
        * Don't overload operators with built-in meanings. It is usually not a good idea to overload the comma(,), address-of(&), logical AND(&&), or logical OR(||) operators.
        * Before designing the overloaded operators, it is important to firstly define the interface. Once defined, we can think about what operators to overload. Normally operations with a logical mapping to an operator are good candidates.(==, <<, >>, !)
        * Classes that will be used as the key type of an associative container should define "<" operator. If the type will be stored in a sequential container, the class ordinarily should define the equality (==) and less-than (<) operators.
        * The assignment (=), subscript([]), call(()), and member access arrow (->) operators must be defined as members.
        * The compound-assignment operators ordinarily ought to be members of the class. 
        * Operators that change the state of their object or that are closely tied to their given type, such as increment, decrement, and dereference, usually should be members of the class.
        * Symmetric operators, such as the arithmetic, equality, relational, and bitwise operators, are best defined as ordinary nonmember functions.
    + Input and Output operators: Classes supporting I/O should define overloaded operators for input(>>) and output(<<).
        * The "output" operator should take an *ostream&* as the first parameter, and a reference to a *const* object of the class type as its second. The operator should return a reference to its *ostream* parameter.
        * Generally, output operators should print the contents of the object, with minimal formatting. They should not print a newline.
        * Unlike "output" operator, "input" operator take a nonconst Class reference as the second parameter.
    + The equality and inequality operators should always be defined in tearms of each other.
    + Assignment operator should return a reference to *this.
    + Classes that represent containers from which individual elements can be retrieved usually define the subscript operator, *operator[]*. It must be defined as a class member function. Normally, a class that defines subscript needs to define two versions: nonconst version, and const version.
    + Arrow operator *operator->* should be defined as a member function, while deference operator (*) is recommended to be defined as a member function.
    + The overloaded arrow operator must return either a pointer to a class type, or an object of a class type that defines its own operator arrow.
    + *increment (++)* and *decrement(--)* operators are most often implemented for classes that provide pointerlike behavior on the elements of a sequence. Ordinarily, it is best to define both the prefix and postfix versions.
    + *function call operator()*: typicallythe call operator is overloaded for classes that represent an operation. It must be declared as a member function. A class may define multiple versions of the call operator, each of which differs as to the number or types of their parameters.
    + *function objects* are most often used as arguments to the generic algorithms.
    + The standard library defines a set of arithmetic, relational, and logical function-object classes. The are defined inthe *functional* header.
        * each of the library function-object classes represents an operator.
        * each of the function-object classes is a class template to which we supply a single type.
    + The standard library defines two binder adaptors: *bind1st, bind2nd*, and two negators: *not1, not2*.
    + Conversions to an array or function type are not allowed. Conversions to a pointer types, both data and function pointers, and to reference types are allowed. 
        * The conversion function must be a member function. It should not specify a return type, and also the parameter list should be empty.
        * Althoug not specifying a return type, each conversion function should return a value of the named type.
        * Only one class-type conversion can be applied.
        * The rank of the standard conversion, if any, following the conversion function is used to select the best match, if two conversion operators/constructors can be used in a call.
        * *avoid writing pairs of classes where each offers an implicit conversion to the other.*
        * There should be only one conversion to a built-in type.
        * A programmer facing with an ambiguous conversion can use a cast to indicate explicitly which conversion operation to apply.
        * Needing to use a constructor or a cast to convert an argument in a call to an overloaded function is a sign of bad design.

**Chapter 15 Object-Oriented Programming**

- Definition
    + Object-oriented programming (OOP) is based on three fundamental concepts: data abstraction, inheritance, and dynamic binding.
    + The key idea behind *OOP* is *polymorphism*. In C++, polymorphism applies only to references or pointers to types related by inheritance.
    + *Inheritance* lets us define classes that model relationships among types, sharing what's common and specializing only that which is inerently different. Members defined by the *base class* are inherited by its *derived calss*.
    + *Dynamic binding*: it allows us to write programs that use objects of any type in an inheritance hierarchy without caring about the objects' specific types.
    + *Polymorphism*: it referes to the ability to obtain type-specific behavior based on the dynamic type of a reference or pointer.
    + *protected* access label is for members accessible by the derived classes, but not accessible by general users of the type.
    + *class derivation list*: it names one or more base classes and has the form *class classname: access-label base-class*, where access-label is one of *public, protected or private*, and the *base-class* is the name of a previously defined class.
    + *Immediate base class*: it is the class named in the derivation list.
    + *Refactoring*: refactoring involves redesigning a class hierarchy to move operations and/or data from one class to another. It happens most often when classes are redesigned to add new functionality. 
    + *Virtual function*: a member function that defines type-specific behavior.
    + *Pure virtual function*: a pure virtual function is specified by writing = 0 after the function parameter list. Defining a pure virtual function indicates that the function provides an interface for subsequent types to override but that the version in this class will never be called. 
    + *Abstract base class*: a class contains one or more pure virtual functions is an abstract base class. An attempt to create an object of an abstract base class is a compile-time error.
    + *handle class*: the handle class stores and manages a pointer to the base class.
- Notes
    + The fact that *the static and dynamic types of references and pointers can differ* is the cornerstone of how C++ supports polymorphism.
    + In C++, we use *class* for *data abstraction*, *class derivation* to *inherit* one class from another: a derived class inherits the members of its base class(es). *Dynamic binding* lets the compiler determine at run time whether to use a function defined in the base or derived class.
    + Inheritance lets us write new classes that share behavior with their base class(es), but redefine that behavior as needed. Dynamic binding lets the compiler decide at runtime which version of a function to run based on an object's dynamic type. 
    + Classes related by inheritance are often described as forming an inheritance hierarchy. 
    + Functions defined as *virtual* are ones that the base expects its derived classes to redefine. Functions that the base class intends its children to inherit are not defined as virtual.
    + Classes used as the root class of an inheritance hierarchy generally define a virtual destructor.
    + Calls to nonvirtual functions are resolved at compile time. Calls to virtual functions are resolved at run time.
    + A derived object may access the *protected* members of its base class only through a derived object. The derived class has no special access to the protected members of base type objects.
    + The declaration of a virtual function in the derived class must exactly match the way the function is defined in the base, with only one exception: the virtual function returns a reference to the base class.
    + The key to dynamic binding in C++: the actual type of the object might differ from the static type of the reference or pointer addressing that object.
    + There is automatic conversion which converts a reference/pointer to a derived type to a reference/pointer to its base type(s). However, it is not autoamatic to convert from reference/pointer to base to reference/pointer to derived.
    + Constructors and the copy-control members are not inherited. Each class defines its own constructors and copy-control members.
    + Constructor of derived class initializes its base class in addition to initializing its own data members. A derived constructor indirectly initializes the members it inherits by including its bas class in its constructor initializer list.
        * The constructor initializer list supplies initial values for a class' base class and members. The base class is initialized first and then the members of the derived class are initialized in the order in which they are declared.
        * If a derived class defines its own copy constructor, that copy constructor usually should explicitly use the base-class copy constructor to initialize the base part of the project.
        * Unlike copy constructor and assign operator, the derived destructor is never responsible for destroying the members of its base objects. The compiler always implicitly invokes the destructor for the base part of a derived object. *Each destructor does only what is necessary to clean up its own members.*
        * To ensure that the proper destructor is run, *the destructor must be virtual in the base class*. The root class of an inheritance hierarchy should define a virtual destructor even if the destructor has no work to do.
    + Under inheritance, the scope of the derived class is nested within the scope of its base classes.
        * Name lookup happens at compile time.
        * A derived-class member with the same name as a member of the base class hides direct access to the base-class member, which should be avoided though.
        * Functions defined in a derived class do not overload members defined in the base. The base class functions are considered only if the derived does not define the function at all.
    + Name Lookup and Inheritane:
        * Start by determining the static type of the object, reference, or pointer through which the function is called.
        * Look for the function in that class. If not found, look in the immediate base class and continue up the chain of classes.
        * Once the name is found, do normal type-checking.
        * Assuming the call is legal, the compiler generates code.
    + Object does not support object-oriented programming in C++, instead we must use pointers and references to support OOP.
        * Handles that cover an inheritance hierarchy typically behave like either a smart pointer or a value.

**Chapter 16 Templates and Generic Programming**

- Definitions
    + *Templates*: A template is a type-independent blueprint that the compiler uses to generate a variety of type-specific instances.
        * *function template*: a function template is a type-independent function which is used as a formula for generating a type-specific version of the function. 
        * *class template*: a class definition can be used to define a set of type-specific classes.
        * Template definition starts with the keyword *template*, followed by a *template parameter list*, a comma-separated list of one or more template parameters.
    + *Instantiation*: The process of generating a type-specific instance of a template is known as instantiation.
    + The process of determining the types and values of the template arguments from the type of the function arguments is called *template argument deduction*.
    + *member templates*: a member that is itself a class or function template in a class is referred to as member templates. They may not be virtual.
    + *Template Specialization*: it is a sepratate definition in which the actual type(s) or value(s) of one or more template parameter(s) is (are) specified.
    + *Partial specialization*: a class template partial specialization is itself a template. The definition of a partial specialization looks like a template definition. The template parameter list of a partial class specialization is a subset of the parameter list of the corresponding class template definition.
    + *export* keyword: it is used to indicate that the compiler must remember the location of the associated template definition.
- Notes
    + a template parameter can be a *type parameter*, which represents a type, or a *nontype parameter*, which represents a constant expression. A type parameter is defined following the keyword *class* or *typename*.
        * the name of a template parameter can be used after it is declared until the end of the template declaration or definition.
        * a name used as a template parameter may not be reused within the template.
        * the name of a template parameter can be used only once within the same template parameter list.
        * in addition to defining data or function members, a class may define type members. Explicitly telling the compiler *typename* could treat the declared member as a type.
        * It's always a good idea to specify *typename* if you intend to declare a name as a type.
        * each type parameter is bound to an actual type.
        * *nontype parameters* are values when the function is called. The type of that value is sepcified in the template parameter list.
        * When writing template code, it is useful to keep the number of requirements placed on the argument types as small as possible.
    + Each instantiation of a class template consistutes an independent class type.
        * When instantiating a class template, we must always specify the template arguments explicitly.
        * The type defined by a template class always includes the template argument(s).
        * Multiple type parameter arguments must match exactly. If the designer of a function template wants to allow normal conversions on the arguments, then the function must be defined with different type parameters.
        * In general, arguments are not converted to match an existing instantiation, instead a new instantiation is generated.
        * *const* conversions and "array/function to pointer conversions" are two exceptions while instantiating template class/function.
        * normal conversions apply for nontemplate arguments.
    + For *class template members*, inside the scope of a class template, we may refer to the class itself using its unqualified name. However, if you refer to other template class, you need to use the full name (i.e. including the template parameters)
        * To define a member function of a class template, it must start with the keyword *template* followed by the template parameter list for the class.
        * It must indicate the class of which it is a member.
        * The class name must include its template parameters.
        * member-function template parameters are fixed by the template arguments of the object.
        * Nontype template arguments must be compile-time constant expressions.
        * When we grant access to all instances of a given template, there need not be a declaration for that class or function template in scope. When we want to restrict friendship to a specific instantiation, the class or function must have been declared before it can be used in a friend declaration.
        * When a member template is a member of a class template, its definition must include the class-template paramters as well as its own template parameters. The class-template parameter list comes first, followed by the member's own template parameter list.
    + The form of a *template specialization* is:
        * the keyword *template* followed by an *empty* bracket pair (< >).
        * followed by the template name and a bracket pair specifying the template parameters that this specialization defines.
        * When we define a nontemplate function, normal conversions are applied to the arguments. When we specialize a template, conversions are not applied to the argument types.
        * A program cannot have both an explicit specialization and an instantiation for the same template with the same set of template arguments. It is an error for a specialization to appear after a call to that instance of the template has been seen.
        * A class template specialization ought to define the same interface as the template it specializes.
        * Member specializations are declared just as any other function template specialization. They must start with an empty template parameter list.
    + The viable functions by the kinds of conversions, if any, required to make the call is ranked. If the call is ambiguous, remove any function template instances from the set of viable functions, which consists of ordinary nontemplate viable functions and function template instances.
        * It is almost always better to define a function-template specialization than to use a nontemplate version.


**Chapter 17 Tools for Large Programs**

- Definitions
    + *stack unwinding* continues up the chain of nested function calls until a *catch* clause for the exception is found.
    + *exception object*: it is used to communicate between the throw and catch sides of an exception.
    + *exception specifier*: it is a type name followed by an optional parameter name. The type of the specifier determines what kinds of exceptions the handler can catch. It must either be a built-in type or a programmer-defined type. A forward declaration for the type is not sufficient.
    + *exception specification*: used on a function declaration to indicate what (if any) exception types a function throws.
    + *rethrowing*: the process that when a catch cannot completely handle an exception, the exxception will be passed out to another catch further up the list of function calls, is called rethrowing. It is a throw not followed by a type or an expression.
    + *catch-all*: it is a catch clause with the form (...), which hanles all the exceptions. When combined with other clauses, catch-all will always be at the last place.
    + *exception safe*: the programs operate correctly even if an exception occurs. 
    + *Resource Allocation Is Initialization (RAII)* is a technique that guarantees that resources are properly freed by defining a class to encapsulate the acquisition and release of a resource.
    + *auto_ptr* is a template class that takes a single type parameter, which provides exception safety for dynamically allocated objects. It is defined in the *memory* header.
    + *namespace*. a namespace definition begin with the keyword *namespace* followed by the name space name.
    + *using declaration* mechanism to inject a single name from a namespace into the current scope.
    + *using derective*: mechanism for making all the names in a namespace available in the nearest scope containing both the using directive and the namespace itself.
    + *unnamed namespace*: it is a namespace defined without a name, It is local to a particular file and never spans multiple text files.
    + *multiple inheritance* is the ability to derive a class from more than one immediate base class.
    + *virtual inheritance*: it is a mechanism whereby a class specifies that it is willing to share the state of its virtual base class. Under virtual inheritance, only one shared base-class subobject is inherited for a given virtual base regardless of how many times the class occurs as a virtual base within the derivation hierarchy.
- Notes
    + Exceptions let us separate problem detection from problem resolution. The part of the program that detects a problem need not know how to deal with it.
    + An *exception* is *raised* by *throwing* an object. The type of that object determies which handler will be invoked. It must be possible to copy the throwed object.
    + Exception object is managed by the compiler and is guaranteed to reside in space that will be accessible to whatever *catch* is invoked.
    + it is usually a bad idea to throw a pointer.
    + during stack unwinding, the memory used by local objects is freed and destructors for local objects of class type are run.
        * while stack unwinding is in progress for an exception, a destructor that throws another exception of its own, causes the library terminate function called. Destructors should never throw exceptions.
        * Uncaught exceptions terminate the program.
    + The selected catch exception specifier is the first catch found that can handle the exception, not necessarily the one matching the exception best.
        * most conversions are not allowed between the types of the exception and the *catch* specifier, except the followings: conversions from nonconst to const, conversions from derived type to base type, and an array to a pointer to the type of the array.
        * a catch clause that handles an exception of a type related by inheritance ought to define its parameter as a referee.
        * multiple *catch* clauses with types related by inheritance must be ordered from most derived type to least derived.
    + rethrowing: the exception that is thrown is the original exception object, not the catch parameter. The type depends on the dynamic type of the exception object, not the static type of the catch parameter.
    + The only way for a constructor to handle an exception from a constructor initializer is to write the constructor as a function try block.
    + using classes to anage acquisition and deallocation ensures that resources are freed if an exception occurs.
    + *auto_ptr* may hold only a pointer to an object, and may not be used to point to a dynamically allocated array. 
        * It is a template, so that it can hold pointers of any type.
        * In most common case, we initialize an *auto_ptr* to the address of an object returned by a *new* expression.
        * When we copy an *auto_ptr* or assign its value to another *auto_ptr*, ownership of the underlying object is transferred from the original to the copy. The *original auto_ptr* is *reset to an unbound state*.
        * To test the *auto_ptr*, we must use its *get* member, which returns the underlying pointer contained in the *auto_ptr*.
        * Do not use an *auto_ptr* to hold a pointer to a statically allocated object.
        * Never use two *auto_ptrs* to refer to the same object.
        * Do not use an *auto_ptr* to hold a pointer to a dynamically allocated array.
        * Do not store an *auto_ptr* in a container.
    + *exception specification* follows the function parameter list. it is the keyword *throw* followed by a list of exception types enclosed in parentheses.
        * An empty specification list says that the function does not throw any exception.
        * if a function throws an exception not listed in its specification, the library function *unexpected* is invoked, which calls *terminate* to abort the program.
        * The exception specification cannot be checked at compile time,.
        * The exception specification of a derived-class virtual function must be either equally or more restrictive than the exception specification of the corresponding base-class virtual function.
        * exception specification can be provided in the definition of a pointer to function. The specification of the source pointer must be at leaset as restrictive as the specification of the destination pointer.
    + the name of a namespace must be unique within the scope in which the namespace is defined.
        * a namespace definition does not end with a semicolon.
        * entities defined within the namespace are called namespace members.
        * a namespace can be defined in several parts.
        * members may not be defined in unrelated namespaces.
        * names defined inside a nested namespace are local to that namespace.
        * names defined in an unnamed namespace are visible only to the file containing the namespace.
        * unnamed namespaces are used to declare entities that are local to a file.
        * header files should NOT contain *using* directives or *using* declarations, except inside functions or other scopes.
        * a namespace can have many synonyms, or aliases, which can be used interchangeably with the original namespace.
        * a *using* directive does not declare local aliases for the namespace member names. It has the effect of lifting the namespace members into the nearest scope that contains both the namespace itself and the *using* directive.
        * If the name is not local to the member function, we first try to resolve the name to a class member before looking in the outer scopes.
        * The qualified name indicates the scopes that are searched, in reverse order.
        * Functions that take parameters of a class type, which are defined in the same namespace as the itself, are visible when an object of the class type is used as an argument.
    + The base-class constructors are invoked in the order in which they appear in the class derivation list. Destructors are always invoked in the reverse order from which the constructors are run.
        * The same base-class can only be declared once in the class derivation list.
        * A pointer or reference to a derived class can be converted to a pointer or reference to any of its base classes.
        * using a pointer to one class does not allow the access to members of another base.
        * Each base class is implicityle constructed, assigned or destroyed, using that base calss' own copy constructor, assign operator, or destructor.
        * When a class has multiple base classes, name lookup happens simultaneously through all the immediate base classes.
        * Specifying virtual derivation has an impact only in classes derived from the class that specifies a virtual base. It is a statement about the derived class' relationship to its own, future derived class.
        * The *virtual* specifier states a willingness to share a single instance of the named base class within a subsequenty derived class.
        * In a virtual derivation, the virtual base is initialized by the *most derived constructor*.
        * *virtual base classes are always constructed prior to nonvirtual base classes regardless of where they appear in the inheritance hierarchy*.

**Chapter 18 Specialized Tools and Techniques**

- Definitions
    + *allocator* class is a template that provides typed memory allocation and object construction and destruction.
    + *freelist* is a memory management technique that involves preallocating unconstructed memory to hold ojbects that will be created as needed.
    + *Run-Time Type Identification (RTTI)* helps program to retrieve the actual derived types of the objects, which are referred to by pointers or references.
    + *new expression* allocates and constructs an object of a specified type.
    + *pointer to member* embodies the type of the calss as well as the type of the member. It applies to nonstatic member of a class.
    + *function tabel*: it is a collection of cuntion pointers from which a given call is selected at run time.
    + a *union* is a special kind of class. A *union* may have multiple data members, but at any point in time, only one of the members may have a value. When a value is assigned to one member of the *union*, all other members become undefined.
    + *local class*: a class defined inside a function body.
    + *porting* is the process of moving a program to a new machine. C programs are said to be portable.
    + *bit-filed* is a special class data member which can be declared to hold a specified number of bits. It is normally used when a program needs to pass binary data to another program or hardware device.
    + *linkage directives* are to indicate the language used for any non-C++ function.
    + *volatile*: it is a type qualifier that signifies to the compiler that a variable might be changed outside the direct control of the program. It is a signal to the compiler that it may not perform certain optimizations.

- Notes
    + C++ has two tways to allocate and free unconstructed, raw memory:
        * *allocator* class. It provides type-aware memory allocation.
        * The library operator *new* and *delete*.
    + C++ has various ways to construct and destroy objects in raw memory:
        * *allocator* class has *construct* and *destroy* members.
        * *new* to construct.
        * *uninitilalized_fill* and *uninitialized_copy* construct objects in their destination rather than assigning to them.
    + users of *allocator* class must separately *construct* and *destroy* objects placed in the allocated memory.
    + In general, it is more type-safe to use an *allocator* rather than using the *operator new* and *operator delete* functions directly.
    + A class may manage the memory used for objects of its type by defining its own members named *operator new* and *operator delete*.
    + If storage was allocated with a *new* expression invoking the global *operator new* function, then the *delete* expression should also invoke the global *operator delete* function.
    + Modern C++ programs should use the *allocator* classes rather than these library functions (*new operator* and *delete operator*).
    + *RTTI* is provided through two operators:
        * *typeid* operator: it returns the actual type of the object referred to by a pointer or a reference.
            - *typeid* can be used to expressions of any type. It is usually used to compare the types of two expressions, or to compare the type of an expression to a specifid type.
            - The operands to the *typeid* should be objects, not pointers.
        * *dynamic_cast*: it safely converts from a pointer or reference to a base type to a pointer or a reference to a derived type.
            - if a *dynamic_cast* operator fails, the result of the *dynamic_cast* is 0.
        * These operators return dynamic type information only for classes with one or more virtual functions.
        * *type_info* class varies by compiler. However, there are 4 common functions which should be provided by all compilers: "==, !=, t.name(), t1.before(t2)". *type_info* objects may not be copied.
    + A pointer to member function is defined by specifying the function return type, parameter list, and a class.
        * The pointer-to-member dereference operator (.*) fetches the member from an object or reference.
        * The pointer-to-member arrow operator(->*) fetches the member through a pointer to an object.
    + *nested class* are independent classes and are largely unrelated to their enclosing class. Objects of the enclosing and nested classes are independent from one another.
        * classes nested inside a class template are templates.
        * If a nested class had declared a static member, its definition would also need to be defined in the outer scope.
        * A nested class of a class template is not instantiated automatically when the enclosing class template is instantiated. The nested class is instantiated only if it is itself used in a context that requires a complete class type.
        * When processing the declarations of the class members, any name used must appear piror to its use. When processing definitions, the entire nested and enclosing class(es) are in scope.
    + Unions provide a convenient way to represent a set of mutually exclusive values that may have different types.
        * The amount of storage allocated for a union is at least as much as the amount necessary to contain its largest data member.
        * A union may not serve as a base class.
        * A union cannot have a static data member, a member that is a reference, or a member of a class type that defines a constructor, destructor, or assignment operator.
        * *discriminant* is a programming technique which uses an object to determine which actual type is held in a union at any given time. It keeps track of what value is stored in the *union*, to avoid accessing the *union* value through the wrong member.
        * An anonymous *union* cannot have private or protected members, nor can an anonymous *union* define member functions.
    + All members including functions of a local class must be completely defined inside the class body.
        * a local class is not allowed to define *static* data members.
        * local classes may not use variables from the function's scope, except static variables, enumerators defined within the enclosing local scopes, and type names.
        * normal protection rules apply to local classes. In practice, private members are hardly ever necessary in a local class.
    + A bit-filed must be an integral data type.
        * Ordinarily it is best to make a bit-filed an unsigned type.
        * Bit-fields with more than one bit are usually manipulated using the built-in bitwise operators.
        * The address-of operator (&) cannot be applied to a bit-filed. So there can be no pointers referring to class bit-fileds. Nor can a bit-field be a static member of its class.
    + Programs using *volatile* usually must be changed when they are moved to new machines or compilers.
        * An object should be declared *volatile* when its value might be changed in ways outside either the control or detection of the compiler.
        * Synthesized copy control does not apply to volatile objects.
    + Linkage directive may not appear inside a class or function definition. It must appear on the first declaration of a function.
        * An entire header file can be imported by using linkage directives.
        * By using the linkage directive on a function definition, we can make a C++ function available to a program written in another language.
        * C doesn't support function overloading. Thus it is an error to declare more than one function with C linkage with a given name.
        * To declare a pointer to a function written in another programming language, we must use a linkage directive.
        * A pointer to a C function cannot be initialized or be assigned to point to a C++ function (and vice versa).
        * Linkage directives apply to the entire declaration.