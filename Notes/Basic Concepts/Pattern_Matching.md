# Pattern Matching

Pattern matching is one of the most powerful features in Elixir, allowing for concise and expressive code. It is used extensively in variable binding, control structures, and function definitions. This will cover the basics of pattern matching, including its syntax, usage, and common patterns.

---
### Basics of Pattern Matching

In Elixir, the `=` operator is used for pattern matching. Instead of being an assignment operator, it matches the value on the right side to the pattern on the left side.

1. **Simple Matching**:
    ```elixir
    x = 1  # x is bound to 1
    1 = x  # This matches because x is 1

    {a, b} = {1, 2}  # a is bound to 1, b is bound to 2
    ```

2. **Mismatch**:
    ```elixir
    2 = x  # This will cause a MatchError because x is 1
    ```

### Matching Complex Data Structures

Pattern matching can be used with more complex data structures like tuples, lists, and maps.

1. **Tuples**:
    ```elixir
    {status, value} = {:ok, 42}
    # status is :ok, value is 42

    {:ok, result} = {:ok, 42}  # This matches
    {:error, _reason} = {:error, :not_found}  # This matches, _reason is :not_found
    ```

2. **Lists**:
    ```elixir
    [head | tail] = [1, 2, 3]
    # head is 1, tail is [2, 3]

    [first, second | rest] = [10, 20, 30, 40]
    # first is 10, second is 20, rest is [30, 40]
    ```

3. **Maps**:
    ```elixir
    %{key: value} = %{key: "value"}
    # value is "value"

    %{name: name, age: age} = %{name: "Alice", age: 30}
    # name is "Alice", age is 30
    ```

### Pattern Matching in Function Definitions

Pattern matching is often used in function definitions to execute different code based on the shape of the input data.

1. **Multiple Function Clauses**:
    ```elixir
    defmodule Math do
      def zero?(0), do: true
      def zero?(_), do: false
    end

    Math.zero?(0)  # true
    Math.zero?(1)  # false
    ```

2. **Pattern Matching with Tuples**:
    ```elixir
    defmodule ResultHandler do
      def handle_result({:ok, value}), do: "Success: #{value}"
      def handle_result({:error, reason}), do: "Error: #{reason}"
    end

    ResultHandler.handle_result({:ok, 42})  # "Success: 42"
    ResultHandler.handle_result({:error, :not_found})  # "Error: not_found"
    ```

### Pattern Matching with Case

The `case` construct allows pattern matching against multiple patterns in a concise way.

1. **Basic Case Matching**:
    ```elixir
    case {1, 2, 3} do
      {4, 5, 6} -> "This won't match"
      {1, x, 3} -> "This will match and bind x to 2"
      _ -> "This is the default case"
    end
    ```

2. **Complex Case Matching**:
    ```elixir
    case {1, 2, 3} do
      {1, x, 3} when x > 1 -> "Matched with guard"
      _ -> "Default case"
    end
    ```

### Pattern Matching with `cond`

The `cond` construct is used to evaluate multiple conditions and execute the first one that returns true.

1. **Using cond**:
    ```elixir
    cond do
      2 + 2 == 5 -> "This is not true"
      2 * 2 == 3 -> "This is also not true"
      1 + 1 == 2 -> "This is true"
      true -> "This will always be executed as a fallback"
    end
    ```

### Pattern Matching with `with`

The `with` construct is useful for chaining multiple pattern matches together in a sequence.

1. **Using with**:
    ```elixir
    user = %{name: "Alice", age: 30}

    with {:ok, name} <- Map.fetch(user, :name),
         {:ok, age} <- Map.fetch(user, :age) do
      "Name: #{name}, Age: #{age}"
    else
      :error -> "Key not found"
    end
    ```

### The Pin Operator (`^`)

The pin operator (`^`) is used to match against the value of an existing variable, rather than rebinding it.

1. **Using the Pin Operator**:
    ```elixir
    x = 1
    ^x = 1  # This matches because x is 1

    list = [1, 2, 3]
    [^x, 2, 3] = list  # This matches because x is 1 and list starts with 1
    ```

### Pattern Matching in `for` Comprehensions

Pattern matching can be used in list comprehensions to filter and transform elements.

1. **Using Pattern Matching in Comprehensions**:
    ```elixir
    list = [{:ok, 1}, {:error, :not_found}, {:ok, 2}]
    for {:ok, value} <- list, do: value
    # [1, 2]
    ```

>> Pattern matching is a versatile and expressive feature in Elixir that simplifies code and makes it more readable. By understanding and using pattern matching, we can write more concise and powerful Elixir code. This feature is not only useful for variable assignment but also for control flow and function definitions, making it a cornerstone of idiomatic Elixir programming.

---
