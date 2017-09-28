# prometheus_mqtt_exporter

Master: [![Build Status](https://travis-ci.org/sansible/prometheus_mqtt_exporter.svg?branch=master)](https://travis-ci.org/sansible/prometheus_mqtt_exporter)
Develop: [![Build Status](https://travis-ci.org/sansible/prometheus_mqtt_exporter.svg?branch=develop)](https://travis-ci.org/sansible/prometheus_mqtt_exporter)

* [ansible.cfg](#ansible-cfg)
* [Installation and Dependencies](#installation-and-dependencies)
* [Tags](#tags)
* [Examples](#examples)

This roles installs Prometheus MQTT Exporter.

Prometheus MQTT Exporter makes availble MQTT metrics for collection by Prometheus server.

For more information about Prometheus MQTT Exporter please visit
[https://github.com/inovex/mqtt_blackbox_exporter](https://github.com/inovex/mqtt_blackbox_exporter).

For more information about Prometheus Server please visit
[https://prometheus.io](https://prometheus.io).


## ansible.cfg

This role is designed to work with merge "hash_behaviour". Make sure your
ansible.cfg contains these settings

```INI
[defaults]
hash_behaviour = merge
```




## Installation and Dependencies

This role will install `sansible.users_and_groups` for managing `prometheus_mqtt_exporter` user.

To install run `ansible-galaxy install sansible.prometheus_mqtt_exporter` or add this to your
`roles.yml`.

```YAML
- name: sansible.prometheus_mqtt_exporter
  version: v1.0
```

and run `ansible-galaxy install -p ./roles -r roles.yml`




## Tags

This role uses tags: **build** and **configure**

* `build` - Installs Prometheus MQTT Exporter and all it's dependencies.
* `configure` - Configures Prometheus MQTT Exporter.



## Examples

Simply include role in your playbook

Default broker: tcp://localhost:1883
Default exporter: 0.0.0.0:9214

```YAML
- name: Install and configure prometheus_mqtt_exporter
  hosts: "somehost"

  roles:
    - role: sansible.prometheus_mqtt_exporter
```

```YAML
- name: Install and configure prometheus_mqtt_exporter
  hosts: "somehost"

  roles:
    - role: sansible.prometheus_mqtt_exporter
      prometheus_mqtt_exporter:
        start_on_boot: yes
```

```YAML
- name: Install and configure prometheus_mqtt_exporter
  hosts: "somehost"

  roles:
    - role: sansible.prometheus_mqtt_exporter
      prometheus_mqtt_exporter:
        config:
          - name: my broker
            broker_url: tcp://mybroker:1883
            topic: internal/monitoring/nonssl/myexporter
            client_prefix: internal.monitoring.nonssl.myexporter
            messages: 20
            interval: 60s
        start_on_boot: yes
```

