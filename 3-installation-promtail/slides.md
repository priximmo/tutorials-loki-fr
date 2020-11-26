%title: LOKI
%author: xavki


# LOKI : Installation Promtail


<br>


* promtail = agent qui envoi les logs vers loki

<br>


* installation

Sources : https://github.com/grafana/loki/releases

```
sudo wget https://github.com/grafana/loki/releases/download/v1.5.0/promtail-linux-amd64.zip
sudo unzip -d /usr/local/bin/ promtail-linux-amd64.zip
sudo mv /usr/local/bin/promtail-linux-amd64 /usr/local/bin/promtail
sudo chmod +x /usr/local/bin/promtail
sudo mkdir /etc/promtail
sudo vim /etc/promtail/promtail.yml
```

-------------------------------------------------------------------------------

# LOKI : Installation Promtail

<br>


* configuration

```
server:
  http_listen_port: 9080
  grpc_listen_port: 0
positions:
  filename: /tmp/positions.yaml
client:
  url: http://loki:3100/loki/api/v1/push
scrape_configs:
  - job_name: nginx
    static_configs:
    - targets:
        - localhost
      labels:
        job: nginx
        env: production
        host: srv1
        __path__: /var/log/nginx/*.log
  - job_name: journal
    journal:
      max_age: 1h
      path: /var/log/journal
      labels:
        job: systemd
        env: production
    relabel_configs:
      - source_labels: ['__journal__systemd_unit']
        target_label: 'unit'
```

-------------------------------------------------------------------------------

# LOKI : Installation Promtail

<br>


* cration du service systemd

```
[Unit]
Description=Promtail service
After=network.target
[Service]
Type=simple
ExecStart=/usr/local/bin/promtail -config.file /etc/promtail/promtail.yml
[Install]
WantedBy=multi-user.target
```


<br>


* installation grafana

```
sudo apt install grafana
sudo systemctl start grafana-server
```
