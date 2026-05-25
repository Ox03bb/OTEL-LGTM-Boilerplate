# OTEL-LGTM-Boilerplate

Production-ready observability boilerplate using OpenTelemetry and the LGTM stack (Loki, Grafana, Tempo, Mimir). This repo ships a Docker Compose setup, a preconfigured OpenTelemetry Collector, and Grafana provisioning with a host metrics dashboard.

## Stack

- Grafana for visualization
- Loki for logs
- Tempo for traces
- Mimir for metrics
- OpenTelemetry Collector for ingest and routing

## Quick start

1. Start the stack:

```bash
docker compose --env-file .env -f <your_composer_1> -f...  -f docker-compose.monitoring.yml up -d
```

2. Open Grafana:

- URL: http://localhost:3000
- User: `admin`
- Password: `admin`

You can override credentials with environment variables:

```bash
export GF_SECURITY_ADMIN_USER=myuser
export GF_SECURITY_ADMIN_PASSWORD=mypassword
```

## Services

- `grafana` is exposed on port 3000
- `loki`, `tempo`, `mimir`, and `otel-collector` run on the internal Docker network

If you need to send telemetry from the host machine, add explicit port mappings to `otel-collector` and update the collector config.

## Configuration

Key config files:

- `monitoring/otel/collector-config.yaml` - OpenTelemetry Collector pipelines, receivers, exporters, and processors.
- `monitoring/loki/loki-config.yaml` - Loki storage, retention, and ingestion settings.
- `monitoring/tempo/tempo-config.yaml` - Tempo trace storage and receiver settings.
- `monitoring/mimir/mimir-config.yaml` - Mimir metrics storage and limits.
- `monitoring/grafana/provisioning/datasources/datasources.yaml` - Grafana data source definitions for Loki, Tempo, and Mimir.
- `monitoring/grafana/provisioning/dashboards/dashboards.yaml` - Grafana dashboard provisioning rules.
- `monitoring/grafana/dashboards/metrics.json` - Prebuilt host metrics dashboard.

