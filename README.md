## StoreOfSocksApp
 
**Веб-приложение, с помощью которого склад может учитывать и автоматизировать учет товаров на складе интернет-магазина носков**

## **Описание веб-приложения**

Пользователь (работник склада) имеет возможность:

- учитывать приход и отпуск носков;
- узнать общее количество носков определенного цвета и состава в данный момент времени;
- дополнительно иметь возможность парсить (читать и преобразовывать данные) файлы с данными по товару.

Внешний интерфейс приложения представлен в виде REST API.

Товар имеет следующие характеристики: 

- цвет носков (Все цвета заранее перечислены и зафиксированы без возможности добавления) 
- размер носков (Все размеры заранее перечислены и зафиксированы без возможности добавления)
- состав носков (Выражается в % соотношение хлопка в составе от 0 до 100 целыми числами)
- наличие на складе (т.е. нельзя отгрузить носков больше, чем осталось на складе)

# Бэкенд-часть проекта предполагает реализацию следующего функционала:

## **Список URL HTTP-методов**

### **POST /api/socks**

Регистрирует приход товара на склад.

Параметры запроса передаются в теле запроса в виде JSON-объекта со следующими атрибутами:

- color — цвет носков, строка (например, black, red, yellow);
- size — размер носков, числовое значение (например, размер 36 или размер 37,5);
- cottonPart — процентное содержание хлопка в составе носков, целое число от 0 до 100 (например, 30, 18, 42);
- quantity — количество пар носков, целое число больше 0.

Результаты:

- HTTP 200 — удалось добавить приход;
- HTTP 400 — параметры запроса отсутствуют или имеют некорректный формат;
- HTTP 500 — произошла ошибка, не зависящая от вызывающей стороны.

### **PUT /api/socks**

Регистрирует отпуск носков со склада. Здесь параметры и результаты аналогичные, но общее количество носков указанного цвета и состава не увеличивается, а уменьшается. 

Параметры запроса передаются в теле запроса в виде JSON-объекта со следующими атрибутами:

- color — цвет носков, строка;
- size — размер носков, числовое значение;
- cottonPart — процентное содержание хлопка в составе носков;
- quantity — количество пар носков, целое число больше 0.

В данном методе необходимо добавить проверку на доступность остатка товара на складе. 

Результаты: 

- HTTP 200 — удалось произвести отпуск носков со склада;
- HTTP 400 — товара нет на складе в нужном количестве или параметры запроса имеют некорректный формат;
- HTTP 500 — произошла ошибка, не зависящая от вызывающей стороны.

### **GET /api/socks**

Возвращает общее количество носков на складе, соответствующих переданным в параметрах критериям запроса. В данном методе количество носков остается неизменным, так как мы запрашиваем информацию о товарах на складе. 

Параметры запроса передаются в URL:

- color — цвет носков, строка;
- size — размер носков, числовое значение;
- cottonMin — минимальное значение хлопка в товаре;
- cottonMax — максимальное значение хлопка в товаре.

Результаты:

- HTTP 200 — запрос выполнен, результат в теле ответа в виде строкового представления целого числа;
- HTTP 400 — параметры запроса отсутствуют или имеют некорректный формат;
- HTTP 500 — произошла ошибка, не зависящая от вызывающей стороны.

### DELETE **/api/socks**

Регистрирует списание испорченных (бракованных) носков. 

Параметры запроса передаются в теле запроса в виде JSON-объекта со следующими атрибутами:

- color — цвет носков, строка;
- size — размер носков, числовое значение;
- cottonPart — процентное содержание хлопка в составе носков;
- quantity — количество пар носков, целое число больше 0.

Результаты:

- HTTP 200 —  запрос выполнен, товар списан со склада;
- HTTP 400 — параметры запроса отсутствуют или имеют некорректный формат;
- HTTP 500 — произошла ошибка, не зависящая от вызывающей стороны.

## Использован следующий стек технологий: ##

Веб-приложение выполнено в виде RESTful-сервиса\
Java11\
SpringBoot\
Swagger\
Lombok

*Выполнил задание - [Алексей Петкун](https://github.com/AlekseyPetkun "AlekseyPetkun")*

[![Typing SVG](https://readme-typing-svg.herokuapp.com?color=%2336BCF7&lines=thank+you+for+your+attention)](https://git.io/typing-svg)
