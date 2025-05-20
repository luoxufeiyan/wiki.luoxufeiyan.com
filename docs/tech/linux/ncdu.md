# ncdu: The Lazy Admin’s Disk-Space Detective


**ncdu** (NCurses Disk Usage) is a command-line tool that turns disk-space sleuthing into a breeze. 

ncdu 是一款命令行下的磁盘分析工具，使用交互界面，查询系统中的大文件。

### Installation
```bash
sudo apt install ncdu        # Debian/Ubuntu
sudo yum install ncdu        # CentOS/RHEL
brew install ncdu            # macOS (via Homebrew)
```

### Basic usage
1. **Scan your system**:
   ```bash
   ncdu /                  # Scan root (use sudo for system directories)
   ncdu ~/Downloads        # Target a specific folder
   ```

2. **Navigate**:
   - ↑/↓: Move between items.
   - **Enter**: Open a directory.
   - ←: Go back.
   - **d**: Delete selected file/dir (*double-check before hitting this!*).
   - **?**: Toggle help menu.

3. **Quit**: Press **q** or **Ctrl+C**.

---

### Pro tips
- **Limit scan depth** to save time:
  ```bash
  ncdu --max-depth=3 /   # Scan only 3 subdirectory levels
  ```
- **Exclude folders** (e.g., external drives):
  ```bash
  ncdu --exclude /mnt /
  ```
- **Export/Reload results**:
  ```bash
  ncdu -o scan_result.txt /path   # Save scan
  ncdu -f scan_result.txt         # Reopen later
  ```