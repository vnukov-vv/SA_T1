# Задание №7
> Постановка задачи на разработку

Взять любой спроектированный метод из ДЗ №3 (не GET, не DELETE)
Описать бизнес – задачу на разработку с проектированием нового метода API (по шаблону)

<sup>*</sup> *вставить диаграмму последовательности и SQL-скрипт*

-----
<details><summary> <i> см. выбранный метод в OpenAPI (Swagger) (развернуть)</i> </summary>

```swagger
openapi: 3.0.0
info:
  title: Bank API
  description: метод API для открытия банковского счета клиенту
  version: 1.0.0
  contact:
    name: Bank API Support
    url: https://www.bank.com/support
    email: support@bank.com
servers:
  - url: https://webinarOpenSchool.org/api/v1
tags:
  - name: Счета

# Методы

## Счета
paths:  

  /accounts:
     post:
      deprecated: false
      tags:
        - Счета
      summary: Создать банковский счет
      description: Открытие в АБС Банка счета Клиенту (юридическому, физическому лицу или индивидуальному предпринимателю), заведенному в Систему.
      requestBody:
        content:
          application/json:
            schema:
              type: object
              properties:
                clientId:
                  type: string
                  description: Уникальный идентификатор клиента
                  example: "0001010"
      # Клиента не расписываем т.к. для юрлица и физлица разные атрибуты, остальные параметры транзитивно связаны, поэтому достаточно указать клиента, балансовый счет второго порядка и валюту.
                bals:
                  type: string
                  description: Балансовый счет
                  example: "40817"
                currency:
                  type: string
                  description: Балансовый счет
                  example: "RUB"
                accountName:
                  type: string
                  description: Наименование счета
                  example: "не заполнено"
      responses:
        '201':
          description: Создано
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Account'
        '400':
          description: Некорректный запрос
        '401':
          description: Не авторизован
        '403':
          description: Доступ запрещен
        '422':
          description: Проверьте введенные данные
        '500':
          description: Сервер недоступен
          
# Схемы

components:
  schemas:
    Account:
      type: object
      description: Данные счета
      properties:
        accountId:
          type: string
          description: Уникальный идентификатор счета
          example: "00000001234"
        accountName:
        # потому что счета могут быть внутрибанковскими (доходы, расходы и т.д.)
          type: string
          description: Наименование счета
          example: "не заполнено"
        clientId:
          type: string
          description: Уникальный идентификатор клиента
          example: "0001010"
        clientName:
          type: string
          description: Уникальный идентификатор клиента
          example: "Иванов Петр Сидорович"
          # Прочие атрибуты Клиента не расписываем
          # т.к. для юрлица и физлица они разные
        bals:
          type: string
          description: Балансовый счет
          example: "40817"
        currency:
          type: string
          description: Балансовый счет
          example: "RUB"
        accountNumber:
          type: string
          description: Номер счета
          example: "40817810300000000003"
        accountType:
          type: string
          description: Тип счета
          example: "П"
          enum:
           - А
           - П
        status:
          type: string
          description: Статус счета 
          example: "ACTIVE"
          enum:
            - ACTIVE
            - CLOSED
            - RESERVED
            - DELETED
        balance:
          type: number
          format: money
          description: Текущий баланс счета
          example: 0.01
        timeStamp:
          description: Дата модификации
          type: string
          format: date-time
      required:
        - clientId
        - bals
        - currency
```
</details>

<table width="1000" border="1">
<thead>
  <tr>
    <td rowspan="3"><img width="300px" src="https://github.com/user-attachments/assets/9d985eaa-c3fc-4ab3-b84c-4acbd7c1bbb2"></td>
    <td colspan="2" width="700"><p align="center"><b> API. Открытие счета в АБС Банка </b></p></td>
  </tr>
  <tr>
    <td>Дата</td>
    <td>25.08.2024</td>
  </tr>
  <tr>
    <td>Версия</td>
    <td>1.0</td>
  </tr>
</thead>
</table>

<details><summary> <i> см. Шаблон (развернуть)</i> </summary>

# Я как клиент банка хочу увидеть информацию о счете

## История версий
|Задача|Тип изменения|Цвет изменения|Дата|Автор|
|-|-|-|-|-|
|Ссылка на задачу|Создано|-|01.08.2024|Герасимова Е|
|Ссылка на задачу|Изменено (указать раздел и пункт)|синий|10.08.2024|Герасимова Е|

