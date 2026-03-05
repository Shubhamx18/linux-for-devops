# Copy, Move, Sort & Text Utilities

---

## sort — Sort file content

```bash
sort names.txt                    # alphabetical (ascending)
sort -r names.txt                 # reverse order
sort -n numbers.txt               # numeric sort (not lexicographic)
sort -rn numbers.txt              # numeric descending
sort -u names.txt                 # sort and remove duplicates
sort -f names.txt                 # case-insensitive sort
sort -k2 data.txt                 # sort by 2nd column
sort -k2 -n data.txt              # sort by 2nd column numerically
sort -t: -k3 -n /etc/passwd       # sort by 3rd field, colon-delimited
sort -h sizes.txt                 # human-readable number sort (1K, 2M, etc.)
sort names.txt -o sorted.txt      # write output to file instead of stdout
sort -R names.txt                 # random shuffle
```

---

## uniq — Remove duplicate lines

`uniq` only removes **consecutive** duplicates. Always sort first if you want all duplicates removed.

```bash
uniq names.txt                    # remove consecutive duplicates
sort names.txt | uniq             # sort then deduplicate all
sort names.txt | uniq -c          # prefix each line with occurrence count
sort names.txt | uniq -d          # show only duplicated lines
sort names.txt | uniq -u          # show only unique (non-duplicated) lines
sort names.txt | uniq -i          # case-insensitive deduplication
```

---

## head / tail — View specific lines

```bash
head file.txt                     # first 10 lines
head -n 25 file.txt               # first 25 lines
head -c 512 file.txt              # first 512 bytes

tail file.txt                     # last 10 lines
tail -n 25 file.txt               # last 25 lines
tail -f /var/log/syslog           # follow live updates
tail -F /var/log/app.log          # follow + reopen on rotation

# Combine — lines 20 to 30
head -n 30 file.txt | tail -n 11
```

---

## cut — Extract columns from text

```bash
cut -d ":" -f1 /etc/passwd        # first field, colon-separated
cut -d "," -f2,4 data.csv         # 2nd and 4th fields, comma-separated
cut -d " " -f1-3 file.txt         # fields 1 through 3
cut -c1-10 file.txt               # first 10 characters of each line
cut -c5- file.txt                 # from character 5 to end of line
cut --complement -d: -f1 file.txt # everything except field 1
```

---

## paste — Merge lines from files

```bash
paste file1.txt file2.txt         # merge side by side (tab-separated)
paste -d "," file1.txt file2.txt  # use comma as separator
paste -s file.txt                 # merge all lines of one file into one line
```

---

## tr — Translate or delete characters

```bash
tr 'a-z' 'A-Z' < file.txt        # lowercase to uppercase
tr 'A-Z' 'a-z' < file.txt        # uppercase to lowercase
tr -d '0-9' < file.txt           # delete all digits
tr -d '[:punct:]' < file.txt     # delete all punctuation
tr -d '\r' < file.txt            # remove Windows carriage returns
tr ' ' '\n' < file.txt           # replace spaces with newlines
tr -s ' ' < file.txt             # squeeze multiple spaces into one
tr -cd '[:print:]' < file.txt    # keep only printable characters
echo "hello" | tr 'a-z' 'A-Z'   # works inline
```

---

## wc — Count lines, words, bytes

```bash
wc file.txt                       # lines, words, bytes
wc -l file.txt                    # line count only
wc -w file.txt                    # word count only
wc -c file.txt                    # byte count
wc -m file.txt                    # character count
wc -L file.txt                    # length of longest line
wc -l *.txt                       # count lines in multiple files
cat file.txt | wc -l              # pipe input
```

---

## fold / fmt — Format line length

```bash
fold -w 80 file.txt               # wrap lines at 80 characters
fold -s -w 80 file.txt            # wrap at word boundaries
fmt file.txt                      # reformat paragraphs to ~75 chars
fmt -w 100 file.txt               # set target line width
```

---

## column — Align output into columns

```bash
column -t file.txt                # auto-align whitespace-separated data
column -t -s "," data.csv         # align CSV data
mount | column -t                 # useful for making tabular output readable
```

---

## tee — Read from stdin, write to file and stdout

```bash
command | tee output.txt          # show output AND save to file
command | tee -a output.txt       # append instead of overwrite
command | tee file1.txt file2.txt # write to multiple files
```

Useful when you want to both see output and log it.

---

## xargs — Pass stdin as arguments

```bash
cat files.txt | xargs rm                       # delete files listed in a file
find . -name "*.log" | xargs rm                # delete all found log files
find . -name "*.txt" | xargs grep "error"      # search inside found files
echo "one two three" | xargs -n 1 echo        # one argument per line
find . -name "*.jpg" | xargs -I{} mv {} /backup/  # move with placeholder
cat urls.txt | xargs -P 4 wget                 # parallel downloads (4 at a time)
```

---

## Path Concepts Quick Reference

| Notation | Meaning | Example |
|----------|---------|---------|
| `/` | Root (start of absolute path) | `/etc/nginx/nginx.conf` |
| `~` | Home directory | `~/projects/app` |
| `.` | Current directory | `./script.sh` |
| `..` | Parent directory | `../config.yaml` |
| `-` | Previous directory (cd only) | `cd -` |
