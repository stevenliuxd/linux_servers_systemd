# Server Configs

## Path: /etc/systemd/system

### ranchbot.service - requires docker
```
[Unit]
Description=Ranchbot Discord Bot Service
After=network.target docker.service
Requires=docker.service

[Service]
ExecStart=/usr/bin/docker run --rm --env-file /home/steven/code/ranchbot/.env ranchbot
WorkingDirectory=/home/steven/code/ranchbot
Restart=always
User=steven
StandardOutput=journal
StandardError=journal

[Install]
WantedBy=multi-user.target
```

### ftb.service
```
[Unit]
Description=FTB Server
After=network.target

[Service]
User=root
Group=root
WorkingDirectory=/home/steven/servers/unstable_1_2_0
ExecStart=/bin/bash start.sh
ExecStop=/bin/bash stop.sh
Restart=on-failure
RestartSec=20

[Install]
WantedBy=multi-user.target
```

### satisfactory.service
```
[Unit]
Description=Satisfactory Server
After=network.target

[Service]
User=steven
Group=steven
WorkingDirectory=/home/steven/servers/satisfactory
ExecStart=/bin/bash FactoryServer.sh start
ExecStop=/bin/bash FactoryServer.sh stop
Restart=on-failure
RestartSec=20

[Install]
WantedBy=multi-user.target
```

### prometheus.service
```
[Unit]
Description=Prometheus
After=network.target

[Service]
WorkingDirectory=/home/steven/monitoring/prometheus
Type=simple
ExecStart=/home/steven/monitoring/prometheus/prometheus --config.file=/home/steven/monitoring/prome>
Restart=on-failure
User=steven

[Install]
WantedBy=default.target
```

### grafana.service
```
[Unit]
Description=Grafana
After=network.target

[Service]
Type=simple
ExecStart=/home/steven/monitoring/grafana/bin/grafana-server -homepath /home/steven/monitoring/graf>
Restart=on-failure
User=steven

[Install]
WantedBy=default.target
```

### node_exporter.service
```
[Unit]
Description=Prometheus Node Exporter
After=network.target

[Service]
ExecStart=/usr/local/bin/node_exporter
Restart=always
User=node_exporter

[Install]
WantedBy=default.target
```

#### Note that prometheus/grafana/node_exporter was installed via tarball, and we moved the binary from the node_exporter into /usr/local/bin