# Prometheus-Grafana-Stack
A practical stack include Prometheus and Grafana to learn and practice monitoring tasks.

## Installing Prometheus

        wget https://github.com/prometheus/prometheus/releases/download/v3.5.0/prometheus-3.5.0.linux-amd64.tar.gz
        tar -xzf prometheus-*.linux-amd64.tar.gz
        cd prometheus-*.linux-amd64

Modify prometheus.yml like the file in repo

        ./prometheus &

## Installing node exporter

        wget https://github.com/prometheus/node_exporter/releases/download/v1.8.2/node_exporter-1.8.2.linux-amd64.tar.gz
        tar -xzf node_exporter-*.linux-amd64.tar.gz
        cd node_exporter-*.linux-amd64
        ./node_exporter &

## Installing Alertmanager

        wget https://github.com/prometheus/alertmanager/releases/download/v0.27.0/alertmanager-0.27.0.linux-amd64.tar.gz
        tar -xzf alertmanager-0.27.0.linux-amd64.tar.gz
        cd alertmanager-0.27.0.linux-amd64
