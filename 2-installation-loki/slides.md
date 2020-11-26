%title: LOKI
%author: xavki


# LOKI : Installation


<br>


* loki = base de données centralisée

<br>


* loki releases :
https://github.com/grafana/loki/releases

<br>




```
sudo wget https://github.com/grafana/loki/releases/download/v1.5.0/loki-linux-amd64.zip
sudo unzip -d /usr/local/bin/ loki-linux-amd64.zip
sudo mv /usr/local/bin/loki-linux-amd64 /usr/local/bin/loki
sudo chmod +x /usr/local/bin/loki
sudo mkdir /etc/loki
sudo vim /etc/loki/loki.yml
sudo mkdir /var/lib/loki
```

--------------------------------------------------------------------------------------

# LOKI : Installation

* configuration : https://grafana.com/docs/loki/latest/configuration/examples/

```
auth_enabled: false
server:
  http_listen_port: 3100
ingester:
  lifecycler:
    address: 127.0.0.1
    ring:
      kvstore:
        store: inmemory
      replication_factor: 1
    final_sleep: 0s
  chunk_idle_period: 5m
  chunk_retain_period: 30s
schema_config:
  configs:
  - from: 2020-05-15
    store: boltdb  #https://github.com/boltdb/bolt
    object_store: filesystem
    schema: v11
    index:
      prefix: index_
      period: 168h
storage_config:
  boltdb:
    directory: /var/lib/loki/index
  filesystem:  #https://grafana.com/blog/2020/02/19/how-loki-reduces-log-storage/
    directory: /var/lib/loki/chunks
limits_config:
  enforce_metric_name: false
  reject_old_samples: true
  reject_old_samples_max_age: 168h
```

--------------------------------------------------------------------------------------

# LOKI : Installation

* service systemd

```
sudo vim /etc/systemd/system/loki.service
[Unit]
Description=Service Loki
After=network.target
[Service]
Type=simple
ExecStart=/usr/local/bin/loki -config.file /etc/loki/loki.yml
[Install]
WantedBy=multi-user.target
```
