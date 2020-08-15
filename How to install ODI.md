# How to install ODI

Download files from oracle website

You'll obtain 2 fzipped files

Create a folder called odi and move the files to this folder
```bash
$ mkdir odi
$ mv fmw_12.2.1.3.0_odi_Disk1_1of2.zip odi/
$ mv fmw_12.2.1.3.0_odi_Disk1_2of2.zip odi/
```
Go to the odi folder and unzip the files
```bash
[oracle@dbserver ~]$ cd Downloads/
[oracle@dbserver Downloads]$ mkdir odi
[oracle@dbserver Downloads]$ mv fmw_12.2.1.3.0_odi_Disk1_1of2.zip  odi/
[oracle@dbserver Downloads]$ mv fmw_12.2.1.3.0_odi_Disk1_2of2.zip  odi/
[oracle@dbserver Downloads]$ cd odi
[oracle@dbserver odi]$ ls
fmw_12.2.1.3.0_odi_Disk1_1of2.zip  fmw_12.2.1.3.0_odi_Disk1_2of2.zip
[oracle@dbserver odi]$ unzip fmw_12.2.1.3.0_odi_Disk1_1of2.zip 
Archive:  fmw_12.2.1.3.0_odi_Disk1_1of2.zip
  inflating: fmw_12.2.1.3.0_odi.jar  

  inflating: fmw_12213_readme.htm    
[oracle@dbserver odi]$ unzip fmw_12.2.1.3.0_odi_Disk1_2of2.zip 
Archive:  fmw_12.2.1.3.0_odi_Disk1_2of2.zip
  inflating: fmw_12.2.1.3.0_odi2.jar  
[oracle@dbserver odi]$ ls
fmw_12.2.1.3.0_odi2.jar            fmw_12.2.1.3.0_odi.jar
fmw_12.2.1.3.0_odi_Disk1_1of2.zip  fmw_12213_readme.htm
fmw_12.2.1.3.0_odi_Disk1_2of2.zip
[oracle@dbserver odi]$ java -jar fmw_12.2.1.3.0_odi
fmw_12.2.1.3.0_odi2.jar            fmw_12.2.1.3.0_odi_Disk1_2of2.zip
fmw_12.2.1.3.0_odi_Disk1_1of2.zip  fmw_12.2.1.3.0_odi.jar

```
Now you have 2 files with a .jar extension. You can install ODI using the following command
```bash
[oracle@dbserver odi]$ java -jar fmw_12.2.1.3.0_odi.jar
Launcher log file is /tmp/OraInstall2020-01-26_03-06-56PM/launcher2020-01-26_03-06-56PM.log.
Extracting the installer . . . . . . . Done
Checking if CPU speed is above 300 MHz.   Actual 2591.998 MHz    Passed
Checking monitor: must be configured to display at least 256 colors.   Actual 16777216    Passed
Checking swap space: must be greater than 512 MB.   Actual 8063 MB    Passed
Checking if this platform requires a 64-bit JVM.   Actual 64    Passed (64-bit not required)
Checking temp space: must be greater than 300 MB.   Actual 31423 MB    Passed
Preparing to launch the Oracle Universal Installer from /tmp/OraInstall2020-01-26_03-06-56PM
Log: /tmp/OraInstall2020-01-26_03-06-56PM/install2020-01-26_03-06-56PM.log
Logs successfully copied to /u01/app/oraInventory/logs.
```

```bash
[oracle@dbserver ~]$ cd /u01/
[oracle@dbserver u01]$ ls
app
[oracle@dbserver u01]$ cd app
[oracle@dbserver app]$ ls
oracle  oraInventory
[oracle@dbserver app]$ pwd
/u01/app
[oracle@dbserver app]$ mkdir MiddleWare
```


![Image](https://www.dropbox.com/s/nxebpdbmssenzdl/SyhJsMs-8_ByMrQugMU.png?dl=1)


![Image](https://www.dropbox.com/s/5xlp9s27m3a3wai/SyhJsMs-8_H11vX_xGL.png?dl=1)


```bash
[oracle@dbserver ~]$  cd /u01/app/Middleware/Oracle_Home/odi/studio
[oracle@dbserver studio]$ ls
bin  configuration  extensions  odi64.exe  odi.exe  odi.sh
[oracle@dbserver studio]$ ./odi.sh 
```

```bash
[oracle@dbserver ~]$ lsnrctl start

LSNRCTL for Linux: Version 12.2.0.1.0 - Production on 26-JAN-2020 16:35:00

Copyright (c) 1991, 2016, Oracle.  All rights reserved.

Starting /u01/app/oracle/product/12.2.0/dbhome_1/bin/tnslsnr: please wait...

TNSLSNR for Linux: Version 12.2.0.1.0 - Production
System parameter file is /u01/app/oracle/product/12.2.0/dbhome_1/network/admin/listener.ora
Log messages written to /u01/app/oracle/diag/tnslsnr/dbserver/listener/alert/log.xml
Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=dbserver)(PORT=1521)))
Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=ipc)(KEY=EXTPROC1521)))

Connecting to (DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=dbserver)(PORT=1521)))
STATUS of the LISTENER
------------------------
Alias                     LISTENER
Version                   TNSLSNR for Linux: Version 12.2.0.1.0 - Production
Start Date                26-JAN-2020 16:35:02
Uptime                    0 days 0 hr. 0 min. 0 sec
Trace Level               off
Security                  ON: Local OS Authentication
SNMP                      OFF
Listener Parameter File   /u01/app/oracle/product/12.2.0/dbhome_1/network/admin/listener.ora
Listener Log File         /u01/app/oracle/diag/tnslsnr/dbserver/listener/alert/log.xml
Listening Endpoints Summary...
  (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=dbserver)(PORT=1521)))
  (DESCRIPTION=(ADDRESS=(PROTOCOL=ipc)(KEY=EXTPROC1521)))
The listener supports no services
The command completed successfully

```


```bash
[oracle@dbserver ~]$ sqlplus / as sysdba

SQL*Plus: Release 12.2.0.1.0 Production on Sun Jan 26 16:37:30 2020

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to an idle instance.

SQL> startup
ORACLE instance started.

Total System Global Area 2466250752 bytes
Fixed Size		    8623688 bytes
Variable Size		  671091128 bytes
Database Buffers	 1778384896 bytes
Redo Buffers		    8151040 bytes
Database mounted.
Database opened.
SQL> 

```

```bash
SQL> create user ODI_MASTER_REPO identified by odimaster default tablespace USERS;

User created.

SQL> grant connect, resource to ODI_MASTER_REPO;

Grant succeeded.

```
