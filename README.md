# ansible-role-monit

A versatile role to setup monit, created using this philosophy:
https://github.com/jriguera/ansible-role-pattern/blob/master/README.md

Ansible 2.0, Works with Ubuntu Trusty, Xenial and Centos 7


## Configuration

Default configuration parameters are:

```
monit_enabled_on_startup: True

# Install from upstream repos or directly from operating system packages
monit_os_packages: True

# Global options  
# The number of seconds to determine if a process is down or not.
monit_interval: 120

# The number of seconds before starting to monitor a process which just launched.
# Set this to 0 to disable it.
monit_start_delay: 30

# Define a motd message
monit_update_motd: True

# Enable cpu/memory and fs monitoring
monit_monitoring_system: True

# Log file. If it is not defined, it will use syslog
monit_logfile: "/var/log/monit.log" 
monit_syslog_facility: "log_daemon"

# List of mail servers, the first item in the list will be tried first.
monit_mail_server_list:
  - host: "localhost"  
    port: 25
    #username: "user"
    #password: "pass"
    # Available encryption types are:
    # SSLAUTO, SSLV2, SSLV3, TLSV1, TLSV11, TLSV12
    #encryption: SSLAUTO

# Who sent it and how should the message be formatted?
monit_mail_from: "monit@{{ ansible_fqdn }}"
monit_mail_reply_to: "monit@{{ ansible_fqdn }}"
monit_mail_subject: "[Monit] $EVENT $SERVICE"
monit_mail_message: |
  $EVENT Service $SERVICE
  Date:        $DATE  
  Action:      $ACTION
  Host:        $HOST
  Description: $DESCRIPTION

  Your faithful employee,
  Monit

# Where should the alerts get sent to?
# Use a comma separated list to provide more than 1 event.
# When undefined or blank it will send an alert on all events.
# You can disable alerting completely by providing an empty list.
#monit_mail_alert_list:
#  - monitoring1@email.com:
#  - monitoring2@email.com: [ "timeout", "nonexist" ]

# Limit the maximal queue size using the SLOTS option (if omitted, the queue is
# limited by space available in the back end filesystem).
monit_event_slots: 200 

# M/Monit and HTTP
#monit_mmonit_url: http://user:password@mmonithost:8080/collector

# Run the http server and allow localhost to view it, this is required to
# make monit's CLI function.
monit_http_port: 2812
monit_http_signature: False
monit_http_bind: "0.0.0.0"
monit_http_allow_net_list: []
monit_http_allow_user_list: [ "admin:admin" ]
monit_http_allow_user_ro_list: [ "guest:guest" ]

# To enable SSL you have to define the cert file
#monit_https_cert: "/path/to/file.pem"
#monit_https_client: "/path/to/client.pem"
#monit_https_selfcertification: True

# Monitoring
# start and stop dictionaries are optional if script is defined,
# they are only needed to define additional parameters
#monit_monitoring_list:
#  - name: "name"
#    type: "process"
#    delete: True
#    script: "/etc/init.d/name %"
#    target: "/var/run/process/process.pid"
#    start: { script: "/etc/init.d/name start", uid: "user", gid: "group", timeout: 10 }
#    #stop: { script: "/etc/init.d/name stop" }
#    restart: { script: "/etc/init.d/name restart" }
#    rules:
#      - "if totalcpu > 80% for 3 cycles then alert"
#      - "if totalmem > 400.0 MB for 5 cycles then alert"
#      - "if children > 250 then alert"
#      - "if loadavg(5min) > 20 for 8 cycles then alert"
monit_monitoring_list:
```


## Author

José Riguera López <jriguera@gmail.com>
