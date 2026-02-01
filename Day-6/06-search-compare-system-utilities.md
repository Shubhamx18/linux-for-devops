<h1 align="center">🧰 Day 6 – Search, Compare & Useful Linux Utilities</h1>

<p align="center">
  <img src="https://img.shields.io/badge/Linux-Search_&_Tools-FCC624?style=for-the-badge&logo=linux&logoColor=black"/>
  <img src="https://img.shields.io/badge/Day-6-Terminal_Skills-success?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Level-Beginner-blue?style=for-the-badge"/>
</p>

<p align="center">
  Learn file splitting, searching text, comparing files, finding files, and important Linux utility commands.
</p>

---

## ✂️ `split` — Split a Large File

Split into smaller files:

```bash
split bigfile.txt part_
```

Split by number of lines:

```bash
split -l 100 bigfile.txt part_
```

---

## 🔍 `grep` — Search Text Inside Files

Basic search:

```bash
grep "error" logfile.txt
```

Ignore case:

```bash
grep -i "error" logfile.txt
```

Show line numbers:

```bash
grep -n "error" logfile.txt
```

Count matches:

```bash
grep -c "error" logfile.txt
```

Search recursively:

```bash
grep -r "error" /home/user/
```

---

## 🌟 Wildcards (Pattern Matching)

| Symbol | Meaning | Example |
|--------|---------|---------|
| `*` | Matches any characters | `ls *.txt` |
| `?` | Matches one character | `ls file?.txt` |
| `[ ]` | Match range | `ls file[1-3].txt` |

---

## 🔀 `shuf` — Shuffle File Content

```bash
shuf names.txt
```

---

## 🔢 `wc -l` — Count Lines in File

```bash
wc -l file.txt
```

---

## 🆚 Compare Files

### `cmp` — Check if Files are Identical

```bash
cmp file1.txt file2.txt
```

---

### `diff` — Show Differences Between Files

```bash
diff file1.txt file2.txt
```

---

### `diff -u` — Unified Format (Better View)

```bash
diff -u file1.txt file2.txt
```

---

## 🔎 `find` — Search Files by Name or Type

Find file by name:

```bash
find /home/user -name "file.txt"
```

Find directories only:

```bash
find /home/user -type d
```

Find files by extension:

```bash
find /home/user -name "*.log"
```

---

## ⚡ `locate` — Quickly Find Files

Update database first:

```bash
sudo updatedb
```

Search file:

```bash
locate file.txt
```

---

## 📅 `cal` — Display Calendar

```bash
cal
cal 2025
```

---

## 🎥 `script` — Record Terminal Session

Start recording:

```bash
script session.txt
```

Stop recording:

```bash
exit
```

---

## 📘 `man` — Command Manual

```bash
man ls
man grep
```

Press `q` to quit.

---

## ❓ `--help` — Quick Command Help

```bash
ls --help
grep --help
```

---

## 🧠 Extra Useful Commands

### `which` — Show Command Location

```bash
which ls
```

---

### `whereis` — Locate Binary, Source, and Manual

```bash
whereis ls
```

---

### `history` — Show Command History

```bash
history
```

---

<p align="center">
  🎉 You now know how to search, compare, locate, and use powerful Linux utility commands!
</p>
