# Setting up a Dev Container for Rust

**Primary Author**: [Aidan Lee](https://github.com/aidanjlee5)  
**Reviewer**: [Sushant Marella](https://github.com/sushmarella)

---

## Prerequisites

Before starting, make sure you have the following installed and accessible:

- **GitHub** account to host the project online.
- **Git** to manage version control and upload the project to GitHub.
- **Visual Studio Code (VS Code)** to compile Rust code and configure the dev container.
- **Docker** to run the development container.
- **WiFi** to access remote repositories.

---

## Part 1: Project Setup - Creating the Repository

### Step 1: Create a Local Repository

1. Open your **terminal** or **command prompt**.
2. Create a new directory for your project, preferably in an easily accessible location:

    ```bash
    mkdir rust-hello-423
    cd rust-hello-423
    ```

3. Initialize a Git repository in your folder:

    ```bash
    git init
    ```

    !!! note
        This Git repository will help manage your commits and local project changes.

4. Create a `README.md` file to document your project:

    ```bash
    echo "COMP423 Rust Tutorial: https://aidanjlee5.github.io/comp423-course-notes/tutorials/rust-setup/" > README.md
    ```

    !!! note
        This is optional for the tutorial, but linking to the tutorial source is good for citing purposes.

### Step 2: Create Your GitHub Repository

1. Log in to your GitHub account.
2. Navigate to the **Create a New Repository** page.
3. Use the following settings for your repository:
   - **Repository Name**: `rust-hello-423`
   - **Description**: A basic Rust tutorial that outputs "Hello COMP423".
   - **Visibility**: Public.
   - Do **not** initialize with a README, `.gitignore`, or license file.

### Step 3: Link Your Local Repository to GitHub

1. Add the GitHub repository as a remote:

    ```bash
    git remote add origin https://github.com/<your-username>/rust-hello-423.git
    ```

2. Check your branch name with `git branch`. If it’s not `main`, rename it to `main`:

    ```bash
    git branch -M main
    ```

    !!! note
        Older versions of Git use `master` as the primary branch. Modern conventions use `main`.

3. Push your local commits to the GitHub repository:

    ```bash
    git push --set-upstream origin main
    ```

    !!! tip
        The `--set-upstream` flag (short version: `-u`) links your local branch to the remote branch. After this, you can simply run `git push` or `git pull` without specifying branch names.

4. Refresh your GitHub repository in your browser to confirm the push was successful. The commit ID and message in your local repository should match those on GitHub.

---

## Part 2: Setting Up the Development Environment

### Step 1: Create the Development Container

1. Open the `rust-hello-423` directory in VS Code:
   - Use **File > Open Folder** in the menu, or  
   - Run the command:

    ```bash
    code .
    ```

2. Install the **Dev Containers** extension in VS Code.
3. Create a `.devcontainer` directory in the root of your project. Inside this directory, add a `devcontainer.json` file with the following content:

    ```json
    {
        "name": "Rust Development Environment",
        "image": "mcr.microsoft.com/devcontainers/rust:latest",
        "customizations": {
            "vscode": {
                "extensions": [
                    "rust-lang.rust-analyzer"
                ]
            }
        }
    }
    ```

### Step 2: Open the Project in a Dev Container

1. Reopen the project in a Dev Container:
   - Press `Ctrl+Shift+P` (or `Cmd+Shift+P` on Mac).
   - Type: **Dev Containers: Reopen in Container** and select it.
2. Wait a few minutes for the container image to download and install.
3. Verify that Rust is installed by running:

    ```bash
    rustc --version
    ```

### Step 3: Create a New Binary Project

1. Run the following command to create a new Rust project:

    ```bash
    cargo new hello_world --vcs none
    ```

    !!! explanation
        The `--vcs none` flag prevents Cargo from creating another Git repository for the project.

2. Overwrite the contents of the `main.rs` file in the `src` directory with this code:

    ```rust
    fn main() {
        println!("Hello COMP423!");
    }
    ```

### Step 4: Build the Rust Program

1. Change into the `hello_world` directory:

    ```bash
    cd hello_world
    ```

2. Build your Rust program:

    ```bash
    cargo build
    ```

    !!! note
        This command compiles the program and creates an executable in the `target/debug/` directory by default. For optimized builds, executables go to the `target/release` directory.

3. Run the compiled executable:

    ```bash
    ./target/debug/hello_world
    ```

    !!! note
        This is similar to using `gcc` in COMP211, where:

        ```bash
        gcc -o hello_world main.c
        ```

        generates a `hello_world` binary that can be run with `./hello_world`.

    !!! Warning
        Remember to ```cd ..``` before committing the project or making any other changes using the terminal

### Step 5: Running the Project

Instead of building and running separately, you can use:

    
    cargo run
    
This compiles the program and immeidately runs the resulting binary

### Step 6: Commit and Push your changes

When you have tested the application, run the following commands:

```
git add .
git commit -m "New Rust Hello COMP423 Project"
```

Push to GitHub if you have a remote setup
```
git remote add origin <your-repo-url>
git push -u origin main
```

### Conclusion:
By following this tutorial, you now have a fully functional Rust development environment using VS Code Dev Containers. You’ve also created a basic Rust program that outputs "Hello COMP423" and learned the basics of working with Cargo for building and running projects. This setup mirrors professional workflows in Rust development, giving you insight into its use in the industry.