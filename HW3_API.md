# Задание №3
> API, Swagger, YAML

1. В [Swagger](https://editor.swagger.io/) вставить полученный файл[^1], спроектировать и описать 2 метода в YAML: PATCH и DELETE.
   Можно переиспользовать схемы NewAccount и/или UserUpdate или придумать и описать новую(ые) схему(ы).
2. Любой из методов пометить устаревшим (для этого используется специальный булев атрибут).

[^1] : <details><summary> файл </summary>

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
-----

<table width="1000" border="1">
<thead>
  <tr>
    <td rowspan="3"><img width="300px" src="https://github.com/user-attachments/assets/9d985eaa-c3fc-4ab3-b84c-4acbd7c1bbb2"></td>
    <td colspan="2" width="700"><p align="center"><b>API Доставка карты Клиенту Курьером</b></p></td>
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
