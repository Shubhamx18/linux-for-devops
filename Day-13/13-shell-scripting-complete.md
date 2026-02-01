<h1 align="center">🐚 Day 13 – Shell Scripting Complete Guide</h1>

<p align="center">
  <img src="https://img.shields.io/badge/Linux-Shell_Scripting-FCC624?style=for-the-badge&logo=gnu-bash&logoColor=black"/>
  <img src="https://img.shields.io/badge/Day-13-Automation-success?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Level-DevOps_Foundation-blue?style=for-the-badge"/>
</p>

<p align="center">
  Learn how to write, run, and automate tasks using Bash shell scripts from beginner to advanced level.
</p>

---

# 📜 What is Shell Scripting?

Shell scripting is writing a set of Linux commands in a file to automate tasks.

Used for:
- Automation  
- DevOps pipelines  
- System maintenance  
- Backups  

---

# 📝 Creating Your First Script

Create file:
```bash
nano script.sh
```

Add:
```bash
#!/bin/bash
echo "Hello Shubham"
```

Make executable:
```bash
chmod +x script.sh
```

Run:
```bash
./script.sh
```

---

# 🔤 Variables

```bash
name="Shubham"
echo "Hello $name"
```

User input:
```bash
read username
echo "Welcome $username"
```

---

# 🔢 Special Variables

| Variable | Meaning |
|----------|---------|
| `$0` | Script name |
| `$1, $2...` | Command line arguments |
| `$#` | Number of arguments |
| `$@` | All arguments |
| `$?` | Exit status |

---

# ➕ Arithmetic Operations

```bash
a=10
b=5
echo $((a + b))
```

Using expr:
```bash
expr $a + $b
```

---

# 🔀 Conditional Statements

## if statement
```bash
if [ $a -gt 5 ]; then
  echo "Greater"
fi
```

## if-else
```bash
if [ $a -gt 5 ]; then
  echo "Greater"
else
  echo "Smaller"
fi
```

## if-elif
```bash
if [ $a -eq 1 ]; then
  echo "One"
elif [ $a -eq 2 ]; then
  echo "Two"
else
  echo "Other"
fi
```

---

# 🔁 Loops

## for loop
```bash
for i in 1 2 3 4 5
do
  echo $i
done
```

## while loop
```bash
count=1
while [ $count -le 5 ]
do
  echo $count
  ((count++))
done
```

## until loop
```bash
count=1
until [ $count -gt 5 ]
do
  echo $count
  ((count++))
done
```

---

# 🔄 Case Statement

```bash
read choice
case $choice in
  1) echo "One" ;;
  2) echo "Two" ;;
  *) echo "Invalid" ;;
esac
```

---

# 🧠 Functions

```bash
function greet() {
  echo "Hello $1"
}

greet Shubham
```

---

# 📂 File Testing

| Test | Meaning |
|------|---------|
| `-f` | File exists |
| `-d` | Directory exists |
| `-r` | Readable |
| `-w` | Writable |
| `-x` | Executable |

```bash
if [ -f file.txt ]; then
  echo "File exists"
fi
```

---

# 📊 String Operations

```bash
str="Linux"
echo ${#str}     # Length
echo ${str:0:3}  # Substring
```

---

# 🔧 Command Substitution

```bash
today=$(date)
echo "Today is $today"
```

---

# 📤 Redirecting Output

```bash
echo "Hello" > file.txt
echo "Again" >> file.txt
```

---

# 📌 Exit Status

```bash
ls
echo $?   # 0 = success
```

---

# ⚠️ Debugging Scripts

```bash
bash -x script.sh
```

---

# 🧾 Scheduling Scripts (Cron)

```bash
crontab -e
```

Example:
```
0 2 * * * /home/user/script.sh
```

---

# 🔒 Shebang Variations

| Shebang | Meaning |
|---------|---------|
| `#!/bin/bash` | Bash shell |
| `#!/bin/sh` | POSIX shell |
| `#!/usr/bin/env bash` | Portable bash path |

---

# 🚀 Best Practices

✔ Use comments  
✔ Use meaningful variable names  
✔ Handle errors  
✔ Quote variables `"${var}"`  
✔ Use functions for reuse  

---

<p align="center">
  🎉 You now understand shell scripting fundamentals used in automation and DevOps!
</p>