## Бизнес-анализ
[Ссылка на бизнес-анализ](#)

## Назначение и цель
Отображение клиенту информации по запрашиваемому счету

## Предварительные действия
- Реализована модель данных в СУБД
![image](https://github.com/user-attachments/assets/493c53f7-d036-409a-a5f5-ab32c9227022)


- Пользователь прошел аутентификацию и авторизацию

## Ограничения по ролям
- Доступ к интерфейсу возможен для авторизованного клиента с ролью `CLIENT_ALL`

## Макеты
[Ссылка на Figma/Pixco/draw.io](#)

## Основной сценарий (успешный сценарий)

1. Пользователь переходит на страницу `https://....` в свой личный кабинет.
2. Front делает запрос на Back `GET /accounts` ([ссылка на API](#)).
   - Если Back вернул ошибки 4xx, 5xx см. альтернативный сценарий 1.
3. Front отображает список счетов в соответствии с п. [Макеты](#макеты).
4. Пользователь выбирает любой из счетов.
5. Front делает запрос на Back `GET /accounts/{accountId}` ([ссылка на API](#)).
   - Если Back вернул ошибки 4xx, 5xx см. альтернативный сценарий 1.
6. Front отображает детальную информацию по счету в соответствии с п. [Макеты](#макеты).

## Альтернативный сценарий
1. Front отображает ошибку от Back.

## Требования к интерфейсу

|Название<br>атрибута|Тип|Длина|Редактируемость|Маска<br>ввода/отображения|Обязательность|Сортировка|Значение<br>по умолчанию| Источник<br>данных|Примечания|
|-|-|-|-|-|-|-|-|-|-|
|Номер счета|Label|20|-|-|+|-|-|Back|Пример: 40781000208102500000|
|Текущий баланс счета|Label|15,2|-|-|+|-|0.00 Р|Back|-|
|Статус счета|Label|20|-|-|+|-|-|Back|<font color="green">ACTIVE</font> - Активен<br><font color="grey">CLOSED</font> - Закрыт<br><font color="orange">RESERVED</font> - Зарезервирован|

## Результат

- Клиент в ЛК видит информацию о конкретном счете.

---

# `GET /accounts/{accountId}` Получить информацию о банковском счете

## История версий
|Задача|Тип изменения|Цвет изменения|Дата|Автор|
|-|-|-|-|-|
|Ссылка на задачу|Создано|-|10.06.2024|Герасимова Е|

## Сервис 
**Микросервис:** account-number

### Алгоритм вызова
- Sequence UML (вставить картинку)

Акторы:
- Пользователь
- Фронт
- Бек
- БД
- + Альтернативные сценарии

### Свойства вызова

|Свойство|Описание|
|-|-|
|Тип взаимодействия|REST/Kafka/Артемис MQ/gRPC/GraphQL|
|Формат запроса/ответа|JSON/XML|
|Тип вызова| Синхронный/Асинхронный|
|Протокол взаимодействия|HTTPS/MTLS|
|Способ аутентификации|Bearer Token/ API key/ JWT|

### Формат запроса

|Параметр|Тип|Длина|Расположение<br>(path/query)|Обязательность|Описание|
|-|-|-|-|-|-|
|accountId|string|-|path|+|Уникальный идентификатор счета|

#### Пример
*GET /accounts/40781000287777000002*

### Тело запроса
|Параметр|Тип|Длина|Расположение (body)|Обязательность|Описание|Место для сохранения|
|-|-|-|-|-|-|-|
|-|-|-|-|-|-|Таблица.поле|

#### Пример

### Формат ответа

|Параметр|Тип|Длина|Обязательность|Описание|Источник данных|Отображение на фронте|
|-|-|-|-|-|-|-|
|*accountId*|integer|20|+|Уникальный идентификатор счета|account_info.id|-|
|*accountNumber*|string|20|+|Номер счета|account_info.number|Номер счета|
|*balance*|number($double)|15,2|+|Текущий баланс счета|account_info.balance|Баланс счета|
|*status*|string|20|+|Статус счета<br>Enum:[ACTIVE, CLOSED, RESERVED]|account_info.status|Статус|

#### Пример

```json
{
  "accountId": 70203333,
  "accountNumber": "40781000208102500000",
  "balance": 471230.77,
  "status": "ACTIVE"
}
```
## Коды ответов

|Код|Название|Описание|Поведение системы|
|-|-|-|-|
|200|OK|Запрос обработан|Продолжить процесс|
|400|Bad Request| Некорректный счет|Отобразить ошибку|
|403|Forbidden| Доступ запрещен|Отобразить ошибку|
|404|Not Found| Счет не найден|Отобразить ошибку|
|500|Internal Server Error|Внутренняя ошибка сервера|Отобразить ошибку|

## Алгоритм обработки запроса

1. **Back** при получении запроса, обращается в таблицу `user`, находит список счетов и проводит валидацию на совпадение.
   - (Приложить пример SQL запроса)
2. **Back** по запрошенному счету, обращается в таблицу `account_info` и отдает ответ на **Front** в соответствии с п. [Формат ответа](#формат-ответа).

## Альтернативные процессы

- Ошибки 4xx, 5xx:
  - **Back** возвращает ошибку с текстом на **Front** в соответствии с п. [Коды ответов](#коды-ответов).

------------------------------------------------------------------------------------------------------
</details>

# User Story
Я как Клиент хочу открыть счёт в Банке, чтобы начать им пользоваться

## История версий
|Задача|Тип изменения|Цвет изменения|Дата|Автор|
|-|-|-|-|-|
|[Ссылка на задачу](https://online.stepup.study/course_sessions/3501/tasks/2464/take?return_url=/viewer/sessions/3501/tasks/2464)|Создано|-|28.08.2024|Внуков В.В.|

## Бизнес-анализ

**AS_IS**: Открытие Счета производится при личной явке Клиента в Отделение Банка 

**TO_BE**: Открытие Счета к выбранному продукту производится через удаленные каналы обслуживания

- Повышение качества обслуживания Клиентов в дистанционных каналах
- Сокращение сроков открытия Счета в АБС Банка 
- Открытие Счета в АБС Банка без участия сотрудников
- Переиспользование в омниканальных платформах

Необходимо создание функциональности для дистанционного открытия Клиенту банковского счета в АБС Банка через API, что также позволит снизить операционные издержки.

## Назначение и цель
Целью проекта является реализация функциональности дистанционного открытия cчета Клиента в АБС Банка с использованием API

## Предварительные действия
- [x] Реализована модель данных в СУБД

![](https://github.com/vnukov-vv/SA_T1/blob/main/DB_ACC.svg)

<details><summary> <i> Код DBML</i> </summary>

```
/* ACCOUNTS - Счета */

// База данных предназначена для управления счетами в АБС Банка в удаленных каналах.

// Описание таблицы ACC
Table acc as acc [note: 'Счет']{
  accountId bigint [primary key, unique, note: 'Первичный ключ.(12)']	
  accountName nvarchar [null, note: 'Наименование Счета.(50)']
  clientId bigint [not null, note: 'ID Клиента.(9)']
  clientName nvarchar [not null, note: 'ID Клиента.(50)']
  bals smallint [not null, note: 'Балансовый Счет.(5)']
  cur smallint [not null, note: 'Балансовый Счет.(5)']
  S bigint [not null, note: 'Номер счета.(20)']
  type nvarchar [not null, note: 'Тип Счета А/П.(1)']
  status nvarchar [not null, note: 'Статус Счета А/П.(20)']
  edited timeStamp [not null, note: 'Дата модификации']
}

// Описание таблицы CLIENTS
Table clients as cli [note: 'Клиенты Банка'] {
  сlientId bigint [primary key, unique, note: 'Уникальный идентификатор в АБС.(8)']
  clientName nvarchar [not null, note: 'ФИО или Наименование (255)']  
}

// Описание таблицы BALS
Table bals as bals [note: 'Балансовый Счет'] {
  bal smallint [not null, note: 'Балансовый Счет.(5)'] 
  name nvarchar [not null, note: 'Описание.(50)']  
}

// Описание таблицы CUR
Table cur as cur [note: 'Валюты'] {
  id nvarchar [primary key, unique, note: 'Цифровой код (3)'] 
  code nvarchar [note: 'Буквенный код.(3)']
  name nvarchar [not null, note: 'Наименование Валюты.(50)']  
}

// Описание таблицы STATUSES
Table statuses as stat [note: 'Статусы'] {
  id smallint [primary key, increment, note: 'Первичный ключ.(2)'] 
  name nvarchar [note: 'Наименование Статуса.(20)']
  ext nvarchar [note: 'Описание Статуса.(50)']
}

// Описание Внешних Ключей

Ref:acc.bals > bals.bal
Ref: acc.clientId > cli.сlientId
Ref: acc.clientName > cli.clientName
Ref: acc.cur > cur.code
Ref: acc.status > stat.id

```
</details>

- [x] Клиент существует в Системе
- [x] Пользователь прошел аутентификацию и авторизацию

## Ограничения по ролям
- Доступ к интерфейсу возможен для авторизованного пользователя с ролями `CLIENT_ALL`(просмотр всех Клиентов), `ACC_CREATE`(открытие Счетов)

## <a id="Макеты"> Макеты </a>
Не требуются.
- Дизайн элементов интерфейса для осуществления целевого действия и отображения уведомления о результатах запроса разрабатывается продуктовыми командами самостоятельно с учетом требований гайда дизайн-кода Банка.
- Фактическое отображение результатов запроса Клиенту может производиться как полностью, так и в сокращённом виде.
- В целях приемочного тестирования успешным считается получение JSON с полным набором данных отображаемым в служебном интерфейсе.

## Основной сценарий (успешный сценарий)

1. Клиент находится в личном кабинете соответствующей платформы.
2. После выбора банковского продукта Клиент совершает целевое действие "Открыть Счет".
3. Front делает запрос на Back `POST/accounts`.
4. Back предварительно валидирует полученные параметры в БД.
5. Back инициирует создание новой записи в БД.
  - Если в пп. 4,5 Back возвращает ошибки 4xx, 5xx см. альтернативный сценарий 1.
6. Back получает подтверждение завершения транзакции и отдаёт результат на Front
7. Front отображает детальную информацию по счету в соответствии с п. [Макеты](#макеты).

<sup>*</sup> UAT: пп.1-2 имитируются через служебный интерфейс

## Альтернативный сценарий
1. Front отображает ошибку от Back.

## Требования к интерфейсу

Служебный интерфейс ввода данных
|Название<br>атрибута|Тип|Длина|Редактируемость|Маска<br>ввода/отображения|Обязательность|Сортировка|Значение<br>по умолчанию| Источник<br>данных|Примечания/<br>Пример|
|-|-|-|-|-|-|-|-|-|-|
|*clientId*|string|11|+|-|-|-|-|Front|"0001010"|
|*bals*|string|5|+|-|-|-|-|Front|"40817"|
|*currency*|string|3|+|-|-|-|-|Front|"RUB"|
|*accountName*|string|50|+|-|-|-|-|Front|"любой произвольный текст"|

Служебный интерфейс вывода данных
|Название<br>атрибута|Тип|Длина|Редактируемость|Маска<br>ввода/отображения|Обязательность|Сортировка|Значение<br>по умолчанию| Источник<br>данных|Примечания/<br>Пример|
|-|-|-|-|-|-|-|-|-|-|
|*clientId*|string|11|-|-|-|-|-|Back|"0001010"|
|*bals*|string|5|-|-|-|-|-|Back|"40817"|
|*currency*|string|3|-|-|-|-|-|Back|"RUB"|
|*accountName*|string|50|-|-|-|-|-|Back|"любой произвольный текст"|
|*accountId*|string|11|-|-|-|-|-|Back|"00000001234"|
|*accountNumber*|string|20|-|-|-|-|-|Back|"40817810300000000003"|
|*accountType*|string|1|-|-|-|-|-|Back|"П"|
|*status*|string|20|-|-|-|-|-|Back|"ACTIVE"|
|*balance*|number($double)|15,2|-|-|-|-|-|Back|"NULL"|
|*edited*|string|24|-|-|-|-|-|Back|"2024-08-28T18:12:00.466Z"|

## Результат

- В служебном интерфейсе отображается информация об открытом счете

---

# `POST /accounts/` Открыть Счёт

## История версий
|Задача|Тип изменения|Цвет изменения|Дата|Автор|
|-|-|-|-|-|
|-|Создано|-|28.08.2024|Внуков В.В.|

## Сервис 
**Микросервис:** account-manager

### Алгоритм вызова

![](https://www.plantuml.com/plantuml/svg/TLHDInjH5Ds_Nt6PLGgQVj1kf8WVs99IeZKkN7JpvgCGEft8p0kqY336XHO5eSj2RQMuZz5OQytu5-xxHpsNYO-ffWxEpBltldFFEVTDvZAZKzFz42lJDd54yokDEl6HxV6LpUq-dfSy93wskpp4eazAwS1qKlBuA_-H98zipoETKH2tbT_vYFzk4khq4talqavYeYIKDBsJXTf0jtRGtj298Mz11-zlqpxULQYDzdKMaJU_k2XX2dsbK2Augjan4UaWxMGPpH1_8Pjp8II8lykBFU1VU0wu3wP3h0-9hn6u4Eh40yZPjZsxmpTIOGyG8jkhsrqeFhSv4cT8ODCnNw9ICAwX62BH0r70v417xcq27nG4q_HiAGo4l8fjG7UcUQJA4jIAIfIkBhNMQ6MvjVPG1m7iCXbjlcejDxUKaefAfKHfbbflNhjCw2EEtb5Y6k6Kh-DiAkYcj8cQhRBe-VHqMPL6MJSsuvJIiL5H37Vv6wHTSG6gkRo1ziZkys-2Vts-4LljTkqfd_39r3EvFr24Fy5sWcS8SlVWpIcG-hI-laurFeAri0SWe_BS5AxaiiHmJa0087x0y6sf4I8ymbLW6n0ANAVsCu9Z92ohSCEnaf-elO7BUvMjK75-Im41TtHhJnuzTaeccrpDmi8PQZHRIwjhzNgzz11PXDqK5fPUDfhtaWwuF9VdQ3wGiyCNuEK43S0Ch922ELIpEqx9U1R5U5zl8cTq16LXVdys9CEvtGq72C3_uS7NQ5JzsktXNSjeCOsqYSA90vGsCgaSIYwSkAeOfC-u-6SmTxee-SALciDTVeZ-0W00)


<details><summary> <i> см. PlantUML</i> </summary>

```PlantUML
@startuml
title API. Открытие Счета 

actor "Клиент" as cli
box
boundary "Frontend" as front
participant "Backend" as back
database "ACC" as db

endbox

Note across : В роли Пользователя может выступать в т.ч. другая Система или Сервис\n 


cli -> front : "Открыть Счет" 
front -> back : REST POST/accounts {JSON}

back -> back : JSON > SQL
back -> db : clientId,bals,cur {SQL}
back <-- db : result {SQL}

alt
else Некорректный запрос(4ХХ,5ХХ)
    back -> front: Ошибка XXX (Описание ошибки)
    front -> cli: Расширенное сообщение об ошибке
else Успешное создание счета (201)
    back -> back : JSON > SQL
    back -> db: INSERT...{SQL}
    db -> db : BEGIN...{SQL}
    db --> back : Подтверждение вставки (успешный ответ)
    back -> back : SQL > JSON
    back -> front : Ответ с подтверждением открытия счета (201 Created)
    front -> cli: Отображение успешного создания счета

end

@enduml
```
</details>

### Свойства вызова

|Свойство|Описание|
|-|-|
|Тип взаимодействия|REST|
|Формат запроса/ответа|JSON|
|Тип вызова|Асинхронный|
|Протокол взаимодействия|MTLS|
|Способ аутентификации|JWT|

### Формат запроса
Нет path/query параметров
|Параметр|Тип|Длина|Расположение<br>(path/query)|Обязательность|Описание|
|-|-|-|-|-|-|
|-|-|-|-|-|-|

#### Пример
```POST /accounts/```

### Тело запроса
|Параметр|Тип|Длина|Расположение (body)|Обязательность|Описание|Место для сохранения|
|-|-|-|-|-|-|-|
|*clientId*|string|body|11|+|Уникальный идентификатор счета|acc.clientId|
|*bals*|string|body|5|+|Балансовый счет второго порядка|acc.bals|
|*currency*|string|body|3|+|Валюта счета счета|acc.cur|
|*accountName*|string|body|50|-|Наименование счета|acc.name|

#### Пример

```json
{
  "clientId": "0001010",
  "bals": "40817",
  "currency": "RUB",
  "accountName": "не заполнено"
}
```

### Формат ответа

|Параметр|Тип|Длина|Обязательность|Описание|Источник данных|Отображение на фронте|
|-|-|-|-|-|-|-|
|*accountId*|string|11|+|Уникальный идентификатор счета|acc.accountId|-|
|*accountName*|string|50|-|Наименование счета|acc.accountName|Название счета|
|*clientId*|string|9|+|Уникальный идентификатор клиента|acc.clientId|-|
|*bals*|string|5|+|Балансовый счет|acc.bals|-|
|*currency*|string|3|+|Код валюты|acc.cur|Валюта|
|*accountNumber*|string|20|+|Номер счета|acc.S|Номер счета|
|*accountType*|string|1|+|Тип счета (Enum: [A, П])|acc.type|Тип счета|
|*status*|string|20|+|Статус счета<br>(Enum: [ACTIVE, CLOSED, RESERVED, DELETED])|acc.status|Статус счета|
|*balance*|number($double)|15,2|-|Текущий баланс счета|acc.balance|Баланс счета|
|*edited*|string|24|+|Дата и время последнего обновления (в формате ISO 8601)|acc.edited|-|

<sup>*</sup> *balance помечен как необязательный т.к. при открытии нового счета будет возвращаться значение `NULL`*

#### Пример

```json
{
  "accountId": "00000001234",
  "accountName": "не заполнено",
  "clientId": "0001010",
  "clientName": "Иванов Петр Сидорович",
  "bals": "40817",
  "currency": "RUB",
  "accountNumber": "40817810300000000003",
  "accountType": "П",
  "status": "ACTIVE",
  "balance": 0.01,
  "timeStamp": "2024-08-28T02:37:13.568Z"
}
```

## Коды ответов

|Код|Название|Описание|Поведение системы|
|-|-|-|-|
|**201**|*Created*|Счет открыт|Отобразить результат|
|**400**|*Bad Request*|Синтаксическая ошибка или ошибка формата|Отобразить ошибку|
|**401**|*Unauthorized*|Не авторизован|Отобразить ошибку|
|**403**|*Forbidden*|Доступ запрещен|Отобразить ошибку|
|**422**|*Unprocessable Entity*|Ошибка валидации данных.<br>Клиент, Балансовый счёт или Валюта не существуют|Отобразить ошибку|
|**500**|*Internal Server Error*|Внутренняя ошибка сервера|Отобразить ошибку|

## Алгоритм обработки запроса

1. **Back** при получении запроса, предварительно валидирует его на корректность проверяя существование клиента, балансового счета и валюты

<details><summary> <i> см. SQL-скрипт</i> </summary>

```sql
BEGIN;

-- Шаг 1: Проверка существования клиента
DO $$
BEGIN
    IF NOT EXISTS (SELECT 1 FROM clients WHERE clientId = :clientId) THEN
        RAISE EXCEPTION 'Client with ID % does not exist', :clientId;
    END IF;
END $$;

-- Шаг 2: Проверка существования балансового счета
DO $$
BEGIN
    IF NOT EXISTS (SELECT 1 FROM bals WHERE bal = :bals) THEN
        RAISE EXCEPTION 'Balance account % does not exist', :bals;
    END IF;
END $$;

-- Шаг 3: Проверка существования валюты
DO $$
BEGIN
    IF NOT EXISTS (SELECT 1 FROM cur WHERE code = :currency) THEN
        RAISE EXCEPTION 'Currency % does not exist', :currency;
    END IF;
END $$;
```
</details>

2. **Back** при успешной валидации запроса, выполняет вставку в таблицу `acc` , преобразует результат `SELECT` подтверждения в JSON и отдает ответ на **Front** в соответствии с п. [Формат ответа](#формат-ответа).

<details><summary> <i> см. SQL-скрипт</i> </summary>

```sql
BEGIN;

/* Вставка нового счета для существующего клиента */
INSERT INTO acc (
    accountId,
    accountName,
    clientId,
    clientName,
    bals,
    cur,
    S,
    type,
    status,
    edited
)
VALUES (
    DEFAULT,                    -- accountId автоинкрементируется, поэтому используем DEFAULT
    :accountName,               -- Наименование счета (может быть NULL)
    :clientId,                  -- Идентификатор существующего клиента
    (SELECT clientName FROM clients WHERE clientId = :clientId), -- Получение имени клиента
    :bals,                      -- Балансовый счет
    :currency,                  -- Код валюты
    open_acc(:bals, :currency), -- Генерация номера счета с помощью отдельной функции open_acc
    :accountType,               -- Тип счета (например, "А" или "П")
    'ACTIVE',                   -- Статус счета по умолчанию "ACTIVE"
    now()                       -- Время создания или модификации записи
);

COMMIT;

/* Подтверждение создания счета: возвращаем данные нового счета */
SELECT 
    accountId,
    accountName,
    clientId,
    bals,
    cur as currency,
    S as accountNumber,
    type as accountType,
    status,
    balance,
    edited
FROM acc
WHERE accountId = currval('acc_accountid_seq');  -- currval для автоинкрементного accountId

```
</details>

## Альтернативные процессы

- Ошибки 4xx, 5xx:
  - **Back** возвращает ошибку с текстом на **Front** в соответствии с п. [Коды ответов](#коды-ответов).
