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

### Collectors

O Node Exporter possui os `collectors` que são os responsáveis por capturar as métricas do sistema operacional. Por padrão, o Node Exporter vem com um monte de coletores habilitados, mas você pode habilitar outros, caso queira.

Para que você possa consultar a lista de `collectors` que vem habilitados por padrão, você pode acessar o link abaixo:

[Lista dos Collectors habilitados por padrão](https://github.com/prometheus/node_exporter#enabled-by-default)

[Lista dos Collectors desabilitados por padrão](https://github.com/prometheus/node_exporter#disabled-by-default)

#### Collectors mais utéis

* `arp`: Coleta métricas de ARP (Address Resolution Protocol) como por exemplo, o número de entradas ARP, o número de resoluções ARP, etc.
* `bonding`: Coleta métricas de interfaces em modo bonding.
* `conntrack`: Coleta métricas de conexões via Netfilter como por exemplo, o número de conexões ativas, o número de conexões que estão sendo rastreadas, etc.
* `cpu`: Coleta métricas de CPU.
* `diskstats`: Coleta métricas de IO de disco como por exemplo o número de leituras e escritas.
* `filefd`: Coleta métricas de arquivos abertos.
* `filesystem`: Coleta métricas de sistema de arquivos, como tamanho, uso, etc.
* `hwmon`: Coleta métricas de hardware como por exemplo a temperatura.
* `ipvs`: Coleta métricas de IPVS.
* `loadavg`: Coleta métricas de carga do sistema operacional.
* `mdadm`: Coleta métricas de RAID como por exemplo o número de discos ativos.
* `meminfo`: Coleta métricas de memória como por exemplo o uso de memória, o número de buffers, caches, etc.
* `netdev`: Coleta métricas de rede como por exemplo o número de pacotes recebidos e enviados.
* `netstat`: Coleta métricas de rede como por exemplo o número de conexões TCP e UDP.
* `os`: Coleta métricas de sistema operacional.
* `selinux`: Coleta métricas de SELinux como estado e políticas.
* `sockstat`: Coleta métricas de sockets.
* `stat`: Coleta métricas de sistema como uptime, forks, etc.
* `time`: Coleta métricas de tempo como sincronização de relógio.
* `uname`: Coleta métricas de informações.
* `vmstat`: Coleta métricas de memória virtual.

#### Habilitando novo Collector

```bash
sudo su
mkdir /etc/node_exporter
vim /etc/node_exporter/node_exporter_options
chown -R node_exporter:node_exporter /etc/node_exporter
```

[Arquivo node_exporter_options](../conf/node_exporter_options)

### Criar o serviço do SystemD

```bash
sudo vim /etc/systemd/system/node_exporter.service
sudo systemctl daemon-reload
```

[Arquivo node_exporter.service](../conf/node_exporter.service)