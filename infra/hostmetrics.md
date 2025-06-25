# Resource detection processor complete config

## For System Metrics
```yaml
receivers:
  hostmetrics:
        collection_interval: 10s
        scrapers:
          paging:
            metrics:
              system.paging.usage:
                enabled: true
              system.paging.operations:
                enabled: true
              system.paging.faults:
                enabled: true
              system.paging.utilization:
                enabled: true

          memory:
            metrics:
              system.memory.limit:
                enabled: true
              system.memory.usage:
                enabled: true
              system.memory.page_size:
                enabled: true
              system.linux.memory.available:
                enabled: true
              system.linux.memory.dirty:
                enabled: true
              system.memory.utilization:
                enabled: true

          cpu:
            metrics:
              system.cpu.time:
                enabled: true
              system.cpu.utilization:
                enabled: true
              system.cpu.physical.count:
                enabled: true
              system.cpu.logical.count:
                enabled: true
              system.cpu.frequency:
                enabled: true
          load:
            metrics:
              system.cpu.load_average.1m:
                enabled: true
              system.cpu.load_average.5m:
                enabled: true
              system.cpu.load_average.15m:
                enabled: true 
          filesystem:
            metrics:
              system.filesystem.usage:
                enabled: true
              system.filesystem.inodes.usage:
                enabled: true
              system.filesystem.utilization:
                enabled: true 

          network: 
            metrics:
              system.network.packets:
                enabled: true
              system.network.dropped:
                enabled: true
              system.network.errors:
                enabled: true
              system.network.io:
                enabled: true
              system.network.connections:
                enabled: true
              system.network.conntrack.count:
                enabled: true
              system.network.conntrack.max:
                enabled: true   
          processes: 
            metrics:
              system.processes.created:
                enabled: true
              system.processes.count:
                enabled: true
          process:
            metrics:
              process.cpu.time:
                enabled: true
              process.cpu.utilization:
                enabled: true
              process.memory.usage:
                enabled: true
              process.memory.virtual:
                enabled: true
              process.memory.utilization:
                enabled: true
              process.disk.io:
                enabled: true
              process.paging.faults:
                enabled: true
              process.signals_pending:
                enabled: true
              process.threads:
                enabled: true
              process.open_file_descriptors:
                enabled: true
              process.handles:
                enabled: true
              process.context_switches:
                enabled: true
              process.disk.operations:
                enabled: true
              process.uptime:
                enabled: true
          system:
            metrics:
              system.uptime:
                enabled: true
          disk:
            metrics:
              system.disk.io:
                enabled: true
              system.disk.operations:
                enabled: true
              system.disk.io_time:
                enabled: true
              system.disk.operation_time:
                enabled: true
              system.disk.weighted_io_time:
                enabled: true
              system.disk.pending_operations:
                enabled: true
              system.disk.merged:
                enabled: true

exporters:
  debug:
    verbosity: detailed

processors:
  resourcedetection:
    detectors: ["system"]
    system:
      resource_attributes:
        host.arch:
          enabled: true
        host.cpu.cache.l2.size:
          enabled: true
        host.cpu.family:
          enabled: true
        host.cpu.model.id:
          enabled: true
        host.cpu.model.name:
          enabled: true
        host.cpu.stepping:
          enabled: true
        host.cpu.vendor.id:
          enabled: true
        host.id:
          enabled: true
        host.ip:
          enabled: true
        host.mac:
          enabled: true
        host.name:
          enabled: true
        os.description:
          enabled: true
        os.type:
          enabled: true
        os.version:
          enabled: true


service:
      pipelines:
        metrics:
          receivers: [hostmetrics]
          processors: [resourcedetection]
          exporters: [debug]
```

> This will collect all the available metrics that otel collector supports as of now and add resource attributes to it.


