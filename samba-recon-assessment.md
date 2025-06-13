# 🛠 Samba Recon: Basics  
**Assessment Methodologies:** Enumeration  
**Lab Ortamı:** demo.ine.local  
**IP:** 192.174.120.3  

---

## 1️⃣ Smbd tarafından kullanılan varsayılan TCP portlarını bulun.

**Komut:**
nmap -Pn -sV -sC demo.ine.local

Çıktı:
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-06-13 17:28 IST
Nmap scan report for demo.ine.local (192.174.120.3)
Host is up (0.000023s latency).
Not shown: 998 closed tcp ports (reset)
PORT    STATE SERVICE     VERSION
139/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: RECONLABS)
445/tcp open  netbios-ssn Samba smbd 4.3.11-Ubuntu (workgroup: RECONLABS)

Sonuç:

smbd tarafından kullanılan varsayılan TCP portları: 139 ve 445

2️⃣ nmbd tarafından kullanılan varsayılan UDP portlarını bulun

Komut:
nmap -sU --top-ports 25 demo.ine.local

Çıktıdan ilgili kısımlar:

137/udp   open          netbios-ns
138/udp   open|filtered netbios-dgm

Sonuç:

nmbd tarafından kullanılan varsayılan UDP portları: 137 (netbios-ns) ve 138 (netbios-dgm)

3️⃣ Samba sunucusunun çalışma grubu adı nedir?
Komut:
nmap -Pn -sV -sC demo.ine.local
Çıktıdan ilgili satır:(workgroup: RECONLABS)

4️⃣ Uygun nmap betiğini kullanarak samba sunucusunun tam sürümünü bulun.
Komut:
nmap --script smb-os-discovery.nse -p 445 demo.ine.local
Çıktı:| smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.3.11-Ubuntu)

Sonuç:

Samba sunucusunun tam sürümü: Samba 4.3.11-Ubuntu

5️⃣ Samba sunucusunun tam sürümünü smb_version metasploit modülünü kullanarak bulma
Komutlar:
use scanner/smb/smb_version
set RHOSTS demo.ine.local
run
Çıktı:
[*] 192.174.120.3:445 - Host could not be identified: Windows 6.1 (Samba 4.3.11-Ubuntu)
Sonuç:

Metasploit modülü ile tespit edilen sürüm: Samba 4.3.11-Ubuntu

6️⃣ Samba sunucusunun NetBIOS bilgisayar adı nedir? (nmap script ile)
Komut:
nmap --script smb-os-discovery.nse -p 445 demo.ine.local

Çıktı:
NetBIOS computer name: SAMBA-RECON\x00
Sonuç:
NetBIOS bilgisayar adı: SAMBA-RECO

7️⃣ Samba sunucusunun NetBIOS bilgisayar adını nmblookup ile bulma
Komut:
nmblookup -A demo.ine.local
Çıktı:
php-template
Kopyala
Düzenle
SAMBA-RECON     <00> -         H <ACTIVE>
SAMBA-RECON     <03> -         H <ACTIVE>
SAMBA-RECON     <20> -         H <ACTIVE>
Sonuç:

nmblookup ile tespit edilen NetBIOS bilgisayar adı: SAMBA-RECON

✅ 8️⃣ smbclient kullanılarak anonim bağlantıya (null oturum) izin verilip verilmediğini belirleme
Komut:
smbclient -L demo.ine.local -N
Çıktıdan özet:
mathematica
Kopyala
Düzenle
Sharename       Type      Comment
public          Disk      
john            Disk      
emma            Disk      
everyone        Disk      
...
Sonuç:
Paylaşımlar şifre istemeden listeleniyor.

Anonim (null session) bağlantıya izin verilmektedir.

✅ 9️⃣ rpcclient kullanarak anonim bağlantıya izin verilip verilmediğini belirleme
Komut:
rpcclient -U "" -N demo.ine.local
Çıktı:
rpcclient $>
Sonuç:
Herhangi bir hata olmadan bağlantı sağlandığı için anonim bağlantıya izin verilmektedir.

