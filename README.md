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

## Uplaod RPD

```Bash
./data-model-cmd.sh uploadrpd -I /home/oracle/uat_bi.rpd -W Admin123 -U weblogic -P pass -SI uat_instance
```
