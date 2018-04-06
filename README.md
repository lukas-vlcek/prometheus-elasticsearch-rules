# Prometheus alert rules for Elasticsearch

Assuming ES metrics are collected via <https://github.com/vvanholl/elasticsearch-prometheus-exporter/> plugin.

Verify rules file:

```
promtool check rules ./elasticsearch_logging.yaml
```