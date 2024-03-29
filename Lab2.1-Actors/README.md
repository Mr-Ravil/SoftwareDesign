## Лабораторная 2.1. Actors

Цель: получить практический опыт применения акторов.

Необходимо реализовать поисковой агрегатор, который по запросу пользователя собирает
top 5 ответов через API известных поисковиков и выдает их пользователю. Например, делает
запрос в Google, Яндекс, Bing и возвращает 15 ответов (должно быть ясно, какой ответ от какой
поисковой системы). Реальное API можно не использовать, а реализовать StubServer, который
будет отдавать результаты в удобном формате (json, xml, protobuf и тд).

Архитектура приложения:
+ На каждый запрос создается master-actor, который будет собирать результаты от
поисковиков
+ Master-actor для каждого поисковика создает child-actor, которому посылает исходный
"поисковый запрос"
+ Master-actor устанавливает себе receive timeout, сколько времени он будет ждать
ответы от child-actors
+ Child-actor делает запрос в соответствующий поисковый сервис и отправляет его
результат в master-actor
+ Master-actor при получении каждого ответа сохраняет их у себя, если получил все 3
ответа или прошло время таймаута, то отправляет собранный агрегированный
результат на дальнейшую обработку
+ Master-actor должен умирать после того, как вернул агрегированный результат

Указания:
+ В stub-server необходимо реализовать возможность залипания, чтобы можно было
проверить сценарий, когда master-actor не дождался ответов от всех поисковиков
+ Примеры из лекции:
https://github.com/akirakozov/software-design/tree/master/java/akka

Баллы:
+ 20 баллов
+ необходимо добавить тесты (без тестов -5 баллов)
