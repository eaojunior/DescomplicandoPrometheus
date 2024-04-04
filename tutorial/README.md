# Tutorial Instalação e Configuração do Prometheus

Este documento tem o objetivo de auxiliar na instalação e configuração do Prometheus em um servidor Linux.

### 1 - Download

```bash
curl -LO https://github.com/prometheus/prometheus/releases/download/v2.51.0/prometheus-2.51.0.linux-amd64.tar.gz
```

### 2 - Extrair arquivos

```bash
tar -xvf prometheus-2.51.0.linux-amd64.tar.gz
cd prometheus-2.51.0.linux-amd64
```

### 3 - Criar diretórios

```bash
sudo su
mkdir /etc/prometheus
mkdir /var/lib/prometheus
mkdir /var/log/prometheus
mv prometheus.yml /etc/prometheus
mv console_libraries/ /etc/prometheus/
mv consoles /etc/prometheus
```

### 4 - Criar grupo e usuário do prometheus e corrigir permissões

```bash
sudo su
addgroup --system prometheus
adduser --shell /sbin/nologin --system --group prometheus
chown -R prometheus:prometheus /etc/prometheus/
chown -R prometheus:prometheus /var/lib/prometheus/
chown -R prometheus:prometheus /var/log/prometheus
chown -R prometheus:prometheus /usr/local/bin/prometheus
chown -R prometheus:prometheus /usr/local/bin/promtool
```

### 5 - Ajustar configurações do serviço do Prometheus

```bash
sudo vim /etc/prometheus/prometheus.yml
```

```yaml
global:
  scrape_interval: 15s
  evaluation_interval: 15s
  scrape_timeout: 10s
rule_files:
scrape_configs:
  - job_name: "prometheus"
    static_configs:
      - targets: ["localhost:9090"]
```

### 6 - Criar serviço do Prometheus no SystemD

```bash
sudo vim /etc/systemd/system/prometheus.service
```

```bash
[Unit] 
Description=Prometheus 
Documentation=https://prometheus.io/docs/introduction/overview/ 
Wants=network-online.target 
After=network-online.target 

[Service] 
Type=simple 
User=prometheus
Group=prometheus
ExecReload=/bin/kill -HUP \$MAINPID
ExecStart=/usr/local/bin/prometheus \
    --config.file=/etc/prometheus/prometheus.yml \
    --storage.tsdb.path=/var/lib/prometheus \
    --web.console.templates=/etc/prometheus/consoles \
    --web.console.libraries=/etc/prometheus/console_libraries \
    --web.listen-address=0.0.0.0:9090 \
    --web.external-url= 

SyslogIdentifier=prometheus 
Restart=always 

[Install] 
WantedBy=multi-user.target
```

### 7 - Atualizar a base de dados do SystemD e iniciar o serviço

```bash
sudo systemctl daemon-reload
sudo systemctl start prometheus
sudo systemctl enable prometheus
```

#### 7.1 - Para efetuar troubleshoot

```bash
sudo journalctl -u prometheus
```

### 8 - Testando

```bash
curl -GET http://localhost:9090/metrics
```