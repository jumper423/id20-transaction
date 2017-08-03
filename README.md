##Описание
В компании работают водители, которые совершают поездки на корпоративных автомобилях. В течение рабочего времени, они совершают расходы, приобретая услуги (заправка топливом, мойка, шиномонтаж) на различных автозаправках, которые оплачивают топливными картами компании.
В некоторых случаях происходят возвраты средств по приобретенным услугам. Например, водитель попросил оператора заправочной станции заправить автомобиль 50 литрами топлива. При этом оператор совершает списание по топливной карте ДО начала заправки. По окончании заправки выясняется, что в топливный бак вместилось только 48 литров. В этом случае, оператор оформляет возврат средств (2 литра, которые не вместились) на топливную карту.
Данные о приобретенных услугах по топливным картам передаются (в реальном времени) и хранятся в БД.
Таким образом таблица с данным о расходах по топливным картам содержит данные по списанию и возвратам.
####Задание 1. Должно выполняться с использованием MySQL (и при желании с PHP)
Преобразовать данные таблицы таким образом, чтобы в ней содержались ТОЛЬКО транзакции-расходы. То есть, все транзакции-возвраты должны быть учтены в предшествующих им транзакциях-расходах.
Пример. Дамп данных содержит две следующие транзакции.
ID	Номер карты	Дата/время	Объем	Услуга	ID заправочной станции
31769	257473011	2015-10-18 11:10:36	-68	ДТ	41
31768	257473011	2015-10-18 11:21:15	2,44	ДТ	41

Где транзакция ID 31769 – расход, а ID 31768 возврат по этой транзакции.
В результате преобразования, транзакция ID 31769 должна иметь объем 65,56, а транзакция ID 31768 должна быть удалена.
Цель выполнения задания
Исполнитель должен продемонстрировать высокий уровень знаний языка SQL.

####Задание 2. Должно выполняться на Yii2 (PHP и MySQL)
Создать страницу со списком транзакций по топливным картам. Слева должна располагаться панель, где будет отображены информация о количестве транзакций по месяцам и по годам.
Пример:
2010 (27)
  сентябрь (1)
  июль (4)
  июнь (7)
  март (12)
  февраль (3)
2009 (1)
  июнь (1)

Создать фильтры по номеру карты, по году, по месяцу

Цель выполнения задания
Исполнитель должен продемонстрировать понимание построения запросов к БД и умение работать с платформой Yii2.
