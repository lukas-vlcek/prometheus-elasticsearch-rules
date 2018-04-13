# Prometheus alert rules for Elasticsearch

[![Build Status](https://travis-ci.org/lukas-vlcek/prometheus-elasticsearch-rules.svg?branch=master)](https://travis-ci.org/lukas-vlcek/prometheus-elasticsearch-rules)

Assuming <https://github.com/vvanholl/elasticsearch-prometheus-exporter/> plugin is installed on every ES node to enable
scraping metrics by Prometheus server. 

## Verify rules file

Use `promtool` utility (it is part of Prometheus installation).
```
promtool check rules ./logging_elasticsearch.rules.yaml
```

This ^^ check is part of [Travis integration](.travis.yml).

## Deploy rules into Prometheus server

The following is a _quick & dirty_ description how to deploy rules file into Prometheus server. For more information
consult [Prometheus documentation](https://prometheus.io/docs/prometheus/latest/configuration/recording_rules/).

```bash
# Assuming the default Prometheus installation
$ pwd
/etc/prometheus

wget https://raw.githubusercontent.com/lukas-vlcek/prometheus-elasticsearch-rules/master/logging_elasticsearch.rules.yaml

$ ls 
logging_elasticsearch.rules.yaml
prometheus.yml

# Add rules file into Prometheus configuration file
$ vi prometheus.yml

## Add the following to the file:
rule_files:
  - logging_elasticsearch.rules.yaml

# Restart Prometheus server to make it reload configuration.
kill -HUP `pgrep prometheus`
```

Navigate to the Prometheus WEB UI and go to "Alerts" tab.
