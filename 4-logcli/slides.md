%title: LOKI
%author: xavki


# LOKI : logcli


<br>
* logcli : requêter par la ligne de commande uns erveur loki

<br>
* release : https://github.com/grafana/loki/releases

```
wget https://github.com/grafana/loki/releases/download/v1.5.0/logcli-linux-amd64.zip
sudo unzip -d /usr/local/bin logcli-linux-amd64.zip
sudo mv /usr/local/bin/logcli-linux-amd64 /usr/local/bin/logcli
sudo chmod +x /usr/local/bin/logcli
```

<br>
* localisation du serveur loki

```
export LOKI_ADDR=<votre_serveur>
ou
--addr="http://localhost:3100"
```

<br>
* lister les labels

```
logcli labels
logcli labels host
```

<br>
* afficher les logs avec filtre

```
logcli query '{host="srv1",job="nginx"}'
```

<br>
* mode tail

```
logcli query '{host="srv1",job="nginx"}' --tail
```


