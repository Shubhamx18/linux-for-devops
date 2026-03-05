# Archives, Downloads & Text Processing

---

## zip / unzip

```bash
zip archive.zip file.txt                   # zip single file
zip archive.zip file1.txt file2.txt        # zip multiple files
zip -r archive.zip myfolder/               # zip entire directory
zip -r archive.zip dir1/ dir2/             # zip multiple directories
zip -e archive.zip file.txt                # encrypt with password
zip -9 archive.zip file.txt                # maximum compression
zip -j archive.zip path/to/file.txt        # store without directory structure
zip -u archive.zip newfile.txt             # update/add files to existing zip
zip -d archive.zip file.txt                # remove file from zip

unzip archive.zip                          # extract to current directory
unzip archive.zip -d /output/folder/       # extract to specific directory
unzip -l archive.zip                       # list contents without extracting
unzip -t archive.zip                       # test archive integrity
unzip -o archive.zip                       # overwrite existing files
unzip -n archive.zip                       # never overwrite existing files
unzip -p archive.zip file.txt              # extract single file to stdout
unzip "archive.zip" "*.txt" -d output/     # extract only .txt files
```

---

## gzip / gunzip

gzip compresses a single file and replaces it (no archiving).

```bash
gzip file.txt                              # compress (replaces original)
gzip -k file.txt                           # compress and keep original
gzip -9 file.txt                           # maximum compression
gzip -1 file.txt                           # fastest compression
gzip -v file.txt                           # verbose — show compression ratio
gzip -l file.txt.gz                        # list compression info
gzip -d file.txt.gz                        # decompress
gzip -r directory/                         # compress all files in directory

gunzip file.txt.gz                         # same as gzip -d
zcat file.txt.gz                           # view compressed file without extracting
zless file.txt.gz                          # page through compressed file
zgrep "error" file.txt.gz                  # grep inside compressed file
```

---

## tar

`tar` archives multiple files into one. Often combined with gzip for `.tar.gz` (also called tarballs).

```bash
# Create archives
tar -cf archive.tar myfolder/             # create tar (no compression)
tar -czf archive.tar.gz myfolder/         # create + gzip compress
tar -cjf archive.tar.bz2 myfolder/        # create + bzip2 compress
tar -cJf archive.tar.xz myfolder/         # create + xz compress (best ratio)
tar -czf archive.tar.gz dir1/ dir2/       # archive multiple directories
tar -czf archive.tar.gz -C /path dir/     # change to /path before archiving

# Extract archives
tar -xf archive.tar                       # extract tar
tar -xzf archive.tar.gz                   # extract tar.gz
tar -xjf archive.tar.bz2                  # extract tar.bz2
tar -xJf archive.tar.xz                   # extract tar.xz
tar -xzf archive.tar.gz -C /output/       # extract to specific directory
tar -xzf archive.tar.gz specificfile.txt  # extract one file

# Inspect archives
tar -tf archive.tar                       # list contents
tar -tzf archive.tar.gz                   # list contents of compressed archive
tar -tvf archive.tar                      # list with details (permissions, size)

# Append and update
tar -rf archive.tar newfile.txt           # append file to existing tar
tar -uf archive.tar file.txt              # update if file is newer

# Common flags
# -c  create
# -x  extract
# -t  list
# -f  filename (always needed)
# -z  gzip
# -j  bzip2
# -J  xz
# -v  verbose
# -C  change to directory
# -p  preserve permissions
# --exclude=pattern  skip matching files
```

Example: backup and restore:
```bash
tar -czf backup-$(date +%Y%m%d).tar.gz /home/user/
tar -xzf backup-20240310.tar.gz -C /restore/
```

---

## bzip2 / xz

```bash
bzip2 file.txt                    # compress (replaces original)
bzip2 -k file.txt                 # keep original
bzip2 -d file.txt.bz2             # decompress
bunzip2 file.txt.bz2              # same as bzip2 -d
bzcat file.txt.bz2                # view without extracting

xz file.txt                       # compress with xz (best ratio, slowest)
xz -k file.txt                    # keep original
xz -d file.txt.xz                 # decompress
xzcat file.txt.xz                 # view without extracting
```

Compression comparison: gzip = fast, bzip2 = slower/better, xz = slowest/best ratio.

---

## wget — Download files

```bash
wget https://example.com/file.tar.gz               # download file
wget -c https://example.com/file.tar.gz            # resume interrupted download
wget -O newname.tar.gz https://example.com/file    # save with custom name
wget -P /downloads/ https://example.com/file.zip  # save to specific directory
wget -q https://example.com/file                   # quiet mode
wget --no-check-certificate https://...            # skip SSL verification
wget -r -np https://example.com/docs/             # recursive download
wget --limit-rate=1m https://example.com/big.iso  # limit download speed
wget -i urls.txt                                   # download list of URLs from file
wget --spider https://example.com/file            # check if URL exists (no download)
wget --tries=3 https://example.com/file           # retry up to 3 times
```

---

## curl — HTTP requests and downloads

