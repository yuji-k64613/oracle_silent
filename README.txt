groupadd -g 1101 oper
groupadd -g 1102 backupdba
groupadd -g 1103 dgdba
groupadd -g 1104 kmdba

groupadd -g 2001 oinstall
groupadd -g 2002 dba

useradd oracle -g oinstall
usermod -u 54321 -g oinstall -G dba,oper,backupdba,dgdba,kmdba oracle

passwd oracle

mkdir -p /u01/app/oracle
chown -R oracle:oinstall /u01/app/oracle
chmod -R 775 /u01

df -k | grep shm

mkdir /opt/image
cd /opt/image
unzip /vagrant/linuxamd64_12102_database_1of2.zip
unzip /vagrant/linuxamd64_12102_database_2of2.zip

mkdir /u01/app/oraInventory
chown oracle:oinstall /u01/app/oraInventory

yum update -y
yum install -y gcc-c++
yum install -y ksh
yum install -y libaio-devel
yum install -y compat-libstdc++-33.x86_64
yum install -y compat-libcap1.x86_64

/opt/image/database/runInstaller -jreLoc /usr/lib/jvm/jre-1.8.0-openjdk -ignoreSysPrereqs -waitforcompletion -silent -responseFile /home/oracle/db.rsp
/u01/app/oracle/product/12.1.0/dbhome_1/bin/dbca -silent -responseFile /home/oracle/dbca.rsp
/u01/app/oracle/product/12.1.0/dbhome_1/bin/netca -silent -responseFile /home/oracle/netca.rsp
