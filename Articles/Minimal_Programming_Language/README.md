# Minimal Programming Language

## data type

### construction

- constant {}
- union <A, B, ...>
- tuple {A, B, ...}
  - array A[...]

note:
- the constructing types A, B, ... in a union or a tuple can be repeated
- a union or a tuple with only one constructing type is the same as the constructing type
- array is a rewriting of tuple with a fixed number of copies of a certain type

```
{}
<{}, {}>
{<{}, {}>, <{}, {}>}
<{}, {}>[32]
```

### storage size

- constant types have size of 0
- union types have ceil(log2(n)) bits for the encoding part, where n is the number of constructing types in the union, plus the size of the current type it holds
- tuple types have size of sum of the size of its constructing types

### subtyping

- each constructing type is a subtype of a union
- a combination of subtypes of each constructing type is a subtype of a tuple

```
tuple<true, true>
tuple<bool, true>
tuple<bool, bool>
```

### constant subtype

- constant subtype is a subtype and at the same time a constant

### alias

- an alias can be declared as a type construction or another alias, and can be referenced in a type construction

```
false : {}
true : {}
boolean : <false, true>
bool : boolean
bit : boolean
int : bit[32]
```

### conversion

- a type can be converted from a subtype or another type of the same construction

### *isomorphism

```
<{}, {}, {}, {}> ~ {<{}, {}>, <{}, {}>}
```

## computation

### map

- a map can be declared as a table mapping a union type to another union type, with each constant subtype mapping to a certain constant subtype

```
not: bool -> bool where
  true -> false
  false -> true

and: {bool, bool} -> bool where
  {false, false} -> false
  {false, true} -> false
  {true, false} -> false
  {true, true} -> true

or: {bool, bool} -> bool where
  {false, false} -> false
  {false, true} -> true
  {true, false} -> true
  {true, true} -> true
```

- a map can be applied to a constant subtype of its input type

```
not true
and {false, true}
```

### variable

- 

### expression
