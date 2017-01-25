sa-rsyslog-server
=================

Implementation of the centralized syslog server. Note, make sure, 514 port is opened for your slave nodes.

[![Build Status](https://travis-ci.org/softasap/sa-rsyslog-server.svg?branch=master)](https://travis-ci.org/softasap/sa-rsyslog-server)


Example of use: check box-example

Simple:

```YAML


     - {
         role: "sa-rsyslog-server"
       }

```


Advanced:

```YAML

rsyslog_conf_custom_props:
   - {regexp: '^[#]?module(load="imudp")', line: 'module(load="imudp")'}
   - {regexp: '^[#]?input(type="imudp" port="514")', line: 'input(type="imudp" port="514")'}
   - {regexp: '^[#]?module(load="imtcp")', line: 'module(load="imtcp")'}
   - {regexp: '^[#]?input(type="imtcp" port="514")', line: 'input(type="imtcp" port="514")'}
   - {regexp: '^[#]?$IncludeConfig /etc/rsyslog.d/*.conf', line: '$IncludeConfig /etc/rsyslog.d/*.conf'}

rsyslog_confd_custom_parts:
   - {src: '{{root_dir}}/templates/syslog/write_2_postgres.conf.j2', dest: '99-write_2_postgres.conf' }

```

```YAML


     - {
         role: "sa-rsyslog-server",
         rsyslog_conf_props: "{{rsyslog_conf_custom_props}}",
         rsyslog_confd_parts: "{{rsyslog_confd_custom_parts}}"
       }

```


Copyright and license
---------------------


Code licensed under the [BSD 3 clause] (https://opensource.org/licenses/BSD-3-Clause) or the [MIT License] (http://opensource.org/licenses/MIT).

Subscribe for roles updates at [FB] (https://www.facebook.com/SoftAsap/)
