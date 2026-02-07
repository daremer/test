
# Jar
java -jar plantuml.jar -gui

# Podman
```sh
$ podman pull plantuml/plantuml-server:jetty
Resolving "plantuml/plantuml-server" using unqualified-search registries (/etc/containers/registries.conf)
Trying to pull docker.io/plantuml/plantuml-server:jetty...
Getting image source signatures
Copying blob 7a2ccf660fc8 done   |
Copying blob 5a7813e071bf done   |
Copying blob dbe46403441a done   |
Copying blob e3da94a33fa1 done   |
Copying blob f9f4ee04af87 done   |
Copying blob f03e4717322c done   |
Copying blob 4f4fb700ef54 skipped: already exists
Copying blob 1120195dbf4e done   |
Copying blob 21464c501fa2 done   |
Copying blob 294549697571 done   |
Copying blob e3c0bab91d84 done   |
Copying blob 263b6156e49f done   |
Copying blob 4f4fb700ef54 skipped: already exists
Copying blob 4f4fb700ef54 skipped: already exists
Copying blob 01d5b59d6b17 done   |
Copying blob 847bdb640bc5 done   |
Copying blob 4daaa2d656e6 done   |
Copying blob 7e9f7a12cef4 done   |
Copying config 85b1c65e78 done   |
Writing manifest to image destination
85b1c65e78aed9cfe70553ed8469c72e154e2781fe9b0f2f8aed4f004b6c84a7
```

```sh
$ podman run -d -p 8080:8080 plantuml/plantuml-server:jetty
3238ab6b7b63f800a96d1dc63ecef7ee9cdf20d2cced128b902a32581ff9e2d2
```

Access http://localhost:8080

# Podman compose

File `docker-compose.yml`:
```yaml
version: "3.9"

services:
  plantuml:
    image: plantuml/plantuml-server:jetty
    container_name: plantuml
    ports:
      - "8080:8080"
    restart: unless-stopped

    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:8080"]
      interval: 30s
      timeout: 5s
      retries: 3
      start_period: 10s
```

```sh
podman-compose up -d
```

Access http://localhost:8080
