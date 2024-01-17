# Задание
1. Используя директорию [help](./help) внутри этого домашнего задания, запустите связку prometheus-grafana.
2. Зайдите в веб-интерфейс grafana, используя авторизационные данные, указанные в манифесте docker-compose.
3. Подключите поднятый вами prometheus, как источник данных.
4. Решение домашнего задания — скриншот веб-интерфейса grafana со списком подключенных Datasource.

# Решение
![image](https://github.com/Kul-RB/monitoring/assets/53901269/9d928d95-77c5-4d9e-9bae-0aea2959b990)

# Задание 
Изучите самостоятельно ресурсы:

1. [PromQL tutorial for beginners and humans](https://valyala.medium.com/promql-tutorial-for-beginners-9ab455142085).
1. [Understanding Machine CPU usage](https://www.robustperception.io/understanding-machine-cpu-usage).
1. [Introduction to PromQL, the Prometheus query language](https://grafana.com/blog/2020/02/04/introduction-to-promql-the-prometheus-query-language/).

Создайте Dashboard и в ней создайте Panels:

- утилизация CPU для nodeexporter (в процентах, 100-idle);
- CPULA 1/5/15;
- количество свободной оперативной памяти;
- количество места на файловой системе.

Для решения этого задания приведите promql-запросы для выдачи этих метрик, а также скриншот получившейся Dashboard.

# Решение
1. 100 - (rate(node_cpu_seconds_total{mode="idle", instance="node1s.carfix.local:9100", cpu="0"}[5m]))
![image](https://github.com/Kul-RB/monitoring/assets/53901269/198ed4a4-682c-4d90-a010-922c4e700975)

2. node_load15{instance="node1s.carfix.local:9100",job="node1s"}
   node_load5{instance="node1s.carfix.local:9100",job="node1s"}
   node_load1{instance="node1s.carfix.local:9100",job="node1s"}
![image](https://github.com/Kul-RB/monitoring/assets/53901269/7469ecab-8c26-4e94-b144-6a28530ce8f3)

3. node_memory_MemFree_bytes{instance="node1s.carfix.local:9100", job="node1s"}
![image](https://github.com/Kul-RB/monitoring/assets/53901269/b21b511f-fcf5-4e08-ba33-3944f3353478)

4. node_filesystem_avail_bytes{instance="node1s.carfix.local:9100", job="node1s", mountpoint="/",fstype!="rootfs"}
![image](https://github.com/Kul-RB/monitoring/assets/53901269/3a449b75-d3c9-488f-a647-4637f39a5bd1)

# Задание 
1. Создайте для каждой Dashboard подходящее правило alert — можно обратиться к первой лекции в блоке «Мониторинг».
2. В качестве решения задания приведите скриншот вашей итоговой Dashboard.

