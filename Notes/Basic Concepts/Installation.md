# Installation
Getting started with Elixir involves setting up the necessary tools and environment on your machine. This section will guide you through the installation process for Elixir, including its dependencies.

---
### Step 1: Install Erlang/OTP

Elixir runs on the Erlang Virtual Machine (BEAM), so the first step is to install Erlang/OTP. The installation process varies depending on your operating system.

### Windows

1. **Download the Erlang/OTP installer**: Go to the [Erlang Solutions website](https://www.erlang-solutions.com/resources/download.html) and download the installer for Windows.
2. **Run the installer**: Follow the prompts to complete the installation.
3. **Verify the installation**: Open a command prompt and run:
    ```sh
    erl
    ```
   You should see the Erlang shell prompt.

### macOS

1. **Using Homebrew**: The easiest way to install Erlang/OTP on macOS is using Homebrew. If you don't have Homebrew installed, follow the instructions on [brew.sh](https://brew.sh/).
2. **Install Erlang/OTP**: Open a terminal and run:
    ```sh
    brew install erlang
    ```
3. **Verify the installation**: Run the following command in your terminal:
    ```sh
    erl
    ```
   You should see the Erlang shell prompt.

### Linux

1. **Debian/Ubuntu**: 
    ```sh
    sudo apt update
    sudo apt install erlang
    ```
2. **Fedora**:
    ```sh
    sudo dnf install erlang
    ```
3. **Arch Linux**:
    ```sh
    sudo pacman -S erlang
    ```
4. **Verify the installation**: Open a terminal and run:
    ```sh
    erl
    ```
   You should see the Erlang shell prompt.

### Step 2: Install Elixir

Once Erlang/OTP is installed, you can proceed with installing Elixir.

### Windows

1. **Download the Elixir installer**: Go to the [Elixir-lang website](https://elixir-lang.org/install.html#windows) and download the installer for Windows.
2. **Run the installer**: Follow the prompts to complete the installation.
3. **Verify the installation**: Open a command prompt and run:
    ```sh
    elixir -v
    ```
   You should see the installed version of Elixir.

### macOS

1. **Using Homebrew**:
    ```sh
    brew install elixir
    ```
2. **Verify the installation**: Run the following command in your terminal:
    ```sh
    elixir -v
    ```
   You should see the installed version of Elixir.

### Linux

1. **Debian/Ubuntu**:
    ```sh
    sudo apt update
    sudo apt install elixir
    ```
2. **Fedora**:
    ```sh
    sudo dnf install elixir
    ```
3. **Arch Linux**:
    ```sh
    sudo pacman -S elixir
    ```
4. **Verify the installation**: Open a terminal and run:
    ```sh
    elixir -v
    ```
   You should see the installed version of Elixir.

### Step 3: Install Hex and Rebar

Hex is the package manager for the Erlang ecosystem, and Rebar is a build tool. These tools are essential for managing dependencies in Elixir projects.

1. **Install Hex**: Run the following command to install Hex:
    ```sh
    mix local.hex
    ```
2. **Install Rebar**: Run the following command to install Rebar:
    ```sh
    mix local.rebar
    ```

### Step 4: Setting Up Your First Elixir Project

To ensure everything is set up correctly, let's create a simple Elixir project.

1. **Create a new project**:
    ```sh
    mix new my_first_project
    ```
2. **Navigate to the project directory**:
    ```sh
    cd my_first_project
    ```
3. **Compile the project**:
    ```sh
    mix compile
    ```
4. **Run the project**: You can start an interactive Elixir shell within the context of your project by running:
    ```sh
    iex -S mix
    ```
   This command should open an interactive shell where you can execute Elixir code.

### Troubleshooting

- **Path Issues**: Ensure that the paths to Erlang and Elixir binaries are added to your system's PATH environment variable.
- **Version Compatibility**: Verify that the versions of Erlang/OTP and Elixir are compatible. Sometimes newer versions of Elixir might require specific versions of Erlang/OTP.

### Additional Resources

- [Elixir Getting Started Guide](https://elixir-lang.org/getting-started/introduction.html)
- [Erlang Solutions Downloads](https://www.erlang-solutions.com/resources/download.html)
- [Homebrew](https://brew.sh/)
---
