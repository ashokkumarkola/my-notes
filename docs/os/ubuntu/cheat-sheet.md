# Ubuntu Cheat Sheet

## Navigation + files

```bash
pwd; ls -lah; cd ~; cd -              # where, list, home, previous
mkdir -p a/b/c
touch f.txt
cp -r src dst
mv old new
rm -rf dir                            # no undo
cat f; less f; head -n 20 f; tail -f log
ln -s target link                     # symlink
tree -L 2 -I 'node_modules|.venv'
```

## Search

```bash
find . -name "*.md"
find . -type f -size +100M
grep -rn "text" .
grep -rni "text" --include=*.py .
```

## Permissions

```bash
chmod +x script.sh
chmod 644 f          # rw-r--r--
chmod 755 d          # rwxr-xr-x
chmod 400 key.pem    # owner read only
chown user:group f
sudo !!              # rerun last command with sudo
```

| Digit | Permission |
|---|---|
| 4 | read |
| 2 | write |
| 1 | execute |

Order: owner · group · others.

## Packages

```bash
sudo apt update                       # refresh index
sudo apt upgrade -y
sudo apt install -y git curl
sudo apt remove pkg
sudo apt autoremove
apt search pkg
apt list --installed | grep pkg
sudo dpkg -i file.deb
sudo snap install code --classic
```

## Processes + services

```bash
ps aux | grep name
top                                   # or htop
kill PID; kill -9 PID
pkill name
command &                             # run in background
jobs; fg %1
sudo systemctl status nginx
sudo systemctl start|stop|restart|enable nginx
journalctl -u nginx -f                # service logs
```

## Disk + system

```bash
df -h                 # disk free
du -sh *              # folder sizes
free -h               # memory
uname -a              # kernel
lsb_release -a        # Ubuntu version
nproc                 # CPU cores
```

## Network

```bash
ip a                              # IPs
ping -c 4 google.com
curl -I https://example.com
ss -tulpn                         # listening ports
sudo lsof -i :8000                # who uses port
ssh user@host
scp file user@host:/path
```

## Archives

```bash
tar -czvf out.tar.gz dir/          # create
tar -xzvf out.tar.gz               # extract
zip -r out.zip dir/; unzip out.zip
```

## Users + env

```bash
whoami; id
sudo adduser name
sudo usermod -aG docker $USER      # add to group, re-login
echo $PATH
export VAR=value                   # session only
nano ~/.bashrc; source ~/.bashrc   # persist
```

## Terminal shortcuts

| Key | Action |
|---|---|
| `Ctrl+Alt+T` | Open terminal |
| `Ctrl+C` | Stop command |
| `Ctrl+R` | Search history |
| `Ctrl+L` | Clear |
| `Ctrl+A / E` | Line start / end |
| `Ctrl+U` | Delete to line start |
| `Tab` | Autocomplete |
| `!!` | Repeat last command |
