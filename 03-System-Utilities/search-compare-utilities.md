# Search, Compare & Useful Utilities

---

## grep — Search text inside files

```bash
grep "error" logfile.txt              # basic search
grep -i "error" logfile.txt           # case-insensitive
grep -n "error" logfile.txt           # show line numbers
grep -c "error" logfile.txt           # count matching lines (not the lines themselves)
grep -l "error" *.txt                 # list only filenames that match
grep -L "error" *.txt                 # list files that do NOT match
grep -v "error" logfile.txt           # invert — show non-matching lines
grep -r "error" /var/log/             # search recursively in directory
grep -rl "error" /var/log/            # recursive, filenames only
grep -A 3 "error" logfile.txt         # show 3 lines after match
grep -B 3 "error" logfile.txt         # show 3 lines before match
grep -C 3 "error" logfile.txt         # show 3 lines before and after
grep -w "error" logfile.txt           # match whole word only
grep -x "exactly this" file.txt       # match entire line
grep -m 5 "error" logfile.txt         # stop after 5 matches
grep -o "error[0-9]*" logfile.txt     # print only the matched part
grep -E "error|warn|crit" log.txt     # extended regex (OR)
grep -P "\d{3}-\d{4}" file.txt        # Perl-compatible regex
grep "^root" /etc/passwd              # lines starting with "root"
grep "bash$" /etc/passwd              # lines ending with "bash"
grep -e "error" -e "warn" log.txt     # multiple patterns
```

---

## find — Search files by any attribute

```bash
# By name
find /home/user -name "file.txt"          # exact name
find /home/user -name "*.log"             # by extension
find /home/user -iname "*.LOG"            # case-insensitive name
find . -name "*.txt" -not -name "temp*"   # name with exclusion

# By type
find . -type f                            # files only
find . -type d                            # directories only
find . -type l                            # symlinks only

# By size
find . -size +10M                         # larger than 10MB
find . -size -1k                          # smaller than 1KB
find . -size +1M -size -100M              # between 1MB and 100MB

# By time
find . -mtime -7                          # modified in last 7 days
find . -mtime +30                         # modified more than 30 days ago
find . -newer reference.txt               # modified after reference.txt
find . -atime -1                          # accessed in last 24 hours

# By permissions and owner
find . -perm 644                          # exact permissions
find . -perm /u+x                         # user has execute bit
find . -user alice                        # owned by alice
find . -group developers                  # owned by developers group

# Execute commands on results
find . -name "*.log" -delete              # delete all found files
find . -name "*.txt" -exec cat {} \;      # run command on each
find . -name "*.txt" -exec grep -l "error" {} \;
find . -type f -exec chmod 644 {} \;
find . -name "*.sh" -exec chmod +x {} \;
find / -name "nginx.conf" 2>/dev/null     # suppress permission errors

# Combining conditions
find . -type f -name "*.log" -size +1M    # AND (default)
find . -name "*.txt" -o -name "*.md"      # OR
find . -not -name "*.log"                 # NOT
```

---

## locate — Fast filename search

```bash
sudo updatedb                   # update the database first
locate nginx.conf               # search by name
locate -i readme                # case-insensitive
locate -c "*.conf"              # count results
locate -r "\.log$"              # regex pattern
```

`locate` is much faster than `find` but searches a database that's only updated periodically (via cron). Use `find` when you need real-time results.

---

## which / whereis / type

```bash
which python3                   # path of the command that runs
which -a python3                # all matching executables in PATH

whereis ls                      # binary, source, and manual page locations
whereis python3

type ls                         # whether it's alias, builtin, or file
type -a ls                      # all definitions
```

---

## diff — Compare files

```bash
diff file1.txt file2.txt              # line-by-line differences
diff -u file1.txt file2.txt           # unified format (easier to read, used in patches)
diff -i file1.txt file2.txt           # ignore case
diff -w file1.txt file2.txt           # ignore all whitespace
diff -B file1.txt file2.txt           # ignore blank lines
diff -r dir1/ dir2/                   # compare directories recursively
diff -q file1.txt file2.txt           # just say if files differ, no details
diff --side-by-side file1.txt file2.txt  # side-by-side comparison
```

Reading diff output:
```
< line only in file1
> line only in file2
--- separator
```

Unified format (`-u`) uses `+` for additions and `-` for removals — this is the standard patch format.

---

## cmp — Binary file comparison

```bash
cmp file1.txt file2.txt          # reports first byte that differs
cmp -l file1.txt file2.txt       # list all differing bytes
cmp -s file1.txt file2.txt       # silent, just return exit code (0=same, 1=differ)
```

`cmp` works on any file type including binaries. `diff` is better for text.

---

## Wildcards (Glob Patterns)

These are expanded by the shell before the command sees them.

| Pattern | Matches |
|---------|---------|
| `*` | Any string (including empty) |
| `?` | Any single character |
| `[abc]` | Any character in set |
| `[a-z]` | Any character in range |
| `[^abc]` | Any character NOT in set |
| `{a,b,c}` | Any of the listed strings |
| `**` | Any path (recursive, needs `globstar` in bash) |

```bash
ls *.txt                          # all .txt files
ls file?.txt                      # file1.txt, fileA.txt, etc.
ls file[1-3].txt                  # file1.txt, file2.txt, file3.txt
ls {*.txt,*.md}                   # all .txt and .md files
mv report-{jan,feb,mar}.txt /archive/  # brace expansion
```

---

## split — Split large files

```bash
split bigfile.txt part_           # 1000 lines per file: part_aa, part_ab, ...
split -l 500 bigfile.txt chunk_   # 500 lines per file
split -b 10M bigfile.tar chunk_   # split by size (10MB each)
split -n 4 bigfile.txt part_      # split into exactly 4 equal parts
cat part_* > reassembled.txt      # reassemble
```

---

## wc, shuf, and other small tools

```bash
shuf names.txt                    # shuffle lines randomly
shuf -n 5 names.txt               # pick 5 random lines
shuf -i 1-100 -n 10               # 10 random numbers between 1 and 100

# Count unique values
sort file.txt | uniq -c | sort -rn   # frequency count, most common first

# Check if two files are identical
md5sum file1 file2                # compare checksums
sha256sum file.txt                # more secure hash
diff -q file1 file2               # quick text comparison
```

---

## Reference Commands

```bash
man ls                    # full manual page
man 5 passwd              # section 5 (file formats)
man -k "copy files"       # search manuals by keyword

info coreutils            # GNU info pages (more detailed for some tools)

ls --help                 # quick usage summary
grep --help

history                   # show command history
history | grep ssh        # search history
!100                      # run command #100 from history
!!                        # run previous command
!ssh                      # run most recent command starting with ssh
Ctrl+R                    # reverse search through history
```
