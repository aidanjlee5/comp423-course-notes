# Setting up a dev container for Rust

* Primary Author: Aidan Lee (https://github.com/aidanjlee5)
* Reviewer: Sushant Marella (https://github.com/sushmarella)

<h3>
Prerequisites
</h3>

- **GitHub** account is needed to post the project online
- **Git** is needed to save the project and upload to GitHub
- **Visual Studio Code** is needed to compile the rust dev container and rust files
- **Docker** is required to run the dev container
- Access to **WiFi** for accessing the remote repo 

<h3>Part 1. Project Setup: Creating the Repository<h3>
<h4>Step 1: Create a local repository<h4>
Open your terminal or command prompt
Create a new directory for your project, preferably in a folder you'll know where it is on your computer

```
mkdir rust-hello-423
cd rust-hello-423
```

Intialize a git repository in your folder

```
git init
```

> This git repository is necessary for controlling all your commits and your local repository

Create a README file: 

```
echo"COMP423 Rust Tutorial: https://github.com/<your-username>/comp423-course-notes" > README.md
```

!!!Note

This is not necessary for your project, but I linked the tutorial to this project for citing purposes 

<h4>Step 2. Creating your GitHub Repository</h4>
Login to your GitHub account and navigate to the Create a New Repository page

Before creating the repository, make sure 

<ol>
    <li>
    Repository Name: rust-hello-423
    </li>
    <li>
    Description: A basic rust tutorial that outputs Hello 423
    </li>
    <li>
    Visibility: Public
    </li>
    <li>
    No README, .gitignore, or licence.
    </li>
</ol>

<h4> Step 3. Linking your local repository to GitHub</h4>

Add the GitHub repository as a remote

```
git remote add origin https://github.com/<your-username>/comp423-course-notes.git
```

Check your default branch name with the subcommand git branch. If it's not main, rename it to main with the following command: git branch -M main. Old versions of git choose the name master for the primary branch, but these days main is the standard primary branch name.

Push your local commits to the GitHub repository: 

```
git push --set-upstream origin main
```

!!! Understanding the --set-upstream Flag

```git push --set-upstream origin main```: This command pushes the main branch to the remote repository origin. The ```--set-upstream``` flag sets up the main branch to track the remote branch, meaning future pushes and pulls can be done without specifying the branch name and just writing ```git push origin``` when working on your local main branch. This long flag has a corresponding ```-u``` short flag


Back in your web browser, refresh your GitHub repository to see that the same commit you made locally has now been pushed to remote. You can use git log locally to see the commit ID and message which should match the ID of the most recent commit on GitHub. This is the result of pushing your changes to your remote repository

<h3>Part 2. Setting up the Development Environment</h3>
<h4>Step 1. Creating the Development Container</h4>
In VS code, open your comp423-course-notes directory. You can do this via: File > Open Folder or ```code.``` in the terminal

Install the Dev Containers extension for VS Code 

Create a .devcontainer directory in the root of your project with the following file inside of this "hidden" configuartion directory

```.devcontainer/devcontainer.json```

Paste the following line into the devcontainer.json file: 

```{
    "name": "Rust Development Environment",
    "image": "mcr.microsoft.com/devcontainers/rust:latest",
    "customizations": {
        "vscode": {
            "extensions": [
                "rust-lang.rust-analyzer"
            ]
        }
    }
} ```

<h4> Step 2. Open the project in a VScode Dev Container </h4>

Reopen the project in the container by pressing ```Ctrl+Shift+P``` or ```Cmd+Shift+P``` on Mac, typing "Dev Containers: Reopen in Container," and selecting the option. This may take a few minutes while the image is downloaded and the requirements are installed.

After the dev container is open, run the command: ```rustc --version``` to prove that a recent version of rust is installed

<h4>Step 3. Create a new binary project</h4>

Run the command ```cargo new hello_world --vcs none``` 

!!! Explanation 

    --vcs none flag ensures that a new git repository isn't created on your behalf
---
Make sure the following code overwrited the main.rs file: 
```fn main() {
    println!("Hello COMP423!");
}
```

<h4>Step 4. Building the rust program</h4>

Run the following commmands to compile your Rust program, creating an executable in the target/debug/ directory by default (optimized builds go to target/release)

```
cd hello_world
cargo build
```

Once this finishes compiling, you run the compiled executable using the following command. This is similar to 211's gcc command where
```gcc -o hello_world main.c ```
generates a hello_world binary and can be run by ./hello_world

```
.target/debug/hello_world
```


<h4>Step 5. Running the project</h4>
Alternatively you can run the project using the command 
```cargo run ``` which compiles the repository and immediately runs the resulting binary

Either running or building the project should run the command with an output of Hello COMP423 

By following this tutorial, you will be able to get a better understanding of Rust and its functions in industry. 