```bash
# Basic requests
curl https://example.com                              # GET request
curl -o file.zip https://example.com/file.zip         # download to file
curl -O https://example.com/file.zip                  # download keeping remote name
curl -I https://example.com                           # headers only (HEAD request)
curl -L https://example.com                           # follow redirects
curl -s https://api.github.com                        # silent (no progress bar)
curl -v https://example.com                           # verbose (see full request/response)

# POST requests
curl -X POST https://example.com/api \
  -d "name=alice&age=30"                              # form data
curl -X POST https://example.com/api \
  -H "Content-Type: application/json" \
  -d '{"name":"alice","age":30}'                      # JSON body

# Headers and auth
curl -H "Authorization: Bearer token123" https://api.example.com
curl -H "Accept: application/json" https://api.example.com
curl -u username:password https://example.com/api    # basic auth

# Other methods
curl -X PUT -d '{"status":"active"}' https://api/resource/1
curl -X DELETE https://api/resource/1
curl -X PATCH -d '{"field":"value"}' https://api/resource/1

# Useful options
curl -w "%{http_code}\n" https://example.com          # print HTTP status code
curl --retry 3 https://example.com                    # retry on failure
curl --connect-timeout 10 https://example.com         # connection timeout
curl -k https://self-signed.example.com               # ignore SSL errors
curl --proxy http://proxy:8080 https://example.com    # use proxy
```

---

## Environment Variables

```bash
# View variables
env                               # list all environment variables
printenv                          # same
printenv HOME                     # print one variable
echo $HOME
echo $PATH
echo $USER
echo $SHELL

# Set temporary (current session only)
export NAME="alice"
export PATH="$PATH:/usr/local/go/bin"

# Set permanent — add to config file
echo 'export NAME="alice"' >> ~/.bashrc
source ~/.bashrc                  # reload (or start new shell)

# Unset a variable
unset NAME

# Use variable in string
echo "Hello, $NAME"
echo "Hello, ${NAME}"            # braces avoid ambiguity with longer names
echo "Home: ${HOME}/projects"

# Default value if unset
echo ${NAME:-"unknown"}          # use "unknown" if NAME is not set
echo ${PORT:-8080}               # common pattern for optional env vars

# Common system variables
echo $HOME        # home directory
echo $PATH        # executable search path
echo $USER        # current username
echo $HOSTNAME    # machine name
echo $SHELL       # current shell
echo $PWD         # current directory
echo $OLDPWD      # previous directory
echo $EDITOR      # default text editor
echo $LANG        # locale setting
echo $TERM        # terminal type
```

---

## alias — Shortcut commands

```bash
# Create alias (current session only)
alias ll='ls -la'
alias la='ls -A'
alias grep='grep --color=auto'
alias ..='cd ..'
alias ...='cd ../..'
alias ports='ss -tulnp'
alias update='sudo apt update && sudo apt upgrade -y'

# List all aliases
alias

# Remove alias
unalias ll

# Make permanent — add to ~/.bashrc or ~/.bash_aliases
echo "alias ll='ls -la'" >> ~/.bashrc
source ~/.bashrc
```

---

## sed — Stream editor

```bash
sed -n '5p' file.txt                # print line 5 only
sed -n '5,10p' file.txt             # print lines 5 to 10
sed 's/old/new/' file.txt           # replace first occurrence per line
sed 's/old/new/g' file.txt          # replace all occurrences
sed 's/old/new/gi' file.txt         # replace all, case-insensitive
sed -i 's/old/new/g' file.txt       # edit file in place
sed -i.bak 's/old/new/g' file.txt   # edit in place, save backup as .bak
sed '/^$/d' file.txt                # delete empty lines
sed '/^#/d' file.txt                # delete comment lines
sed '5d' file.txt                   # delete line 5
sed '5,10d' file.txt                # delete lines 5 to 10
sed 's/^/    /' file.txt            # indent every line
sed 's/ *$//' file.txt              # remove trailing whitespace
sed -n '/error/p' log.txt           # print only lines containing "error"
sed 's/\t/,/g' file.txt            # replace tabs with commas
```

---

## awk — Text processing and field manipulation

```bash
awk '{print $1}' file.txt             # print first field
awk '{print $1, $3}' file.txt         # print fields 1 and 3
awk -F: '{print $1}' /etc/passwd      # colon delimiter, print username
awk -F, '{print $2}' data.csv         # CSV, print second column
awk 'NR==5' file.txt                  # print line 5
awk 'NR>=5 && NR<=10' file.txt        # print lines 5-10
awk '/error/' log.txt                 # print lines matching pattern
awk '!/error/' log.txt                # print lines NOT matching
awk '{sum += $1} END {print sum}' file.txt     # sum first column
awk -F: '$3 >= 1000 {print $1}' /etc/passwd   # users with UID >= 1000
awk '{print NR, $0}' file.txt         # print line numbers
awk 'END {print NR}' file.txt         # count total lines (like wc -l)
awk -F: '{print $1": "$NF}' /etc/passwd  # username and shell
```
