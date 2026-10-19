# Code Editor: Creating and Managing Python Projects

Organize your Python projects using Visual Studio Code (VS Code).

## 1. Create a Projects Folder

Before you start coding, create a dedicated folder to store all your Python projects.

Keeping your projects organized makes it easier to find your code, manage files, and work on multiple projects.

### Step 1: Create the Main Projects Folder

Create a folder named `PythonProjects` in the following location:

- **Windows:** `Documents\PythonProjects`
- **macOS:** `~/PythonProjects`
- **Linux:** `~/PythonProjects`

### Step 2: Create Your First Project Folder

Inside `PythonProjects`, create a folder named `python-for-ai`.

We will use this folder throughout the course to store Python programs, exercises, and practice projects.

You can choose any project name you prefer. However, lowercase letters separated by hyphens are a common convention for project directories.

Examples:

- `python-for-ai`
- `my-first-project`
- `devops-automation`

This naming style is called **kebab-case**.

## 2. Open Your Project in VS Code

Once you have created your project folder, open it in Visual Studio Code.

### Method 1: Open a Folder from VS Code

1. Launch Visual Studio Code.
2. Select **File → Open Folder**.
3. Navigate to your `python-for-ai` folder.
4. Select the folder and click **Select Folder** on Windows or **Open** on macOS/Linux.

**Keyboard shortcut:** Use `Ctrl + K`, followed by `Ctrl + O` on Windows/Linux. On macOS, use `Cmd + K`, followed by `Cmd + O`.

Note: `Ctrl + O` or `Cmd + O` by itself opens a file, not the folder-selection dialog.

### Method 2: Open the Folder from Your File Manager

- **Windows:** Right-click the folder and select **Open with Code**, if available.
- **macOS:** Drag the folder onto the VS Code application icon, or open VS Code and use **File → Open Folder**.
- **Linux:** Right-click the folder and select **Open with Code**, if available.

If the **Open with Code** option is unavailable, use Method 1.

### Method 3: Open the Project Using the Terminal

If the `code` command is available in your terminal, you can open your project directly.

**Windows PowerShell:**

```powershell
cd "$HOME\Documents\PythonProjects\python-for-ai"
code .
```

**macOS/Linux:**

```bash
mkdir -p ~/PythonProjects/python-for-ai
cd ~/PythonProjects/python-for-ai
code .
```

The `code .` command opens the current directory in VS Code.

## 3. Understand the VS Code Interface

When you open your project folder, you will see several important areas.

### Explorer (Left Sidebar)

Displays your project folders and files. You can create, rename, move, and delete files from this panel.

### Editor (Main Area)

This is where you write and edit Python code.

### Integrated Terminal (Bottom Panel)

Allows you to execute Python programs and run commands without leaving VS Code.

Open it using **Terminal → New Terminal**.

### Problems and Output Panels

- **Problems:** Displays detected errors and warnings.
- **Output:** Displays messages from extensions and other VS Code components.
- **Debug Console:** Displays debugging information when debugging a program.

### Menu Bar and Editor Tabs

The menu bar provides access to VS Code commands, while editor tabs help you switch between open files.

**Important:** VS Code can open individual files, but opening a project folder provides the workspace context needed for project-specific settings, file navigation, and development tools.

## 4. Save Your Project as a Workspace

A VS Code workspace allows you to save project-specific settings and, when using a workspace file, the folders included in that workspace.

For a simple Python project, opening the project folder is usually sufficient. Saving a `.code-workspace` file is optional.

### Steps to Create a Workspace File

1. Open your `python-for-ai` folder in VS Code.
2. Select **File → Save Workspace As...**.
3. Navigate to your `python-for-ai` folder.
4. Enter the filename `python-for-ai.code-workspace`.
5. Click **Save**.

Your workspace file will be created inside the project directory.

### What Does a Workspace Store?

A `.code-workspace` file can store:

- Workspace folder references.
- Workspace-specific editor settings.
- Recommended extensions.
- Debugging configurations and other workspace configuration.

Open files and the current editor layout may be restored by VS Code, but they are not simply a guaranteed, complete snapshot of every open file and editor state.

### Workspace vs. Project Folder

- **Project folder:** Contains your Python source code, resources, and project files.
- **Workspace file:** Stores workspace configuration and folder references.

For a single-folder Python project, you can continue working without creating a separate workspace file.

## 5. Test Your Workspace

If you created a `.code-workspace` file, verify that it opens correctly.

1. Save your changes in VS Code.
2. Close VS Code.
3. Navigate to your `python-for-ai` folder.
4. Double-click `python-for-ai.code-workspace`.
5. Confirm that VS Code opens with your project folder available in the Explorer.

You can also create a desktop shortcut to the workspace file if you want quick access to the project.

## 6. Verify Your Project Structure

Your project should now look like this:

```text
PythonProjects/
└── python-for-ai/
    └── python-for-ai.code-workspace
```

The workspace file is optional. Your project folder is the essential part.

Later, we will add Python files, a virtual environment, and other project resources:

```text
PythonProjects/
└── python-for-ai/
    ├── .venv/
    ├── hello.py
    └── python-for-ai.code-workspace
```

**Note:** The `.venv` directory will be created when you configure a Python virtual environment. It does not need to exist at this stage.


### Reference Image

<img width="1024" height="1536" alt="Python Project Setup in VS Code Guide" src="https://github.com/user-attachments/assets/55e657aa-2b38-496d-b30c-85d294499bbb" />


