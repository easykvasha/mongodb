# mongodb
Описание работы с Mongodb

# Введение
В данном отчете я расскажу о проделанной работе с MongoDB

# Установка
Подробности расписывать не буду, тк есть множество видео в YouTube с тем, как это делается. Но основные моменты опишу:

1. Тк я пользуюсь Windows, то скачивал я с официального сайта https://www.mongodb.com/ версию MongoDB Community
2. После загрузки была произведена установка без каких-либо проблем. Но нужно было внести путь к папке в специальный реестр в системе Windows.
3. Не мало важным была установка MongoDB Compass, ведь через него идет основное взаимодействие.

# Запуск
После запуска программы передо мной предстал следующий интерфейс:
![](https://github.com/easykvasha/mongodb/blob/main/%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D0%BA.png)

Тут наверно нет смысла писать про каждое слово на иллюстрации, поэтому перейдем сразу к делу. Я решил выбрать следующую базу данных для пробного использования https://www.reddit.com/r/datasets/comments/1uyd0t/200000_jeopardy_questions_in_a_json_file/ 
Это база данных с различными параметрами вопросов c телепередачи Jeopardy!

# Создание базы и каталога 
Насколько я понял, создание возможно через терминал или же через кнопки в приложении. Файл, который мы загружаем в качестве данных, был в формате JSON.
### Создадим новую базу:
![](https://github.com/easykvasha/mongodb/blob/main/%D1%81%D0%BE%D0%B7%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5%20%D0%B4%D0%B1.png)
### И новый каталог:
![](https://github.com/easykvasha/mongodb/blob/main/%D1%81%D0%BE%D0%B7%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5%20%D0%BA%D0%BE%D0%BB%D0%BB%D0%B5%D0%BA%D1%86%D0%B8%D0%B8.png)

# Запросы на выборки
### 1. Вывести топ-3 самых поздних вопроса в категории NEW YEAR\'S DAY, которые задавались с 2000 по 2001 год. ![](https://github.com/easykvasha/mongodb/blob/main/newyear.png)
### 2. Вывести все неповторяющиеся суммы денег, которые появлялись в раунде Jeopardy! или Double Jeopardy! в категории HISTORY c номером игры 4680 или 2047. ![](https://github.com/easykvasha/mongodb/blob/main/money.png)
### 3. Вывести первые 10 ответов, начиноющихся с буквы а, которые были в раунде Final Jeopardy! или Double Jeopardy!, и в вопросах которых встречалось слово the. ![](https://github.com/easykvasha/mongodb/blob/main/answer.png)

# Запросы на обновление данных
1. Изменим категорию с Истории на Астрономию. ![](https://github.com/easykvasha/mongodb/blob/main/change1.png)
2. Изменим у всех строк с категорией История, которые стоили 250, цену на 275 
 * привожу первые 3 строки ![](https://github.com/easykvasha/mongodb/blob/main/change2.png)
* Теперь выполныем запрос ![](https://github.com/easykvasha/mongodb/blob/main/change22.png)
* И получаем ![](https://github.com/easykvasha/mongodb/blob/main/change222.png)

# Создание индексов и сравнение производительности
## 1. Индекс одного поля
* до индексов ![](https://github.com/easykvasha/mongodb/blob/main/index.png)
* создаем индекс 
![](https://github.com/easykvasha/mongodb/blob/main/index1.png)
* после использования с индексами ![](https://github.com/easykvasha/mongodb/blob/main/index2.png)
### Вывод:
Значительно улучшена производительность запросов благодаря простой настройке индексации.

1. Мы рассматриваем только один документ и возвращаем только один документ. Это соотношение (возвращенные документы, поделенные на изученные документы) 1 идеально.
2. Мы используем лучший подход, который заключается в сканировании индекса вместо сканирования всей коллекции. Это приводит к лучшей производительности.
## 2. Составные полевые индексы
* до индексов 
![](https://github.com/easykvasha/mongodb/blob/main/sost.png)
* создаем индекс
 ![](https://github.com/easykvasha/mongodb/blob/main/sost1.png)
* после использования с индексами ![](https://github.com/easykvasha/mongodb/blob/main/sost2.png)
 ![](https://github.com/easykvasha/mongodb/blob/main/sost3.png)
 
### Важное замечание
Составной индекс учитывает порядок полей при создании индекса, поэтому в запросе надо учитывать порядок.
# Итог
## Плюсы MongoDB:

* Динамическая схема: данная СУБД позволяет гибко работать со схемой данных без необходимости изменять сами данные.
* Масштабируемость: MongoDB горизонтально масштабируема, что позволяет легко уменьшить нагрузку на сервера при больших объёмах данных.
* Удобство в управлении: СУБД не нуждается в отдельном администраторе базы данных. Благодаря достаточному удобству в использовании, ей легко могут пользоваться как разработчики, так и системные администраторы.
* Скорость: Высокая производительность при выполнении простых запросов.
* Гибкость: В MongoDB можно без вреда для существующих данных, их структуры и производительности СУБД добавлять поля или колонки.

## Минусы MongoDB

* Он не построен для транзакционных данных.
* Там нет функции или хранимой процедуры, где логика может быть связана.
* Все NoSQL, большинство решений не являются ACID-совместимыми.
* MongoDB не обеспечивает долговечность как функцию инструмента, он позволяет настраивать конфигурацию набора реплик, но это означает, что нужно жертвовать достаточной производительностью.

