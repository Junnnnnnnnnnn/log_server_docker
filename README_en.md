## Development Environment
- **Windows 10**: The operating system used for development and testing.
- **Loki**: Log aggregation system for storing and querying logs.
- **Grafana**: Visualization platform for displaying logs from Loki.
- **Promtail**: Agent for collecting logs and sending them to Loki.
- **Docker Compose**: Tool for defining and running multi-container Docker applications.
- **Docker Desktop**: Application for running Docker containers on Windows.

## Description
> Building a log monitoring server using Loki, Grafana, Promtail, and Docker Compose.

## Development Process and Understanding
![alt text](log_flow.png)

1. Create `log file` inside the `application` (using Winston).
2. The `promtail container` catches the generated log file.
3. The captured log data is pushed to the `loki container`.
4. The pushed data is provided to the `grafana container`.


## grafana loki Query
Logs are categorized by the `job name` set in [promtail.conf](promtail-config.yml)
```
loki query

{job="kakao_clone_back"}
```
> View all logs for the desired project.

```
loki query

{job="kakao_clone_back"} |= "7c9b1247-1bd9-4946-aff6-a232dd1daa2b"
```
> View logs containing the specific string for the desired project.

## prometheus
Metrics are categorized by the `job name` set in [prometheus.yml](prometheus.yml)

## Notes
- All containers are part of the `app network`.
- When accessing the `loki container`, use `loki:3100` instead of `localhost:3100`.

> ❗ When deploying to development or production servers, set the app domain and grafana domain.