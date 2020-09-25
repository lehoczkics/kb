# Personal long-term command cache

## Linux
TCP port check:
`nc -zv HOST PORT`

Get only matching strings ( example: *.mydoma.in ) with grep -o:
`grep -o '[^/]*\.mydoma\.in' myfile`

Get public IPv4 address:
`dig -4 +short myip.opendns.com @resolver1.opendns.com`

Publish current directory via HTTP on port 8000:
`python3 -m http.server 8000 &`

unix timestamp to normal date:
`date -d @<unixtime>`

List of available SSL ciphers of example.com:
`nmap --script ssl-enum-ciphers -p 443 www.example.com`<br>
`sslscan example.com`

generate load; 1 CPU core to 100%:
`yes > /dev/null &`

tcpdump capture traffic on specified port:
`tcpdump -peni any -w /tmp/capture.pcap -s 0 host HOSTNAME port PORT`

udpdump: add `-A udp` to above

## Windows CMD
Force clean shutddown:
`shutdown /s /f /t 0`

Force checkdisk on next reboot:
`chkdsk C: /f /r /x`

System info:
`systeminfo /FO csv > machine.csv`
`gpresult.exe /F /H machine.html`

## Windows PowerShell
Enable ps1 file execution:
`Set-ExecutionPolicy Bypass -Scope Process -Force`

Telnet client:
```
$tcp = New-Object System.Net.Sockets.TcpClient
$tcp.connect('<remote server>', <port>)
```

## OpenSSL
Cert debug:<br>
```
openssl s_server -accept PORT -cert ca.cert -key ca.key
openssl s_client -CAfile ca.cert -connect HOST:PORT
openssl s_client -host HOST -port PORT
openssl s_client -connect localhost:PORT
```

Read pem(base64 format) cert:<br>
`openssl x509 -noout -text -in mycert.pem`

Read CSR:<br>
`openssl req -noout -text -in mycsr.csr`

Generate new CSR and key:<br>
`openssl req -nodes -new -newkey  rsa:2048 -out mycsr.csr -keyout mykey.key`

Generate new CSR from existing key:<br>
`openssl req -nodes -new -key my_existing.key -out mynewcsr.csr`

Generate new CSR from existing certificate and Key:<br>
`openssl x509 -x509toreq -in my_existing.crt -signkey my_existing.key -out mynew.csr`

Verify a cert matches a private key:
```
openssl x509 -noout -modulus -in mycert.crt
openssl rsa -noout -modulus -in mykey.key
```
Fingerprint a cert:<br>
`openssl x509 -fingerprint -noout -in mycert.crt [-sha1 -md5]`

## Misc
regex to match xml tags and content:
`<mytag>[\s\S]*?<\/mytag>`
