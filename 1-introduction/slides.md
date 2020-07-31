%title: LOKI
%author: xavki


# LOKI : collecte de journaux de logs


<br>
* Prometheus/Grafana > métriques (systèmes, applis...)

* Loki/Grafana > journaux (systèmes...)

<br>
Dépôt : https://github.com/grafana/loki
Site : https://docs.loki.network/
Doc : https://github.com/grafana/loki/tree/master/docs

<br>
* même principe ? presque
		* promtrail : agent collecte et envoi des journaux
		* loki : base de centralisation
		* grafana : valorisation

<br>
* cheminement :
	* promtrail > loki > grafana
	* route < prometheus > grafana

<br>
* concurrence ELK : un peu différent
		* plus simple
		* moins consommateurs en ressources
			* pas d'indexation full text
		* principe d'étiquettes (comme prometheus)
		* moins complet aussi
		* insiste sur sa facilité pour k8s

<br>
* l'idée est de faciliter la résolution d'incidents : 
		* alert > monitoring > analyse > logs > analyse (> opentracing > analyse) > solution

* LOKI > compléter grafana

<br>
* driver docker que l'on peut ajouter (docker plugin)


