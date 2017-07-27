Filebeat
========

Ansible role to install and configure Filebeat 5.x

> WARNING:
>    Support Filebeat v1.x removed. 
>    Use an earlier version (git commit: 8cddaa0eab307ac168d690cfe9a9d26f93098530) 
>    of this role for v1.x support

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
    filebeat_global_opts:
      registry_file: "{{ filebeat_data_dir }}/registry"
    filebeat_outputs:
      logstash:
        hosts: [ "localhost:5044" ]
      file:
        path: "/tmp/filebeat"
    filebeat_general:
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


## Testing

To test this role, run:

```
kitchen test
```


## Dependencies:

None
