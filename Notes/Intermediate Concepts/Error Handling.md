
# Error Handling
Elixir, inheriting its philosophy from Erlang, has a unique approach to error handling that promotes the development of fault-tolerant systems. 

---
### The Philosophy: Let It Crash

One of the key philosophies in Elixir (borrowed from Erlang) is "let it crash." This means that instead of trying to prevent errors from happening, we often let processes crash and rely on supervisors to restart them. This approach simplifies error handling and leads to more robust systems.

### try/catch/after

Elixir provides the `try/catch/after` construct for handling errors explicitly. This is useful when you need to perform cleanup actions or handle specific error cases.

1. **Basic try/catch**:

    ```elixir
    try do
      1 / 0
    rescue
      ArithmeticError -> IO.puts("Caught an arithmetic error!")
    end
    ```

    In this example, dividing by zero raises an `ArithmeticError`, which we catch and handle by printing a message.

2. **Using after for Cleanup**:

    ```elixir
    try do
      raise "An error occurred"
    rescue
      RuntimeError -> IO.puts("Caught a runtime error!")
    after
      IO.puts("This is printed no matter what")
    end
    ```

    The `after` block is executed regardless of whether an error occurred, making it perfect for cleanup actions.

3. **catch for Throwing**:

    ```elixir
    try do
      throw(:error)
    catch
      :throw, :error -> IO.puts("Caught a thrown error!")
    end
    ```

    The `catch` block can handle errors thrown with `throw/1`.

### Pattern Matching for Error Handling

Pattern matching is a powerful feature in Elixir, and it can be used effectively for error handling. Many Elixir functions return `{:ok, result}` or `{:error, reason}` tuples, which can be easily pattern matched.

1. **Basic Pattern Matching**:

    ```elixir
    case File.read("nonexistent_file.txt") do
      {:ok, content} -> IO.puts("File content: #{content}")
      {:error, reason} -> IO.puts("Failed to read file: #{reason}")
    end
    ```

    Here, we attempt to read a file. If the file doesn't exist, the function returns `{:error, reason}`, which we handle appropriately.

2. **With Clauses**:

    ```elixir
    with {:ok, file} <- File.open("nonexistent_file.txt"),
         {:ok, content} <- File.read(file) do
      IO.puts("File content: #{content}")
    else
      {:error, reason} -> IO.puts("Failed to process file: #{reason}")
    end
    ```

    The `with` construct allows for more readable sequential error handling. If any step fails, the `else` block handles the error.

### Custom Error Definitions

Defining custom errors can make your code more readable and manageable. You can define custom error modules using `defexception`.

1. **Defining a Custom Error**:

    ```elixir
    defmodule MyCustomError do
      defexception message: "An error occurred", status: 500
    end

    raise MyCustomError, message: "Something went wrong", status: 404
    ```

    This defines a custom error with a default message and status code.

2. **Rescuing Custom Errors**:

    ```elixir
    try do
      raise MyCustomError, message: "Something went wrong", status: 404
    rescue
      e in MyCustomError -> IO.puts("Caught custom error: #{e.message} with status: #{e.status}")
    end
    ```

    Here, we rescue the custom error and access its fields.

### Supervisors

Supervisors are a cornerstone of Elixir’s fault-tolerance model. They monitor worker processes and restart them if they crash.

1. **Defining a Supervisor**:

    ```elixir
    defmodule MyApp.Supervisor do
      use Supervisor

      def start_link(_init_arg) do
        Supervisor.start_link(__MODULE__, :ok, name: __MODULE__)
      end

      @impl true
      def init(:ok) do
        children = [
          {Task, fn -> loop() end}
        ]

        Supervisor.init(children, strategy: :one_for_one)
      end

      defp loop do
        receive do
          :crash -> raise "crash"
        end

        loop()
      end
    end
    ```

    This supervisor starts a task that runs a loop function. If the task crashes, the supervisor restarts it.

2. **Starting the Supervisor**:

    ```elixir
    {:ok, _sup_pid} = MyApp.Supervisor.start_link(:ok)
    ```

    This starts the supervisor, which in turn starts the worker process.

3. **Strategies**:

    Supervisors support different strategies for restarting children:

    - **:one_for_one**: Restarts the crashed child only.
    - **:one_for_all**: Restarts all children if one crashes.
    - **:rest_for_one**: Restarts the crashed child and any children started after it.

    You can specify the strategy in the supervisor’s `init` function.

    ```elixir
    Supervisor.init(children, strategy: :rest_for_one)
    ```

### Logger

Logging is an essential part of error handling. Elixir’s `Logger` module provides a simple and flexible way to log messages.

1. **Basic Logging**:

    ```elixir
    require Logger

    Logger.info("This is an info message")
    Logger.warn("This is a warning message")
    Logger.error("This is an error message")
    ```

    You can log messages of different severity levels: `debug`, `info`, `warn`, and `error`.

2. **Configuring Logger**:

    You can configure the Logger in your application’s configuration file (`config/config.exs`):

    ```elixir
    config :logger, level: :info
    ```

    This sets the logging level to `info`, so only messages with a severity of `info` or higher are logged.


>> Error handling in Elixir is all about building robust and fault-tolerant applications. By embracing the "let it crash" philosophy, using try/catch/after constructs, leveraging pattern matching, defining custom errors, and utilizing supervisors, you can effectively manage errors in your Elixir applications. Logging with the Logger module also plays a crucial role in monitoring and debugging. With these tools and techniques, you'll be well-equipped to handle any errors that come your way, ensuring your applications are resilient and maintainable.

---
