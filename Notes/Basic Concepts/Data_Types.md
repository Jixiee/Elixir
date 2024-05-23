
# Data Types

Elixir has a rich set of data types that allow developers to handle a variety of programming tasks. Understanding these data types is essential for writing effective Elixir code. This section covers the primary data types in Elixir, including their characteristics and usage.

---
### Atoms

Atoms are constants where their name is their value. They are often used to represent fixed values, like identifiers or keys.

- **Syntax**: Atoms are prefixed with a colon (`:`).
- **Examples**:
  ```elixir
  :ok
  :error
  :foo
  ```

Atoms are unique, and each atom is stored only once in memory, making them very efficient for comparison operations.

### Numbers

Elixir supports two types of numbers: integers and floats.

1. **Integers**: Whole numbers, which can be positive or negative.
    - **Syntax**: Written as regular numbers.
    - **Examples**:
      ```elixir
      42
      -7
      0
      ```
    - **Binary, Octal, Hexadecimal**:
      ```elixir
      0b1010  # binary
      0o1234  # octal
      0x1F4   # hexadecimal
      ```

2. **Floats**: Numbers with a decimal point.
    - **Syntax**: Written with a decimal point.
    - **Examples**:
      ```elixir
      3.14
      -0.5
      0.0
      ```

### Booleans

Booleans in Elixir are a special type of atom. They represent truth values and are used in conditional expressions.

- **Values**:
  ```elixir
  true
  false
  ```

Booleans are just atoms:
```elixir
is_atom(true)  # true
is_atom(false)  # true
```

### Strings

Strings are sequences of Unicode characters enclosed in double quotes. Elixir strings are UTF-8 encoded.

- **Syntax**: Enclosed in double quotes.
- **Examples**:
  ```elixir
  "Hello, world!"
  "Elixir is fun!"
  ```

String interpolation and concatenation:
- **Interpolation**:
  ```elixir
  name = "Alice"
  "Hello, #{name}!"
  ```
- **Concatenation**:
  ```elixir
  "Hello, " <> "world!"
  ```

Multiline strings:
- **Multiline**:
  ```elixir
  """
  This is a
  multiline string.
  """
  ```

### Lists

Lists are ordered collections of elements. They can contain elements of different types and are implemented as linked lists.

- **Syntax**: Enclosed in square brackets.
- **Examples**:
  ```elixir
  [1, 2, 3]
  ["a", "b", "c"]
  [1, "two", :three]
  ```

List operations:
- **Concatenation**:
  ```elixir
  [1, 2] ++ [3, 4]  # [1, 2, 3, 4]
  ```
- **Subtraction**:
  ```elixir
  [1, 2, 3] -- [2]  # [1, 3]
  ```
- **Head and Tail**:
  ```elixir
  hd([1, 2, 3])  # 1
  tl([1, 2, 3])  # [2, 3]
  ```

### Tuples

Tuples are ordered collections of elements with a fixed size. They are typically used to group a fixed number of elements together.

- **Syntax**: Enclosed in curly braces.
- **Examples**:
  ```elixir
  {:ok, "Success"}
  {1, 2, 3}
  {"Alice", 30, :female}
  ```

Tuple operations:
- **Element Access**:
  ```elixir
  elem({:ok, "Success"}, 1)  # "Success"
  ```
- **Tuple Size**:
  ```elixir
  tuple_size({1, 2, 3})  # 3
  ```

### Maps

Maps are collections of key-value pairs. They provide constant-time access to keys.

- **Syntax**: Enclosed in `%{}` with key-value pairs separated by `=>` or `:`.
- **Examples**:
  ```elixir
  %{:a => 1, :b => 2}
  %{"name" => "Alice", "age" => 30}
  %{a: 1, b: 2}  # shorthand syntax for atom keys
  ```

Map operations:
- **Accessing Values**:
  ```elixir
  map = %{"name" => "Alice", "age" => 30}
  map["name"]  # "Alice"
  ```
- **Updating Values**:
  ```elixir
  map = %{:a => 1, :b => 2}
  %{map | :a => 3}  # %{:a => 3, :b => 2}
  ```

### Keyword Lists

Keyword lists are lists of tuples where the first element of each tuple is an atom. They are often used for passing options to functions.

- **Syntax**: List of tuples with atom keys.
- **Examples**:
  ```elixir
  [a: 1, b: 2]
  [name: "Alice", age: 30]
  ```

Keyword lists are ordered and allow duplicate keys:
```elixir
kw = [a: 1, a: 2]
```

### Binaries

Binaries are sequences of bytes. They are used to store raw binary data.

- **Syntax**: Enclosed in `<<>>`.
- **Examples**:
  ```elixir
  <<1, 2, 3>>
  <<255, 256::size(16)>>
  ```

### References

References are unique values created with the `make_ref/0` function. They are mainly used to generate unique identifiers.

- **Example**:
  ```elixir
  ref = make_ref()
  ```

### Functions

Functions in Elixir are first-class citizens. They can be anonymous or named, and they can be passed as arguments to other functions.

- **Anonymous Functions**:
  ```elixir
  add = fn a, b -> a + b end
  add.(1, 2)  # 3
  ```

- **Named Functions** (defined within modules):
  ```elixir
  defmodule Math do
    def add(a, b) do
      a + b
    end
  end

  Math.add(1, 2)  # 3
  ```
---
