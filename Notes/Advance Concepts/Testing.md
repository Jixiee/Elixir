
# Testing
Testing is a crucial aspect of software development that ensures our code works correctly and helps us catch bugs early. Elixir has robust support for testing through its built-in testing framework, ExUnit. 

---

### Why Testing Matters
Before we get into the nitty-gritty, let's talk about why testing is so important. Testing:
- Ensures the code works as expected.
- Helps catch bugs early, saving time and effort in the long run.
- Provides documentation on how the code is supposed to work.
- Facilitates refactoring by giving the confidence that changes don't break existing functionality.

### Getting Started with ExUnit

ExUnit is Elixir's built-in testing framework. It provides everything we need to write and run tests. Let's start with a basic setup.

1. **Setting Up ExUnit**:

    ExUnit is included with Elixir, so there's no need to install anything extra. To start using it, ensure that `ExUnit.start()` is called in the test helper file (usually `test/test_helper.exs`).

    ```elixir
    ExUnit.start()
    ```

2. **Writing the First Test**:

    Create a new file in the `test` directory, for example, `test/my_module_test.exs`.

    ```elixir
    defmodule MyModuleTest do
      use ExUnit.Case

      test "the truth" do
        assert 1 + 1 == 2
      end
    end
    ```

    This is a simple test case that checks if `1 + 1` equals `2`. We can run our tests with the `mix test` command.

### Basic Assertions

ExUnit provides various assertions to check different conditions in the tests.

1. **Common Assertions**:

    - `assert`: Checks if a condition is true.
    - `refute`: Checks if a condition is false.
    - `assert_raise`: Checks if an exception is raised.

    ```elixir
    test "assertions" do
      assert 1 + 1 == 2
      refute 1 + 1 == 3
      assert_raise ArithmeticError, fn -> 1 / 0 end
    end
    ```

2. **Pattern Matching in Assertions**:

    We can use pattern matching within assertions to check complex conditions.

    ```elixir
    test "pattern matching" do
      assert {:ok, value} = {:ok, 42}
    end
    ```

### Testing with Contexts

Contexts allow us to set up common test data or conditions that multiple tests can share.

1. **Using Setup Callbacks**:

    ```elixir
    defmodule MyModuleTest do
      use ExUnit.Case

      setup do
        {:ok, %{initial_value: 42}}
      end

      test "using context", %{initial_value: value} do
        assert value == 42
      end
    end
    ```

    The `setup` callback runs before each test and the returned value is available to the tests as the context.

### Mocking and Stubbing

In testing, mocking and stubbing are techniques used to simulate parts of our application. Mox is a popular library in Elixir for creating mocks.

1. **Setting Up Mox**:

    Add Mox to the `mix.exs` dependencies:

    ```elixir
    defp deps do
      [
        {:mox, "~> 1.0"}
      ]
    end
    ```

    Run `mix deps.get` to install the dependencies.

2. **Defining Mocks**:

    Define a behaviour and a mock for your module.

    ```elixir
    defmodule MyApp.MyBehaviour do
      @callback my_function(arg :: any()) :: any()
    end

    defmodule MyApp.MyMock do
      use Mox
      defmock(MyApp.MyMock, for: MyApp.MyBehaviour)
    end
    ```

3. **Using Mocks in Tests**:

    ```elixir
    defmodule MyApp.MyModuleTest do
      use ExUnit.Case
      import Mox

      setup :verify_on_exit!

      test "mocking example" do
        MyApp.MyMock
        |> expect(:my_function, fn _ -> :mocked_value end)

        assert MyApp.MyMock.my_function(:arg) == :mocked_value
      end
    end
    ```

    This test sets up an expectation that `my_function/1` will return `:mocked_value` when called.

### Property-Based Testing

Property-based testing allows us to test properties or invariants of our code across a wide range of inputs. StreamData is a library for property-based testing in Elixir.

1. **Setting Up StreamData**:

    Add StreamData to the `mix.exs` dependencies:

    ```elixir
    defp deps do
      [
        {:stream_data, "~> 0.5"}
      ]
    end
    ```

    Run `mix deps.get` to install the dependencies.

2. **Writing Property-Based Tests**:

    ```elixir
    use ExUnitProperties

    property "list concatenation" do
      check all list1 <- list_of(integer()),
                list2 <- list_of(integer()) do
        assert length(list1 ++ list2) == length(list1) + length(list2)
      end
    end
    ```

    This test checks that the length of concatenated lists is the sum of the lengths of the individual lists.

### Testing with Phoenix

If working with a Phoenix application, there are specific tools and conventions for testing controllers, views, channels, and more.

1. **Controller Tests**:

    ```elixir
    defmodule MyAppWeb.PageControllerTest do
      use MyAppWeb.ConnCase

      test "GET /", %{conn: conn} do
        conn = get(conn, "/")
        assert html_response(conn, 200) =~ "Welcome to Phoenix!"
      end
    end
    ```

    This test sends a GET request to the root path and checks if the response contains the expected text.

2. **Channel Tests**:

    ```elixir
    defmodule MyAppWeb.MyChannelTest do
      use MyAppWeb.ChannelCase

      test "ping replies with status ok", %{socket: socket} do
        ref = push(socket, "ping", %{})
        assert_reply ref, :ok, %{"status" => "ok"}
      end
    end
    ```

    This test sends a message to a channel and checks the reply.

### Advanced Testing Techniques
1. **Testing Asynchronous Code**:

    ```elixir
    test "async example" do
      task = Task.async(fn -> :timer.sleep(1000); :done end)
      assert Task.await(task) == :done
    end
    ```

2. **Using Fixtures**:

    Fixtures are reusable pieces of setup code that can be shared across tests.

    ```elixir
    defmodule MyApp.DataCase do
      use ExUnit.CaseTemplate

      using do
        quote do
          alias MyApp.Repo

          import Ecto
          import Ecto.Changeset
          import Ecto.Query
        end
      end

      setup do
        :ok = Ecto.Adapters.SQL.Sandbox.checkout(MyApp.Repo)
        :ok
      end
    end
    ```

3. **Measuring Test Coverage**:

    One can measure test coverage using the built-in coverage tool. Run the tests with `mix test --cover` to see a coverage report.


>> Testing is a cornerstone of building reliable and maintainable software. Elixir’s ExUnit framework, combined with libraries like Mox and StreamData, provides a powerful toolkit for writing robust tests. 

---
