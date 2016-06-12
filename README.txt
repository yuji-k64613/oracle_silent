/opt/image/database/runInstaller -jreLoc /usr/lib/jvm/jre-1.8.0-openjdk -ignoreSysPrereqs -waitforcompletion -silent -responseFile /home/oracle/db.rsp
/u01/app/oracle/product/12.1.0/dbhome_1/bin/dbca -silent -responseFile /home/oracle/dbca.rsp
/u01/app/oracle/product/12.1.0/dbhome_1/bin/netca -silent -responseFile /home/oracle/netca.rsp
