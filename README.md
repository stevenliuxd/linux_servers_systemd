# Server Configs

## Path: /etc/systemd/system

### ranchbot.service
```
[Unit]
Description=Ranchbot Python Script
After=network.target

[Service]
User=steven
Group=steven
WorkingDirectory=/home/steven/code/ranchbot
ExecStart=/usr/bin/python3 /home/steven/code/ranchbot/ranchbot.py
Restart=on-failure
RestartSec=20

[Install]
WantedBy=multi-user.target
```

### ftb.service
```
[Unit]
Description=Minecraft Server - Direwolf1.12
After=network.target

[Service]
User=steven
Group=steven
WorkingDirectory=/home/steven/servers/direwolf1_12
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

