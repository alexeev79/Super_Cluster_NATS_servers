# Super_Cluster_NATS_servers
2 clusters of 2 and 3 servers connected in one supercluster.

Добавлена роль для генерации файлов конфигурации серверов с настройкой объединения в суперкластер.
-
Для использования роли в файле `config_nats1.yml` в разделе `vars` по аналогии опишите структуру ваших кластеров. В `SCluster` перечислите желаемые имена кластеров, далее для каждого кластера определите принадлежность серверов, перечислив их имена. В master определите **только один** сервер который будет организовывать соединения внутри своего кластера. В разделе `loop` пеерчислите имена тех серверов для которых необходимо сформировать файл конфигурации. **Обязательно проверьте, чтобы совпадали имена серверов в файле `docker-compose.yaml` и `config_nats1.yml`.**
```
  vars: 
#             Specify the structure for the supercluster.
    SCluster: 
        - cluster1
        - cluster2
    cluster1:
        - nod1a
        - nod1b
    cluster2:
        - nod2a
        - nod2b
        - nod2c
    master:
#             Specify the structure for the masters servers.
        - nod1a
        - nod2a
...
    loop: 
#           Specify the names of the servers to generate the configuration for.
      - nod1a
      - nod1b
      - nod2a
      - nod2b
      - nod2c

```

Также выложен отдельный плейбук `config_nats1.yml`, тогда действуйте по инструкции ниже.

Инструкция по установке.
-
1. Создаем директорию `/home/nats/` копируем `docker-compose.yaml` и директорию `/clust/`.

2. Запускаем сервера из директории `/home/nats/sudo docker-compose -f docker-compose.yaml up`

Видим, что все сервера имеют подключения `rid` и `gid` с состоянием `registered`.


В папке nats2 выложен похожий конфиг кластера.
-
В этой версии, каждый кластер находится в отдельных подсетях `(nats, nats2)`, сервера по бродкасту друг друга не видят. С использованием третьей сети (shar) они организуют межкластерные соединения.

Для запуска:
1. Создаем директорию `/home/nats2/` копируем туда все файлы.

2. Запускаем сервера из директорию `/home/nats2/sudo docker-compose -f docker-compose.yaml up`.

Видим что все сервера имеют подключени `rid` и `gid` с состоянием `registered`.
Для этой версии также можно использовать автогенерацию конфига для серверов.
