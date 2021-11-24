## Audit Log Plugin Installation

### Percona MySQL Server
Percona MySQL Server already comes with the audit log plugin, but it is not enabled by default. To enable it, login to the MySQL instance and do the following:
```
INSTALL PLUGIN audit_log SONAME 'audit_log.so';
```

### MySQL Community Edition
MySQL Community Edition does not come with the audit log plugin by default. To download the audit log plugin, follow the below steps.

*Note: The Percona MySQL Server version in below steps should match your corresponding MySQL Server version to download the audit_log.so file.*

#### Download
For MySQL 5.7+
```
wget https://www.percona.com/downloads/Percona-Server-5.7/LATEST/binary/tarball/Percona-Server-5.7.34-37-Linux.x86_64.glibc2.12.tar.gz
```

For MySQL 8.0+
```
wget https://www.percona.com/downloads/Percona-Server-8.0/LATEST/binary/tarball/Percona-Server-8.0.25-15-Linux.x86_64.glibc2.12.tar.gz
```

Extract the downloaded Percon Server
```
tar xfz Percona-Server-<version number>-Linux.x86_64.glibc2.12.tar.gz
```

Navigate to `lib/mysql/plugin` folder
```
cd Percona-Server-<version number>-Linux.x86_64.glibc2.12/lib/mysql/plugin
```

Find the plugin location of MYSQL community Edition
```
show global variables like 'plugin%';
```

Copy audit_log.so plugin file to <MYSQL_PLUGIN_PATH>
```
cp audit_log.so <MYSQL_PLUGIN_PATH>
```

Login into your MySQL server
```
mysql -u <user_name> -p <password>
```

Enable the audit log plugin
```
INSTALL PLUGIN audit_log SONAME 'audit_log.so';
```

Verify installation
```
show global variables like '%audit%';
```

## Fluentd Installation

Install td-agent 4
```
#Ubuntu Focal
curl -L https://toolbelt.treasuredata.com/sh/install-ubuntu-focal-td-agent4.sh | sh
```

Launch Daemon
```
sudo systemctl start td-agent.service
sudo systemctl status td-agent.service
```

## Configuration
Fluentd's configuration file is present at `/etc/td-agent/td-agent.conf`.

Edit it
```
<source>
    @type tail
    read_from_head true
    path /var/log/mysql/audit.log*
    pos_file /opt/td-agent/audit/fluentd/audit.log.pos
    <parse>
      @type json
    </parse>
    tag audit
</source>
<match audit>
  @type http
  endpoint_url https://api-dev.accuknox.com/agent-data-collector/api/v1/collect-data/dp-mysql-audit-logs
  <buffer>
    flush_interval 10s
  </buffer>
  <format>
   @type json
  </format>
  http_method post
</match>
```

In the above code snippet, `/var/log/mysql/audit.log*` is the path where the MySQL audit log is being read from and then pushed to the http endpoint url. 

User `td-agent` requires `read` permission to read the logs at `/var/log/mysql/audit.log*`. Otherwise, `td-agent` throws log unreadable error.

Add 'td-agent' user to the ‘adm’ group, as the audit log file’s group name is 'adm':
```
usermod -a -G adm td-agent
```

Check whether the 'adm' group been added to the 'td-agent' user, by running following command:
```
id td-agent
```

Then,
```
sudo chown 640 /var/log/mysql/audit.log
```

The pos files generated by fluentd will be stored at `/opt/td-agent/audit/fluentd`.  Make sure `td-agent` has permission: 
```
sudo chown td-agent -R /opt/td-agent/audit/fluentd
```

To reflect the changes made in config file, we need to restart the td-agent service:
```
sudo service td-agent restart
```

To check td-agent's logs
```
sudo tail -f /var/log/td-agent/td-agent.log
```