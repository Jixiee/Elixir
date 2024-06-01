# Concurrency

Elixir is built on the Erlang VM, which has been designed from the ground up to support highly concurrent and distributed systems. This makes Elixir an excellent choice for building scalable and fault-tolerant applications.

---
### Processes

In Elixir, processes are lightweight and isolated units of computation. They are not OS-level processes but rather run within the Erlang VM, making them incredibly lightweight and efficient to create and manage. Processes in Elixir are the foundation of its concurrency model.

1. **Spawning Processes**: You can create a new process using the `spawn` function.

    ```elixir
    spawn(fn -> IO.puts("Hello from a new process!") end)
    ```

    This will print "Hello from a new process!" to the console from a new process. The `spawn` function returns a process identifier (PID), which you can use to interact with the process.

    ```elixir
    pid = spawn(fn -> IO.puts("Process PID: #{inspect(self())}") end)
    ```

2. **Process Communication**: Processes communicate with each other using message passing. You can send a message to a process using the `send` function and receive messages using the `receive` block.

    ```elixir
    send(pid, {:hello, "world"})

    receive do
      {:hello, msg} -> IO.puts("Received message: #{msg}")
    end
    ```

3. **Self PID**: Each process has a unique PID, and you can get the PID of the current process using `self()`.

    ```elixir
    pid = self()
    IO.puts("Current process PID: #{inspect(pid)}")
    ```

### Message Passing

Message passing is the primary way processes communicate in Elixir. This approach ensures that processes remain isolated and only share data explicitly through messages, which helps prevent many common concurrency issues.

1. **Sending and Receiving Messages**:

    ```elixir
    defmodule Messenger do
      def send_message(pid, message) do
        send(pid, message)
      end

      def receive_message do
        receive do
          msg -> IO.puts("Received: #{inspect(msg)}")
        after
          5000 -> IO.puts("No message received in 5 seconds")
        end
      end
    end

    pid = spawn(Messenger, :receive_message, [])
    Messenger.send_message(pid, {:hello, "Elixir"})
    ```

    In this example, the `Messenger` module has functions to send and receive messages. The `receive` block can pattern match on different message formats and includes an `after` clause to handle cases where no message is received within a specified time.

### Task Module

Elixir provides the `Task` module to simplify working with concurrent processes. Tasks are great for short-lived concurrent activities.

1. **Using Task for Asynchronous Work**:

    ```elixir
    task = Task.async(fn -> 1 + 2 end)
    result = Task.await(task)
    IO.puts("Result: #{result}")
    ```

    The `Task.async` function starts a new process to execute the given function and returns a task struct. You can then use `Task.await` to block until the task completes and get the result.

2. **Task with Multiple Concurrent Operations**:

    ```elixir
    task1 = Task.async(fn -> :timer.sleep(1000); 1 + 1 end)
    task2 = Task.async(fn -> :timer.sleep(2000); 2 + 2 end)

    results = [Task.await(task1), Task.await(task2)]
    IO.inspect(results)  # [2, 4]
    ```

    This example demonstrates running multiple tasks concurrently. The tasks sleep for different durations and then return their results.

### Agents

Agents provide a simple way to manage state in Elixir. They allow you to create a process that maintains state and can be updated or read asynchronously.

1. **Creating and Using Agents**:

    ```elixir
    {:ok, agent} = Agent.start(fn -> %{} end)

    Agent.update(agent, fn state -> Map.put(state, :key, "value") end)
    value = Agent.get(agent, fn state -> Map.get(state, :key) end)

    IO.puts("Value: #{value}")
    ```

    In this example, an agent is started with an initial state of an empty map. The `Agent.update` function modifies the state, and the `Agent.get` function retrieves a value from the state.

2. **Stopping Agents**:

    ```elixir
    Agent.stop(agent)
    ```

    Stopping an agent will terminate the process, freeing up resources.

### GenServer

For more complex stateful processes and behaviors, Elixir provides the `GenServer` module. A GenServer is a generic server process that follows a standard set of conventions, making it easier to build and understand concurrent applications.

1. **Creating a GenServer**:

    ```elixir
    defmodule Counter do
      use GenServer

      # Client API

      def start_link(initial_value) do
        GenServer.start_link(__MODULE__, initial_value, name: __MODULE__)
      end

      def increment do
        GenServer.call(__MODULE__, :increment)
      end

      def get do
        GenServer.call(__MODULE__, :get)
      end

      # Server (callbacks)

      @impl true
      def init(initial_value) do
        {:ok, initial_value}
      end

      @impl true
      def handle_call(:increment, _from, state) do
        {:reply, state + 1, state + 1}
      end

      @impl true
      def handle_call(:get, _from, state) do
        {:reply, state, state}
      end
    end
    ```

    In this example, we define a `Counter` GenServer with functions to start the server, increment the counter, and get the current value. The `handle_call` callbacks handle synchronous messages sent to the server.

2. **Using the GenServer**:

    ```elixir
    Counter.start_link(0)
    Counter.increment()
    current_value = Counter.get()

    IO.puts("Current counter value: #{current_value}")
    ```

    This code starts the GenServer with an initial value of 0, increments the counter, and retrieves the current value.

>> Concurrency is a fundamental aspect of Elixir, enabling you to build scalable and fault-tolerant applications. By leveraging lightweight processes, message passing, and powerful abstractions like Tasks, Agents, and GenServers, you can manage concurrent operations effectively. Understanding these concurrency primitives and patterns will help you harness the full potential of Elixir's concurrency model. 

---
