# pip-library-unistaller

If you want to uninstall all the pip-installed libraries and revert to the default Python environment on your Windows 11 machine, you can follow these steps:

### Step 1: List All Installed Packages
First, list all the packages installed via pip. Open a Command Prompt or PowerShell window and run:

```bash
pip list --format=freeze > installed_packages.txt
```

This will create a file named `installed_packages.txt` containing all the installed packages.

### Step 2: Identify Default Packages
Python comes with a set of default packages that are part of the standard library. These packages are not installed via pip and should not be uninstalled. You can find a list of these packages in the [Python documentation](https://docs.python.org/3/library/).

### Step 3: Create a Script to Uninstall Non-Default Packages
You can create a Python script to uninstall all packages that are not part of the default Python installation.

1. Open a text editor and create a new file, e.g., `uninstall_non_default.py`.
2. Paste the following code into the file:

```python
import os
import sys
from pip._internal.utils.misc import get_installed_distributions

# List of default packages that come with Python
default_packages = {
    'argparse', 'ast', 'base64', 'binascii', 'bisect', 'builtins', 'bz2', 'calendar',
    'cmath', 'collections', 'copy', 'csv', 'datetime', 'decimal', 'difflib', 'email',
    'enum', 'fnmatch', 'fractions', 'functools', 'gc', 'getopt', 'glob', 'gzip',
    'hashlib', 'heapq', 'hmac', 'html', 'http', 'importlib', 'inspect', 'io', 'itertools',
    'json', 'logging', 'math', 'mmap', 'multiprocessing', 'operator', 'os', 'pathlib',
    'pickle', 'pprint', 'queue', 'random', 're', 'select', 'shutil', 'signal', 'socket',
    'sqlite3', 'ssl', 'stat', 'string', 'struct', 'subprocess', 'sys', 'tempfile', 'textwrap',
    'threading', 'time', 'traceback', 'types', 'typing', 'unicodedata', 'urllib', 'uuid',
    'warnings', 'weakref', 'xml', 'zipfile', 'zlib'
}

# Get all installed packages
installed_packages = {pkg.key for pkg in get_installed_distributions()}

# Packages to uninstall
packages_to_uninstall = installed_packages - default_packages

# Uninstall packages
for package in packages_to_uninstall:
    os.system(f"{sys.executable} -m pip uninstall -y {package}")
```

3. Save the file and close the text editor.

### Step 4: Run the Script
Run the script using Python:

```bash
python uninstall_non_default.py
```

This script will uninstall all packages that are not part of the default Python installation.

### Step 5: Verify the Uninstallation
After running the script, you can verify that only the default packages are left by running:

```bash
pip list
```

This should show only the default packages and any packages that are part of the standard library.

### Step 6: (Optional) Reinstall Specific Packages
If you need to reinstall specific packages later, you can do so using pip:

```bash
pip install <package_name>
```

### Step 7: (Optional) Use Virtual Environments
To avoid cluttering your global Python environment in the future, consider using virtual environments for your projects:

```bash
python -m venv myenv
myenv\Scripts\activate
```

This will create an isolated environment where you can install packages without affecting the global Python installation.

### Conclusion
By following these steps, you can clean up your global Python environment and revert to the default set of packages. This is particularly useful if you want to start fresh or if your environment has become cluttered with too many installed packages.
