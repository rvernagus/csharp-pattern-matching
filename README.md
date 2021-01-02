# csharp-pattern-matching
A guide to all C# pattern matching forms. Each example illustrates a code snippet that can be run in a Jupyter C# notebook.

The result of an expression or a `Console.WriteLine` call will follow the code with `>>`.

### Where can pattern matching be used?
- `switch` statements
- `is` operator
- `switch` expressions

## Introduced in C# 7
___
### `is` Expressions
No output:
```
object input = "1";
if (input is int num)
    Console.WriteLine(num + 1);
```

```
object input = 1;
if (input is int num)
    Console.WriteLine(num + 1);
>> 2
```

### `when` Conditions
```
var aNum = 1;
aNum switch
{
    int n when n < 5           => "small",
    int n when n >= 5 && n < 8 => "medium",
    int n when n >= 8          => "large",
    _                          => "not a number"
}
>> small
```

### Type Patterns
```
object value = DateTime.Now;
value switch
{
    string s => "it's a string!",
    int i    => "it's an int!",
    _        => "it's something else!"
}
>> it's something else!
```

## Introduced in C# 8
___
### `is` Patterns Extended to Test Expressions Against Patterns
```
var d = DateTime.UtcNow;
if (d is { Kind: DateTimeKind.Utc })
{
    Console.WriteLine("UTC DateTime");
}
else
{
    Console.WriteLine("Not UTC DateTime");
}
>> UTC DateTime
```

### Property Patterns
```
var d = DateTime.UtcNow;
d switch
{
    { Year: 2020 } => "current year",
    { Year: 2019 } => "previous year",
    _              => "too far past or future"
}
>> current year
```

### Declaration Patterns
```
object o = 1;
if (o is int i)
{
    Console.WriteLine($"int of {i}");
}
else
{
    Console.WriteLine("o is either null or non-int");
}
>> int of 1
```
```
int? o = null;
if (o is int i)
{
    Console.WriteLine($"int of {i}");
}
else
{
    Console.WriteLine("o is either null or non-int");
}
>> o is either null or non-int
```

### Constant Patterns
```
var bits = (0, 1);
var result = bits switch
{
    (0, 0)           => false,
    (0, 1) or (1, 0) => true,
    (1, 1)           => true,
    _                => false
};

Console.WriteLine(result);
>> True
```

### Positional Patterns
```
var newState = (GetState(), action, hasKey) switch
{
        (DoorState.Closed, Action.Open, _) => DoorState.Opened,
        (DoorState.Opened, Action.Close, _) => DoorState.Closed,
        (DoorState.Closed, Action.Lock, true) => DoorState.Locked,
        (DoorState.Locked, Action.Unlock, true) => DoorState.Closed,
        (var state, _, _) => state
};
```

### Property Patterns
```
object o = "123";
o switch
{
    string { Length: 1 } s => "length 1 string",
    string { Length: 2 } s => "length 2 string",
    string { Length: 3 } s => "length 3 string",
    int i                  => "an int",
    _                      => "null or not a string",
}
> length 3 string
```
