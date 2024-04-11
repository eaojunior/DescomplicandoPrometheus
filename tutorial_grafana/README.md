# Tutorial Instalação e Configuração do Grafana

Este documento tem o objetivo de auxiliar na instalação e configuração do Grafana em um servidor Linux.

### 1 - Download e Instalação

```bash
sudo apt-get install -y apt-transport-https software-properties-common wget
sudo mkdir -p /etc/apt/keyrings/
wget -q -O - https://apt.grafana.com/gpg.key | gpg --dearmor | sudo tee /etc/apt/keyrings/grafana.gpg > /dev/null
echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://apt.grafana.com stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
# Updates the list of available packages
sudo apt-get update
# Installs the latest OSS release:
sudo apt-get install grafana
```

### 2 - Acesso

[Página do Grafana](http://localhost:3000/)

```yaml
Login: admin
Senha: admin
```

### 3 - Ajustar configurações do serviço do Grafana

```bash
sudo vim /etc/grafana/grafana.yml
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

#### 7.1 - Para efetuar troubleshoot

```bash
sudo journalctl -u prometheus
```

### 8 - Testando

```bash
curl -GET http://localhost:9090/metrics
```