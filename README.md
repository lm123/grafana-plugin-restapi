# Overview

Grafana provides plugin mechanism to extend its supported datasources. grafana-prometheus-alertmanager-datasource is one good example to declare Prometheus alertmanager as one of Grafana's datasource. Prometheus alertmanager implements REST API /api/v1/alerts to enable application to retrieve all its alerts. The alerts can be displayed in the Table panel.

CSF CALM has the similar REST API /api/alma/alarms to get all the alarms. So grafana-prometheus-alertmanager-datasource can be updated to make CSF CALM as one of Grafana datasource.

The major code change is existed in src/datasource.js, there are following changes:
	query(option)
		/api/v1/alerts -> /api/alma/alarms
          	response.data ->  response
          	response.data.data ->  response.data
	getColumnDict(data, labelSelector)
		data is not array, just one dict

# Proof Of Concept

## Source Code gcd.tar

## How to build the plugin?

1) install npm https://github.com/nodejs/help/wiki/Installation
2) set env

    export VERSION=v10.15.3

    export DISTRO=linux-x64

    export PATH=/usr/local/lib/nodejs/node-$VERSION-$DISTRO/bin:$PATH

3) tar xvf gcd.tar

4) build

    npm install -g yarn

    yarn install

    npm run build

5) ln -s /root/lm/grafana-plugins/grafana-calm-datasource/dist /var/lib/grafana/plugins/grafanacalm-datasource

6) restart grafana-server


# References & useful links

https://github.com/camptocamp/grafana-prometheus-alertmanager-datasource

