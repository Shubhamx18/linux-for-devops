# File Transfer — Windows ↔ Linux & Remote ↔ Remote

---

## SCP — Secure Copy

SCP transfers files over SSH. It requires SSH access to the remote server.

### Local → Remote

```bash
scp file.txt alice@192.168.1.10:/home/alice/           # copy a file
scp -r myfolder/ alice@192.168.1.10:/home/alice/       # copy an entire folder
scp *.log alice@192.168.1.10:/home/alice/logs/          # copy multiple files (wildcard)
```

### Remote → Local

```bash
scp alice@192.168.1.10:/home/alice/file.txt .           # copy file (. = current dir)
scp -r alice@192.168.1.10:/home/alice/myfolder/ .       # copy folder
scp alice@192.168.1.10:/var/log/nginx/access.log ./     # copy a log file
```

### Remote → Remote (via your local machine)

```bash
scp alice@server1:/path/file.txt bob@server2:/path/
scp -r alice@server1:/home/alice/folder bob@server2:/home/bob/
```

### Remote → Remote (directly from Server 1)

```bash
ssh alice@server1
scp file.txt bob@server2:/home/bob/
```

### SCP Flags

```bash
scp -i ~/.ssh/key.pem file.txt alice@192.168.1.10:/home/alice/   # private key
scp -P 2222 file.txt alice@192.168.1.10:/home/alice/             # custom port
scp -p file.txt alice@192.168.1.10:/home/alice/                  # preserve permissions
scp -C file.txt alice@192.168.1.10:/home/alice/                  # compress during transfer
scp -v file.txt alice@192.168.1.10:/home/alice/                  # verbose
scp -l 500 file.txt alice@192.168.1.10:/home/alice/              # limit bandwidth (Kbps)
```

---

## rsync — Fast Syncing and Large Transfers

`rsync` is better than `scp` for large transfers and syncing — it only copies what changed, and can resume interrupted transfers.

```bash
# Basic transfer
rsync -avz file.txt alice@192.168.1.10:/home/alice/
rsync -avz myfolder/ alice@192.168.1.10:/home/alice/myfolder/

# Sync a directory (delete files on destination that don't exist in source)
rsync -avz --delete src/ alice@192.168.1.10:/dest/

# Dry run — show what would be transferred without actually doing it
rsync -avz --dry-run src/ alice@192.168.1.10:/dest/

# With SSH key
rsync -avz -e "ssh -i ~/.ssh/key.pem" myfolder/ alice@192.168.1.10:/dest/

# Custom SSH port
rsync -avz -e "ssh -p 2222" file.txt alice@192.168.1.10:/home/alice/

# Exclude files
rsync -avz --exclude "*.log" src/ alice@192.168.1.10:/dest/
rsync -avz --exclude-from=exclude.txt src/ alice@192.168.1.10:/dest/

# Show progress per file
rsync -avz --progress file.txt alice@192.168.1.10:/home/alice/

# Resume/partial transfers
rsync -avz --partial --progress largefile.iso alice@192.168.1.10:/home/alice/
```

| Flag | Meaning |
|------|---------|
| `-a` | Archive: recursive + preserve permissions, timestamps, symlinks, owner |
| `-v` | Verbose |
| `-z` | Compress data during transfer |
| `-P` | Shorthand for `--partial --progress` |
| `--delete` | Delete files in destination not present in source |
| `--dry-run` | Simulate without making any changes |

---

## SFTP — Interactive File Transfer

SFTP gives you an interactive shell to navigate and transfer files.

```bash
sftp alice@192.168.1.10
sftp -P 2222 alice@192.168.1.10         # custom port
sftp -i ~/.ssh/key.pem alice@192.168.1.10
```

Inside the SFTP session:

```
ls                   # list remote directory
lls                  # list local directory
pwd                  # show remote current directory
lpwd                 # show local current directory
cd folder            # change remote directory
lcd folder           # change local directory
mkdir folder         # create remote directory

get file.txt                  # download file to local current dir
get file.txt /local/dest/     # download to specific local path
get -r folder/                # download folder recursively

put file.txt                  # upload file to remote current dir
put file.txt /remote/dest/    # upload to specific remote path
put -r folder/                # upload folder recursively

rm file.txt          # delete a remote file
rmdir folder         # remove a remote directory
rename old new       # rename a remote file
chmod 755 file.sh    # change remote file permissions

df -h                # remote disk usage
exit / bye / quit    # close SFTP session
```

---

## WinSCP — Windows GUI File Transfer

WinSCP is a free Windows application for transferring files to/from Linux servers over SFTP or SCP.

### Initial Setup

1. Download and install WinSCP from winscp.net
2. Open WinSCP → New Site
3. File Protocol: **SFTP**
4. Host Name: your Linux server IP
5. Port: **22** (or your custom SSH port)
6. Username and password (or configure SSH key under Advanced → SSH → Authentication)
7. Click Login

### Transferring Files

- Left panel = your Windows machine
- Right panel = the remote Linux server
- Drag files between panels to transfer in either direction
- Folders transfer recursively

### Using SSH Keys in WinSCP

1. Advanced → SSH → Authentication
2. Private key file: browse to your `.ppk` file (WinSCP uses PuTTY format)
3. To convert an OpenSSH key to PuTTY format, use PuTTYgen

---

## Other Windows SSH/Transfer Tools

| Tool | Purpose |
|------|---------|
| PuTTY | SSH terminal client for Windows |
| MobaXterm | Terminal + file manager + X11 forwarding |
| Windows Terminal + OpenSSH | Built-in SSH on Windows 10/11 |
| FileZilla | GUI FTP/SFTP client (cross-platform) |

```bash
# Windows 10/11 have native OpenSSH — use from PowerShell or CMD:
ssh alice@192.168.1.10
scp file.txt alice@192.168.1.10:/home/alice/
```

---

## Common Transfer Errors

| Error | Cause | Fix |
|-------|-------|-----|
| `Permission denied` | Wrong credentials or key not authorized | Check username, password, or `~/.ssh/authorized_keys` |
| `Connection refused` | SSH service not running or wrong port | Check `systemctl status sshd` on the server |
| `No such file or directory` | Wrong remote path | Verify the path exists on the remote |
| `Connection timed out` | Firewall blocking port 22 | Check `ufw status` and security groups |
| `Host key verification failed` | Server fingerprint changed | Run `ssh-keygen -R <ip>` to clear old entry |
| `Too many authentication failures` | Too many keys being tried | Use `-o IdentitiesOnly=yes -i key.pem` |
