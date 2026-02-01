<h1 align="center">📦 Day 7 – Archives, Downloads, Environment Variables & Text Processing</h1>

<p align="center">
  <img src="https://img.shields.io/badge/Linux-Utilities-FCC624?style=for-the-badge&logo=linux&logoColor=black"/>
  <img src="https://img.shields.io/badge/Day-7-Terminal_Skills-success?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Level-Intermediate-blue?style=for-the-badge"/>
</p>

<p align="center">
  Learn compression, downloading files, calling APIs, environment variables, and powerful text processing commands.
</p>

---

# 🏷️ `alias` — Create Shortcut Commands

Temporary alias:
```bash
alias ll='ls -la'
```

Permanent alias (add to `~/.bashrc`):
```bash
alias ll='ls -la'
source ~/.bashrc
```

---

# 📦 ZIP COMMANDS

### Zip single file
```bash
zip archive.zip file.txt
```

### Zip multiple files
```bash
zip archive.zip file1.txt file2.txt
```

### Zip folder
```bash
zip -r archive.zip myfolder
```

### Zip multiple folders
```bash
zip -r archive.zip folder1 folder2
```

### List zip contents
```bash
unzip -l archive.zip
```

### Extract zip
```bash
unzip archive.zip
```

### Extract to folder
```bash
unzip archive.zip -d output_folder
```

### Delete file from zip
```bash
zip -d archive.zip file.txt
```

---

# 📦 GZIP COMMANDS

### Compress file
```bash
gzip file.txt
```

### Keep original file
```bash
gzip -k file.txt
```

### Decompress
```bash
gzip -d file.txt.gz
```

or

```bash
gunzip file.txt.gz
```

---

# 📦 TAR ARCHIVES

### Create tar archive
```bash
tar -cf archive.tar myfolder
```

### Extract tar archive
```bash
tar -xf archive.tar
```

### Create compressed tar.gz
```bash
tar -czf archive.tar.gz myfolder
```

### Extract tar.gz
```bash
tar -xzf archive.tar.gz
```

---

# 🌐 DOWNLOAD FILES FROM INTERNET

### Using wget
```bash
wget https://example.com/file.txt
```

### Using curl
```bash
curl -O https://example.com/file.txt
```

---

# 🔗 CALL AN API USING curl

```bash
curl https://api.github.com
```

With headers:
```bash
curl -H "Accept: application/json" https://api.github.com
```

---

# 🌱 ENVIRONMENT VARIABLES

### Temporary variable
```bash
export NAME="Shubham"
echo $NAME
```

### Permanent variable
Add to `~/.bashrc`
```bash
export NAME="Shubham"
```
Then:
```bash
source ~/.bashrc
```

---

# 📊 `cut` — Print Columns

Print first column:
```bash
cut -d " " -f1 file.txt
```

First two characters:
```bash
cut -c1-2 file.txt
```

---

# 📄 Display Specific Line

```bash
sed -n '5p' file.txt
```

---

# 🔄 `tr` — Text Transformation

Lowercase to uppercase:
```bash
tr 'a-z' 'A-Z' < file.txt
```

Uppercase to lowercase:
```bash
tr 'A-Z' 'a-z' < file.txt
```

Delete digits:
```bash
tr -d '0-9' < file.txt
```

Delete punctuation:
```bash
tr -d '[:punct:]' < file.txt
```

Replace spaces with newline:
```bash
tr ' ' '\n' < file.txt
```

---

# 📏 EXTEND / SHRINK LINES

Wrap long lines:
```bash
fold -w 20 file.txt
```

Format nicely:
```bash
fmt file.txt
```

---

# 📊 DISPLAY TEXT VERTICALLY

```bash
column -t file.txt
```

---

<p align="center">
  🎉 You now know how to compress files, download data, use APIs, manage environment variables, and process text like a Linux pro!
</p>
