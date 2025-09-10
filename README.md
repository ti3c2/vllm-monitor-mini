# vLLM Monitor

Docker-based monitoring setup for vLLM instances using Prometheus and Grafana.

## Setup Instructions

1. **Configure your vLLM endpoint**:
   Edit `prometheus/prometheus.yml` and add your vLLM endpoints `<VLLM_HOST>:<PORT>` (e.g., `10.20.0.15:8000`).

2. **Add the dashboard**:
   Use default dashboard or place your own JSON file in `grafana/dashboards/` as `vllm_grafana_dashboard.json`.

3. **Start the services**:
   ```bash
   docker compose up -d
   ```

4. **Access Grafana**:
   Go to http://localhost:2000 and enter credentials (login:pwd = `admin`:`admin`)

## Available URLs

- **Grafana**: http://localhost:2000 (login: `admin` / `admin`)
- **Prometheus**: http://localhost:9090


### Authentication
If your vLLM `/metrics` endpoint requires authentication, uncomment and configure the relevant sections in `prometheus/prometheus.yml`:

```yaml
# Defaults are admin:admin
basic_auth:
  username: YOUR_USER
  password: YOUR_PASS
```

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
