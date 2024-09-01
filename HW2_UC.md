# Задание №2 
> Use Case, Sequence

<details>
  
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
</details>
  
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

<details><summary> см. код plantUML </summary>
  
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
</details>


<table width="1000" border="1">
<thead>
  <tr>
    <td rowspan="3"><img width="300px" src="https://github.com/user-attachments/assets/9d985eaa-c3fc-4ab3-b84c-4acbd7c1bbb2"></td>
    <td colspan="2" width="700"><p align="center"><b>Заказ Карты через Сайт</b></p></td>
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

![SVG](https://www.plantuml.com/plantuml/svg/dLVHRXj557sVhxZoIq35KF4ODQYbBxnHYJxouYQB5CdObUsMeifIOhUbA1Kk4HAe0YeaFc2zjPlDEgb_uSuVSOucszaPZKcWKhN9xDnpppttp9tDpU6eCnWz-BPhpAtTKNyW-afNMkfIp-t4c7lzHxAbFskkvrfjcS_x3tfxdS7tqjA_i7Pg9otf3EMxx9wOEy3Ptzs_t-cD-5fBUsWdm3dJNBxkwJkTsmF4pFKTbYijkVYhvdQc1LvM19B-O2yR30Ce85K8ET0I5DwOhBSd85KpEqFeMrtQYG3-o4xi2m7SELQUeu2PdKd8PClSxdUxsUvelzyRYhx6nXyqPrpuuXUaP50Ej4fpdtQh-SyqnP9hrqouqFwCoc1TjaMFxLDmNGZ8vMAVOSiA_mixjJy9Kr4Sl2ljCpirPf1z8_s7sO00Y8xanDubLT4pPjA5vW0izTHmjyjgJF_-AAHpeztc6t5iZhHmVDP40yQAKd8haLYmCJixmXPH0JsXCt9x0AP7ihEJAjL3pzan1uqSTgeLkDC6BO_dP6yPq-cEn4ZM7MOIO0A5Yb1-4QaL2VPyLElp4ZfEt1gKUeBtbHF5pZxHbrfWsNdef5wkC_u1XWKedmR0p0W1-TYeuTzAIFP32oScVwmjxHp-WJs43Bg4ReVOWTxhohu0r142Is68djU_ViXq49wFJUfIlZMGLhGtZT_82ECmkdQ1EqpEVdU-_EgkF6wGoyV6lVSxiOsXhD6lV7hzkkYV-cgpdV3ObfOU0_ev1JZnEPm3Ib9b_rka5nkdRJoHwB0JEatTT71G7tP6MJmUOe0OqX-iQESsgvox0uNps9WYMcALlGmF8HSlJnVDYy3hZOhaOYYkw15IS9wFu1_vLbrqzTRTsr_8O_XzfJas4AK-NEE6XRt0WVPis-yupKmfzIZLC-5vGEUcB5RBUgYYOZy2fgqcRll2k1jAquMR_XiBytNvedJDLCnAboCfU5Rr01gdGCZ2c_vgvH-xiYAAx-lKF4LaJ3Ei6OGT1GytmaiQeo6TLes1cLJBpzZVqB0tR1vdaQv8WYnJ4pTzkRmEoBpLXOE826aUZOQKXTPfA3iRCvZilSHUsEPDUkd4uPaF0cA0UkEDTh2EGCyuy1YhhCSY-JBP_t62b-j7ZPtmCRlkBZSgu_gTSkaY-7Oeqxrdt-ElZAltk_WF7nEfoNrnRTed_WgBMDESIGBRxs-xnkrbduRE2iOJcqV1TCvBEg5Gv2p2nD84dheSpyiT0oN1KxjYX_nBinBXxKYxHDPBZsvSLY9Df7TybcDTaaJZpu1W12_TI6HK-6cZXR1y-B3KeYduJHW7Vqxy0m00)

<details><summary> см. код plantUML </summary>

```plantuml
@startuml

Actor Клиент

box 'Банк'
Boundary "Сайт" as web 
Participant "Система \nобработки \nЗаявок" as orders
Participant Скоринг
end box

box 'может быть внешняя Система'
Collections Печать
Collections Доставка
end box

'''''''''''''
Клиент ++

Клиент -> web ++ : Вход на целевую страницу

ref over web : Система рекомендаций
web -> web

opt
Клиент <-- web  : Вывод предложений
end

== Заказ Карты ==

Клиент -> web  : Выбор продукта \n"Заказать"

alt 
 else Клиент банка
   ref over Клиент, web : Аутентификация/Авторизация
 else Новый Клиент
   opt
   Клиент <-- web  : Форма ввода Заявки \n(с персональными данными)
   end
   Клиент -> web  : Заполняет Заявку
end

web -> orders ++ : POST {Заявка}
orders -> orders : 
web <-- orders : 200 ОК
opt
Клиент <-- web -- : "Ваша заявка принята"
end

Клиент --

orders -> Скоринг -- : POST {Заявка}

activate Скоринг
Скоринг -> Скоринг
ref over Скоринг : Обмен с внешними \nСистемами
Скоринг -> Скоринг

'''''''''''''

alt 
 else Заявка отклонена
   Скоринг x-> orders  ++ : PATCH {флаг отказа}
   opt
   orders -> Клиент : "Мы не можем выпустить вам Карту"
   orders --
   end 
 else Заявка одобрена
   Скоринг -> orders  : PATCH {параметры карты}
   Скоринг --
   orders ++
   opt
   orders -> Клиент : "Вам одобрена Карта {параметры} \nподтвердите выпуск Карты"
   orders --
   end
end

== Изготовление Карты ==

Клиент -> web ++ : Подтверждение выпуска
web -> orders  : PATCH {флаг подтверждения}
web --
orders ++
orders -> Печать ++ : POST {Заявка}
orders --

Печать -> Печать 
orders <- Печать -- : PATCH {Заявка выполнена}
orders ++
   opt
   orders -> Клиент : "Вам выпущена Карта. \nВыберите параметры доставки"
   orders --
   end

== Доставка Карты ==

Клиент -> web ++ : вход на целевую страницу
opt
Клиент <- web : форма доставки
end
Клиент -> web : ввод данных
web -> orders ++ : PATCH {атрибуты доставки}
web --
orders -> Доставка ++ : POST {атрибуты доставки}
orders --
Доставка -> Доставка 
Доставка -> Клиент : Доставка Карты
Доставка --
Клиент --> Доставка ++ : Подтверждение доставки
Доставка -> orders ++ : PATCH {флаг доставки}
Доставка --
orders -> orders : PATCH {перенос Заявки в архив}
orders --
@enduml

```
</details>

