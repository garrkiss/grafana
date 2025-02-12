# Домашнее задание к занятию "`Средство визуализации Grafana`" - `Бакулев Евгений`

# Задание 1

![Скриншот](https://github.com/garrkiss/systemmonitoring/blob/main/img/%D0%B3%D1%80%D0%B0%D1%84%D0%B8%D0%BA.png)

# Задание 2

![Скриншот](https://github.com/garrkiss/systemmonitoring/blob/main/img/%D0%B3%D1%80%D0%B0%D1%84%D0%B8%D0%BA.png)


```
100 - avg(irate(node_cpu_seconds_total{job="nodeexporter", mode="idle"}[1m])) * 100
```

```
node_load1
node_load5
node_load15
```

```
node_load1
node_load5
node_load15
```

```
node_memory_MemFree_bytes
```

```
node_filesystem_avail_bytes
```

# Задание 3

![Скриншот](https://github.com/garrkiss/systemmonitoring/blob/main/img/%D0%B3%D1%80%D0%B0%D1%84%D0%B8%D0%BA.png)

# Задание 4

[JSON](https://github.com/garrkiss/systemmonitoring/blob/main/img/%D0%B3%D1%80%D0%B0%D1%84%D0%B8%D0%BA.png)

9. Изучите список [telegraf inputs](https://github.com/influxdata/telegraf/tree/master/plugins/inputs). 
Добавьте в конфигурацию telegraf следующий плагин - [docker](https://github.com/influxdata/telegraf/tree/master/plugins/inputs/docker):
```
[[inputs.docker]]
  endpoint = "unix:///var/run/docker.sock"
```

Дополнительно вам может потребоваться донастройка контейнера telegraf в `docker-compose.yml` дополнительного volume и 
режима privileged:
```
  telegraf:
    image: telegraf:1.4.0
    privileged: true
    volumes:
      - ./etc/telegraf.conf:/etc/telegraf/telegraf.conf:Z
      - /var/run/docker.sock:/var/run/docker.sock:Z
    links:
      - influxdb
    ports:
      - "8092:8092/udp"
      - "8094:8094"
      - "8125:8125/udp"
```

После настройке перезапустите telegraf, обновите веб интерфейс и приведите скриншотом список `measurments` в 
веб-интерфейсе базы telegraf.autogen . Там должны появиться метрики, связанные с docker.

Факультативно можете изучить какие метрики собирает telegraf после выполнения данного задания.

Ответ
![Скриншот](https://github.com/garrkiss/systemmonitoring/blob/main/img/image.png)