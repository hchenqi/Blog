# What Is Value Type

There's a distinction between "value type" and "reference type" in some programming languages, like Java. The value type contains the raw data of an object, for the types such as `bool`, `int` and `float`, while the reference type is a pointer to the actual object and might be null.

But here I will say, values are also references. And from this point of view, the distinction between "value type" and "reference type" is not significant.

## value type

Taking a look at the simpliest value type `bool`, there can be only two possible values taken, `true` or `false`. The type bool occupies one bit, which encodes its value. So, the value type is actually an encoding of all possible values it can rerepresent. `int` encodes a certain set of integers, and `float` encodes a certain set of numbers that might be fractions. `enum` type is the best example of encoding. It allows user to define a type with a specified set of possible values. Moreover, all data stored in a computer is just an encoding of things.

## value

Value `true`, `12`, or `"hello"` are of type `bool`, `int` and `string` respectively, by intuition. But they are also constants. Actually, they don't take up any storage space. Why? Because constants are fixed, so there's no need to store extra information. Only when two things need to distinguish from each other, a bit will be needed. So if a variable can either be `12` or `"hello"`, only a bit is needed to store its current value, as large as the type `bool`. All constants are equal, but they get differentiated and assigned special meanings only when they need to be grouped together.

Apart from numbers like `int` which can do mathematical calculations, the value of a variable matters at the point when it's being dispatched. As a variable only encodes its possible values, it will only be decoded in the following procedure. An `enum` typed variable is only to be used in a `switch-case` expression. And after being dispatched, the variable no longer has a reason to exist.

## map

A `switch-case` or `if-else` clause can be seen as a map between values. When the map itself is constant, and input is determined, then the output is determined. The evaluation of a program is just looking up the map table with a certain input, retrieve the result, and repeat.

## reference

Reference types are also just encodings. They encode the relative address of an object in the computer memory. But actually, every encoding is also an addressing. `enum` encodes a set of values it can represent, so as to say, it defines an addressing rule for the values, and it stores the "address" that maps to a certain value. A variable of type `enum` stores the reference to its meaning, and it will be interpreted with a `switch-case` clause. A memory address stores the reference to an object, and the computer architecture has a large built-in `switch-case` clause to interpret an address, mapping it to the object.

## constant

There are different aspects of constants. There are run-time constants and compile-time constants. Codes are fist written and then run. Before being run, a variable might have already taken a constant value, as a compile-time constant. Or its value is not yet determined, and only when the program is running and from the user's input, the value will get initialized, and if its value never gets changed, then it's a run-time constant.

Whenever a variable takes a constant value, the variable is no longer necessary to exist. The constant value will only get propagated, and the variable destructs itself. Constant propagation at run-time is just the evaluation of the program, and a compile-time constant causes compile-time evaluation. The only difference between compile-time and run-time is when the value of a variable will be determined. Ideally, a program after compilation will contain no variables assigned with a constant value, though there might still be partially evaluated values. The drive of evaluation of a program is the assignment of a variable with a constant value. Programs are designed just to handle undetermined run-time inputs, and if the input of a program never changes, then the program can be reduced to a single constant.

## A programming model

Values are encodings. Values can group to form tuples and de-group. Maps are pairs of values. Maps can be modified. Evaluation is to apply a map to a constant value and get the mapped value. A program is a sequence of mapping, grouping and de-grouping. Writing a program is to define the encoding and decoding rules, provide partial constants, and design the evaluation sequence.
