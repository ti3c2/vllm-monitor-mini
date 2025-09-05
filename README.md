# vLLM Monitor

Docker-based monitoring setup for vLLM instances using Prometheus and Grafana.

## Setup Instructions

1. **Configure your vLLM endpoint**:
   Edit `prometheus/prometheus.yml` and replace `<VLLM_HOST>:<PORT>` with your actual vLLM endpoint (e.g., `10.20.0.15:8000`).

2. **Add the dashboard**:
   Place your vLLM Grafana dashboard JSON file in `grafana/dashboards/` as `vllm_grafana_dashboard.json`.

3. **Start the services**:
   ```bash
   docker compose up -d
   ```

## Access URLs

- **Prometheus**: http://localhost:9090
- **Grafana**: http://localhost:3000 (login: `admin` / `admin`)

## Configuration

### Multiple vLLM targets
To monitor multiple vLLM instances, edit `prometheus/prometheus.yml` and add more targets:

```yaml
static_configs:
  - targets:
      - "10.20.0.15:8000"
      - "10.20.0.16:8000"
```

### Authentication
If your vLLM `/metrics` endpoint requires authentication, uncomment and configure the relevant sections in `prometheus/prometheus.yml`:

```yaml
# basic_auth:
#   username: YOUR_USER
#   password: YOUR_PASS
```

### HTTPS/TLS
For HTTPS endpoints, change `scheme: http` to `scheme: https` in `prometheus/prometheus.yml`.

## Files Structure

```
vllm_monitor/
├── docker-compose.yml
├── prometheus/
│   ├── prometheus.yml      # Prometheus configuration
│   └── alerts.yml          # Alert rules
├── grafana/
│   ├── provisioning/
│   │   ├── datasources/
│   │   │   └── datasource.yml    # Prometheus datasource config
│   │   └── dashboards/
│   │       └── dashboards.yml    # Dashboard provisioning config
│   └── dashboards/
│       └── README.md             # Instructions for dashboard placement
└── README.md                     # This file
```

## Commands

- Start services: `docker compose up -d`
- Stop services: `docker compose down`
- View logs: `docker compose logs -f`
- Restart services: `docker compose restart`
