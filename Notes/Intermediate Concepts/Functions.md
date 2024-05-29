# Functions

Functions are the building blocks of Elixir programs. They encapsulate behavior and allow for code reuse. In Elixir, functions come in two flavors: anonymous functions and named functions. Understanding how to define and use these functions, along with advanced features like recursion, higher-order functions, and pattern matching in function heads, is crucial for effective Elixir programming.

---
### Anonymous Functions

Anonymous functions in Elixir are functions that are not bound to a name. They are often used for short-lived operations or passed as arguments to higher-order functions.

1. **Defining Anonymous Functions**: 
    - Use the `fn` keyword to define an anonymous function.
    - Use `->` to separate the function's parameters from its body.
    - Call an anonymous function using the `.` operator.
    
    ```elixir
    add = fn a, b -> a + b end
    add.(1, 2)  # 3
    ```

    We can also define multi-clause anonymous functions:

    ```elixir
    multiply = fn
      0, _ -> 0
      _, 0 -> 0
      a, b -> a * b
    end

    multiply.(2, 3)  # 6
    multiply.(0, 5)  # 0
    ```

2. **Shortened Syntax**:
    - Use the capture operator (`&`) for a more concise function definition.
    
    ```elixir
    add = &(&1 + &2)
    add.(1, 2)  # 3
    ```

### Named Functions

Named functions are defined within modules and are typically used for more complex or reusable operations.

1. **Defining Named Functions**:
    - Use the `defmodule` keyword to define a module.
    - Use the `def` keyword to define a named function within the module.
    
    ```elixir
    defmodule Math do
      def add(a, b) do
        a + b
      end
    end

    Math.add(1, 2)  # 3
    ```

2. **Function Arity**:
    - Arity refers to the number of arguments a function takes.
    - In Elixir, functions are uniquely identified by their name and arity.
    
    ```elixir
    defmodule Math do
      def add(a, b), do: a + b
      def add(a, b, c), do: a + b + c
    end

    Math.add(1, 2)     # 3
    Math.add(1, 2, 3)  # 6
    ```

3. **Private Functions**:
    - Private functions are only accessible within the module they are defined in.
    - Use the `defp` keyword to define a private function.
    
    ```elixir
    defmodule Secret do
      def public_function do
        private_function()
      end

      defp private_function do
        "This is private"
      end
    end

    Secret.public_function()  # "This is private"
    Secret.private_function()  # ** (UndefinedFunctionError)
    ```

### Pattern Matching in Function Heads

Pattern matching in function heads allows for elegant and expressive function definitions that handle different cases.

1. **Basic Pattern Matching**:
    ```elixir
    defmodule Greeter do
      def greet({:ok, name}), do: "Hello, #{name}!"
      def greet({:error, reason}), do: "Error: #{reason}"
    end

    Greeter.greet({:ok, "Alice"})   # "Hello, Alice!"
    Greeter.greet({:error, :not_found})  # "Error: not_found"
    ```

2. **Using Guards**:
    - Guards provide additional checks for pattern matches.
    - Use the `when` keyword to define guards.
    
    ```elixir
    defmodule NumberChecker do
      def check_number(x) when is_integer(x) and x > 0 do
        "#{x} is a positive integer"
      end

      def check_number(x) when is_integer(x) and x < 0 do
        "#{x} is a negative integer"
      end

      def check_number(_), do: "Not an integer"
    end

    NumberChecker.check_number(5)  # "5 is a positive integer"
    NumberChecker.check_number(-3) # "-3 is a negative integer"
    NumberChecker.check_number(0.5) # "Not an integer"
    ```

### Higher-Order Functions

Higher-order functions are functions that take other functions as arguments or return functions as results. They are a hallmark of functional programming and are used extensively in Elixir.

1. **Passing Functions as Arguments**:
    ```elixir
    defmodule ListHelper do
      def apply_to_all(list, func) do
        Enum.map(list, func)
      end
    end

    ListHelper.apply_to_all([1, 2, 3], fn x -> x * 2 end)  # [2, 4, 6]
    ListHelper.apply_to_all([1, 2, 3], &(&1 + 1))  # [2, 3, 4]
    ```

2. **Returning Functions**:
    ```elixir
    defmodule Greeter do
      def greeter(name) do
        fn -> "Hello, #{name}!" end
      end
    end

    greet = Greeter.greeter("Alice")
    greet.()  # "Hello, Alice!"
    ```

### Recursion

Recursion is a fundamental concept in Elixir and functional programming. Instead of using loops, Elixir relies on recursion for repetitive tasks.

1. **Basic Recursion**:
    ```elixir
    defmodule Factorial do
      def calculate(0), do: 1
      def calculate(n) when n > 0 do
        n * calculate(n - 1)
      end
    end

    Factorial.calculate(5)  # 120
    ```

2. **Tail Recursion**:
    - Tail recursion is a special case of recursion where the recursive call is the last operation in the function.
    - Elixir optimizes tail-recursive functions to prevent stack overflow.

    ```elixir
    defmodule Factorial do
      def calculate(n), do: calculate(n, 1)

      defp calculate(0, acc), do: acc
      defp calculate(n, acc) when n > 0 do
        calculate(n - 1, acc * n)
      end
    end

    Factorial.calculate(5)  # 120
    ```

### Modules as Function Collections

Modules in Elixir serve as containers for related functions, allowing for better organization and reuse of code.

1. **Defining Modules**:
    ```elixir
    defmodule Math do
      def add(a, b), do: a + b
      def subtract(a, b), do: a - b
    end

    Math.add(3, 4)  # 7
    Math.subtract(10, 5)  # 5
    ```

2. **Using `import`**:
    - Use the `import` keyword to import functions from another module.
    
    ```elixir
    defmodule Calculator do
      import Math

      def calculate, do: add(3, 4)
    end

    Calculator.calculate()  # 7
    ```

3. **Using `alias`**:
    - Use the `alias` keyword to create a shortcut to a module name.
    
    ```elixir
    defmodule MyApp do
      alias Math, as: M

      def run, do: M.add(5, 6)
    end

    MyApp.run()  # 11
    ```

>> Functions are at the heart of Elixir programming. From anonymous functions for short-lived operations to named functions for reusable logic, pattern matching, higher-order functions, and recursion, Elixir provides powerful tools to write clean and expressive code. Mastering these concepts will help leverage the full potential of Elixir and build efficient, maintainable applications.

---
