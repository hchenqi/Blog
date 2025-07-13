# Minimal Programming Language

principle:
- functions are expressions with unbound variables
- if-else/switch-case are mappings from boolean/enum to function calls carrying context
- context is also unbound variables for functions
- mappings are functions, and the mapping key is the unbound variable
- supplying a function with bound values makes a copy of the function and then evaluates and reduces to a value

principle:
- a function is a value(constant) that is bound to a name or a part of a larger function
- supplying a value to a function creates a new function which is closed and reduces itself to a value

example:
```
true
false
bool: union<true, false>
not: bool -> bool where
    false -> true
    true -> false
and: tuple{bool, bool} -> bool where
    {false, false} -> false
    {false, true} -> false
    {true, false} -> false
    {true, true} -> true
```

principle:
- names can be directly bound to empty constants
- types are created by union and tuple
- variables have union type, and can be the key for a map
- a tuple of union types creates a larger union type

example:
```
and_true: (x: bool) -> bool is
    and {x, true}
```

example:
```
and: [x: bool, y: bool] -> and{x, y}
and_true: [x: bool] -> and {x, true}
```

example:
```
true == expr(not{false})
and_true = expr([x: bool], and{x, true})
```

principle:
- operator == compares two variables of the same union type, or one variable and a constant, and outputs bool


