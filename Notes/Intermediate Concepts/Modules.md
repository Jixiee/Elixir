
# Modules

Hey there! Let's dive into one of the core concepts in Elixir: modules. Think of modules as containers that group related functions together. They help us organize our code, making it easier to read, maintain, and reuse. In this section, I'll walk you through everything you need to know about modules in Elixir.

---
### What is a Module?

In Elixir, a module is a way to encapsulate functions and other definitions, such as macros and structs. By grouping related functions into a module, we can keep our code organized and modular.

Here's a basic example of a module:

```elixir
defmodule Math do
  def add(a, b) do
    a + b
  end

  def subtract(a, b) do
    a - b
  end
end
```

In this example, the `Math` module contains two functions: `add/2` and `subtract/2`. Now, whenever we need to perform these operations, we can call them through the `Math` module.

```elixir
Math.add(3, 4)      # 7
Math.subtract(10, 5) # 5
```

### Naming Conventions

Modules in Elixir are usually named using PascalCase. This means that each word in the module name starts with a capital letter, and there are no underscores between words. For example: `MyApp`, `UserProfile`, `OrderProcessor`.

### Organizing Code with Modules

Modules help us structure our code into logical units. For instance, in a web application, you might have modules for handling user accounts, orders, and payments:

```elixir
defmodule UserAccount do
  def create(user), do: # Implementation
  def delete(user), do: # Implementation
end

defmodule Order do
  def place(order), do: # Implementation
  def cancel(order), do: # Implementation
end

defmodule Payment do
  def process(payment), do: # Implementation
  def refund(payment), do: # Implementation
end
```

This way, each module is responsible for a specific part of your application, making the code easier to navigate and maintain.

### Nesting Modules

Elixir supports nested modules, allowing us to create hierarchical structures. This is useful for further organizing related functionality.

```elixir
defmodule MyApp.Accounts do
  defmodule User do
    def create(params), do: # Implementation
    def delete(user), do: # Implementation
  end

  defmodule Admin do
    def create(params), do: # Implementation
    def delete(admin), do: # Implementation
  end
end
```

We can access the functions in nested modules like this:

```elixir
MyApp.Accounts.User.create(%{name: "Alice"})
MyApp.Accounts.Admin.create(%{name: "Admin"})
```

### Module Attributes

Modules can have attributes, which are used to store metadata. The most common module attribute is `@moduledoc`, which provides documentation for the module.

```elixir
defmodule Math do
  @moduledoc """
  A module for basic arithmetic operations.
  """

  @doc """
  Adds two numbers.
  """
  def add(a, b), do: a + b

  @doc """
  Subtracts the second number from the first.
  """
  def subtract(a, b), do: a - b
end
```

We can access these docs in IEx (Interactive Elixir) using the `h` helper:

```elixir
h Math
```

### Importing, Alias, and Require

Elixir provides mechanisms to bring functions from other modules into the current module's scope. These are `import`, `alias`, and `require`.

1. **Import**: Use `import` to bring functions or macros from another module into the current module's namespace.

    ```elixir
    defmodule Main do
      import Math

      def do_math do
        add(1, 2)  # We can call add/2 directly
      end
    end
    ```

2. **Alias**: Use `alias` to create a shortcut for a module name.

    ```elixir
    defmodule Main do
      alias MyApp.Accounts.User, as: User

      def create_user(params) do
        User.create(params)  # We can use User instead of MyApp.Accounts.User
      end
    end
    ```

3. **Require**: Use `require` to ensure a module is compiled and available, typically for macros.

    ```elixir
    defmodule Main do
      require Logger

      def log_message(message) do
        Logger.info(message)
      end
    end
    ```

### Using Modules in IEx

Working with modules in IEx is straightforward. We can compile and use our modules directly in the interactive shell.

1. **Compile a Module**: Save the module to a file (e.g., `math.ex`) and compile it in IEx.

    ```elixir
    c("math.ex")
    ```

2. **Call Functions**: After compiling, we can call the functions defined in your module.

    ```elixir
    Math.add(2, 3)  # 5
    ```

### Structs

Modules can also define structs, which are special maps with a defined set of keys and default values. Structs are used to represent structured data.

```elixir
defmodule User do
  defstruct name: "", age: 0
end

# Creating a struct
user = %User{name: "Alice", age: 30}
user.name  # "Alice"
user.age   # 30
```

### Module Documentation

It's a good practice to document our modules and functions using `@moduledoc` and `@doc` attributes. This helps others understand what our code does.

```elixir
defmodule Math do
  @moduledoc """
  A module for basic arithmetic operations.
  """

  @doc """
  Adds two numbers.
  ## Examples

      iex> Math.add(2, 3)
      5

  """
  def add(a, b), do: a + b
end
```
>> Modules are essential in Elixir for organizing and structuring our code. They allow us to group related functions, create nested structures, and encapsulate logic in a clean and maintainable way. By using attributes for documentation and understanding how to import, alias, and require other modules, we can write clear and concise Elixir code. 
---
