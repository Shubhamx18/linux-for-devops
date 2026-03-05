# File & Directory Management

---

## Viewing File Content

```bash
cat file.txt              # print entire file
cat -n file.txt           # print with line numbers
cat -A file.txt           # show special characters (tabs, line endings)

tac file.txt              # print file in reverse (last line first)

less file.txt             # scroll through file (recommended for large files)
                          # j/k or arrows to scroll, q to quit, /term to search

more file.txt             # older pager, forward-only

head file.txt             # first 10 lines
head -n 20 file.txt       # first 20 lines
head -c 100 file.txt      # first 100 bytes

tail file.txt             # last 10 lines
tail -n 20 file.txt       # last 20 lines
tail -f /var/log/syslog   # follow live (great for log monitoring)
tail -F /var/log/syslog   # follow + reopen if file rotates

# View specific line range
sed -n '10,20p' file.txt  # lines 10 to 20
awk 'NR>=10 && NR<=20' file.txt
```

`less` shortcuts: `Space` = next page, `b` = back, `g` = top, `G` = bottom, `q` = quit, `/word` = search

---

## Creating Files

```bash
touch file.txt                     # create empty file (or update timestamp)
touch file1.txt file2.txt          # create multiple files at once
touch -t 202401010000 file.txt     # set specific timestamp

echo "hello world" > file.txt      # create file with content (overwrites)
echo "more content" >> file.txt    # append to file

printf "line1\nline2\n" > file.txt # write with formatting

cat > file.txt                     # type content, Ctrl+D when done
cat >> file.txt                    # append, Ctrl+D when done

# Create file from heredoc
cat > file.txt << EOF
line one
line two
EOF
```

---

## Creating Directories

```bash
mkdir docs                         # create directory
mkdir -p project/src/utils         # create nested path (no error if exists)
mkdir -m 755 public                # create with specific permissions
mkdir dir1 dir2 dir3               # create multiple at once

# Create date-stamped backup dir
mkdir backup-$(date +%Y-%m-%d)
```

---

## Deleting Files and Directories

```bash
rm file.txt                        # delete file
rm file1.txt file2.txt             # delete multiple files
rm *.log                           # delete by wildcard
rm -i file.txt                     # prompt before each delete
rm -f file.txt                     # force delete, no error if not found
rm -r myfolder                     # delete directory and contents
rm -rf myfolder                    # force recursive delete — no prompt
rm -rf /path/to/dir/*              # delete contents but keep directory

rmdir emptydir                     # delete empty directory only
rmdir -p a/b/c                     # remove nested empty dirs

# Safer mass deletion — preview first
ls *.tmp                           # check what matches
rm *.tmp                           # then delete
```

> `rm -rf` is permanent. There is no trash bin. Double-check the path before running.

---

## Copying Files and Directories

```bash
cp file.txt backup.txt                    # copy and rename
cp file.txt /home/user/docs/              # copy to directory
cp file1.txt file2.txt /destination/      # copy multiple files
cp -r myfolder/ backupfolder/            # copy directory recursively
cp -p file.txt backup.txt                # preserve permissions and timestamps
cp -u file.txt dest/                     # copy only if newer than destination
cp -i file.txt dest/                     # prompt before overwriting
cp -v file.txt dest/                     # verbose — show what's copied
cp -a source/ dest/                      # archive: recursive + preserve all attributes
cp ../file.txt .                         # copy from parent to current directory
```

---

## Moving and Renaming

```bash
mv file.txt /home/user/docs/             # move file
mv oldname.txt newname.txt               # rename file
mv oldfolder/ newfolder/                 # rename directory
mv file.txt /path/to/dir/newname.txt     # move and rename at once
mv -i file.txt dest/                     # prompt before overwriting
mv -u file.txt dest/                     # move only if source is newer
mv -v file.txt dest/                     # verbose output
mv *.txt /home/user/docs/                # move all .txt files
```

---

## File Links

```bash
# Hard link — same file, different name
ln file.txt hardlink.txt

# Symbolic (soft) link — pointer to another path
ln -s /path/to/original symlink.txt
ln -s /usr/local/bin/python3 /usr/local/bin/python

# List symlinks
ls -la | grep ^l

# Remove a symlink
unlink symlink.txt
rm symlink.txt
```

Hard links share the same inode (same data, multiple names). Symlinks are separate files pointing to a path.

---

## Text Editors

### nano — beginner friendly

```bash
nano file.txt
```

| Action | Keys |
|--------|------|
| Save | Ctrl+O, then Enter |
| Exit | Ctrl+X |
| Search | Ctrl+W |
| Cut line | Ctrl+K |
| Paste | Ctrl+U |
| Go to line | Ctrl+_ |

### vim — powerful, ubiquitous

```bash
vim file.txt
vi file.txt     # same on most systems
```

Vim is modal — you're either viewing or editing.

| Mode | How to enter |
|------|-------------|
| Normal | `Esc` |
| Insert | `i` (before cursor), `a` (after), `o` (new line below) |
| Visual | `v` (char), `V` (line), `Ctrl+v` (block) |
| Command | `:` from normal mode |

Common normal mode commands:
```
dd        delete current line
yy        yank (copy) current line
p         paste
u         undo
Ctrl+r    redo
/word     search forward
n         next match
:w        save
:q        quit
:wq       save and quit
:q!       quit without saving
:set nu   show line numbers
:%s/old/new/g   find and replace all
```

### nano vs vim

Use nano when you just need to make a quick edit. Learn vim because it's on every server, even minimal installs, and nothing else comes close for efficiency once learned.
