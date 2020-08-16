# How to create a Data Lake - on premises

Create 3 VMs:
- CentOS
- Minimal installation
- Set bridge mode
- Update OS (**$ yum install update**)

- 1 Namenode with 2GB memory
  - hostname: hdpmaster
- 2 Datanode with 1GB each
  - hostname: hdpslave1, hdpslave2

Get IP address och each machine: (**$ ip addr show**)
- hdpmaster: 192.168.62.184
- hdpslave1: 192.168.62.113
- hdpslave2: 192.168.62.177

Connect to them using ssh. You need to keep the machines active(opened/minimized) while you're using ssh. If you're note sure whether your machine has ssh or not, you can check them using **$ service sshd status**

As accessing them using their names instead of IP addresses is easier, we can setup that for each machine at /etc/hosts

```bash
vi /etc/hosts
```
And add the other machines
```bash
192.168.62.113 hdpslave1
192.168.62.177 hdpslave2
```

If you want to check if its working, you can simply ping them ($ ping hdpxxx)

Java installation

```bash
cd /opt/
```
Install wget
```bash
yum install wget
```
Download Java JDK direclty from cli or from oracle website
```bash
wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u171-b11/512cd62ec5174c3487ac17c61aaa89e8/jdk-8u171-linux-x64.tar.gz"
```
Untar file
```bash
tar xzf jdk-8u171-linux-x64.tar.gz
```
Check version
```bash
java -version
```
Set environment variables
```bash

vi .bash_profile

# Java JDK 1.8
export JAVA_HOME=/opt/jdk
export JRE_HOME=/opt/jdk/jre
export PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
```
Update bash
```bash
source .bash_profile

java -version
```


SETUP HADOOP USER ACCOUNT
Create it in each machine

```bash
useradd -m hadoop
passwd hadoop
```

Setup SSH 
Create it in each machine
```bash
vi /etc/ssh/sshd_config
```

Uncomment the following lines:
```bash
Port 22
ListenAddress 0.0.0.0
ListenAddress ::

PubkeyAuthentication yes
```
Restart the service
```bash
systemctl restart sshd.service
```
```none


```
```bash
su hadoop
cd ~
ssh-keygen
/home/hadoop/.ssh/hdp-key
```

```bash
Generating public/private rsa key pair.
Enter file in which to save the key (/home/hadoop/.ssh/id_rsa): /home/hadoop/.ssh/hdp-key
Created directory '/home/hadoop/.ssh'.
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/hadoop/.ssh/hdp-key.
Your public key has been saved in /home/hadoop/.ssh/hdp-key.pub.
The key fingerprint is:
SHA256:6GbvTITZ1SoQjFOvjUMC1zSoAeRbJpSdxU1VtvJHyws hadoop@hdpmaster
The key's randomart image is:
+---[RSA 2048]----+
|o++ =OB....o     |
|o..=+.o=  ...    |
| o =..o ......   |
|  *  o X .o.o .  |
| .    B S .E +   |
|     . o .  o .  |
|      + .    .   |
|     o +         |
|       .+        |
+----[SHA256]-----+
[hadoop@hdpmaster ~]$ clear

[hadoop@hdpmaster ~]$ ssh-copy-id -i ~/.ssh/hdp-key.pub hadoop@hdpslave1
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/hadoop/.ssh/hdp-key.pub"
The authenticity of host 'hdpslave1 (192.168.62.113)' can't be established.
ECDSA key fingerprint is SHA256:AeI5fPFHQWvGA4Zr2p/eEKfptGpwV9PYW6Owhc+vJZs.
ECDSA key fingerprint is MD5:ee:2e:ff:64:19:19:f2:d7:e1:26:d5:1c:f4:6c:17:f1.
Are you sure you want to continue connecting (yes/no)? yes
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
hadoop@hdpslave1's password: 
Permission denied, please try again.
hadoop@hdpslave1's password: 

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'hadoop@hdpslave1'"
and check to make sure that only the key(s) you wanted were added.

[hadoop@hdpmaster ~]$ ssh-copy-id -i ~/.ssh/hdp-key.pub hadoop@hdpslave2
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/hadoop/.ssh/hdp-key.pub"
The authenticity of host 'hdpslave2 (192.168.62.177)' can't be established.
ECDSA key fingerprint is SHA256:AXoNiEcetoJP5PwbjYEAKM8fyMCmVyEFBiKbFbbIZzA.
ECDSA key fingerprint is MD5:8a:a4:f3:0b:2c:91:bf:89:e8:41:8d:a8:34:6a:fb:6a.
Are you sure you want to continue connecting (yes/no)? yes
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
hadoop@hdpslave2's password: 

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'hadoop@hdpslave2'"
and check to make sure that only the key(s) you wanted were added.

[hadoop@hdpmaster ~]$ 

```

Install hadoop

```bash
cd /opt/
wget hadoop
ls -la
tar -xvf hadoop-3.1.0.tar.gz
mv hadoop-3.1.0 hadoop
rm -rf hadoop-3.1.0.tar.gz
ls -la
chown -R hadoop:hadoop hadoop/
ls -la

su hadoop
cd /opt/hadoop/
cd bin/
ls -la
./hadoop version

cd ~
vi .bash_profile
```

Add 

```bash
# Hadoop
export HADOOP_HOME=/opt/hadoop
export PATH=$PATH:$HADOOP_HOME/bin
```

```bash
source .bash_profile
hadoop version
```

Configure hadoop ---for namenode

```bash
su hadoop
echo $HADOOP_HOME
exit
su - hadoop
echo $HADOOP_HOME
```


```bash
cd $HADOOP_HOME/etc/hadoop
pwd
/opt/hadoop/etc/hadoop
ls -la

```
