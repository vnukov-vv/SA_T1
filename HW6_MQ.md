# Задание №6
>Требования к брокерам сообщений

Разработать документацию к сервису, отображающему информацию, полученную из внешней системы с помощью Кафка.

<details>

## ОБЯЗАТЕЛЬНО
- ФТ, НФТ, структура документа
- С4
- Описание топиков и подключение к Кафка
- Кто какой топик читает
- Кто в какой топик пишет
- Описание сообщения для каждого топика
- Маппинг значений в топике в БД, с преобразованиями если они нужны

Все остальное будет плюсом

</details>

<table width="1000" border="1">
<thead>
  <tr>
    <td rowspan="3"><img width="300px" src="https://github.com/user-attachments/assets/9d985eaa-c3fc-4ab3-b84c-4acbd7c1bbb2"></td>
    <td colspan="2" width="700"><p align="center"><b> Сервис интеграции ГАР </b></p></td>
  </tr>
  <tr>
    <td>Дата</td>
    <td>23.08.2024</td>
  </tr>
  <tr>
    <td>Версия</td>
    <td>1.0</td>
  </tr>
</thead>
</table>


## Оглавление
[1. Предметная область. Термины и определения](#title1) <br> 
[2. User Story](#title2)</br>
[3. Проблематика и цель](#title3)</br>
[4. Нефункциональные требования](#title4)</br>
[5. Функциональные требования](#title5)</br>
[6. ...](#title6)</br>
[7. ...](#title7)</br>

## <a id="title1"> 1. Предметная область. Термины и определения </a>

|Термин	|Определение|
|---|---|
|**Адрес**|Комплекс наименований адресообразующих элементов (страна, субъект Российской Федерации, федеральная территория, муниципальное образование, населенный пункт, элемент улично-дорожной сети, элемент планировочной структуры)|
|**ГАР**	|Государственный адресный реестр. Информационный ресурс, содержащий сведения об адресах.|
|**ФИАС**	|федеральная (государственная) информационная адресная система, обеспечивающая формирование, ведение и использование **ГАР**. Оператором **ФИАС** определена Федеральная налоговая служба (**ФНС**)|
|**Система**	|Комплекс программного и технического обеспечения предназначенный для поддержки бизнес-процессов **Банка**|
|**Сервис**	|Настоящий сервис интеграции **ГАР**, как комплекс программного и технического обеспечения предназначенный для обеспечения взаимодействия **ФИАС** и **Системы**|


### <a id="title1_2"> 1.2 Ссылки на существующую документацию </a>
|Описание|Ссылка|
|---|---|
|Раздел "Разработчикам" на сайте ФИАС/ФНС|[см. по ссылке](https://fias.nalog.ru/Frontend)|
|Условия использования API-сервисов ФИАС|[скачать .pdf](https://fias.nalog.ru/docs/Условия%20использования%20API-сервисов%20ФИАС.pdf)|
|Сервис «Получение сведений из ГАР»|[в формате Swagger](https://fias-public-service.nalog.ru/api/spas/v2.0/swagger/index.html)|

## <a id="title2"> 2. User Story </a>

- Я, как **Система**, хочу хранить адреса **Клиентов** в формате **ГАР**, чтобы исключить некорректное заполнение адресных данных Банка, Клиентов, Контрагентов во внутренних и  исходящих документах и отчетности Банка;

## <a id="title3"> 3. Проблематика и цель </a>

Привести разрозненные сведения об адресах к единому, унифицированному написанию, исключить дубли, ошибки и противоречия в адресах при информационном взаимодействии с **Системой**;

Обеспечить пользователям **Системы** возможность получить, проверить, сохранить **Адрес**  в формате **ГАР**.

Настроить регулярное обновление справочника **ГАР** в информационной системе **Банка**;

## <a id="title4"> 4. Нефункциональные требования и ограничения</a>

- **Сервис** не изменяет и не удаляет данные, полученные из **ФИАС**, без явного указания.

- Допустимые объемы информационного обмена устанавливаются и изменяются **ФНС** в одностороннем порядке в зависимости от имеющихся технических возможностей с учетом нагрузки, формируемой пользователями **ФИАС**.

- В настоящее время установлено ограничение на количество направляемых запросов, равное 100 запросов в минуту и 10 000 запросов в день.

## <a id="title5"> 5. Функциональные требования </a>

- Получение сообщений с обновлениями адресной информации из ФИАС.
- Обработка и преобразование данных в соответствии с внутренними стандартами.
- Запись обработанных данных в базу данных.
- Предоставление API для доступа к обработанной адресной информации.

## <a id="title6"> 6. ... </a>

![SVG](https://www.plantuml.com/plantuml/svg/TLFDRjD04BxlKmova4OagZX6K1Kf8Ig4Wj8KzO1KRPjDPU7OZdTT2gSs23XGKNxE840yW0c4f0qnhp3xHiokOoCIkFXd_CttCpjUbug7AkgvJ3dA5O0Vy2lECC4XJd54JnCSWJx1N_eOOoec-eKjNc0C-0vVuqV60c9mzfs0UmeANOVBYiTT_w0IHWNW4ao5xVb7V-Fm4uw8SuWJVG8FF4mMTVNPNC2II14Uidua8W65sxpxaDjgVucJsFI027vYdFOzbanu7IFFDdqbWE-7lfHG1NmBb2B1cSLVf7s0Ouhv7MEAEG7oDwBNAUKTwwVaTq2einJpJHzJQMmfpi4WvdP13wWqrQVca_r0PYYHVeCpkhxKpy08v2zf5usWLCBt-0K_bqhL_nq3c5p6AxtJarKX59Y3iJe9_h1jvmGs-fGWCSdqgNvL8Gt6UAHyB-hjYP0nCrGehzaJeecqwbjjQDJRX6i8rUHIrVn7dklppat75HjUrqyxhfNBMSlLrTKgtDgwkqaznViYb8xlRNIkD7YuSwTP4wxYswtcoXybUw-IkNITJ32wnjbeYIKd8Qkk0YPSIKUUL-4wvC-N2ndlJaQyVQzserqlAgSdQB5xmSfI_wL_4cHvElF0nSK4j4DiAVq13tSx1h9xr7ChJvnWCUUodGL0ke4uDFy2xKsid-F4Ze74rynSyuO-f8Ck7d8t4dA5qMPdzPReHoHWIjPUMfE1xqcHuUYM6uASXArJCFhxVmC0)

<details><summary> <i> см. plantUML (развернуть)</i> </summary>

```plantUML
@startuml
title Обновление справочника ГАР

participant "fias.nalog.ru" as fias
box
participant "Сервис \nобновления ГАР" as serv
queue "Kafka" as q
participant "Система" as sys
endbox

Note across : В контексте задачи реализуется загрузкой из ГАР только изменённых данных ГАР \n**НФТ**: Обновление с максимально возможной скоростью. \n

autonumber

serv -> fias : REST GET \nGetLastDownloadFileInfo
serv <-- fias : 200: JSON \n(VersionId,GarXMLDeltaURL)

serv -> serv : сравнивается \nVersionId

alt 
else "VersionId = VersionId'"
serv ->X serv : UPDATE(timestamp)
else "VersionId != VersionId'"
serv -> fias : download(GarXMLDeltaURL)
end

serv <-- fias : gar_delta_xml.zip
serv -> serv : UPDATE(timestamp)
serv -> serv : конвертация \nXML>JSON
serv -> q : JSON(values)
sys -> q : Request
sys <-- q : Response
sys -> sys : UPDATE (values)

@enduml
```
</details>
  
## <a id="title7"> 7. ... </a>

<details>

</details>
<br>
<br>
