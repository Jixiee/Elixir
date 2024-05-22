# Basic Syntax
Understanding the basic syntax of Elixir is crucial for getting started with the language. This section covers the fundamental elements of Elixir's syntax, including variables, data types, operators, and more.

---
### Variables

In Elixir, variables are bound to values using the `=` operator. Variable names are typically written in snake_case.

```elixir
name = "Alice"
age = 30
```

Variables in Elixir are immutable, meaning once a variable is bound to a value, it cannot be changed. However, you can rebind the variable to a new value.

```elixir
x = 1
x = 2  # x is now bound to 2
```

### Data Types

Elixir provides several basic data types:

1. **Integers**: Whole numbers.
    ```elixir
    int = 42
    ```

2. **Floats**: Numbers with decimal points.
    ```elixir
    float = 3.14
    ```

3. **Atoms**: Constants where their name is their value, often used as identifiers.
    ```elixir
    atom = :hello
    ```

4. **Booleans**: `true` and `false`, which are actually atoms.
    ```elixir
    is_valid = true
    ```

5. **Strings**: Enclosed in double quotes.
    ```elixir
    string = "Hello, world!"
    ```

6. **Lists**: Ordered collections of values.
    ```elixir
    list = [1, 2, 3]
    ```

7. **Tuples**: Fixed-size collections of values.
    ```elixir
    tuple = {:ok, "Success"}
    ```

### Operators

Elixir supports a variety of operators:

1. **Arithmetic Operators**:
    ```elixir
    addition = 1 + 2
    subtraction = 5 - 3
    multiplication = 4 * 2
    division = 8 / 2   # returns a float
    integer_division = div(8, 2)   # returns an integer
    remainder = rem(8, 3)
    ```

2. **Boolean Operators**:
    ```elixir
    and_operator = true and false
    or_operator = true or false
    not_operator = not true
    ```

3. **Comparison Operators**:
    ```elixir
    equal = 1 == 1
    not_equal = 1 != 2
    greater_than = 3 > 2
    less_than = 2 < 3
    greater_or_equal = 3 >= 2
    less_or_equal = 2 <= 3
    ```
    
### Strings and String Interpolation

Strings are enclosed in double quotes, and string interpolation is done using `#{}`.

```elixir
name = "Alice"
greeting = "Hello, #{name}!"  # "Hello, Alice!"
```

Multiline strings can be created using triple double quotes.

```elixir
multi_line_string = """
This is a
multiline string.
"""
```

### Lists and Tuples

Lists and tuples are fundamental data structures in Elixir.

1. **Lists**: Ordered collections that can hold elements of different types.
    ```elixir
    list = [1, 2, 3, "four", :five]
    ```
    Lists support various operations like concatenation and subtraction.
    ```elixir
    list1 = [1, 2, 3]
    list2 = [4, 5, 6]
    combined_list = list1 ++ list2  # [1, 2, 3, 4, 5, 6]
    reduced_list = combined_list -- [2, 5]  # [1, 3, 4, 6]
    ```

2. **Tuples**: Fixed-size collections, often used to group related values.
    ```elixir
    tuple = {:ok, "Success", 42}
    ```
    Access tuple elements using pattern matching or the `elem` function.
    ```elixir
    {:ok, message, code} = tuple
    message  # "Success"
    elem(tuple, 1)  # "Success"
    ```

### Pattern Matching

Pattern matching is a powerful feature in Elixir, used to match values against patterns.

```elixir
# Matching on simple values
{x, y} = {1, 2}
# x = 1, y = 2

# Matching in function arguments
defmodule Math do
  def add({a, b}) do
    a + b
  end
end

Math.add({1, 2})  # 3
```

### Control Structures

Elixir provides several control structures for flow control.

1. **if and unless**: Conditional execution.
    ```elixir
    if true do
      "This will run"
    else
      "This won't run"
    end

    unless false do
      "This will run"
    end
    ```

2. **case**: Pattern matching on multiple conditions.
    ```elixir
    case {1, 2, 3} do
      {1, x, 3} -> "Matched with x = #{x}"
      _ -> "No match"
    end
    ```

3. **cond**: Multiple condition evaluation.
    ```elixir
    cond do
      2 + 2 == 5 -> "This is false"
      2 * 2 == 4 -> "This is true"
      true -> "This will always run as a fallback"
    end
    ```

4. **with**: Used for chaining expressions that depend on pattern matching.
    ```elixir
    user = %{name: "Alice", age: 30}

    with {:ok, name} <- Map.fetch(user, :name),
         {:ok, age} <- Map.fetch(user, :age) do
      "Name: #{name}, Age: #{age}"
    else
      _ -> "User data is incomplete"
    end
    ```

>>> This overview of Elixir's basic syntax provides the foundational knowledge you need to start writing Elixir code. By understanding variables, data types, operators, pattern matching, and control structures, you are well-equipped to explore more advanced topics and build your first Elixir applications.

---
