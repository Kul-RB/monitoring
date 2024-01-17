# Задание
Вам необходимо поднять в докере и связать между собой:

- elasticsearch (hot и warm ноды);
- logstash;
- kibana;
- filebeat.

Logstash следует сконфигурировать для приёма по tcp json-сообщений.

Filebeat следует сконфигурировать для отправки логов docker вашей системы в logstash.

В директории [help](./help) находится манифест docker-compose и конфигурации filebeat/logstash для быстрого 
выполнения этого задания.

Результатом выполнения задания должны быть:

- скриншот `docker ps` через 5 минут после старта всех контейнеров (их должно быть 5);
- скриншот интерфейса kibana;
- docker-compose манифест (если вы не использовали директорию help);
- ваши yml-конфигурации для стека (если вы не использовали директорию help).

# Решение
![image](https://github.com/Kul-RB/monitoring/assets/53901269/92c2fa78-a718-4815-8e39-a08bac5ee824)
![image](https://github.com/Kul-RB/monitoring/assets/53901269/e88106e1-99e4-4614-aa06-b3e91e7f867d)


# Задание
Перейдите в меню [создания index-patterns  в kibana](http://localhost:5601/app/management/kibana/indexPatterns/create) и создайте несколько index-patterns из имеющихся.

Перейдите в меню просмотра логов в kibana (Discover) и самостоятельно изучите, как отображаются логи и как производить поиск по логам.

В манифесте директории help также приведенно dummy-приложение, которое генерирует рандомные события в stdout-контейнера.
Эти логи должны порождать индекс logstash-* в elasticsearch. Если этого индекса нет — воспользуйтесь советами и источниками из раздела «Дополнительные ссылки» этого задания.

# Решение

![image](https://github.com/Kul-RB/monitoring/assets/53901269/968c11f0-5e9e-45ff-9d77-d7e767e9014b)
![image](https://github.com/Kul-RB/monitoring/assets/53901269/e4ac7843-9979-4aef-b549-8fbb87edc066)
![image](https://github.com/Kul-RB/monitoring/assets/53901269/c67e4c59-dcbd-4c32-8c2b-878efa2c2f2f)

