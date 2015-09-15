---
layout : post
category : LearningNote
tags : [C++, Basis]
---

{% include JB/setup %}

This post summarizes the note of some basic C++ syntax, which make me confused.

- *heap vs stack* ([link](http://stackoverflow.com/questions/79923/what-and-where-are-the-stack-and-heap))
    + The *stack* is the memory set aside as *scratch space for a thread of executation*. 
        * The stack is always reserved in a *LIFO (Last In First Out)* order. The most recently reserved block is always the next block to be freed.
        * When a function is called, a block is reserved on the top of the stack for local variables and some bookkeeping data.
        * When the function returns, the block becomes unused and can be used the next time a function is called.
    + The *heap* is the memory set aside for *dynamic allocation*. 
        * Unlike the stack, there is no enforced pattern to the allocation and deallocation of blocks from the heap. You can allocate a block at any time and free it at any time.
        * It is more complex to keep track of which parts of the heap are allocated or free at any given time.
    + Each thread gets a stack, while there is typically only one heap for the application.
    + In summary, the stack is attached to a thread when a thread is claimed, the heap is typically allocated at application startup by the runtime.
    + The size of the stack is set when a thread is created. The size of the heap is set on application startup, but can grow as space is needed.
    + A demonstration for "Stack vs. Heap".
    ![Stack vs. Heap ([source](http://vikashazrati.wordpress.com/2007/10/01/quicktip-java-basics-stack-and-heap/))](http://i.stack.imgur.com/i6k0Z.png)

<!--more-->

- *smart pointers* ([link1](http://stackoverflow.com/questions/106508/what-is-a-smart-pointer-and-when-should-i-use-one), [link2](http://ootips.org/yonat/4dev/smart-pointers.html))
    + A *smart pointer* is a *class* that wraps a 'raw' C++ pointer, to manage the *lifetime of the object being pointed to*. There is no single smart pointer type, but all of them try to abstract a 'raw' pointer in a practical way.
    + In general, smart pointer is a pointer-like type with some additional functionality, e.g. automatic memory deallocation, reference counting etc. (*automatic cleanup, automatic initialization, dangling pointers, garbage collection*).
    + The simplest garbage collection scheme is reference counting or reference linking.
    + When you need to use pointers, you would normally want to use a smart pointer as this can alleviate many of the problems with 'raw' pointers, mainly forgetting to delete the object and leaking memory.
 
    + With a 'raw' C++ pointer, the programmer has to explicitly destroy the object when it is no longer useful.
    
    ``` c++
    MyObject* ptr = new MyObject();
    ptr->doSomething();         // use the object in some way
    delete ptr;                 // destroy the object. done with it.
    // !------------------------------------------------------------
    // what if doSomething() throws an exception?
    ```

    + A smart pointer by comparison defines a policy as to when the object is destroyed. You still have to create the object, but you no longer have to worry about destroying it.
    
    ``` cpp
    SmartPtr<MyObject> ptr(new MyObject());
    ptr->doSomething();         // use the object in some way
    // destruction of the object happens, depending on the policy the
    // smart pointer class uses.
    // destruction would happen even if doSomething() throws an exception
    ```

    + The simplest policy in use involves the scope of the smart pointer wrapper object, such as implemented by *boost::scoped_ptr* or *std::unique_ptr*.

    ``` cpp
    void f()
    {
        {
            boost::scoped_ptr<MyObject> ptr(new MyObject());
            ptr->doSomething();
        }// boost::scoped_ptr goes out of scope, and the MyObject is automatically destroyed
        // ptr->Ooops(); compiler error: "ptr" not defined since it is no longer in scope
    }
    ```

<!-- -->

    + The *boost::scoped_ptr* pointers cannot be copied. This prevents the pointer from being deleted multiple times. You can pass the references to it around to other functions.
    
    + Scoped pointers are useful when you want to tie the lifetime of the object to a particular block of code. 
    
    + A more complex smart pointer policy involves reference counting the pointer. This allows the pointer to be copied. When the last "reference" to the object is destroyed, the object is deleted. It can be implemented by *boost::scoped_ptr* and *std::share_ptr*.

    ```cpp
    void f()
    {
        typedef std::tr1::share_ptr<MyObject> MyObjectPtr;
        MyObjectPtr p1; // empty
        {
            MyObjectPtr p2(new MyObject());
            // there is now one "reference" to the created object.
            p1 = p2; // copy the pointer
            // there are now two references to the object.
        }// p2 is destroyed, leaving one reference to the object.
    }// p1 is destroyed, leaving a reference count of zero.
    // the object is destroyed.
    ```

    + One drawback to reference counted pointers - the possibility of creating a dangling reference.
    + Since C++11 the standard librar has provided sufficient smart pointer types, and you should favour the use of *std::unique_ptr*, *std::shared_ptr* and *std::weak_ptr*.

- *lock. mutex*
- *thread*

- *template*
- *share_ptr*
- *pointer to implementation*