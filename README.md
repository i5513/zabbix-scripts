
# zabbix_get_events
Perl script which recollects zabbix events, run zabbix_get_events --help to see which parameters take. Configure user / password / zabbix server at head of the script

# zabbix_monit_active_pasive
## Configuration
User, password y server of zabbix are configured on /etc/zabbix/zabbix_api.conf or ~/.zabbix_api.conf or the file passed at --config parameter
The config file have a ini format:
[zabbixapi]
user=user
password=password
server=ip_or_name
## Parameters
Python script which take 3 parameter (item, value and template), optionally a config file.


## Use
Having a host with a template applied, and with an item which tell us if the host is in active mode or pasive mode, this script will enable or disable all the items belong to the template when the item have the value passed by parameter. It will never disable the item which say if the host is master or slave.

## Example
We are using it on production, for monitoring ActiveMQ (I will publish zabbix template (for the moment in spanish)):
python /opt/scripts/zabbix_monit_active_pasive \
	--item-key 'jmx["org.apache.activemq:type=Broker,brokerName={$BROKER}",Slave]' \
	--value false \
	--template Plantilla_ActiveMQ_MasterSlave \
	>> /var/log/zabbix/activemq.log 2>&1 

