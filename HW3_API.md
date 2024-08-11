# Задание №3
> API, Swagger, YAML

1. В [Swagger](https://editor.swagger.io/) вставить полученный *файл*, спроектировать и описать 2 метода в YAML: PATCH и DELETE.
   Можно переиспользовать схемы NewAccount и/или UserUpdate или придумать и описать новую(ые) схему(ы).
2. Любой из методов пометить устаревшим (для этого используется специальный булев атрибут).

<details><summary> <i>см. файл (развернуть)</i> </summary>

```yaml
openapi: 3.0.0
info:
  title: Bank API
  description: API для управления банковскими счетами и пользователями
  version: 1.0.1
  contact:
    name: Bank API Support
    url: https://www.bank.com/support
    email: support@bank.com
servers:
  - url: https://webinarOpenSchool.org/api/v1
tags:
  - name: Счета
  - name: Пользователи
  
paths:  
  /accounts/{accountId}:
    get:
      tags:
        - Счета
      summary: Получить информацию о банковском счете
      description: Возвращает информацию о конкретном банковском счете
      parameters:
        - name: accountId
          in: path
          required: true
          description: Уникальный идентификатор счета
          schema:
            type: string
      responses:
        '200':
          description: Успешный запрос
          content:
            application/json:
              schema:
                type: object
                properties:
                  accountId:
                    type: integer
                    description: Уникальный идентификатор счета
                    example: 70203333
                  accountNumber:
                    type: string
                    description: Уникальный идентификатор счета
                    example: "40781000208102500000"
                  balance:
                    type: number
                    format: double
                    description: Текущий баланс счета
                    example: 471230.77
                  status:
                    type: string
                    description: Статус счета 
                    example: "ACTIVE"
                    enum:
                     - ACTIVE
                     - CLOSED
                     - RESERVED
        '400':
          description: Некорректный запрос
        '401':
          description: Не авторизован
        '403':
          description: Доступ запрещен
        '404':
          description: Данные не найдены
        '500':
          description: Сервер не доступен
  
  /accounts:
    post:
      tags:
        - Счета
      summary: Создать новый счет
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/NewAccount'
      responses:
        '201':
          description: Создано
        '400':
          description: Некорректный запрос
        '401':
          description: Не авторизован
        '403':
          description: Доступ запрещен
        '409':
          description: Конфликт
        '500':
          description: Сервер не доступен
          
  /users/{userId}:
    put:
      tags:
        - Пользователи
      summary: Обновить информацию о пользователе
      parameters:
        - name: userId
          in: path
          description: Уникальное значение ID пользователя
          required: true
          schema:
            type: string
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/UserUpdate'
            example:
              name: "Alice Smith"
              email: "alice@example.com"
              age: 30
      responses:
        '200':
          description: Успешный запрос
        '401':
          description: Не авторизован
        '403':
          description: Доступ запрещен
        '404':
          description: Данные не найдены
        '500':
          description: Сервер не доступен
        
components:
  schemas:
    NewAccount:
      type: object
      properties:
        accountType:
          type: string
          description: Тип счета
          example: "DEBET"
        balance:
          type: number
          description: Первоначальный баланс
          example: 10000
        firstName:
          type: string
          description: Фамилия владельца
          example: "Свиридова"
        middleName:
          type: string
          description: Отчество владельца
          example: "Борисовна"
        lastName:
          type: string
          description: Имя владельца
          example: "Елена"
      required:
        - accountType
        - firstName
        - lastName
    UserUpdate:
      type: object
      properties:
        name:
          type: string
          description: Имя и фамилия пользователя
        email:
          type: string
          description: Адрес электронной почты
        age:
          type: integer
          description: Возраст

```
</details>
--------

<table width="1000" border="1">
<thead>
  <tr>
    <td rowspan="3"><img width="300px" src="https://github.com/user-attachments/assets/9d985eaa-c3fc-4ab3-b84c-4acbd7c1bbb2"></td>
    <td colspan="2" width="700"><p align="center"><b>API </b></p></td>
  </tr>
  <tr>
    <td>Дата</td>
    <td>11.08.2024</td>
  </tr>
  <tr>
    <td>Версия</td>
    <td>1.0</td>
  </tr>
</thead>
</table>

<details><summary> <i> Развернуть </i> </summary>

```yaml
openapi: 3.0.0
info:
  title: Bank API
  description: API для управления банковскими счетами и пользователями
  version: 1.0.0
  contact:
    name: Bank API Support
    url: https://www.bank.com/support
    email: support@bank.com
servers:
  - url: https://webinarOpenSchool.org/api/v1
tags:
  - name: Счета
  - name: Пользователи

# Методы

## Счета
paths:  

  /accounts:
     post:
      deprecated: false
      tags:
        - Счета
      summary: Создать банковский счет
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
                  example: "не обязательно"
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
        '409':
          description: Конфликт
        '422':
          description: Проверьте введенные данные
        '500':
          description: Сервер недоступен
          
  /accounts/{accountId}:
    get:
      deprecated: false
      tags:
        - Счета
      summary: Получить информацию о банковском счете
      description: Возвращает информацию о конкретном банковском счете
      parameters:
        - name: accountId
          in: path
          required: true
          description: Уникальный идентификатор счета
          schema:
            type: string
      responses:
        '200':
          description: Успешный запрос
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
        '404':
          description: Данные не найдены
        '500':
          description: Сервер не доступен
  
    put:
      deprecated: false
      tags:
        - Счета
      summary: Обновить информацию о счете
      description: Модифицирует информацию о счете 
      parameters:
        - name: accountId
          in: path
          required: true
          description: Уникальный идентификатор счета
          schema:
            type: string
      requestBody:
        description: Update an existent user in the store
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Account'
      responses:
        '200':
          description: Успешный запрос
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Account'
        '204':
          description: Счет не найден
        '400':
          description: Некорректный запрос
        '401':
          description: Не авторизован
        '403':
          description: Доступ запрещен
        '404':
          description: Счет не найден
        '422':
          description: Проверьте введенные данные
        '500':
          description: Сервер не доступен

          
    patch:
      deprecated: true
      # потому что информация будет обновляться из формы по кнопке "сохранить"
      tags:
        - Счета
      summary: Обновить информацию о счете
      description: Модифицирует информацию о счете 
      parameters:
        - name: accountId
          in: path
          required: true
          description: Уникальный идентификатор счета
          schema:
            type: string
      requestBody:
        description: Update an existent user in the store
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Account'
      responses:
        '200':
          description: Успешный запрос
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Account'
        '204':
          description: Счет не найден
        '400':
          description: Некорректный запрос
        '401':
          description: Не авторизован
        '403':
          description: Доступ запрещен
        '404':
          description: Счет не найден
        '422':
          description: Проверьте введенные данные
        '500':
          description: Сервер не доступен
          
          
    delete:
      deprecated: false
      tags:
        - Счета
      summary: Удалить банковский счет (служебная)
      ## потому что правильнее не удалять, а помечать как удаленный, так как там автоинкременты и алгоритмы нумерации и чтобы можно было переиспользовать, но для исключительных случаев можно оставить.
      description: Удаляет информацию о конкретном банковском счете
      parameters:
        - name: accountId
          in: path
          required: true
          description: Уникальный идентификатор счета
          schema:
            type: string
      responses:
        '200':
          description: Успешный запрос
        '202':
          description: Запрос принят
        '204':
          description: Счет удален
        '400':
          description: Некорректный запрос
        '401':
          description: Не авторизован
        '403':
          description: Доступ запрещен
        '404':
          description: Данные не найдены
        '500':
          description: Сервер не доступен          
          


## Пользователи

  /users/{userId}:
    put:
      tags:
        - Пользователи
      summary: Обновить информацию о пользователе
      parameters:
        - name: userId
          in: path
          description: Уникальное значение ID пользователя
          required: true
          schema:
            type: string
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/User'
      responses:
        '200':
          description: Успешный запрос
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/User'
        '401':
          description: Не авторизован
        '403':
          description: Доступ запрещен
        '404':
          description: Данные не найдены
        '500':
          description: Сервер не доступен

# Схемы

components:
  schemas:

    User:
      type: object
      description: Данные пользователя
      properties:
        userID:
          type: integer
          description: Уникальный ID пользователя
          example: "012345"
        login:
          type: string
          description: login пользователя
          example: "username"
        email:
          type: string
          description: Адрес электронной почты
          example: "username@bank.ru"
        human:
          type: array
          description: Данные пользователя
          items:
            $ref: '#/components/schemas/Human'
        staff:
          description: Признак сотрудника банка
          type: boolean

    Human:
      type: object
      description: Данные физлица
      properties:
        subjId:
          type: string
          description: Уникальный идентификатор
          example: "0001111"
        lastName:
          type: string
          description: Фамилия 
          example: "Банковский"
        firstName:
          type: string
          description: Имя 
          example: "Сотрудник"
        middleName:
          type: string
          description: Отчество 
          example: "Без отчества"
        ## и другие персональные данные


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
          example: "не обязательно"
        clietntId:
          type: string
          description: Уникальный идентификатор клиента
          example: "0001010"
        # Клиента не расписываем т.к. для юрлица и физлица разные атрибуты
        bals:
          type: string
          description: Балансовый счет
          example: "40817"
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
```
</details>
