Terminal Tool (CLI)
=====================

The SeleniumTwo CLI provides comprehensive project management and automation tools for Python development, specifically optimized for web automation projects.

Core Functionality
------------------
The CLI module delivers production-ready automation for Python environment management, dependency handling, and application deployment with enterprise-grade system integration.

Command Reference
-----------------

Virtual Environment Management
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: text

   nr -v, --venv                    Creates virtual environment with all dependencies installed
   nr -vc, --venv-clean             Creates clean virtual environment without dependencies
   nr -rv, --recreate-venv          Recreates venv (without dependencies)
   nr -dv, --delete-venv            Deletes virtual environment
   nr -r, --requirements            Generates optimized requirements.txt file

Executable Generation
~~~~~~~~~~~~~~~~~~~~~

.. code-block:: text

   nr -e, --exe {file.py}           Creates standalone .exe from Python file
   nr -nc, --no-console             Creates .exe without console window
   nr -z, --zip                     Creates zip archive of 'dist' folder
   nr -ic, --icon {path.ico}        Sets custom icon for .exe
   nr -ad, --add-data {folders}     Adds external data/files to .exe

Dependency Management
~~~~~~~~~~~~~~~~~~~~~

.. code-block:: text

   nr -fi, --find-imports {file.py} Discovers all required imports automatically
   nr -vi, --verify-imports         Shows imports that couldn't be installed automatically
   nr -i, --install-imports         Installs all detected dependencies

File Operations
~~~~~~~~~~~~~~~

.. code-block:: text

   nr {filename}                    Specifies target file for operations
   nr -h, --help                    Displays complete command reference

Detailed Functionality
----------------------

Virtual Environment System
~~~~~~~~~~~~~~~~~~~~~~~~~~
- **Smart Environment Creation** (-v): Automatically detects and installs all project dependencies
- **Clean Environments** (-vc): Creates minimal virtual environment without automatic installation
- **Environment Recycling** (-rv): Complete environment rebuild for troubleshooting
- **Requirements Optimization** (-r): Generates requirements.txt with only necessary packages

Executable Builder
~~~~~~~~~~~~~~~~~~
- **Single-File Distribution** (-e): Creates self-contained .exe using PyInstaller
- **Stealth Mode** (-nc): Generates executables without console windows
- **Resource Packaging** (-ad): Embeds external files/folders into executable
- **Custom Branding** (-ic): Applies custom icons to executables
- **Distribution Packaging** (-z): Creates ready-to-distribute zip files

Intelligent Dependency Detection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- **Import Analysis** (-fi): Scans Python files and detects:
  - Direct imports (import, from statements)
  - SeleniumTwo-specific dependencies
  - Image processing libraries (OpenCV, Pillow)
  - Automation tools (pyautogui, pynput)
  - PDF manipulation libraries (PyMuPDF, PyPDF2)
  - Undetected browser drivers
  - CAPTCHA solving services
- **Smart Installation** (-i): Automatically installs detected dependencies
- **Verification System** (-vi): Identifies problematic installations

Multi-Command Scenarios
-----------------------

Complete Project Setup
~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

   nr -v -fi main.py -i -e main.py -z

This single command:
1. Creates virtual environment with dependencies (-v)
2. Analyzes main.py for required imports (-fi)
3. Installs detected dependencies (-i)
4. Generates executable (-e)
5. Creates distribution zip (-z)

Rapid Development Cycle
~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

   nr -rv -fi script.py -i -e script.py -nc -ic icon.ico

Perfect for development:
1. Fresh environment rebuild (-rv)
2. Import analysis for current script (-fi)
3. Dependency installation (-i)
4. Executable generation without console (-nc)
5. Custom icon application (-ic)

Dependency Management Only
~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

   nr -fi project.py -i -r

Focus on dependencies:
1. Import discovery (-fi)
2. Automatic installation (-i)
3. Requirements file generation (-r)

Quick Executable with Resources
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

   nr -e app.py -ad data:data -ad config:config -z

Packaging with external resources:
1. Executable creation (-e)
2. Multiple data folders included (-ad)
3. Zip distribution (-z)

Technical Implementation
------------------------

Advanced Features
~~~~~~~~~~~~~~~~~

- **Real-time Animations**: RGB animated progress indicators
- **Intelligent Import Mapping**: 40+ predefined library mappings
- **Cross-Platform Compatibility**: Windows, Linux, and macOS support
- **Error Resilience**: Continues operation despite individual package failures
- **Automatic Clipboard**: Copies pip commands to clipboard for manual use
- **Shadow DOM Navigation**: Automatically handles Chrome extension configuration

Library Detection Intelligence
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The CLI automatically detects and maps:

.. code-block:: text

   "extract_pdf"          → "PyMuPDF"
   "import requests"      → "requests" 
   "import pyautogui"     → "pyautogui"
   "import cv2"           → "opencv-python"
   "undetected_chromedriver" → "undetected-chromedriver"
   "move_to_image"        → ["pyscreeze", "pyautogui", "Pillow", "opencv-python"]
   "stealth max"          → ["webdriver-manager", "undetected-chromedriver"]
   And 30+ more intelligent mappings...

Production Features
~~~~~~~~~~~~~~~~~~~

- **Enterprise-Grade Error Handling**: Comprehensive exception management
- **Parallel Processing**: Threaded animations during long operations
- **Automatic Cleanup**: Temporary file and directory management
- **Permission Handling**: Windows file locking workarounds
- **Unicode Support**: Full international character support
- **Terminal Control**: Advanced ANSI escape sequence usage

Usage Examples
--------------

Basic Development Workflow
~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

   # 1. Analyze dependencies
   nr -fi my_automation.py
   
   # 2. Create environment and install
   nr -v -i
   
   # 3. Generate executable
   nr -e my_automation.py -nc
   
   # 4. Create distributable package
   nr -z

Advanced Enterprise Deployment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

   # Complete CI/CD pipeline in one command
   nr -rv -fi main.py -i -e main.py -ad assets:assets -ad config:config -ic company.ico -nc -z

Troubleshooting & Verification
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: bash

   # Check for installation issues
   nr -fi script.py -i -vi
   
   # Rebuild from scratch
   nr -dv -v -fi script.py -i -e script.py

Implementation Notes
--------------------

Key Technical Competencies:
- **Self-Contained Executables**: No Python or external dependencies required
- **Advanced Argument Architecture**: Flexible command combination system
- **Cross-Platform Process Management**: Consistent behavior across OS
- **Environment Isolation**: Complete project dependency separation
- **Production-Grade Reliability**: Robust error handling and recovery
- **Automated Dependency Resolution**: Intelligent package detection and installation
- **Real-Time User Feedback**: Animated progress indicators and status updates

The CLI transforms complex development operations into simple, one-line commands while maintaining enterprise-level reliability and feature completeness.