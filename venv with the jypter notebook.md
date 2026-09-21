# 🐍 Python Virtual Environment + Jupyter Kernel

## 🎯 Why Is This Important?

Python packages do not always support the **latest Python version immediately**.

For example, some packages may not yet provide compatible releases for **Python 3.14**. This can happen with packages such as TensorFlow and other libraries that depend on specific Python versions.

Instead of uninstalling your latest Python version, we can install an older/supported Python version and create a **virtual environment** specifically for that project.

For example:

```text
Python 3.14
    ↓
Keep it installed for other projects

Python 3.12
    ↓
Create a virtual environment
    ↓
.venv
    ↓
Install packages that require/support Python 3.12
```

### 💡 Main Idea

A virtual environment allows you to use a **different Python version and separate set of packages for a particular project** without changing your main Python installation.

> ⚠️ The required Python version depends on the package and its current compatibility. Always check the package's supported Python versions before choosing a version.

---

## 1. Create a Virtual Environment

```cmd
py -3.12 -m venv .venv
```

### Breakdown

- `py` → Windows Python Launcher. It lets you choose a specific installed Python version.
- `-3.12` → Tells the Python Launcher to use Python 3.12. u can use also others 
- `-m` → Tells Python to run a module.
- `venv` → Python's built-in module for creating virtual environments.
- `.venv` → The name of the virtual-environment folder that will be created.

### What it does

Creates a new virtual environment named `.venv` using Python 3.12.

---

## 2. Activate the Virtual Environment

```cmd
.venv\Scripts\activate
```

### Breakdown

- `.venv` → The virtual-environment folder.
- `\` → Windows path separator.
- `Scripts` → Folder containing executable scripts for the environment.
- `activate` → Script that activates the virtual environment.

### What it does

Activates `.venv`, so commands such as `python` and `pip` use the Python
and packages inside this virtual environment.

After activation, CMD should look similar to:

```text
(.venv) C:\your-project>
```

---

## 3. Install Jupyter Kernel Support

```cmd
python -m pip install ipykernel
```

### Breakdown

- `python` → Runs Python from the currently active virtual environment.
- `-m` → Tells Python to run a module.
- `pip` → Python's package installer.
- `install` → Tells pip to install a package.
- `ipykernel` → Package that allows a Python environment to be used as a Jupyter kernel.

### What it does

Installs `ipykernel` inside `.venv`, allowing this environment to
communicate with Jupyter Notebook.

---

## 4. Connect the Virtual Environment to Jupyter

```cmd
python -m ipykernel install --user --name .venv --display-name "Python (.venv)"
```

### Breakdown

- `python` → Uses Python from the active virtual environment.
- `-m` → Runs a Python module.
- `ipykernel` → Provides the Jupyter Python kernel functionality.
- `install` → Registers the environment as a Jupyter kernel.
- `--user` → Registers the kernel for the current Windows user.
- `--name .venv` → Gives the kernel an internal name of `.venv`.
- `--display-name` → Sets the name shown in Jupyter.
- `"Python (.venv)"` → The name displayed in Jupyter's kernel selection menu.

### What it does

Registers your `.venv` environment with Jupyter so you can select:

```text
Python (.venv)
```

as the kernel for your notebook.

---

## 5. List Jupyter Kernels

```cmd
jupyter kernelspec list
```

### Breakdown

- `jupyter` → Jupyter's command-line tool.
- `kernelspec` → Manages Jupyter kernel registrations.
- `list` → Displays the registered kernels.

### What it does

Shows the Python environments that Jupyter currently knows about.

Example:

```text
Available kernels:
  python3
  .venv
  tensorflow
```

> ⚠️ This shows **Jupyter kernels**, not every virtual environment on your computer.

---

## 6. Remove the Virtual Environment from Jupyter

```cmd
jupyter kernelspec uninstall .venv
```

### Breakdown

- `jupyter` → Jupyter's command-line tool.
- `kernelspec` → Manages Jupyter kernel registrations.
- `uninstall` → Removes a registered kernel.
- `.venv` → The kernel registration to remove.

### What it does

Removes `.venv` from Jupyter's list of available kernels.

> ⚠️ This does **not** delete the `.venv` folder.
>
> It only removes the Jupyter kernel registration.

---

## 7. Deactivate the Virtual Environment

```cmd
deactivate
```

### Breakdown

- `deactivate` → Command that exits the currently active virtual environment.

### What it does

Stops using `.venv` in the current CMD session.

Before:

```text
(.venv) C:\your-project>
```

After:

```text
C:\your-project>
```

---

## 8. Delete the Virtual Environment

```cmd
rmdir /s /q .venv
```

### Breakdown

- `rmdir` → Windows CMD command for removing a directory.
- `/s` → Removes the directory and everything inside it.
- `/q` → Quiet mode; does not ask for confirmation.
- `.venv` → The virtual-environment folder to delete.

### What it does

Permanently deletes the `.venv` folder and everything inside it,
including packages installed in that environment.

> ⚠️ This does **not** uninstall Python 3.12 from your computer.

---

# 🔄 Complete Setup

Run these commands in order:

```cmd
:: 1. Create the virtual environment
py -3.12 -m venv .venv

:: 2. Activate the virtual environment
.venv\Scripts\activate

:: 3. Install Jupyter kernel support
python -m pip install ipykernel

:: 4. Register the environment with Jupyter
python -m ipykernel install --user --name .venv --display-name "Python (.venv)"

:: 5. Check registered Jupyter kernels
jupyter kernelspec list
```

### Command Breakdown

```text
py -3.12
    ↓
Select Python 3.12

-m venv
    ↓
Run Python's virtual-environment module

.venv
    ↓
Create the environment in a folder named .venv

.venv\Scripts\activate
    ↓
Activate the environment

python -m pip install ipykernel
    ↓
Install Jupyter kernel support

python -m ipykernel install
    ↓
Register the environment with Jupyter

jupyter kernelspec list
    ↓
Check the registered Jupyter kernels
```

---

# 🗑️ Complete Removal

When you want to completely remove the environment:

```cmd
:: 1. Remove the kernel registration from Jupyter
jupyter kernelspec uninstall .venv

:: 2. Deactivate the virtual environment
deactivate

:: 3. Delete the virtual environment folder
rmdir /s /q .venv
```

### Command Breakdown

```text
jupyter kernelspec uninstall .venv
    ↓
Remove .venv from Jupyter

deactivate
    ↓
Exit the virtual environment

rmdir /s /q .venv
    ↓
Delete the actual .venv folder
```

---

# 🧠 Important Difference

```text
Python 3.12
    │
    └── Virtual Environment
            │
            └── .venv
                  │
                  ├── Python
                  ├── pip
                  └── Installed Packages
                          │
                          ↓
                    Jupyter Kernel
                          │
                          └── Python (.venv)
```

| Command | What it does |
|---|---|
| `py -3.12 -m venv .venv` | Creates the virtual environment |
| `.venv\Scripts\activate` | Activates the environment |
| `python -m pip install ipykernel` | Installs Jupyter kernel support |
| `python -m ipykernel install ...` | Registers the environment with Jupyter |
| `jupyter kernelspec list` | Lists Jupyter kernels |
| `jupyter kernelspec uninstall .venv` | Removes the kernel from Jupyter |
| `deactivate` | Exits the active environment |
| `rmdir /s /q .venv` | Deletes the actual virtual environment |

> **Remember:** A Jupyter kernel registration and a Python virtual environment are two different things. Removing the kernel does not automatically delete the virtual environment.