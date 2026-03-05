# Shell Scripting

---

## Creating and Running Scripts

```bash
nano script.sh          # create script file
chmod +x script.sh      # make it executable
./script.sh             # run it
bash script.sh          # run without executable permission
sh script.sh            # run with POSIX sh
```

Every script should start with a shebang — the first line that tells the OS which interpreter to use:

```bash
#!/bin/bash              # use bash (most common)
#!/bin/sh                # use POSIX sh (portable, no bash-specific features)
#!/usr/bin/env bash      # find bash via PATH (better for portability)
```

### Minimal script

```bash
#!/bin/bash
echo "Hello, world"
```

---

## Variables

```bash
name="alice"
age=30

echo $name
echo "Hello, $name"
echo "Hello, ${name}!"      # braces recommended to avoid ambiguity

# Reading input
read username
read -p "Enter your name: " username
read -sp "Enter password: " password    # -s hides input
echo ""
```

Variable naming: no spaces around `=`. Use lowercase for local vars, UPPERCASE for exported/env vars.

---

## Special Variables

| Variable | Meaning |
|----------|---------|
| `$0` | Script name |
| `$1`, `$2` ... `$9` | Positional arguments |
| `${10}`, `${11}` | Arguments beyond 9 (need braces) |
| `$#` | Number of arguments passed |
| `$@` | All arguments as separate words |
| `$*` | All arguments as a single string |
| `$?` | Exit code of last command (0 = success) |
| `$$` | PID of the current script |
| `$!` | PID of last background process |

```bash
#!/bin/bash
echo "Script name: $0"
echo "First arg:   $1"
echo "All args:    $@"
echo "Arg count:   $#"
```

---

## Arithmetic

```bash
a=10
b=3

echo $((a + b))       # 13
echo $((a - b))       # 7
echo $((a * b))       # 30
echo $((a / b))       # 3 (integer division)
echo $((a % b))       # 1 (remainder)
echo $((a ** b))      # 1000 (exponent)

# Increment
((a++))
((a--))
((a += 5))
((a *= 2))

# Using let
let result=a+b
echo $result

# Floating point (requires bc or awk)
echo "scale=2; 10 / 3" | bc       # 3.33
awk "BEGIN {print 10/3}"           # 3.33333
```

---

## Conditionals

```bash
if [ $a -gt 5 ]; then
  echo "greater than 5"
elif [ $a -eq 5 ]; then
  echo "equal to 5"
else
  echo "less than 5"
fi
```

### Integer Comparisons

| Operator | Meaning |
|----------|---------|
| `-eq` | Equal |
| `-ne` | Not equal |
| `-gt` | Greater than |
| `-lt` | Less than |
| `-ge` | Greater or equal |
| `-le` | Less or equal |

### String Comparisons

```bash
if [ "$name" == "alice" ]; then echo "match"; fi
if [ "$name" != "root" ]; then echo "not root"; fi
if [ -z "$name" ]; then echo "empty string"; fi
if [ -n "$name" ]; then echo "not empty"; fi
```

### File Tests

```bash
if [ -f file.txt ]; then echo "is a file"; fi
if [ -d folder ]; then echo "is a directory"; fi
if [ -e path ]; then echo "exists (file or dir)"; fi
if [ -r file.txt ]; then echo "readable"; fi
if [ -w file.txt ]; then echo "writable"; fi
if [ -x script.sh ]; then echo "executable"; fi
if [ -s file.txt ]; then echo "not empty (has content)"; fi
if [ -L link ]; then echo "is a symlink"; fi
```

### Logical Operators

```bash
# AND
if [ $a -gt 0 ] && [ $a -lt 100 ]; then echo "in range"; fi
if [[ $a -gt 0 && $a -lt 100 ]]; then echo "in range"; fi

# OR
if [ $a -lt 0 ] || [ $a -gt 100 ]; then echo "out of range"; fi

# NOT
if ! [ -f file.txt ]; then echo "file does not exist"; fi
```

### Single-line Shortcuts

```bash
[ -f file.txt ] && echo "exists"         # run if condition true
[ -f file.txt ] || echo "missing"        # run if condition false
command && echo "ok" || echo "failed"    # if/else in one line
```

---

## Loops

### for Loop

```bash
# Over a list
for name in alice bob carol; do
  echo "Hello, $name"
done

# Over a range
for i in {1..10}; do
  echo $i
done

# Range with step
for i in {0..20..5}; do
  echo $i
done

# C-style
for ((i=0; i<5; i++)); do
  echo $i
done

# Over files
for file in *.txt; do
  echo "Processing $file"
done

# Over command output
for user in $(cat users.txt); do
  echo "User: $user"
done
```

### while Loop

