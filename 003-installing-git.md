# Installing Git (Windows, macOS, Linux)

## 1. Check if Git is Already Installed

Before installing, check if Git is already available:

```bash
git --version
```

- If you see something like `git version 2.x.x`, Git is already installed.  
- If not, follow the instructions below.

---

## 2. Installing Git on Windows

### Method 1: Using Git for Windows
1. Go to the official site: [https://git-scm.com/download/win](https://git-scm.com/download/win)  
2. Download the installer (`.exe`).  
3. Run the installer:
   - Use default settings (recommended for beginners).
   - Make sure **"Git Bash"** and **"Git GUI"** are selected.
4. After installation, open **Git Bash** or **Command Prompt** and check:

```bash
git --version
```

### Method 2: Using Chocolatey (package manager)
If you have [Chocolatey](https://chocolatey.org/) installed:

```bash
choco install git -y
```

---

## 3. Installing Git on macOS

### Method 1: Using Homebrew (recommended)
If you have [Homebrew](https://brew.sh/) installed:

```bash
brew install git
```

### Method 2: Using Xcode Command Line Tools
Run:

```bash
xcode-select --install
```

This installs Git along with developer tools.

### Method 3: Download from Git Website
1. Go to [https://git-scm.com/download/mac](https://git-scm.com/download/mac)  
2. Download and run the `.dmg` installer.  
3. Verify installation:

```bash
git --version
```

---

## 4. Installing Git on Linux

### Debian / Ubuntu (and derivatives)

```bash
sudo apt update
sudo apt install git
```

### Fedora

```bash
sudo dnf install git
```

### Arch Linux

```bash
sudo pacman -S git
```

### openSUSE

```bash
sudo zypper install git
```

Verify after install:

```bash
git --version
```

---

## 5. Configure Git (First-Time Setup)

After installing Git, set your global username and email:

```bash
git config --global user.name "Your Name"
git config --global user.email "youremail@example.com"
```

Check your configuration:

```bash
git config --list
```

---

## 6. Installation Workflow Diagram

```mermaid
flowchart TD
    A[Check if Git is installed] -->|Yes| B[Ready to use Git]
    A -->|No| C{Choose Operating System}
    C --> D[Windows: Installer or Chocolatey]
    C --> E[macOS: Homebrew / Xcode CLI / dmg]
    C --> F[Linux: apt / dnf / pacman / zypper]
    D --> G[Verify Installation: git --version]
    E --> G
    F --> G
    G --> H[Configure username & email]
    H --> B
```

---

## 7. Summary

- **Windows** → Download installer or use Chocolatey.  
- **macOS** → Use Homebrew, Xcode CLI tools, or Git website.  
- **Linux** → Use your package manager (`apt`, `dnf`, `pacman`, `zypper`).  
- Always configure your **username and email** after installation.

👉 Now you’re ready to start using Git!

---
