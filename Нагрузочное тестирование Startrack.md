---
aliases: [JMeter, jmeter, нагрузочное тестирование]
---
1. Установка и настройка [[Нагрузочное тестирование Startrack|JMeter]]
2. В отдельной ветке пушим нужный для теста код в гитлаб.
3. Создаем МР и дожидаемся прогона тестов. После этого можно будет задеплоить на стейдж
![](https://i.imgur.com/rZouAIp.png)
Ждем, пока деплой пройдет.
4. Параллельно есть смысл отслеживать нагрузку на RabbitMQ. Их [два](https://mimimi.ninja/integration-team/starproxy/-/blob/master/docker-compose.stage.yml).
* `rabbitmq` - сюда старпрокси непосредственно шлет сообщения.
http://51.75.63.221:25672/#/queues
* `admitad_rabbitmq` - сюда перекладываются запросы от `rabbitmq`.
http://51.75.63.221:35672/#/queues

**user**: rabbitmq
**pass**: rabbitmq

В очереди `rabbitmq` почти никогда нет сообщений, потому что они сразу перекладыаются в `admitad_rabbitmq`. Поэтому наблюдать можно только за `admitad_rabbitmq`.
5. [Grafana](https://g.crutches.space/d/W-g6z_7ik/node-exporter-full?orgId=1) - просмотр графиков на стедже.
У нас есть CPU Memory Net Disk:
* **Idle** - процессор ничего не делает.
* **System** - системная нагрузка
* **User** - нагрузка запросами
* **Softirq** - это программные прерывания, обычно соответствуют прерываниям от программных таймеров, переключения контекста, прерываний на ввод/вывод и от системных примитивов. Генерируются ядром и им же обрабатываются.
Когда в него упрется, можно ждать 20-30 минут теста.

6. Имеет смысл нагрузать не менее 30 минут.
Идем в [[JMeter|jmeter]]] и проводим тест.

Интересует стлобец Thraughtoutput = итоговый rps.
7. В `admitad_rabbitmq` можем видеть метрики. После остановки тесты нужно дождаться пока все сообщения дойдут.


Проверяем, сколько съели CPU, памяти. Проверяем минут через 5, что память вернулась (она не течет). При 100% загрузке CPU смотрим на Thraughtoutput.


[Grafana](https://charts.crutches.space/d/dNUbOG3k89vDXQ/starproxy-http-metrics?orgId=1&refresh=15s) - просмотр графиков на бою.

Для теста нужна нода [startrack-stage-qa-ovh-waw1](https://charts.crutches.space/d/dNUbOG3k89vDXQ/starproxy-http-metrics?orgId=1&refresh=15s&var-region=All&var-hostname=startrack-stage-qa-ovh-waw1&var-endpoint=All&var-method=All&var-status=All&var-quantile=0.75)


По окончании тестирования нужно почистить оцереди `admitad_rabbitmq`. Для этого нужно зайти в каждую очередь, кликнов по ее имени
![](https://i.imgur.com/U7vnYWH.png)
и удалить ее
![](https://i.imgur.com/QrvPyB0.png)

Дополнительно можно взять количество успешных сообщений (фильтр по колонке success) и оно должно сходиться с суммарным количеством запросов `pixel_event` и `revised_payment_event_queue` очередей - это гарантирует целостность данных.

