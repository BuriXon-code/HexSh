# HexSh - A Bash-Based Hex Editor

![screenshot](/screenshots/img1.jpg)  

## About

**HexSh** is a simple hex editor written in **pure Bash**. It allows you to **view and edit the hexadecimal content** of files directly from the terminal. Designed for **lightweight operation**, it is suitable for **quick hex modifications** without requiring complex external dependencies.

The script is **not highly efficient** and has limitations when handling large files, which makes it somewhat less versatile.

However, I’m sharing the project as an example of using Bash for **calculations**, **generating hexadecimal arrays**, and handling **keyboard input**.

The script includes a range of safeguards and features to protect the edited file from corruption, as well as various functions and error codes to protect the script from unexpected failures.

>[!WARNING]
> The script may freeze when attempting to edit large files.
> If this happens, you should cancel the script opening with **CTRL+C before the editor screen loads**.

**Key Features:**

- Interactive hex editing with real-time updates.
- Support for undo/redo operations.
- ASCII preview mode for easier analysis.
- Efficient navigation with keyboard shortcuts.
- Optimized for smaller files, but allows handling of larger files with chunk-based loading.
- Works in Debian-based systems and Termux.

## Features

- **Hex Editing:** Modify bytes directly in a hex format.
  - Modifying individual bytes of the file;
  - Highlighting/selecting edited bits;
  - Option for quickly removing individual bytes;
  - Option for appending new lines to add content;
- **Navigation:** Scroll through the file using keyboard shortcuts.
  - Support for arrow key navigation;
  - Support for multiple commands and options via individual keyboard keys;
  - Adjusting the editing field size to the terminal size;
  - Screen refresh after every change and interaction;
  - No use of the `clear` command to avoid screen flickering effect;
- **Undo & Redo:** Correct mistakes efficiently.
  - Option for quickly undoing changes (undo);
  - Option for quickly redoing undone edits (redo);
- **Offset & ASCII Modes:** Toggle visibility of ASCII characters and offsets.
  - Displaying byte offsets;
  - Displaying the converted line content in ASCII;
- **Backup Files:** Prevents data loss by storing backup copies before editing (up to 2 copies of the same filename).
- **Fast Mode:** Increases performance by sacrificing graphical accuracy.

## Installation

To install the package, follow these steps:

```
# Clone the repository
git clone https://github.com/BuriXon-code/HexSh.git
```

```
# Navigate to the directory
cd HexSh
```

```
# Grant execute permissions
chmod +x hexsh
```

```
# Run the script
./hexsh example-file.bin
```

Optionally, you can move the file to a PATH directory to run it from anywhere:

```
# In Linux
sudo cp hexsh /usr/bin/hexsh
```

```
# In Termux
cp hexsh $PREFIX/bin/hexsh
```

## Dependencies and compatibility

HexSh is designed to run in **Unix-based systems and Termux**.
Ensure you have the following commands installed:

- `bash` (Shell/interpreter)
- `tput` (Terminal UI handling)
- `hexdump` (Hex visualization tool)
- `jq` (JSON parsing for undo/redo history management)
- `stty` (Terminal UI handling)
- `file` (Showing edited file info)
- `xxd` (Converting selected data)

>[!NOTE]
> If the script detects missing required packages/commands, it will display an appropriate prompt with information on how to install the missing dependencies.

Script was tested in:

- Debian 12
- Ubuntu 24.04
- Termux 0.119.0-beta.1/-beta.2

Script was tested in bash 5.2.37(1)

![screenshot](/screenshots/img2.jpg)  

## Usage

Run HexSh with a target file:

```
./hexsh myfile.bin
```

### Options:

```
-b    Remove backup files from cache and launch.
-c    Set the columns count.
-h    Show help info and exit.
-i    Start with visible ASCII preview.
-o    Start with hidden offset view.
-r    Set the rows count.
-v    Start with fast mode enabled.
```

### Navigation:

- **Arrow Keys:** Move cursor.
- **Pg Down / Pg Up:** Move cursor by 5 lines.
- **Home / End:** Move to first/last character in the current row.
- **j / n:** Scroll down by 1/5 lines.
- **k / m:** Scroll up by 1/5 lines.
- **l:** Move to a specified line.
- **i:** Jump to a specified offset.

### Editing:

- **Hex Input (0-9, A-F):** Modify current byte.
- **.** Insert hex space (code 20).
- **Enter:** Create new empty line (cannot undo!).
- **x:** Delete selected byte (undo/redo may not work reliably).

### File Operations:

- **z / r:** Undo / Redo last change.
- **s:** Save to a new file.
- **w:** Save changes.
- **q:** Quit editor.

### Performance/aparence:

- **o / p:** Show/hide offset view & ASCII preview.
- **v:** Enable/Disable fast mode (boosts speed, but may affect visuals).

>[!NOTE]
> Switching each of these options affects the script's performance/productivity in exchange for an improvement/deterioration in aesthetics and visual aspects.

## Backup System

HexSh automatically creates backups before editing. Backup files are stored in:

```
$HOME/.cache/BuriXon-code/HexSh/
```

To delete the saved backup files, use the command:

```
hexsh -b
```
