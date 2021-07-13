# fail2ban-action-influxdbpass
This is a simple action to write the offending IP and some information about a violation to an InfluxDB. I created that for statistics in Grafana and to create blocklists out of that InfluxDB database.

## Installation
Copy influxdb.conf to /etc/fail2ban/action.d

## Usage
Just call the action with the jail name as parameter.

Example:
```
[sasl]
enabled  = true
port     = smtp,ssmtp,submission,imap2,imap3,imaps,pop3,pop3s
filter   = postfix-sasl
logpath  = /var/log/maillog
action   = iptables-allports[name=sasl]
           sendmail-whois-lines[name=sasl, logpath=/var/log/maillog]
           influxdb[name=sasl]
bantime  = 604800  ; 1 week
findtime = 86400   ; 1 day
maxretry = 3
```
