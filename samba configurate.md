﻿# samba #



1. **服务细节**

   1. Packages:

   > - samba
   >
   > - samba-common
   >
   > - samba-client
   >
   > - samba-winbind-client

   2. services:

   > - /etc/init.d/smb
   > - /etc/init.d/nmb

   3. daemons:

   > - /usr/sbin/smbd
   > - /usr/sbin/nmbd

   4. ports: 

   > - 137/udp(netbios-ns)
   > - 138/udp(netbios-dgm)
   > - 139/tcp(netbios-ssn)
   > - 446/tcp(microsoft-ds)

   5. configuration:

   > - /etc/samba/smb.conf
   > - /etc/samb/

   6. configuration tools

   > - system-config-samba
   > - samba-swat(http://localhost:901)
2. **配置**

   1. users must have local accounts:
      be translated to a local account through
	`/etc/samba/smbusers`

   2. stored in /var/lib/samba/private/passdb.tdb
   
   3. users added with smbpasswd -a user

   4. users modified with smbpasswd  user
   
   	```
	create user
   	mkdir -m 700 /path
   	chown user /path
   	chcon -t samba_share_t /path
   	vim /etc/samba/smb.conf
   	smbpasswd -a username   	
   	```
   	
   	```
   	smbclient -L //demo
   	put file
   	get file
   	cd directory
   	mount -t cifs //demo/sharepath /mnt/share -o username= ,password= 
   	//demo/sharepath /mnt/share  cifs uersname=,password=
   	```
   	
   	