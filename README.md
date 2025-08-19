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

## Running Prometheus

### Paths:

        PROM_DIR=$HOME/prometheus-3.5.0.linux-amd64
        AM_DIR=$HOME/alertmanager-0.27.0.linux-amd64
        NE_DIR=$HOME/node_exporter-*.linux-amd64

### Users and Directories

        sudo useradd --no-create-home --shell /usr/sbin/nologin prometheus || true
        sudo useradd --no-create-home --shell /usr/sbin/nologin alertmanager || true
        sudo useradd --no-create-home --shell /usr/sbin/nologin node_exporter || true

        sudo mkdir -p /etc/prometheus /var/lib/prometheus
        sudo mkdir -p /etc/alertmanager /var/lib/alertmanager

### Copy binaries to /usr/local/bin

        sudo cp "$PROM_DIR/prometheus" "$PROM_DIR/promtool" /usr/local/bin/
        sudo cp "$AM_DIR/alertmanager" "$AM_DIR/amtool" /usr/local/bin/
        sudo cp $NE_DIR/node_exporter /usr/local/bin/

### Move configs

        [ -f "$HOME/prometheus.yml" ] && sudo cp "$HOME/prometheus.yml" /etc/prometheus/
        [ -f "$HOME/alertmanager.yml" ] && sudo cp "$HOME/alertmanager.yml" /etc/alertmanager/
        [ -f "$HOME/alert.rules.yml" ] && sudo cp "$HOME/alert.rules.yml" /etc/prometheus/

### Access

        sudo chown -R prometheus:prometheus /etc/prometheus /var/lib/prometheus
        sudo chown -R alertmanager:alertmanager /etc/alertmanager /var/lib/alertmanager
        sudo chown node_exporter:node_exporter /usr/local/bin/node_exporter
        sudo chown prometheus:prometheus /usr/local/bin/prometheus /usr/local/bin/promtool
        sudo chown alertmanager:alertmanager /usr/local/bin/alertmanager /usr/local/bin/amtool

### Systemd files in systemd directory in repository

### Enabling and running

        sudo systemctl daemon-reload

        sudo systemctl enable --now prometheus
        sudo systemctl enable --now alertmanager
        sudo systemctl enable --now node_exporter

        systemctl status prometheus --no-pager -l
        systemctl status alertmanager --no-pager -l
        systemctl status node_exporter --no-pager -l

