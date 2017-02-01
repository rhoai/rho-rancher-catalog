# Host Stats

### Topology

A Host Stats instance will be started on every host that does not match the
scheduling rule (default is `host-stats-exclude=true`).

### Operation

This will log CPU, Memory, and Disk utilization stats every 30 seconds by
default. You can configure what to log, add a prefix to the log, and change
the logging frequency.
