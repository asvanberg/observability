# Minimal but complete setup for distributed tracing and metrics

Start everything with `docker compose up`.

Instrumented application can send spans using gRPC or HTTP to the OpenTelemetry
Collector on ports 4317 and 4318 respectively. The Collector will then export
the spans to Jaeger for storage and visualization as well as convert them to
metrics which are sent to Prometheus for storing and querying.

Jaeger's [Service Performance Monitoring (SPM)](https://www.jaegertracing.io/docs/2.17/architecture/spm/)
is enabled by reading the metrics from Prometheus.

Using the ["contrib" version](https://github.com/open-telemetry/opentelemetry-collector-releases/blob/v0.149.0/distributions/otelcol-contrib)
of the OpenTelemetry Collector due to needing the [Span Metrics Connector](https://github.com/open-telemetry/opentelemetry-collector-contrib/tree/v0.149.0/connector/spanmetricsconnector).
The connector is used to generate metrics from spans which can then be exported to Prometheus.

## Components
- [OpenTelemetry Collector](https://opentelemetry.io/docs/collector/) (contrib)
- [Jaeger](https://www.jaegertracing.io/)
- [Prometheus](https://prometheus.io/)

## Exposed ports
- 4317 - OpenTelemetry Collector gRPC receiver
- 4318 - OpenTelemetry Collector HTTP receiver
- 9090 - Prometheus server
- 16686 - Jaeger UI

## Using in production
 - You must secure the exposed ports
 - You may configure a persistent storage for Jaeger to store traces (default is 100k traces in memory)
