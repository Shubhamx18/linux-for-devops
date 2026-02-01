<h1 align="center">🧭 Day 3 – Linux Navigation Commands</h1>

<p align="center">
  <img src="https://img.shields.io/badge/Linux-Navigation-FCC624?style=for-the-badge&logo=linux&logoColor=black"/>
  <img src="https://img.shields.io/badge/Day-3-Terminal_Skills-success?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Level-Beginner-blue?style=for-the-badge"/>
</p>

<p align="center">
  Learn how to move inside the Linux file system and view directory contents using essential navigation commands.
</p>

---

## 📍 `pwd` — Print Current Directory
Shows the full path of where you are in the system.

```bash
pwd
# Example Output:
/home/user
```

---

## 📂 `ls` — List Files & Directories
Displays files and folders in the current location.

```bash
ls
# Example Output:
Documents  Downloads  file.txt
```

---

## 📄 `ls -l` — Detailed File List
Shows permissions, owner, size, and modification date.

```bash
ls -l
# Example Output:
-rw-r--r-- 1 user user 1200 Jan 10 10:00 file.txt
drwxr-xr-x 2 user user 4096 Jan 10 09:00 Documents
```

---

## 👻 `ls -a` — Show Hidden Files
Displays hidden files (names starting with `.`).

```bash
ls -a
# Example Output:
.  ..  .bashrc  file.txt
```

---

## 👻📄 `ls -la` — Detailed + Hidden Files
Combines detailed view and hidden files.

```bash
ls -la
# Example Output:
drwxr-xr-x 3 user user 4096 Jan 10 10:00 .
drwxr-xr-x 5 user user 4096 Jan 10 09:00 ..
-rw-r--r-- 1 user user 220 Jan 10 09:00 .bashrc
```

---

## 📏 `ls -lh` — Human Readable Sizes
Displays file sizes in KB, MB, GB.

```bash
ls -lh
# Example Output:
-rw-r--r-- 1 user user 1.2K Jan 10 file.txt
```

---

## ⏳ `ls -lt` — Newest Files First
Sorts files by most recently modified.

```bash
ls -lt
# Example Output:
file.txt  Documents
```

---

## 🕒 `ls -ltr` — Oldest Files First
Sorts files by oldest modified.

```bash
ls -ltr
# Example Output:
Documents  file.txt
```

---

## ⚡ `ls -f` — Unsorted List
Shows files without sorting.

```bash
ls -f
# Example Output:
file.txt  Documents  Downloads
```

---

## 🔁 `ls -R` — Recursive List
Lists files inside subdirectories.

```bash
ls -R
# Example Output:
.:
Documents file.txt

./Documents:
notes.txt
```

---

## 📁 `cd foldername` — Enter a Directory
Moves you inside a folder.

```bash
cd Documents
pwd
# Example Output:
/home/user/Documents
```

---

## ⬆ `cd ..` — Go One Level Up
Moves back to the parent directory.

```bash
cd ..
pwd
# Example Output:
/home/user
```

---

## 🏠 `cd ~` — Go to Home Directory
Quick shortcut to your home folder.

```bash
cd ~
pwd
# Example Output:
/home/user
```

---

## 🌍 `cd /` — Go to Root Directory
Moves to the top-most directory.

```bash
cd /
pwd
# Example Output:
/
```

---

## 🔙 `cd -` — Return to Previous Directory
Switches back to your last location.

```bash
cd -
# Example Output:
/home/user/Documents
```

---

## 🧭 Absolute Path Navigation
Full path starting from `/`.

```bash
cd /home/user/Documents
pwd
# Example Output:
/home/user/Documents
```

---

## 🧭 Relative Path Navigation
Path from where you currently are.

```bash
cd Documents
pwd
# Example Output:
/home/user/Documents
```

---

<p align="center">
  🎉 You now know how to navigate confidently inside a Linux system!
</p>
