# HOMEWORK_PROMETHEUS_GRAFANA

## Prometheus

wget https://github.com/prometheus/prometheus/releases/download/v2.40.2/prometheus-2.40.2.linux-amd64.tar.gz
tar xvzf prometheus-3.3.1.linux-amd64.tar.gz

mkdir /var/lib/prometheus
mkdir /etc/ptometheus

cp ./prometheus promtool /usr/local/bin/
cp -R ./console_libraries/ /etc/prometheus/
cp -R ./consoles/ /etc/prometheus/
chown -R prometheus:prometheus /etc/prometheus /var/lib/prometheus
chown prometheus:prometheus /usr/local/bin/prometheus
chown prometheus:prometheus /usr/local/bin/promtool


/usr/local/bin/prometheus --config.file /etc/prometheus/prometheus.yml --storage.tsdb.path /var/lib/prometheus/ --web.console.templates=/etc/prometheus/consoles --web.console.libraries=/etc/prometheus/console_libraries


nano /etc/systemd/system/prometheus.service

[Unit]
Description=Prometheus Service Netology Lesson 9.4
After=network.target
[Service]
User=prometheus
Group=prometheus
Type=simple
ExecStart=/usr/local/bin/prometheus \
--config.file /etc/prometheus/prometheus.yml \
--storage.tsdb.path /var/liЬ/prometheus/ \
--web.console.templates=/etc/prometheus/consoles \
--web.console.libraries=/etc/prometheus/console_libraries
ExecReload=/bin/kill -HUP $MAINPID Restart=on-failure
[Install]
WantedBy=muti-user.target

mkdir -p /var/liЬ/prometheus
chown -R prometheus:prometheus /var/liЬ/prometheus



## Nodexporter

wget https://github.com/prometheus/node_exporter/releases/download/vl.4.0/node_exporter-l.4.0.linux-amd64.tar.gz

tar xvzf https://github.com/prometheus/node_exporter/releases/download/vl.4.0/node_exporter-l.4.0.linux-amd64.tar.gz

cd /node_exporter-l.4.0.linux-amd64
mkdir /etc/prometheus/node-exporter/

cp ./node_exporter  /etc/prometheus/node-exporter/

chown -R prometheus:prometheus /etc/prometheus/node-exporter/

ls -la /etc/prometheus/node-exporter/

nano /etc/systemd/system/node-exporter.service

[Unit]
Description=Node Exporter Lesson 9.4
After=network.target
[Service]
User=prometheus
Group=prometheus
Type=simple
ExecStart=/etc/prometheus/node-exporter/node_exporter
[Install]
WantedBy=multi-user.target


### Пропишите автозапуск:
sudo systemctl enable node-exporter
### Запустите сервис:
sudo systemctl start node-exporter
### Проверьте статус сервиса:
sudo systemctl status node-exporter


nano /etc/prometheus/prometheus.yml


## Установка Grafana 

sudo apt-get install -y adduser libfontconfig1 musl
wget https://dl.grafana.com/oss/release/grafana_12.0.0_amd64.deb
sudo dpkg -i grafana_12.0.0_amd64.deb
----
wget https://dl.grafana.com/oss/release/grafana-12.0.0.linux-amd64.tar.gz
tar -zxvf grafana-12.0.0.linux-amd64.tar.gz
----

systemctl enable grafana-server
systemctl start grafana-server
systemctl status grafana-server

http://192.168.230.130:3000/
Admin
admin
art
1234

### сброс пароля
$ sudo sqlite3 /var/lib/grafana/grafana.db

sqlite> update user set password = '59acf18b94d7eb0694c61e60ce44c110c7a683ac6a8f09580d626f90f4a242000746579358d77dd9e570e83fa24faa88a8a6', salt = 'F3FAxVm33R' where login = 'admin';
sqlite> .exit

--------------