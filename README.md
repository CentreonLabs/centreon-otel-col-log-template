# Centreon OpenTelemetry Collector Log Templates

[![License: AGPL v3](https://img.shields.io/badge/License-AGPL%20v3-blue.svg)](https://www.gnu.org/licenses/agpl-3.0)

This repository offers a collection of OpenTelemetry Collector templates
designed to parse and structure various log formats into the OpenTelemetry
Protocol (OTLP) format. These templates adhere to the
[OpenTelemetry Semantic Conventions](https://opentelemetry.io/docs/specs/semconv/),
ensuring best practices for data representation.

## How to Use

1. **Download a Template:**

Download your desired template into your OpenTelemetry Collector configuration
directory (e.g., `/etc/otelcol-contrib` on Linux):

```shell
wget https://raw.githubusercontent.com/CentreonLabs/centreon-otel-col-log-template/refs/heads/main/myfile.yaml -O /etc/otelcol-contrib/myfile.yaml
```

Replace myfile.yaml with the actual template filename you wish to use.

2. **Update Collector Command:**

Modify your OpenTelemetry Collector start command to include the downloaded
configuration file:

```shell
otelcol-contrib --config /etc/otelcol-contrib/myfile.yaml
```

Ensure otelcol-contrib is the correct command for your OpenTelemetry Collector
installation.

### Template Pipelines

Each template includes a pre-configured pipeline designed to process the parsed
logs. By default, these pipelines perform the following actions, in order:

- **Memory Limiting**: Prevents the collector from exceeding its memory budget.
- **Resource Attributes**: Automatically enriches logs with resource attributes from the host, Kubernetes pod, or container where the logs originated.
- **Batching**: Collects logs into batches for efficient export.
- **OTLP Export**: Exports data in OTLP format to an exporter named
  `otlphttp/centreon`.

For more details on OpenTelemetry Collector pipelines, refer to the
[official documentation](https://opentelemetry.io/docs/collector/configuration/#pipelines).

Examples:

```yaml
service:
  pipelines:
    logs/mylog:
      receivers: [filelog/mylog]
      processors: [memory_limiter, resourcedetection, batch]
      exporters: [otlphttp/centreon]
```

## List of templates

### Android

- [Android logcat](file-android-logcat.yaml): Android logcat output in `threadtime` format.
- [HealthApp](file-healthapp.yaml): The Android HealthApp pipe-delimited log file.

### Apache

- [Apache error](file-apache-error.yaml): The log errors of apache.

### Centreon

- [Centreon Broker](file-centreon-broker.yaml): The log file of Centreon Broker.
- [Centreon Engine](file-centreon-engine.yaml): The log file of Centreon Engine.
- [Centreon Gorgone](file-centreon-gorgone.yaml): The log file of Centreon Gorgone.
- [Centreon Web](file-centreon-web.yaml): The log file of Centreon Web.

### Hadoop

- [Hadoop](file-hadoop.yaml): The Hadoop Log4j-style log files (ResourceManager, NodeManager, ...).
- [HDFS](file-hdfs.yaml): The legacy Hadoop HDFS DataNode/NameNode log files.

### HPC

- [BGL RAS](file-bgl-ras.yaml): The IBM Blue Gene/L RAS event log.
- [HPC cluster](file-hpc.yaml): The HPC cluster (mmcs) node event log.

### HTTP

- [Access Log Combined](file-httpd-combined.yaml): The http access log in combined format.

### macOS

- [macOS system log](file-macos-system-log.yaml): The macOS `/var/log/system.log` in BSD syslog framing.

### MariaDB

- [MariaDB](file-mariadb.yaml): The log files of MariaDB.

### Message / Syslog

- [Linux messages](file-message.yaml): The syslog system log file.
- [Thunderbird](file-thunderbird.yaml): The Thunderbird supercomputer centralized syslog (alert label, epoch and origin-host prefix).

### OpenStack

- [OpenStack Nova](file-openstack-nova.yaml): The OpenStack Nova log files (api, compute, scheduler), including WSGI access lines.

### Proxifier

- [Proxifier](file-proxifier.yaml): The Proxifier connection lifecycle log.

### Spark

- [Spark](file-spark.yaml): The Apache Spark log files.

### Tomcat

- [Tomcat](file-tomcat.yaml): The Tomcat log file.

### PostgreSQL

- [PostgreSQL base](file-postgres-base.yaml): The basic PostgreSQL log file. Log
  prefix: `%m [%p] `.

### Redis

- [Redis](file-redis.yaml): Redis log file, with paring role, component, level.

### Windows CBS

- [Windows CBS](file-windows-cbs.yaml): The Windows Component-Based Servicing
  log file (`C:\Windows\Logs\CBS\CBS.log`).

### Windows Event Log

- [Windows Event Log](windows-event-log.yaml): Contains the event log
  application parsing with locale US and FR for level conversions.

### ZooKeeper

- [ZooKeeper](file-zookeeper.yaml): The Apache ZooKeeper Log4j-style log files.
