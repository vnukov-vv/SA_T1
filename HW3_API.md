# Задание №3
> API, Swagger, YAML

<details>

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
</details>

<table width="1000" border="1">
<thead>
  <tr>
    <td rowspan="3"><img width="300px" src="https://github.com/user-attachments/assets/9d985eaa-c3fc-4ab3-b84c-4acbd7c1bbb2"></td>
    <td colspan="2" width="700"><p align="center"><b>API </b></p></td>
  </tr>
  <tr>
    <td>Дата</td>
    <td>11.09.2024</td>
  </tr>
  <tr>
    <td>Версия</td>
    <td>2.0</td>
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
  - url: https://HomeworkOpenSchool.org/api/v2
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
        required: true  # Тело запроса обязательно
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/AccountRequest'
      responses:
        '201':
          description: Создано
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/AccountResponse'
        '400':
          description: Некорректный запрос
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ValidationErrorResponse'
        '401':
          description: Не авторизован
        '403':
          description: Доступ запрещен
        '409':
          description: Конфликт
        '422':
          description: Проверьте праильность введенных данных
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
                $ref: '#/components/schemas/AccountResponse'
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
        description: Изменяемая информация о счете
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/AccountRequest'
      responses:
        '200':
          description: Успешный запрос. Обновленная информация
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/AccountResponse'
        '204':
          description: Запрос выполнен # если нет необходимости в отображении информации
        '400':
          description: Некорректный запрос
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ValidationErrorResponse'
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
      # потому что информация будет обновляться из формы по кнопке "сохранить" т.е. полное обновление ресурса через `PUT`
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
        description: Изменяемая информация о счете
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/AccountRequest'
      responses:
        '200':
          description: Успешный запрос
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/AccountResponse'
        '204':
          description: Нет информации для отображения
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
        '202': # если операция асинхронная
          description: Запрос на удаление счета принят
        '204': # если удаление в момент обработки запроса
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
          
  /accounts/status/{accountId}:

    patch:
      deprecated: false
      tags:
        - Счета
      summary: Изменить статус счета
      description: Изменяет статус счета на один из доступных
      parameters:
        - name: accountId
          in: path
          required: true
          description: Уникальный идентификатор счета
          schema:
            type: string
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                status:
                  type: string
                  description: Новый статус счета
                  example: "DELETED"
                  enum:
                    - ACTIVE
                    - CLOSED
                    - RESERVED
                    - DELETED
      responses:
        '200':
          description: Статус счета изменен
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/AccountResponse'
        '400':
          description: Некорректный запрос
        '401':
          description: Не авторизован
        '403':
          description: Доступ запрещен
        '404':
          description: Счет не найден
        '409':
          description: Конфликт. Статус счета не может быть изменен.
          content:
            application/json:
              schema:
              # oneOf: # так правильно
                anyOf: # так отображаются оба варианта
                  - $ref: '#/components/schemas/ErrorAccResponse' # развернутая ошибка
                  - $ref: '#/components/schemas/AccountResponse' # или текущее состояние счета
        '422':
          description: Некорректные данные. Проверьте формат переданных значений или бизнес-правила.
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ErrorAccResponse'
        '500':
          description: Сервер недоступен


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

    AccountRequest:
      type: object
      description: Данные счета для запроса
      properties:
        clientId:
          type: string
          description: Уникальный идентификатор клиента
          oneOf: # если разный бэк для ФЛ и ЮЛ
            - pattern: "^[0-9]{7}$"  # Валидация с использованием регулярного выражения (7 цифр)
              example: "0001010"
            - pattern: "^[A-Za-z0-9]{6,10}$"  # Вариант для буквенно-цифрового ID (от 6 до 10 символов)
              example: "IP000404"
        bals:
          type: string
          description: Балансовый счет
          example: "40817"
        currency:
          type: string
          description: Валюта счета
          example: "RUB"
          enum:
            - USD   # Доллар США
            - EUR   # Евро
            - RUB   # Российский рубль
        accountName:
          type: string
          description: Наименование счета (необязательное)
          example: "Какое-то наименование"
      required:
        - clientId
        - bals
        - currency  # Обязательные параметры только для запроса

    AccountResponse:
      type: object
      description: Данные счета для ответа
      properties:
        accountId:
          type: string
          description: Уникальный идентификатор счета
          example: "00000001234"
        clientId:
          type: string
          description: Уникальный идентификатор клиента
          example: "0001010"
        bals:
          type: string
          description: Балансовый счет
          example: "40817"
        accountName:
          type: string
          description: Наименование счета (необязательно)
          example: "Для расчетов с использованием банковских карт"
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
        updatedAt:
          description: timestamp модификации (назначается сервером)
          type: string
          format: date-time
      required:
        - accountId
        - clientId
        - bals
        - accountNumber
        - status
        - balance
        - updatedAt

## Ошибки 
    ErrorAccResponse:
      type: object
      description: Возвращены ошибки при выполнении запроса
      properties:
        error:
          type: string
          description: Тип ошибки
          example: "Conflict"
        message:
          type: string
          description: Подробное описание ошибки
          example: "Статус счета не может быть изменен на 'DELETED', так как на счете есть ненулевой остаток."
        details:
          type: object
          description: Дополнительные данные, поясняющие ошибку (опционально)
          properties:
            balance:
              type: number
              format: money
              description: Текущий баланс счета, если ошибка связана с балансом
              example: 150.50
            reason:
              type: string
              description: Причина ошибки, если необходимо пояснить (опционально)
              example: "Баланс должен быть равен 0.00"
      required:
        - error
        - message

    ValidationErrorResponse:
      type: object
      description: Ответ на ошибки валидации полей
      properties:
        error:
          type: string
          description: Тип ошибки
          example: "ValidationError"
        message:
          type: string
          description: Общее описание ошибки
          example: "Одно или несколько полей некорректно заполнены"
        invalidFields:
          type: array
          description: Список полей, которые не прошли валидацию
          items:
            type: object
            properties:
              field:
                type: string
                description: Поле, в котором возникла ошибка
                example: "currency"
              invalidValue:
                type: string
                description: Некорректное значение, переданное в запросе
                example: "GBP"
              message:
                type: string
                description: Сообщение с описанием ошибки для этого поля
                example: "Валюта неизвестна или недоступна"
              details:
                type: object
                description: Дополнительные данные об ошибке
                properties:
                  pattern:
                    type: string
                    description: Ожидаемый шаблон для поля (если применимо)
                    example: "^[0-9]{7}$"
                  validValues:
                    type: array
                    items:
                      type: string
                    description: Допустимые значения (если применимо)
                    example: ["USD", "EUR", "RUB"]
      required:
        - error
        - message
        - invalidFields

```
</details>
