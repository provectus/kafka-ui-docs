# Audit log

Kafka-UI allows you to log all operations to your kafka clusters done within kafka-ui itself.

Logging can be done to either kafka topic and/or console.

See all the available configuration properties:

```
kafka:
  clusters:
    - name: local
      audit:
        topic-audit-enabled: true
        console-audit-enabled: true
        topic: '__kui-audit-log' # default name
        audit-topic-properties: # any kafka topic properties in format of a map
          - retention.ms: 43200000
        audit-topics-partitions: 1 # how many partitions, default is 1
        level: all # either ALL or ALTER_ONLY (default). ALL will log all read operations.
```
