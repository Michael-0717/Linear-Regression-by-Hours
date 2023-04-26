# Линейная регрессия по часам
## Задание
Разделите набор данных на обучающие/проверочные в пропорции 80/20.
Загрузите данные и очистите значения (нулями и средними). Постройте модель линейной регрессии для каждого часа в отдельности, используя температуру воздуха (air_temperature), влажность (dew_temperature), атмосферное давление (sea_level_pressure), скорость ветра (wind_speed) и облачность (cloud_coverage).
Рассчитайте качество построенной модели по проверочным данным. Используйте данные:
http://video.ittensive.com/machine-learning/ashrae/building_metadata.csv.gz
http://video.ittensive.com/machine-learning/ashrae/weather_train.csv.gz
http://video.ittensive.com/machine-learning/ashrae/train.0.0.csv.gz
___
## Решение:
1) Постановка задачи
Разделить набор данных на обучающие/проверочные в пропорции 80/20.
Загрузить данные и очистить значения. 
Построить модель линейной регрессии для каждого часа в отдельности, используя:
- температуру воздуха (air_temperature), 
- влажность (dew_temperature), 
- атмосферное давление (sea_level_pressure), 
- скорость ветра (wind_speed), 
- облачность (cloud_coverage).
Рассчитать качество построенной модели по проверочным данным.
Данные:
•	http://video.ittensive.com/machine-learning/ashrae/building_metadata.csv.gz
•	http://video.ittensive.com/machine-learning/ashrae/weather_train.csv.gz
•	http://video.ittensive.com/machine-learning/ashrae/train.0.0.csv.gz Соревнование: https://www.kaggle.com/c/ashrae-energy-prediction/
© ITtensive, 2020
2) Подключим необходимые библиотеки и загрузим данные.
3) Объединение и фильтрация данных.
- объединяем в таблицу, с помощью параметра how="left" мы указали, что главным является датафрейм слева, название столбца – «building_id».
- добавим отдельную серию «час» из «времени»
- проиндексируем в таблице данных energy_0 по столбцам "timestamp", "site_id"
- проиндексируем в таблице данных weather по столбцам "timestamp", "site_id"
- объединяем в таблицу: слева данные energy_0, справа данные weather
- сбросим индекс по данным  energy_0
- отфильтруем только положительные значения по столбцу meter_reading
- преобразовываем формат времени в столбце timestamp
- атрибут dt.hour возвращает массив данных  timestamp к базовым данным (2,4…) - # добавим отдельную серию «час» из «времени»
- просмотрим первые строки
4) Очистка данных.
- очистим данные: 
для температуры воздуха, влажности, ветра и облачности заменим отсутствующие значения на 0;
для осадков дополнительно занулим отрицательные значения;
для давления и ветра заменим отсутствующие значения средними;
Посмотрим сводную информацию методом info():
мы узнаем, что в таблице 5411 строки (от 704 до 8783), 
17 столбцов - количество ненулевых значений (non-null), тип данных: 
int64 - целые числа (числа размером 8 байт);
object - абстракция Python для данных,
float64 – число с плавающей запятой (числа размером 8 байт).
datetime64 - выполнять операции, связанные с датой.
5) Разделение данных
Данные подготовлены для расчетов
Выделим 20% всех данных на проверку, остальные оставим на обучение
используя модуль train_test_split разделяем данные для машинного обучения.
переменная test_size фактически указывает пропорцию набора тестов – 20%.
6) Линейная регрессия по часам
Модель включает: 
- температуру воздуха (air_temperature), 
- влажность (dew_temperature), 
- атмосферное давление (sea_level_pressure), 
- скорость ветра (wind_speed), 
- облачность (cloud_coverage),
- а так же топливный эквивалент (meter_reading)
Заведем списки параметров модели, добавим в него все коэффициенты для каждого часа.
7) Предсказание и оценка модели.
Модель линейной регрессии для каждого часа в отдельности обладает высоким качеством.

