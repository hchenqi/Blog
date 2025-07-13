# Minimal Programming Language

## type

### type construction

- constant {}
- union <A, B, ...>
- tuple {A, B, ...}

note:
- tuple doesn't contain constants, or it's meaningless, so in tuple {A, B, ...}, A, B, ... must be union types

```
{}
<{}, {}>
{<{}, {}>, <{}, {}>}
```

### array

- array A[...]

note:
- array is a tuple with a fixed number of copies of a certain union type

```
<{}, {}>[32]
```

### type alias

- a name can be bound to a type definition or another name

```
true : {}
false : {}
boolean : <true, false>
bool : boolean
bit : boolean
int : bit[32]
```

### type conversion

- in union <A, B, ...>, A, B, ... are subtypes of the union type
- tuple can also be regarded as union type, where each combination of the subtypes from each element is also a subtype of the tuple

### variable

- a variable can be declared as a union type in the same way as type alias
- a variable can be assigned as one of its subtypes

```
x : tuple<bool, bool>
x = tuple<bool, true>
x = tuple<true, true>
```

note:
- : and = should be the same
- tuple can contain constants here, which is just for type comparision as a partial type
- it's not necessary to assign a constant to a variable, any subtype is also ok
- when a variable is assigned a subtype, it's type has changed and can't be reverted

note:
- variables and types are not distinguished, variables are type aliases, and aliases can be assigned subtypes

## control flow

### function

- a function is an expression with unbound variables, whenever an argument as a subtype is provided, the function eagerly evaluates
- an expression without unbound variables is eagerly evaluated and reduced to a single value

note:
- if the argument is not a constant, the function might output a partial type

note:
- an expression binds values to functions, and the binding is performed by user through editor, and the interpreter examines binding and evaluates eagerly, the evaluation creates a temporary copy of the expression and doesn't change the expression in editor

### branch

