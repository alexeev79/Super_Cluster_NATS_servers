# Super_Cluster_NATS_servers
2 clusters of 2 and 3 servers connected in one super cluster

Инструкция по установке.
1. Создаем директорию /home/nats/ копируем docker-compose.yaml и директорию clust.

2. Запускаем сервера из директорию /home/nats/sudo docker-compose -f docker-compose.yaml up

Видим что все сервера имеют подключения rid и gid с состоянием registered


Для запуска второго кластера nats2 
1. Создаем директорию /home/nats2/ копируем туда все файлы.

2. Запускаем сервера из директорию /home/nats2/sudo docker-compose -f docker-compose.yaml up

Видим что все сервера имеют подключени rid и gid с состоянием registered

В этой версии, каждый кластер находится в отдельной подсети (nats, nats2), сервера по бродкасту друг друга не видят. С использованием третьей сети (shar) они организуют межкластерные соединения. 
