# Control Structures

Control structures are fundamental to programming, enabling us to dictate the flow of execution within our program based on certain conditions. Elixir provides several control structures that are both powerful and expressive. This section covers the key control structures in Elixir, including conditionals, case expressions, cond expressions, and the with construct.

---
### if and unless

The `if` and `unless` constructs are used for basic conditional execution.

1. **if**: Executes the block if the condition is true.
    ```elixir
    if true do
      "This will execute"
    else
      "This won't execute"
    end
    ```

2. **unless**: Executes the block if the condition is false.
    ```elixir
    unless false do
      "This will execute"
    else
      "This won't execute"
    end
    ```

We can also use inline conditionals:
```elixir
result = if true, do: "This will execute", else: "This won't execute"
```

### case

The `case` construct is used for pattern matching against multiple conditions. It allows for branching logic based on the shape and content of data.

1. **Basic Case Expression**:
    ```elixir
    case {1, 2, 3} do
      {4, 5, 6} -> "This won't match"
      {1, x, 3} -> "This will match and bind x to 2"
      _ -> "This is the default case"
    end
    ```

2. **Using Guards**: Guards are additional conditions specified using the `when` keyword.
    ```elixir
    case {1, 2, 3} do
      {1, x, 3} when x > 1 -> "Matched with guard"
      _ -> "Default case"
    end
    ```

### cond

The `cond` construct is used to evaluate multiple conditions sequentially and execute the first block where the condition is true. It is similar to a series of `if` and `else if` statements in other languages.

1. **Using cond**:
    ```elixir
    cond do
      2 + 2 == 5 -> "This is not true"
      2 * 2 == 3 -> "This is also not true"
      1 + 1 == 2 -> "This is true"
      true -> "This will always be executed as a fallback"
    end
    ```

Each condition is evaluated in order, and the block associated with the first true condition is executed. The last condition is typically `true` to act as a default case.

### with

The `with` construct is useful for chaining multiple pattern matches together in a sequence, especially when each step depends on the previous one. It simplifies code that would otherwise require nested case expressions or complex logic.

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

In the `with` construct:
- Each pattern match is tried sequentially.
- If all matches succeed, the do block is executed.
- If any match fails, the else block is executed.

### case, cond, and with Comparison

Understanding when to use `case`, `cond`, and `with` is crucial for writing clear and idiomatic Elixir code:

- **case**: Use when we need to match against specific patterns and potentially bind variables.
    ```elixir
    case my_var do
      :ok -> "It's ok"
      :error -> "It's an error"
      _ -> "It's something else"
    end
    ```

- **cond**: Use when we have multiple conditions that need to be evaluated one after another.
    ```elixir
    cond do
      condition1 -> "Handle condition1"
      condition2 -> "Handle condition2"
      true -> "Handle default case"
    end
    ```

- **with**: Use when we have a sequence of operations that depend on successful pattern matches.
    ```elixir
    with {:ok, result1} <- operation1(),
         {:ok, result2} <- operation2(result1) do
      {:ok, result2}
    else
      error -> error
    end
    ```

### The Pin Operator (`^`)

The pin operator (`^`) is used in patterns to match against the value of an existing variable rather than rebinding the variable.

1. **Using the Pin Operator**:
    ```elixir
    x = 1
    ^x = 1  # This matches because x is 1

    list = [1, 2, 3]
    [^x, 2, 3] = list  # This matches because x is 1 and list starts with 1
    ```

### Loops with Recursion

Elixir does not have traditional loop constructs like `for` or `while` loops found in other languages. Instead, recursion is used for looping. The `Enum` and `Stream` modules provide higher-level abstractions for working with collections.

1. **Recursion**:
    ```elixir
    defmodule Loop do
      def print_times(0), do: :done
      def print_times(n) when n > 0 do
        IO.puts("Hello!")
        print_times(n - 1)
      end
    end

    Loop.print_times(3)
    ```

2. **Using Enum Module**:
    ```elixir
    Enum.each(1..3, fn _ -> IO.puts("Hello!") end)
    ```

Elixir's control structures provide a flexible and expressive way to handle conditional logic and flow control in our programs. By mastering `if`, `unless`, `case`, `cond`, and `with`, as well as understanding the use of recursion for looping, we can write clear, concise, and maintainable Elixir code.

---
