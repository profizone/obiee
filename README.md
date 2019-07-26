# OBIEE Notes

## Script: setRestartMax.py
Set OBIEE server Restart Max attribute. To call the script run: ./wlst.sh setRestartMax.py

Oracle_Home/oracle_common/common/wlst.sh

```python
connect(username='weblogic',password='pass',url='t3://localhost:9900')

print 'Script start'
domainConfig()
edit()
startEdit()

servers=cmo.getServers()
for server in servers:
  print server
  cd('/Servers/' + server.getName())
  cmo.setRestartMax(999)
  print cmo.getRestartMax()

save()
activate(block="true")
print 'Script Completed'
disconnect()
exit()
```
## Useful WLST Commands

```python
# list all
ls()
# list attributes
ls('a')
# cd to parent folder in structure
cd('\\')
# go to folder: Servers
cd('/Servers')
# print to the screen
print 'Script completed'
print servers
```

## Uplaod RPD & Clean-Up Old Repository Content

Upload repository with data-model uploadrpd located under:

```Python
cd /u01/oracle/OBIEE/user_projects/domains/uat_bi/bitools/bin
./data-model-cmd.sh uploadrpd -I /home/oracle/uat_bi.rpd -W Admin123 -U weblogic -P pass -SI uat_instance
```

Navigate to the directory /Middlewarehomebi12/user_projects/domains/bi12/bitools/bin to stop all servers

```Python
./stop.sh 
```
Delete liverpd.* and all other versions of RPDs in the directory 

```Python
/OBIEE/user_projects/domains/bi12/bidata/service_instance/ssi/metadata/datamodel/customizations          
```

Clear the content of file default_diff.xml in the directory:
```Python
/OBIEE/user_projects/domains/bi12/bidata/service_instances/ssi/metadata/datamodel/customizations/default
```

Note: Do not delete this file

Issue the command sh start.sh to start all services from bitools/bin directory

The system should come up with default RPD

Login in to Weblogic as weblogic user to ensure all services are up and running

Now upload new RPD using

```Python
./data-model-cmd.sh uploadrpd
```
