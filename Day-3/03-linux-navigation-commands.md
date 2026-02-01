<h1 align="center">🧭 Day 3 – Linux Navigation Commands</h1>

<p align="center">
  <img src="https://img.shields.io/badge/Linux-Navigation-FCC624?style=for-the-badge&logo=linux&logoColor=black"/>
  <img src="https://img.shields.io/badge/Day-3-Terminal_Skills-success?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Level-Beginner-blue?style=for-the-badge"/>
</p>

<p align="center">
  Master how to move inside the Linux file system and explore directories using essential navigation commands.
</p>

---

## 📍 `pwd` — Print Current Working Directory
Displays the full path of your current location.

```bash
pwd
# Example Output:
/home/user
```

---

## 📂 `ls` — List Files & Directories
Shows files and folders in the current directory.

```bash
ls
# Example Output:
Documents  Downloads  file.txt
```

---

## 📄 `ls -l` — Detailed File Listing
Displays permissions, owner, size, and modification date.

```bash
ls -l
# Example Output:
-rw-r--r-- 1 user user 1200 Jan 10 10:00 file.txt
drwxr-xr-x 2 user user 4096 Jan 10 09:00 Documents
```

---

## 👻 `ls -a` — Show Hidden Files
Lists hidden files that start with a dot (`.`).

```bash
ls -a
# Example Output:
.  ..  .bashrc  file.txt
```

---

## 👻📄 `ls -la` — Detailed + Hidden Files
Combines detailed listing with hidden files.

```bash
ls -la
# Example Output:
drwxr-xr-x 3 user user 4096 Jan 10 10:00 .
drwxr-xr-x 5 user user 4096 Jan 10 09:00 ..
-rw-r--r-- 1 user user 220 Jan 10 09:00 .bashrc
```

---

## 📏 `ls -lh` — Human Readable File Sizes
Shows file sizes in KB, MB, or GB.

```bash
ls -lh
# Example Output:
-rw-r--r-- 1 user user 1.2K Jan 10 file.txt
```

---

## ⏳ `ls -lt` — Sort by Newest Files
Lists files sorted by most recently modified.

```bash
ls -lt
# Example Output:
file.txt  Documents
```

---

## 🕒 `ls -ltr` — Sort by Oldest Files
Lists files sorted by oldest modified.

```bash
ls -ltr
# Example Output:
Documents  file.txt
```

---

## ⚡ `ls -f` — Unsorted Listing
Shows files without any sorting.

```bash
ls -f
# Example Output:
file.txt  Documents  Downloads
```

---

## 🔁 `ls -R` — Recursive Listing
Displays files inside all subdirectories.

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
Moves you into a folder.

```bash
cd Documents
pwd
# Example Output:
/home/user/Documents
```

---

## ⬆ `cd ..` — Move One Level Up
Returns to the parent directory.

```bash
cd ..
pwd
# Example Output:
/home/user
```

---

## 🏠 `cd ~` — Go to Home Directory
Shortcut to your home folder.

```bash
cd ~
pwd
# Example Output:
/home/user
```

---

## 🌍 `cd /` — Go to Root Directory
Moves to the top-level directory.

```bash
cd /
pwd
# Example Output:
/
```

---

## 🔙 `cd -` — Return to Previous Directory
Switches back to the last visited directory.

```bash
cd -
# Example Output:
/home/user/Documents
```

---

## 🧭 Absolute Path Navigation
Uses the full path starting from root.

```bash
cd /home/user/Documents
pwd
# Example Output:
/home/user/Documents
```

---

## 🧭 Relative Path Navigation
Uses a path relative to your current location.

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
