# fail2ban-action-influxdb
This is a simple action for [fail2ban](https://github.com/fail2ban/fail2ban) to write the offending IP and some additional information to an InfluxDB. I created that for statistics in Grafana and to create blocklists out of that InfluxDB database.

## Requirements
* curl

## Installation
Copy influxdb.conf to /etc/fail2ban/action.d

## Configuration
In /etc/action.d/influxdb.conf, in the [init] section, set the following variables to the approriate values:
* influxurl  = <url of your influxdb server>
* influxdb   = <database name - database must exist>
* influxuser = <username of a user with write access to the database>
* influxpass = <password for the user>
* influxhost = <hostname of this host, i.e. the host, fail2ban is running on>


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

## License
This fail2ban-action is free software; you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation; either version 2 of the License, or (at your option) any later version.

This fail2ban-action is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with Fail2Ban; if not, write to the Free Software Foundation, Inc., 51 Franklin Street, Fifth Floor, Boston, MA 02110, USA
