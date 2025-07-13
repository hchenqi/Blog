# Minimal Programming Language

## type

### type construction

- constant {}
- union <A, B, ...>
- tuple {A, B, ...}

note:
- in union <A, B, ...>, A, B, ... are subtypes of the union type
- tuple doesn't contain constants, or it's meaningless, so in tuple {A, B, ...}, A, B, ... must be union types
- tuple can also be regarded as union type, where each combination of the subtypes from each element is also a subtype of the tuple

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
true: {}
false: {}
boolean: <true, false>
bool: boolean
bit: boolean
int: bit[32]
```

### variable

- a variable can be declared as a union type

```
bool x
```

### type conversion

- a variable can be assigned value from its constant subtypes

```
x = true
```

## control flow

- functions are expressions with unbound variables
