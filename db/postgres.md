# Complete Postgres receiver

Run the below commands in the db before using the receiver
```sql
CREATE USER postgres_exporter WITH PASSWORD 'your_password';
GRANT pg_monitor TO postgres_exporter;
```

```yaml
receivers:
  postgresql:
    endpoint: "<rds-endpoint>:5432"
    collection_interval: 10s
    username: "postgres_exporter"
    password: "your_password"
    databases: ["<db-name>"]
    tls:
      insecure_skip_verify: true
    metrics:
      postgresql.database.locks:
        enabled: true
      postgresql.deadlocks:
        enabled: true
      postgresql.sequential_scans:
        enabled: true
      postgresql.bgwriter.buffers.allocated:
        enabled: true
      postgresql.bgwriter.buffers.writes:
        enabled: true
      postgresql.bgwriter.checkpoint.count:
        enabled: true
      postgresql.bgwriter.duration:
        enabled: true
      postgresql.bgwriter.maxwritten:
        enabled: true
      postgresql.blocks_read:
        enabled: true
      postgresql.commits:
        enabled: true
      postgresql.database.count:
        enabled: true
      postgresql.db_size:
        enabled: true
      postgresql.backends:
        enabled: true
      postgresql.connection.max:
        enabled: true
      postgresql.rows:
        enabled: true
      postgresql.index.scans:
        enabled: true
      postgresql.index.size:
        enabled: true
      postgresql.operations:
        enabled: true
      postgresql.replication.data_delay:
        enabled: true
      postgresql.rollbacks:
        enabled: true
      postgresql.table.count:
        enabled: true
      postgresql.table.size:
        enabled: true
      postgresql.table.vacuum.count:
        enabled: true
      postgresql.temp_files:
        enabled: true
      postgresql.wal.age:
        enabled: true
      postgresql.wal.lag:
        enabled: true
      postgresql.wal.delay:
        enabled: true
      postgresql.tup_updated:
        enabled: true
      postgresql.tup_returned:
        enabled: true
      postgresql.tup_fetched:
        enabled: true
      postgresql.tup_inserted:
        enabled: true
      postgresql.tup_deleted:
        enabled: true
      postgresql.blks_hit:
        enabled: true
      postgresql.blks_read:
        enabled: true

exporters:
  debug:
    verbosity: detailed

processors:
  resource:
    attributes:
    - key: service.name
      value: "postgres"
      action: upsert
    - key: host
      value: "<rds-endpoint>"
      action: upsert

service:
  pipelines:
    metrics:
      receivers: [ postgresql ]
      processors: [ resource ]
      exporters: [ debug ] 


```

> This will connect to the pg db and use pg_monitor and pg_stats to get all these data.
