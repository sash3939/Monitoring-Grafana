# Домашнее задание к занятию 14 «Средство визуализации Grafana»

## Задание повышенной сложности

**При решении задания 1** не используйте директорию [help](./help) для сборки проекта. Самостоятельно разверните grafana, где в роли источника данных будет выступать prometheus, а сборщиком данных будет node-exporter:

- grafana;
- prometheus-server;
- prometheus node-exporter.

За дополнительными материалами можете обратиться в официальную документацию grafana и prometheus.

В решении к домашнему заданию также приведите все конфигурации, скрипты, манифесты, которые вы 
использовали в процессе решения задания.

**При решении задания 3** вы должны самостоятельно завести удобный для вас канал нотификации, например, Telegram или email, и отправить туда тестовые события.

В решении приведите скриншоты тестовых событий из каналов нотификаций.

## Обязательные задания

### Задание 1

1. Используя директорию [help](./help) внутри этого домашнего задания, запустите связку prometheus-grafana.
2. Зайдите в веб-интерфейс grafana, используя авторизационные данные, указанные в манифесте docker-compose.
3. Подключите поднятый вами prometheus, как источник данных.
4. Решение домашнего задания — скриншот веб-интерфейса grafana со списком подключенных Datasource.

<img width="736" alt="Datasource Prometheus" src="https://github.com/user-attachments/assets/75135a1b-6da5-4b7b-9958-9950e65cff2a">

<img width="624" alt="Datasource Prometheus1" src="https://github.com/user-attachments/assets/6ea2895e-10f3-4618-8e15-f15b1a670f64">

## Задание 2

Изучите самостоятельно ресурсы:

1. [PromQL tutorial for beginners and humans](https://valyala.medium.com/promql-tutorial-for-beginners-9ab455142085).
2. [Understanding Machine CPU usage](https://www.robustperception.io/understanding-machine-cpu-usage).
3. [Introduction to PromQL, the Prometheus query language](https://grafana.com/blog/2020/02/04/introduction-to-promql-the-prometheus-query-language/).

Создайте Dashboard и в ней создайте Panels:

- утилизация CPU для nodeexporter (в процентах, 100-idle);

**100 - avg(irate(node_cpu_seconds_total{mode="idle"}[5m])) * 100**

<img width="905" alt="CPU Utilization" src="https://github.com/user-attachments/assets/b1273cbf-dccd-4cf4-8037-07597a9d4cd0">

- CPULA 1/5/15;

**avg by (instance)(rate(node_load1{}[1m]))
avg by (instance)(rate(node_load5{}[1m]))
avg by (instance)(rate(node_load15{}[1m]))**

<img width="602" alt="CPULA" src="https://github.com/user-attachments/assets/d1dca878-5f73-478e-9abb-d9f2301a6ee2">

- количество свободной оперативной памяти;

**node_memory_MemFree_bytes{instance="nodeexporter:9100",job="nodeexporter"}**

<img width="635" alt="FreeRAM" src="https://github.com/user-attachments/assets/b7ba1481-045c-47f0-a81d-0002d9fae7e9">


- количество места на файловой системе.

**node_filesystem_avail_bytes{mountpoint="/"}**

<img width="617" alt="FS" src="https://github.com/user-attachments/assets/50e3c66c-af9e-4232-b51a-e292ad4b4227">

Для решения этого задания приведите promql-запросы для выдачи этих метрик, а также скриншот получившейся Dashboard.

<img width="605" alt="All" src="https://github.com/user-attachments/assets/e2553328-244a-48e7-9fcc-773e9d4ef974">

## Задание 3

1. Создайте для каждой Dashboard подходящее правило alert — можно обратиться к первой лекции в блоке «Мониторинг».
2. В качестве решения задания приведите скриншот вашей итоговой Dashboard.

<img width="936" alt="Alert_CPU_Util" src="https://github.com/user-attachments/assets/6d282c5c-2296-44c9-b76a-ad8ee49f402f">

<img width="926" alt="Alert_FS" src="https://github.com/user-attachments/assets/3e5e846c-4e99-4cf6-9611-0ba331350d45">

<img width="932" alt="Alert_RAM" src="https://github.com/user-attachments/assets/5b8d8b2e-c215-4e4b-8eb1-2bc2fe90a6a1">

<img width="919" alt="Alert_CPULA" src="https://github.com/user-attachments/assets/bb65b92a-074c-4eb3-a1af-8c2285cb81b7">

<img width="902" alt="All Alerts" src="https://github.com/user-attachments/assets/b238b47b-eb70-4ec9-b356-4981128487dd">

## Задание 4

1. Сохраните ваш Dashboard.Для этого перейдите в настройки Dashboard, выберите в боковом меню «JSON MODEL». Далее скопируйте отображаемое json-содержимое в отдельный файл и сохраните его.
2. В качестве решения задания приведите листинг этого файла.

---