```bash
count=1
while [ $count -le 5 ]; do
  echo $count
  ((count++))
done

# Read a file line by line
while IFS= read -r line; do
  echo "$line"
done < file.txt

# Infinite loop
while true; do
  echo "running..."
  sleep 5
done
```

### until Loop

Runs until the condition becomes true (opposite of while).

```bash
count=1
until [ $count -gt 5 ]; do
  echo $count
  ((count++))
done
```

### Loop Control

```bash
break       # exit the loop immediately
continue    # skip to the next iteration
```

---

## Case Statement

```bash
read -p "Enter option: " choice
case $choice in
  1)
    echo "Option one"
    ;;
  2|3)
    echo "Option two or three"
    ;;
  "yes"|"y")
    echo "Confirmed"
    ;;
  *)
    echo "Invalid option"
    ;;
esac
```

---

## Functions

```bash
# Define
greet() {
  echo "Hello, $1"
}

# Call
greet alice
greet world

# Function with return value
add() {
  echo $(($1 + $2))
}

result=$(add 5 3)
echo "Result: $result"

# Return exit code
check_file() {
  if [ -f "$1" ]; then
    return 0   # success
  else
    return 1   # failure
  fi
}

check_file file.txt && echo "found" || echo "not found"
```

---

## String Operations

```bash
str="Hello World"

echo ${#str}              # length: 11
echo ${str:0:5}           # substring: Hello
echo ${str:6}             # from position 6: World
echo ${str^^}             # uppercase: HELLO WORLD
echo ${str,,}             # lowercase: hello world
echo ${str/World/Linux}   # replace first: Hello Linux
echo ${str//l/L}          # replace all: HeLLo WorLd

# Remove prefix/suffix
filename="report.tar.gz"
echo ${filename%.gz}      # remove .gz: report.tar
echo ${filename%%.*}      # remove everything after first dot: report
echo ${filename#*.}       # remove up to first dot: tar.gz
echo ${filename##*.}      # remove up to last dot: gz

# Default value if variable is unset
echo ${name:-"unknown"}   # print unknown if $name is empty
name=${name:-"default"}   # assign default if name is unset
```

---

## Command Substitution

```bash
today=$(date)
echo "Today is: $today"

file_count=$(ls | wc -l)
echo "There are $file_count files"

# Old-style backticks (avoid — harder to nest)
today=`date`
```

---

## Output Redirection

```bash
echo "hello" > file.txt           # write (overwrite)
echo "world" >> file.txt          # append
command 2> errors.txt             # redirect stderr only
command > out.txt 2>&1            # redirect stdout and stderr to same file
command &> out.txt                # same (bash shorthand)
command > /dev/null               # discard stdout
command > /dev/null 2>&1          # discard everything
```

---

## Exit Status and Error Handling

```bash
ls /some/path
echo $?          # 0 = success, non-zero = failure

# Exit on first error
set -e

# Treat unset variables as errors
set -u

# Catch pipe failures (e.g., command1 | command2 — if command1 fails)
set -o pipefail

# Recommended at the top of scripts
set -euo pipefail

# Custom exit codes
exit 0          # success
exit 1          # generic failure
exit 2          # misuse of command

# Check a command's success
if ! command -v docker &>/dev/null; then
  echo "Docker is not installed"
  exit 1
fi
```

---

## Debugging

```bash
bash -x script.sh          # trace every command as it runs
bash -v script.sh          # print each line before executing

# Inside the script
set -x                     # enable tracing from this point
set +x                     # disable tracing

# Print useful debug info
echo "DEBUG: variable=$variable" >&2    # print to stderr
```

---

## Practical Script Template

```bash
#!/bin/bash
set -euo pipefail

# --- Config ---
LOG_FILE="/var/log/myscript.log"
BACKUP_DIR="/home/alice/backups"

# --- Functions ---
log() {
  echo "[$(date '+%Y-%m-%d %H:%M:%S')] $1" | tee -a "$LOG_FILE"
}

die() {
  log "ERROR: $1"
  exit 1
}

# --- Main ---
log "Script started"

[ -d "$BACKUP_DIR" ] || mkdir -p "$BACKUP_DIR"

if ! ping -c 1 -W 2 8.8.8.8 &>/dev/null; then
  die "No internet connectivity"
fi

log "All checks passed"
```

---

## Scheduling with Cron

```bash
crontab -e          # edit your cron jobs
crontab -l          # list current jobs
```

```
# Run every day at 2 AM
0 2 * * * /home/alice/backup.sh >> /var/log/backup.log 2>&1

# Every 5 minutes
*/5 * * * * /home/alice/check.sh

# Once on reboot
@reboot /home/alice/startup.sh
```
