# Задание №2 
> Use Case, Sequence

### 1. Составить *Use Case* диаграмму
- 3-5 акторов;
- Все 3 вида связей.

### 2. Составить *Sequence* диаграмму

Мы хотим реализовать процесс заказа **Карты** через **Cайт**.
<br>Процесс выглядит следующим образом:
- Cначала **Клиент** заказывает **Карту** на **Сайте**;
- **Заявка** попадает в **Систему обработки заявок**;
- Далее **Клиент** проверяется в **Системе Скоринга** (можно ли выдавать ему карту);
- Затем **Карта** печатается в **Системе Печать**;
- И доставляется через **Систему Доставка**.

Итого у нас есть 5 систем: **Сайт**, **Система обработки заявок**, **Скоринг**, **Печать**, **Доставка**.
Каждая **Система** для нас является чёрным ящиком. Добавлять или удалять **Системы** нельзя.
Необходимо составить *sequence* диаграмму, которая будет отражать работу **Системы**.

-----

<table width="1000" border="1">
<thead>
  <tr>
    <td rowspan="3"><img width="300px" src="https://github.com/user-attachments/assets/9d985eaa-c3fc-4ab3-b84c-4acbd7c1bbb2"></td>
    <td colspan="2" width="700"><p align="center"><b>Доставка карты Клиенту Курьером</b></p></td>
  </tr>
  <tr>
    <td>Дата</td>
    <td>05.08.2024</td>
  </tr>
  <tr>
    <td>Версия</td>
    <td>1.0</td>
  </tr>
</thead>
</table>

![SVG](https://www.plantuml.com/plantuml/svg/dLHTQnf157sVNt7noLt8jdxeWuW4z5bBeMzzMNHhbfXLrXLQRC5eQIaDJIbzA7rew3_OYajiZEOltFb7FJDJiqRQ5FgmC9wvvznppynuE8pSC1gTz8GO7ll1m0tT4-hvWHUz67ZK3wEZlX0zxrb4KPz2ltiKKSSFlNRazmDHuQ-yuYKdl9RJ2hb3gej7RllOxNgKgLRvEs_aL4xaZ1UyHjqLBskrp5Znv0pu6IToedaDOD_uHltcM4x1CtXBl1AFqSqDkhsjvbAUeYBXQuwXHcEHvOyyDoGqkUGDppdc5ShEdmR4SxBjExJ4jYqbddrIVsY9RCxX2t1MiFGM_1Kf4anejHz0f_AzalYa100cgYoLo5aaidc7l_32185Eh_6zmJVPUe4c97RZujYsx_TMXBU2qhq43exsfWjX3hPEZM8i9yhXlzJA5gAy7NQ1WhbEUw5bz-U5ttj6pbktntod9ARn_qMHIXVCq1VQMm8TC1xmpVxvx4m-IyabFME33WvUrWY7gvTOvDHYD31eNjIt1VbTl93YXIsnk5jGIWjAQPEoQANzMYagzEsYgkCulsz9XVoWtHjrlBsjuj-todjR1QlggCVew67JFJGsU8qQGBtdaHTqX6Zs8pmQ_epqhkIChqtSY4-_o8s-9Xjp3-Iv_23V8TwVs5P7WwpNfaIU_U6yCYhoPax04y4hLiqS5ZepSOZk-4lv1G00)

```plantuml
@startuml

skinparam linetype ortho

left to right direction
:Клиент: as C
Package "<<Сотрудники>>"{
:Курьер: as D
:Оператор: as O
}
Rectangle "<<Система>>" {
(Авторизовался\n в **Системе**) as (UC0)
(1.Получил \n атрибуты **Встречи**) as (UC1) 
(2.Идентифицировал \n **Клиента** в **Системе**) as (UC4)
(3.Изменил статус **Карты** в **Системе**) as (UC6)
}

(1.Подтвердил атрибуты \n **Встречи**) as (UC2)
Package Встреча {
(2.Идентифицировал \n **Клиента**) as (UC3)
(3.Передал/получил \n **Карту**) as (UC5)
}

D --|> UC0
D -- UC1
D -up-|> UC2
C --|> UC2
D -up-|> UC3
C --|> UC3
D -- UC4
D -up-|> UC5
C --|> UC5
D --|> UC6
O --|> UC0
O --|> UC6

(UC0) <... (UC1) : include
(UC0) <... (UC4) : include
(UC0) <... (UC6) : include
(UC3)<.left.(UC5) : include
O .left.> D : extend

Note "Документ\n удостоверяющий\n личность **Клиента**" as N1
UC3 .. N1
N1 .. UC4

@enduml
```
