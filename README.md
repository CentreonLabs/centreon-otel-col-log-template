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
logs. By default, these pipelines perform the following actions:

* **Batching**: Collects logs into batches for efficient export.
* **Resource Attributes**: Automatically enriches logs with resource attributes from the host, Kubernetes pod, or container where the logs originated.
* **OTLP Export**: Exports data in OTLP format to an exporter named
  `otlphttp/centreon`.

For more details on OpenTelemetry Collector pipelines, refer to the
[official documentation](https://opentelemetry.io/docs/collector/configuration/#pipelines).

Examples:

```yaml
service:
  pipelines:
    logs:
      receivers: [filelog/mylog]
      processors: [batch,resourcedetection]
      exporters: [otlphttp/centreon]
```

## List of templates

### Apache

* [Apache error](file-apache-error.yaml): The log errors of apache.

### Centreon

* [Centreon Broker](file-centreon-broker.yaml): The log file of Centreon Broker.
* [Centreon Engine](file-centreon-engine.yaml): The log file of Centreon Engine.
* [Centreon Gorgone](file-centreon-gorgone.yaml): The log file of Centreon Gorgone.
* [Centreon Web](file-centreon-web.yaml): The log file of Centreon Web.

### HTTP

* [Access Log Combibed](file-httpd-combined.yaml): The http access log in combined format.

### MariaDB

* [MariaDB](file-mariadb.yaml): The log files of MaraDB.

### Message / Syslog

* [Linux messages](file-message.yaml): The syslog system log file.

### Tomcat

* [Tomcat](file-tomcat.yaml): The Tomcat log file.
