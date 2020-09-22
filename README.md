# Personal long-term command cache

## Linux
TCP port check:
`nc -zv HOST PORT`

Get only matching strings ( example: *.mydoma.in ) with grep -o:
`grep -o '[^/]*\.mydoma\.in' myfile`

Get public IPv4 address:
`dig -4 +short myip.opendns.com @resolver1.opendns.com`

## Windows CMD
Force clean shutddown:
`shutdown /s /f /t 0`

Force checkdisk on next reboot:
`chkdsk C: /f /r /x`

## Windows PowerShell
Enable ps1 file execution:
`Set-ExecutionPolicy Bypass -Scope Process -Force`

