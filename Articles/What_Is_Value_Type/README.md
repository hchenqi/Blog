# What Is Value Type

There's a distinction between `value type` and `reference type` in some programming languages, like `Java`. The value type contains the raw data of an object, for the types such as `bool`, `int` and `float`, while the reference type is a pointer to the actual object and might be null.

But what actually is a value? What does a specific bool value `false` or `true`, or integer value `3` or `11` mean? How is a value stored and how does its type get determined? What's special with reference type compared with value type? These are what I will try to explain in this article.

## Encoding And Decoding

Modern computer architectures use binary to store all kinds of data. The memory or the disk is just a long fixed-sized array of raw bits, each with two states. All data is encoded in it in some way.

### Enum And Switch

An enum object is just a reference or encoding to what it currently stores.

### Constant And Variable

A constant doesn't occupy any space. Only a variable does. A variable needs space to store what it currently refers to.

A constant can be encoded in a variable, and the encoding rule is defined by the type of the variable. A constant has no type.

A constant as both edit time is a variable. It is already encoded at edit time as a literal string.

## The Address Of An Object

Objects have addresses.

It matters how the data is to be interpreted. And the interpreter is called the runtime environment.

## Runtime Environment

The runtime environment is responsible of resolving the references.

Values are interpreted by the 

## Constant Propagation

There should therefore no longer be such distinction between compile time and run time. A run time is also edit time that connects the function and the constant arguments, which will output the result once it is closed. A compiled program is simply a function.

It creates a copy of the program and then reduces it to a single constant.

Constant propagation happens at edit time. (Now there's only edit time.) The parent function both stores the original objects and the partial evaluated objects (as a cache).

## Partial Evaluation

### Input And Output

A function's input should always be uncertain, or

A function's output should also be uncertain with different inputs, or the function would be useless. The output is variable to encode.


Reference is also a kind of encoding, but the information encoded is the address of an object.
