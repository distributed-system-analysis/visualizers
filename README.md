# LiveMetricVisualizer
- A tool available to visualize Prometheus and PCP data

- Build locally with `podman build -t <name> -f DockerfileLive .`
- Available at quay.io/distributed-systems-analysis/live-metric-visualizer

- Directions:
  -   `podman pull distributed-systems-analysis/live-metric-visualizer`
  -   `podman run --network host distributed-systems-analysis/live-metric-visualizer`
  -   To visualize a run on a remote host, add `-e HOST=<host>`
    - If prometheus is on a different host, it can be individually set with `-e PROM_HOST=<host>`
    - If pmproxy is on a different host, it can be individually set with `-e PM_HOST=<host>`
  -   To change to a custom prometheus port, add `-e PROM_PORT=<port>`
  -   To change to a custom pmproxy port, add `-e PM_PORT=<port>`

- NOTES:
  - Container includes grafana server with preconfigured data sources and dashboards for both prometheus and PCP
  - Will work for live metric viewing alongside existing prometheus or pmlogger/pmproxy, but not for stand-alone post-run visualization
  - Default Grafana credentials are: admin/admin


# PromGrafVisualizer
- A tool available to visualize Prometheus data collected through Pbench after a benchmark run

- Build locally with `podman build -t <name> -f DockerfilePostProm .`
- Available at quay.io/distributed-systems-analysis/prom-graf-visualizer
- Preloaded dashboards for node-exporter and grafana

- Directions:
  -   `podman pull distributed-systems-analysis/prom-graf-visualizer`
  -   `podman run -p 3000:3000 -p 9090:9090 -v absolute/path/to/prometheus_data:/data:Z distributed-systems-analysis/prom-graf-visualizer`

- NOTES: 
  - Works with any other self-obtained prometheus data.
  - Default Grafana credentials are: admin/admin

# PCPGrafVisualizer
- A tool available to visualize PCP data

- Build locally with `podman build -t <name> -f DockerfilePostPCP .`
- Available at quay.io/distributed-systems-analysis/pcp-graf-visualizer
- Preloaded dashboards for pcp data visualization

- Directions:
  -   `podman pull distributed-systems-analysis/pcp-graf-visualizer`
  -   `podman run --network host -v /<path>/<to>/<pcp_log_folder>/data:/var/log/pcp/pmlogger:Z distributed-systems-analysis/pcp-graf-visualizer`
  - If you would rather use your own existing redis instance rather than have one launch internally:
    - You must specify redis host with `-e REDIS_HOST=<port>`
    - If not on the default port (6379), you can also add `-e REDIS_PORT=<port>`

- NOTES:
  - Works with any self-obtained PCP data.
  - Default Grafana credentials are: admin/admin
