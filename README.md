# Personal long-term command cache

## Linux
- TCP port check:
```sh
nc -zv HOST PORT
```

- Get only matching strings ( example: `*.mydoma.in` ) with `grep -o`:
```sh
grep -o '[^/]*\.mydoma\.in' myfile
```

- Get public IPv4 address:
```sh
dig -4 +short myip.opendns.com @resolver1.opendns.com
```

- Publish current directory via HTTP on port 8000:
```sh
python3 -m http.server 8000 &
```

- unix timestamp to normal date:
```sh
date -d @<unixtime>
```

- List of available SSL ciphers of example.com:
```sh
nmap --script ssl-enum-ciphers -p 443 www.example.com
# if available sslscan does the job as well:
sslscan example.com
```

- generate load; 1 CPU core to 100%:
```sh
yes > /dev/null &
```

- tcpdump capture traffic on specified port:

```sh
tcpdump -peni any -w /tmp/capture.pcap -s 0 host HOSTNAME port PORT
```
udpdump: add `-A udp` to above

- Remove duplicate lines from **file** in one step (without sorting it first):
```awk
awk ‘!seen[$0]++’ file
```

- Edit command line in $EDITOR:<br>
**Ctrl-X Ctrl-E**

- Import a repo's gpg key into a separate keyring:
```sh
sudo apt-key --keyring /etc/apt/trusted.gpg.d/mykeyring.gpg add /path/to/mykey.key
```

- ssh connection throug a jumphost. Will end up as root at host given as parameter
```sh
function jump () { ssh -o ServerAliveInterval=60 -J <jumphost name> $1 -t 'sudo -i; bash -l' }
```

### git

- Cherry-picking a range of commits without actually committing them so that you can edit further and even squash them:
```sh
git cherry-pick -n abcd1234^..bcde2345
```

- Fancy trail-like commit track graph: [aliased to *gloga* by git plugin by the way](https://github.com/ohmyzsh/ohmyzsh/blob/master/plugins/git/git.plugin.zsh#L225)
```sh
git log --oneline --decorate --grap --all
```

- Compare a file content between branches:
```sh
git diff mybranch master -- where/is/the/file
```

- git config snippet for gpg signing commits:
```
[user]
	email = csaba[AT]lehoczki[.]me
	name = "Csaba Lehoczki"
	signingkey = AB4E2EC3812ACEE8
[commit]
	gpgsign = true
```

### ZFS

- Remove all snapshots from a ZFS dataset:
```sh
zfs destroy -rvn dataset_or_zvol_name@%
```
remove `-n` if you really want to kill them

- Delete zfs snapshots matching a pattern:
```sh
zfs list -t snapshot -H -o name -r [parent dataset] | grep [pattern] | xargs -n1 echo
```
If you got what you want; substitute `echo` with `zfs destroy`

- zfs send/receive via SSH (one command only; slover but safer)
```sh
zfs send -R zpool/dataset/name@snapshot-to-send | ssh TARGET sudo zfs receive -Fu zpool/dataset/name
```

- zfs send/receive via netcat - plain bitstream instead of ssh tunnel (faster and less CPU intensive)

First start listener on target machine and pipe it to `zfs receive`:
```sh
nc -lp PORT | zfs receive zpool/dataset/name
```
Send snapshot stream recursively from the source machine:
```sh
zfs send -R zpool/dataset/name@snapshot-to-send | nc -w 20 TARGETHOST PORT
```


## Windows CMD
- Force clean shutdown:
```cmd
shutdown /s /f /t 0
```

- Force checkdisk on next reboot:
```cmd
chkdsk C: /f /r /x
```

- System info:
```cmd
systeminfo /FO csv > machine.csv
gpresult.exe /F /H machine.html
```

## Windows PowerShell
- Enable ps1 file execution:
```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force
```

- Telnet client:
```powershell
$tcp = New-Object System.Net.Sockets.TcpClient
$tcp.connect('<remote server>', <port>)
```

- wget:
```powershell
Invoke-Webrequest -Uri <source> -OutFile <destination>
```

- grep: `Select-String is the full name, abbrev sls:`
```powershell
sls pattern .\filename
```


## OpenSSL
- Cert debug:
```sh
openssl s_server -accept PORT -cert ca.cert -key ca.key
openssl s_client -CAfile ca.cert -connect HOST:PORT
openssl s_client -host HOST -port PORT
openssl s_client -connect localhost:PORT
```

- Read pem(base64 format) cert:
```sh
openssl x509 -noout -text -in mycert.pem
```

- Read CSR:
```sh
openssl req -noout -text -in mycsr.csr
```

- Generate new CSR and key:
```sh
openssl req -nodes -new -newkey  rsa:2048 -out mycsr.csr -keyout mykey.key
```

- Generate new CSR from existing key:
```sh
openssl req -nodes -new -key my_existing.key -out mynewcsr.csr
```

- Generate new CSR from existing certificate and Key:
```sh
openssl x509 -x509toreq -in my_existing.crt -signkey my_existing.key -out mynew.csr
```

- Verify a cert matches a private key:
```sh
openssl x509 -noout -modulus -in mycert.crt
openssl rsa -noout -modulus -in mykey.key
```

- Fingerprint a cert:
```sh
openssl x509 -fingerprint -noout -in mycert.crt [-sha1 -md5]
```

## Misc
- regex to match xml tags and content:<br>
```
<mytag>[\s\S]*?<\/mytag>
```

