<h1 align="center">📂 Day 5 – Copying, Moving, Sorting & File Path Concepts</h1>

<p align="center">
  <img src="https://img.shields.io/badge/Linux-File_Operations-FCC624?style=for-the-badge&logo=linux&logoColor=black"/>
  <img src="https://img.shields.io/badge/Day-5-Terminal_Skills-success?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Level-Beginner-blue?style=for-the-badge"/>
</p>

<p align="center">
  Learn how to copy, move, rename, sort, and analyze file content in Linux.
</p>

---

## 📋 `cp` — Copy a File

```bash
cp file1.txt file2.txt
# Creates a copy named file2.txt
```

---

## 📂 Copy File to Another Folder

```bash
cp file.txt /home/user/Documents/
```

---

## 📦 Copy Multiple Files

```bash
cp file1.txt file2.txt file3.txt /home/user/Documents/
```

---

## 📁 Copy a Folder

```bash
cp -r myfolder backupfolder
```

---

## ⬅ Copy File from Parent Directory

```bash
cp ../file.txt .
# Copies file from previous folder to current folder
```

---

## 🗂 Make a Backup Copy of a File

```bash
cp important.txt important_backup.txt
```

---

## 🔀 `mv` — Move a File

```bash
mv file.txt /home/user/Documents/
```

---

## ✏️ Rename a File

```bash
mv oldname.txt newname.txt
```

---

## 📁 Rename a Folder

```bash
mv oldfolder newfolder
```

---

## 🔄 Move and Rename at the Same Time

```bash
mv file.txt /home/user/Documents/newname.txt
```

---

## 🔝 Display Top 5 Lines

```bash
head -n 5 file.txt
```

---

## 🔚 Display Bottom 5 Lines

```bash
tail -n 5 file.txt
```

---

## 🔤 `sort` — Sort File Content Alphabetically

```bash
sort names.txt
```

---

## 🔢 Sort Numerically

```bash
sort -n numbers.txt
```

---

## 🔽 Reverse Sorting

```bash
sort -r names.txt
```

---

## 💾 Save Sorted Output to New File

```bash
sort names.txt > sorted_names.txt
```

---

## 🔁 Remove Duplicate Lines

```bash
uniq names.txt
```

---

## 🔁 Sort + Remove Duplicates

```bash
sort names.txt | uniq
```

---

## 🔢 Count Occurrences of Each Line

```bash
sort names.txt | uniq -c
```

---

## 🔍 Show Only Unique Lines

```bash
sort names.txt | uniq -u
```

---

# 🧭 PATH CONCEPTS (IMPORTANT)

---

## 📍 Absolute Path

Full path starting from root `/`.

```bash
cd /home/user/Documents
```

---

## 📍 Relative Path

Path based on your current location.

```bash
cd Documents
```

---

## 🏠 Home Directory Shortcut

```bash
cd ~
```

---

<p align="center">
  🎉 You now know how to copy, move, rename, sort, and analyze files in Linux!
</p>
