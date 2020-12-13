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
