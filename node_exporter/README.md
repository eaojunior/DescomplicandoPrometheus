# Node Exporter do Prometheus

### Página

Confira a versão mais atual no endereço: https://github.com/prometheus/node_exporter/releases

```bash
wget https://github.com/prometheus/node_exporter/releases/download/v1.7.0/node_exporter-1.7.0.linux-amd64.tar.gz
tar -zxvf node_exporter-1.7.0.linux-amd64.tar.gz
cd node_exporter-1.7.0.linux-amd64
sudo mv node_exporter /usr/local/bin
```

### Instalação

```bash
sudo addgroup --system node_exporter
sudo adduser --shell /bin/nologin --system --group node_exporter
```

### Criar o serviço do SystemD

```bash
sudo vim /etc/systemd/system/node_exporter.service [Arquivo na pasta ../conf]
sudo systemctl daemon-reload
```

