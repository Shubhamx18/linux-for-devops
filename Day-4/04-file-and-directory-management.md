<h1 align="center">📁 Day 4 – Viewing & Managing Files and Directories</h1>

<p align="center">
  <img src="https://img.shields.io/badge/Linux-File_Management-FCC624?style=for-the-badge&logo=linux&logoColor=black"/>
  <img src="https://img.shields.io/badge/Day-4-Terminal_Skills-success?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Level-Beginner-blue?style=for-the-badge"/>
</p>

<p align="center">
  Learn how to view file content, create/delete files & folders, and properly edit files using Linux terminal editors.
</p>

---

## 📖 `cat` — View File Content
Displays the entire file content at once.

```bash
cat file.txt
# Example Output:
Hello Linux
Welcome to DevOps
```

---

## 📜 `less` — Scroll Through File (Recommended)
Used for large files with scroll support.

```bash
less file.txt
```

**Controls:**  
`↑ ↓` scroll • `Space` next page • `q` quit

---

## 📜 `more` — Basic Pager
Older scrolling tool.

```bash
more file.txt
```

---

## 🔝 `head` — View First Lines

```bash
head file.txt
head -n 5 file.txt
```

---

## 🔚 `tail` — View Last Lines

```bash
tail file.txt
tail -n 5 file.txt
```

---

## 🔄 `tail -f` — Live File Monitoring
Used for watching logs in real-time.

```bash
tail -f logfile.log
```

Press `Ctrl + C` to stop.

---

## 🆕 `touch` — Create a New File

```bash
touch notes.txt
```

---

## ✍️ `echo` — Write Text into File

Overwrite file:
```bash
echo "hello shubham" > file.txt
```

Append text:
```bash
echo "welcome to linux" >> file.txt
```

---

## 📂 `mkdir` — Create Directory

```bash
mkdir myfolder
mkdir -p project/src
```

---

## ❌ `rmdir` — Delete Empty Directory

```bash
rmdir myfolder
```

---

## 🗑️ `rm` — Delete File

```bash
rm file.txt
```

---

## 🗑️📁 `rm -r` — Delete Folder with Files

```bash
rm -r myfolder
rm -rf myfolder
```

⚠️ **Danger:** Permanent deletion.

---

## 📋 `cp` — Copy Files

```bash
cp file.txt backup.txt
cp file.txt /home/user/Documents/
```

---

## 🔀 `mv` — Move or Rename Files

```bash
mv oldname.txt newname.txt
mv file.txt /home/user/Documents/
```

---

# ✏️ FILE EDITING

---

## 🟢 `nano` — Beginner-Friendly Editor

Open file:
```bash
nano file.txt
```

### How to Use nano:
| Action | Keys |
|-------|------|
| Type text | Just start typing |
| Save file | `Ctrl + O` then Enter |
| Exit editor | `Ctrl + X` |
| Cancel | `Ctrl + C` |

---

## 🧠 `vi` — Classic Linux Editor

Open file:
```bash
vi file.txt
```

### How to Use vi:
| Action | Keys |
|-------|------|
| Enter insert mode | Press `i` |
| Type text | Start typing |
| Exit insert mode | Press `Esc` |
| Save and quit | Type `:wq` then Enter |
| Quit without saving | Type `:q!` then Enter |

---

## 🚀 `vim` — Advanced vi Editor

Open file:
```bash
vim file.txt
```

### Basic vim Usage (Same as vi):
| Action | Keys |
|-------|------|
| Insert mode | `i` |
| Exit insert mode | `Esc` |
| Save | `:w` |
| Save & quit | `:wq` |
| Quit without saving | `:q!` |

---

<p align="center">
  🎉 You now know how to view, create, delete, copy, move, and properly edit files & directories in Linux!
</p>
