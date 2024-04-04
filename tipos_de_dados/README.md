# Tipos de Dados do Prometheus

### Gauge - Medidor

É um tipo de dado utilizado para métricas que podem ter seus valores alterados tanto para mais quanto para menos, exemplo: ```utilização de memória```, ```utilização de CPU``` e ```temperatura de sua cidade```.

```bash
process_virtual_memory_bytes{instance="localhost:9090", job="prometheus"}
	1626406912
```

### Counter - Contador

É um tipo de dado utilizado para métricas que tem seu valor incrementado ao longo do tempo, exemplo ```Quantidade de visitantes de um site``` e ```Quantidade de falhas do aplicação no fim de semana```

```bash
process_cpu_seconds_total{instance="localhost:9090", job="prometheus"}
	4.82
```

### Histogram - Histograma

É um tipo de dado utilizado para métricas que tem o seu valor através de espaços pré-definidos, por exemplo: ```quantidade de requisições que minha aplicação respondeu de 0s até 0.5s``` ou ```quantidade de requisições que tiveram respostas entre 1,0s e 1,5s```

```bash
prometheus_http_response_size_bytes_bucket{handler="/-/ready", instance="localhost:9090", job="prometheus", le="100"}
	5
```

### Sumary - Resumo

O summary tem uma lógica muito parecida com a do histogram, a diferença que os buckets aqui são chamados de quantiles 
e são valores que variam entre 0 e 1. Outra diferença é que esses valores não são de tempo e sim de Percentil.

```bash
prometheus_sd_kuma_fetch_duration_seconds{instance="localhost:9090", job="prometheus", quantile="0.5"}
	1523
```