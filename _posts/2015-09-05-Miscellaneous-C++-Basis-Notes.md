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

- *smart pointers* ([link](http://stackoverflow.com/questions/106508/what-is-a-smart-pointer-and-when-should-i-use-one))
    + A *smart pointer* is a *class* that wraps a 'raw' C++ pointer, to manage the *lifetime of the object being pointed to*. There is no single smart pointer type, but all of them try to abstract a 'raw' pointer in a practical way.
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
    
    >{% highlight cpp %}
      SmartPtr<MyObject> ptr(new MyObject());
    ptr->doSomething();         // use the object in some way

    // destruction of the object happens, depending on the policy the
    // smart pointer class uses.

    // destruction would happen even if doSomething() throws an exception
    {% endhighlight %} 

    + The simplest policy in use involves the scope of the smart pointer wrapper object, such as implemented by *boost::scoped_ptr* or *std::unique_ptr*.


- *lock. mutex*
- *thread*

- *template*
- *share_ptr*
- *pointer to implementation*