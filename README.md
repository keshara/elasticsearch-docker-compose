# elasticsearch-docker-compose

# Installing
wget https://download.docker.com/linux/static/stable/x86_64/docker-19.03.0.tgz
tar -xvf docker-19.03.0.tgz
cp docker/* /usr/local/bin/
curl -L "https://github.com/docker/compose/releases/download/1.28.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
docker-compose --version

docker-compose up		: first cluster start up
docker-compose down		: destroy the cluster
docker-compose start	: start the cluster
docker-compose stop		: stop the cluster

# systemD unit file
[Unit]
Description=Docker Application Container Engine
After=network-online.target firewalld.service
Wants=network-online.target

[Service]
Type=notify
ExecStart=/usr/local/bin/dockerd
#ExecStart=/usr/local/bin/dockerd --data-root="/mnt"
ExecReload=/bin/kill -s HUP $MAINPID
LimitNOFILE=infinity
LimitNPROC=infinity
LimitCORE=infinity
#TasksMax=infinity
TimeoutStartSec=0
Delegate=yes
KillMode=process
Restart=on-failure
StartLimitBurst=3
StartLimitInterval=60s

[Install]
WantedBy=multi-user.target

