Filebeat
========

Ansible role to install and configure Filebeat.


## Examples

```
- hosts: myhost

  vars:
    filebeat_prospectors:
      - paths: [ "/var/log/*.log" ]
      - paths: [ "/var/log/myapp/myapp.log" ]
        multiline:
          pattern: ^\[
          negate: false
          match: after
          max_lines: 500
        exclude_lines: ["^DBG"]
        include_lines: ["^ERR", "^WARN"]
        exclude_files: [".gz$"]
    filebeat_general_opts:
      registry_file: "{{ filebeat_data_dir }}/registry"
    filebeat_outputs:
      logstash:
        hosts: [ "localhost:5044" ]
      file:
        path: "/tmp/filebeat"
    filebeat_shipper:
      tags: [ "service-X", "webtier" ]
    filebeat_logging:
      to_syslog: true

  roles:
    - wunzeco.filebeat
```


> *Resources that may help with multiline config:*
>    - For multiline config examples:
>        https://www.elastic.co/guide/en/beats/filebeat/master/multiline-examples.html
>    - To test regexp patterns:
>        https://play.golang.org/p/uAd5XHxscu


## Dependencies:

None
