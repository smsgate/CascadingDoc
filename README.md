# Содержание

* [Руководство по взаимодействию с сервисом на основе HTTPS протокола, методом GET](https://github.com/smsgate/CascadingDoc/blob/master/README.md#%D0%A0%D1%83%D0%BA%D0%BE%D0%B2%D0%BE%D0%B4%D1%81%D1%82%D0%B2%D0%BE-%D0%BF%D0%BE-%D0%B2%D0%B7%D0%B0%D0%B8%D0%BC%D0%BE%D0%B4%D0%B5%D0%B9%D1%81%D1%82%D0%B2%D0%B8%D1%8E-%D1%81-%D1%81%D0%B5%D1%80%D0%B2%D0%B8%D1%81%D0%BE%D0%BC-%D0%BD%D0%B0-%D0%BE%D1%81%D0%BD%D0%BE%D0%B2%D0%B5-https-%D0%BF%D1%80%D0%BE%D1%82%D0%BE%D0%BA%D0%BE%D0%BB%D0%B0-%D0%BC%D0%B5%D1%82%D0%BE%D0%B4%D0%BE%D0%BC-get)
* [Руководство по взаимодействию с сервисом на основе JSON документов, методом POST](https://github.com/smsgate/CascadingDoc/blob/master/README.md#%D0%A0%D1%83%D0%BA%D0%BE%D0%B2%D0%BE%D0%B4%D1%81%D1%82%D0%B2%D0%BE-%D0%BF%D0%BE-%D0%B2%D0%B7%D0%B0%D0%B8%D0%BC%D0%BE%D0%B4%D0%B5%D0%B9%D1%81%D1%82%D0%B2%D0%B8%D1%8E-%D1%81-%D1%81%D0%B5%D1%80%D0%B2%D0%B8%D1%81%D0%BE%D0%BC-%D0%BD%D0%B0-%D0%BE%D1%81%D0%BD%D0%BE%D0%B2%D0%B5-json-%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82%D0%BE%D0%B2-%D0%BC%D0%B5%D1%82%D0%BE%D0%B4%D0%BE%D0%BC-post)
* [Руководство по взаимодействию с сервисом на основе XML документа, методом POST](https://github.com/smsgate/CascadingDoc/blob/master/README.md#%D0%A0%D1%83%D0%BA%D0%BE%D0%B2%D0%BE%D0%B4%D1%81%D1%82%D0%B2%D0%BE-%D0%BF%D0%BE-%D0%B2%D0%B7%D0%B0%D0%B8%D0%BC%D0%BE%D0%B4%D0%B5%D0%B9%D1%81%D1%82%D0%B2%D0%B8%D1%8E-%D1%81-%D1%81%D0%B5%D1%80%D0%B2%D0%B8%D1%81%D0%BE%D0%BC-%D0%BD%D0%B0-%D0%BE%D1%81%D0%BD%D0%BE%D0%B2%D0%B5-xml-%D0%B4%D0%BE%D0%BA%D1%83%D0%BC%D0%B5%D0%BD%D1%82%D0%B0-%D0%BC%D0%B5%D1%82%D0%BE%D0%B4%D0%BE%D0%BC-post)

# Руководство по взаимодействию с сервисом на основе HTTPS протокола, методом GET

Запросы необходимо отправлять в UTF-8 кодировке. Не стоит использовать URL длиной более 2,000 символов. Но этот параметр зависит от многих факторов и [может различаться в большую или меньшую сторону](https://github.com/dreikanter/paradigm.ru/blob/master/posts/2007-12-19_url-max-length.md). Одинаковые запросы можно отправлять не чаще 1 раза в 1 минуту. В случае ошибки вернется:
```
error: Попытка отправки более одного одинакового запроса в течение минуты
```

# Запрос на отправку сообщения

Отправляется GET-запрос по адресу:
```
https://имя_хоста/sendmessage.php
```

Пример:
```
https://имя_хоста/sendmessage.php?login=ЛОГИН&password=ПАРОЛЬ&phone=ТЕЛЕФОН&send_viber=1&sender_viber=ИМЯ_ОТПРАВИТЕЛЯ_ВАЙБЕР&text_viber=ТЕКСТ_ВАЙБЕР&button_text=ТЕКСТ_КНОПКИ&button_url=ССЫЛКА_КНОПКИ&image_url=ИЗОБРАЖЕНИЕ&send_sms=3&sender_sms=ИМЯ_ОТПРАВИТЕЛЯ_СМС&text_sms=ТЕКСТ_СМС&validity_period_viber=60&finale_viber_read=0&send_vk=2&templateId=100&templateData={"Name":"Имя","Where":"Москва"}
```
Где:
* **login** – Логин пользователя;
* **password** – Пароль;
* **phone** - Номер абонента, которому адресовано сообщение. Можно несколько телефонов через запятую. Номера в международном формате, например, 79000000001 (для России), 380442589632 (для Украины);
* **send_viber** – Отправлять ли VIBER сообщение. Также является порядком сортировки отправки VIBER сообщения (от меньшего к большему). Может принимать значение от 0 до 9, где 0 - не отправлять VIBER сообщение;
* **sender_viber** – Имя отправителя VIBER. Именно это значение будет выводиться на телефоне абонента в поле от кого сообщение;
* **text_viber** – Текст VIBER сообщения. Не должен превышать более 1000 символов. Обязательный параметр;
* **button_text** – Текст кнопки. Не более 19 символов. Необязательный параметр. При добавлении, обязательно чтоб была указана ссылка кнопки в параметре button_url;
* **button_url** – Ссылка кнопки. Необязательный параметр. При добавлении, обязательно чтоб было указано название кнопки в параметре button_text;
* **image_url** – Ссылка на изображение. Необязательный параметр. В случае добавления изображения, также необходимо наличие кнопки (button_text и button_url);
* **send_sms** – Отправлять ли SMS. Также является порядком сортировки отправки SMS (от меньшего к большему). Может принимать значение от 0 до 9, где 0 - не отправлять SMS;
* **sender_sms** - Отправитель SMS. Именно это значение будет выводиться на телефоне абонента в поле от кого SMS;
* **text_sms** - Текст SMS.
* **validity_period_viber** – Время жизни VIBER сообщения. За этот период, система делает попытки доставить сообщение абоненту. Если за указанный период не будет доставлено сообщение, оно профинализируется со статусом просрочено либо не доставлено. Необязательный параметр. Указывается в минутах, например "60" - что значит 1 час. Если не указано, по умолчанию будет "60";
* **finale_viber_read** – Считать финальным доставленным VIBER сообщением статус "прочитано". В системе VIBER существуют статусы как доставлено и прочитано. В случае если в данном поле указали "1", то в VIBER сообщении, в котором фигурирует статус доставлено, но не прочитано, по истечению время жизни VIBER сообщения - будет попытка переотправки сообщения по другой системе (например через SMS), если в самом XML запросе фигурирует каскадная отправка (send_viber и send_sms);
* **send_vk** - Отправлять ли VK сообщение. Также является порядком сортировки отправки VK сообщения (от меньшего к большему). Может принимать значение от 0 до 9, где 0 - не отправлять VK сообщение. Для открытия данного направления для вас, свяжитесь с вашим менеджером;
* **templateId** - Идентификатор шаблона в системе. Можете посмотреть Идентификатор шаблона в личном кабинете;
* **templateData** - Значения параметров шаблона. Шаблон должен быть согласован VK. В GET запросе должен быть в виде JSON-данных. Можете использовать php функцию urlencode() для этих данных, во избежание ошибок;

В данном примере, первым будет попытка отправки VIBER сообщения, и в случае недоставки, будет попытка инициализация отправки VK сообщения, далее SMS;

## В случае успешной отправки сообщения

Возвращается ID сообщения  в plainText. Пример:
```
1179038981
```
В случае отправки на несколько номеров возращается ID сообщения через запятую в plaintText. Пример:
```
1178440060,1178440061
```

## В случае ошибки

В случае возникновения ошибки возращается текст ошибки в plainText.

# Проверка статуса сообщения

Отправляетя GET-запрос по адресу:
```
https://имя_хоста/sendmessage.php
```

Пример:
```
https://имя_хоста/sendmessage.php?login=ЛОГИН&password=ПАРОЛЬ&id_message=ID_СООБЩЕНИЯ
```
Где:
* **login** – Логин пользователя;
* **password** – Пароль;
* **id_message** – ID сообщения.

## В случае успешного запроса

В случае успешного запроса возращается статус сообщения в plainText:

* **send** - Статус сообщения не получен;
* **not_deliver** - Сообщение не было доставлено. Конечный статус (не меняется со временем);
* **expired** - Абонент находился не в сети в те моменты, когда делалась попытка доставки. Конечный Статус (не меняется со временем);
* **deliver** - Сообщение доставлено. Конечный статус (не меняется со временем);
* **partly_deliver** - Сообщение было отправлено, но статус так и не был получен. Конечный статус (не меняется со временем). В этом случае для разъяснения причин отсутствия статуса необходимо связаться со службой тех. поддержки.

Пример:
```
deliver
```

## В случае ошибки

В случае возникновения ошибки возвращается текст ошибки в plainText.


# Руководство по взаимодействию с сервисом на основе JSON документов, методом POST

# Общие принципы отправки
На определенный адрес сервера отправляются JSON документы (описание JSON документов, их назначение и адреса сервера приведены ниже). При этом используется POST метод.

Заголовки отправляемых данных должны содержать:
```
Content-Type: application/json; charset=utf-8
```
Кодировка JSON документов UTF-8.

## Пример передачи JSON документа на php

```php
$param = array(
	'login' => 'ЛОГИН',
	'password' => 'ПАРОЛЬ'
);
$param_json = json_encode($param);
// JSON-документ
$href = 'https://имя_хоста/sendmessagejson.php'; // адрес сервера
$ch = curl_init();
curl_setopt($ch, CURLOPT_HTTPHEADER, array('Content-Type: application/json','charset=utf-8','Expect:'));
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_POST, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, $param_json);
curl_setopt($ch, CURLOPT_TIMEOUT, 600);
curl_setopt($ch, CURLOPT_URL, $href);
curl_setopt ($ch, CURLOPT_SSL_VERIFYPEER, 0);
curl_setopt ($ch, CURLOPT_SSL_VERIFYHOST, 0);
$res = curl_exec($ch);
$result = json_decode($res, true);
curl_close($ch);
print_r($result);
```

## Отправка сообщения
**Адрес сервера:**
```
https://имя_хоста/sendmessagejson.php
```
**JSON-документ:**
```json
{
	"login":"login",
	"password":"password",
	"message":[
		{
			"send_viber":"1",
			"send_vk" => "2",
			"send_sms":"3",
			"name_delivery":"НАЗВАНИЕ_РАССЫЛКИ",
			"time_send":"ВРЕМЯ_ОТПРАВКИ",
			"sender_viber":"ИМЯ_ОТПРАВИТЕЛЯ_ВАЙБЕР",
			"text_viber":"ТЕКСТ_ВАЙБЕР",
			"button_text":"ТЕКСТ_КНОПКИ",
			"button_url":"ССЫЛКА_КНОПКИ",
			"image_url":"ИЗОБРАЖЕНИЕ",
			"validity_period_viber":"ВРЕМЯ_ЖИЗНИ_ВАЙБЕР_СООБЩЕНИЯ",
			"finale_viber_read":"ФИНАЛЬНЫЙ_СТАТУС_ДОСТАВКИ_КАК_ПРОЧИТАНО",
			"sender_sms":"ИМЯ_ОТПРАВИТЕЛЯ_СМС",
			"text_sms":"ТЕКСТ_СМС",
			"templateId" => "100",
			"templateData" => {
				"Name":"Имя",
				"Where":"Москва"
			},
			"phones":[
				{"phone":"79801234567","client_id_message":"111"},
				{"phone":"79800000001","client_id_message":"112"}
			]
		},
		{
			"send_viber":"1",
			"name_delivery":"НАЗВАНИЕ_РАССЫЛКИ_2",
			"sender_viber":"ИМЯ_ОТПРАВИТЕЛЯ_ВАЙБЕР_2",
			"text_viber":"ТЕКСТ_ВАЙБЕР_2",
			"phones":[
				{"phone":"79800000002","client_id_message":"113"}
			]
		},
		{
			"name_delivery":"НАЗВАНИЕ_РАССЫЛКИ_3",
			"sender_viber":"ИМЯ_ОТПРАВИТЕЛЯ_ВАЙБЕР_3",
			"text_viber":"ТЕКСТ_ВАЙБЕР_3",
			"phones":[
				{"phone":"79800000003"}
			]
		}
	]
}
```
**PHP-данные:**
```php
$param = array(
	'login' => 'login',
	'password' => 'password',
	'message' => array(
		array(
			'send_viber' => '1',
			'send_vk' => '2',
			'send_sms' => '3',
			'name_delivery' => 'НАЗВАНИЕ_РАССЫЛКИ',
			'time_send' => 'ВРЕМЯ_ОТПРАВКИ',
			'sender_viber' => 'ИМЯ_ОТПРАВИТЕЛЯ_ВАЙБЕР',
			'text_viber' => 'ТЕКСТ_ВАЙБЕР',
			'button_text' => 'ТЕКСТ_КНОПКИ',
			'button_url' => 'ССЫЛКА_КНОПКИ',
			'image_url' => 'ИЗОБРАЖЕНИЕ',
			'validity_period_viber' => 'ВРЕМЯ_ЖИЗНИ_ВАЙБЕР_СООБЩЕНИЯ',
			'finale_viber_read' => '1',
			'sender_sms' => 'ИМЯ_ОТПРАВИТЕЛЯ_СМС',
			'text_sms' => 'ТЕКСТ_СМС',
			'templateId' => '100',
			'templateData' => array(
				'Name' => 'Имя',
				'Where' => 'Москва'
			),
			'phones' => array(
				array('phone' => '79801234567', 'client_id_message' => '111'),
				array('phone' => '79800000001', 'client_id_message' => '112')
			)			
		),
		array(
			'send_viber' => '1',
			'name_delivery' => 'НАЗВАНИЕ_РАССЫЛКИ_2',
			'sender_viber' => 'ИМЯ_ОТПРАВИТЕЛЯ_ВАЙБЕР_2',
			'text_viber' => 'ТЕКСТ_ВАЙБЕР_2',
			'phones' => array(
				array('phone' => '79800000002', 'client_id_message' => '113')
			)
		),
		array(
			'name_delivery' => 'НАЗВАНИЕ_РАССЫЛКИ_3',
			'sender_viber' => 'ИМЯ_ОТПРАВИТЕЛЯ_ВАЙБЕР_3',
			'text_viber' => 'ТЕКСТ_ВАЙБЕР_3',
			'phones' => array(
				array('phone' => '79800000003')
			)
        )
    )
);
```

Где:
* **login** – Логин пользователя;
* **password** – Пароль;
* **message** – Сообщения;
	* **name_delivery** – Название рассылки. Если поле является пустым, по умолчанию - "Шлюз";
	* **time_send** – Желательное время отправки сообщения, в формате: YYYY-MM-DD hh:mm где, YYYY-год, MM-месяц, DD-день, hh-часы, mm-минуты. Например 2017-11-23 13:00. Если поле является пустым, то отправка сообщения происходит сразу;
	* **send_viber** – Отправлять ли VIBER сообщение. Также является порядком сортировки отправки VIBER сообщения (от меньшего к большему). Может принимать значение от 0 до 9, где 0 - не отправлять VIBER сообщение;
	* **sender_viber** – Имя отправителя VIBER. Именно это значение будет выводиться на телефоне абонента в поле от кого сообщение;
	* **text_viber** – Текст VIBER сообщения. Не должен превышать более 1000 символов. Обязательный параметр;
	* **button_text** – Текст кнопки. Не более 19 символов. Необязательный параметр. При добавлении, обязательно чтоб была указана ссылка кнопки в параметре button_url;
	* **button_url** – Ссылка кнопки. Необязательный параметр. При добавлении, обязательно чтоб было указано название кнопки в параметре button_text;
	* **image_url** – Ссылка на изображение. Необязательный параметр. В случае добавления изображения, также необходимо наличие кнопки (button_text и button_url);
	* **validity_period_viber** – Время жизни VIBER сообщения. За этот период, система делает попытки доставить сообщение абоненту. Если за указанный период не будет доставлено сообщение, оно профинализируется со статусом просрочено либо не доставлено. Необязательный параметр. Указывается в минутах, например "60" - что значит 1 час. Если не указано, по умолчанию будет "60";
	* **finale_viber_read** – Считать финальным доставленным VIBER сообщением статус "прочитано". В системе VIBER существуют статусы как доставлено и прочитано. В случае если в данном поле указали "1", то в VIBER сообщении, в котором фигурирует статус доставлено, но не прочитано, по истечению время жизни VIBER сообщения - будет попытка переотправки сообщения по другой системе (например через SMS), если в самом JSON запросе фигурирует каскадная отправка (send_viber и send_sms);
	* **send_sms** – Отправлять ли SMS. Также является порядком сортировки отправки SMS (от меньшего к большему). Может принимать значение от 0 до 9, где 0 - не отправлять SMS;
	* **sender_sms** - Отправитель SMS. Именно это значение будет выводиться на телефоне абонента в поле от кого SMS;
	* **text_sms** - Текст SMS;
	* **send_vk** - Отправлять ли VK сообщение. Также является порядком сортировки отправки VK сообщения (от меньшего к большему). Может принимать значение от 0 до 9, где 0 - не отправлять VK сообщение. Для открытия данного направления для вас, свяжитесь с вашим менеджером;
	* **templateId** - Идентификатор шаблона в системе. Можете посмотреть Идентификатор шаблона в личном кабинете;
	* **templateData** - Значения параметров шаблона. Шаблон должен быть согласован VK;
	* **phones** - Получатели сообщений;
		* **phone** – Номер абонента, которому адресовано сообщение. В международном формате, например, 79000000001 (Для России), 380442589632 (Для Украины) и т.д.;
		* **client_id_message** - ID сообщения на стороне клиента. Число. Необязательный параметр, позволяет избежать повторной отправки. Если раннее с этого аккаунта уже было отправлено сообщение с таким номером, то повторная отправка не производится.	

В ответ может быть выдан один из следующих JSON-документов:
### В случае возникновения ошибки в отправляемом JSON-документе

JSON:
```json
{
	"error":"текст ошибки"
}
```
PHP (массив, полученный через php функцию json_decode):
```php
array ('error' => 'текст ошибки')
```

### В случае получения правильного JSON-документа:

JSON:
```json
{
	"message":[
		[
			{"id_message":"ID сообщения в системе для проверки статуса","client_id_message":"ID сообщения на стороне клиента","phone":"Номер телефона получателя сообщения","count_message":"Количество частей в сообщении","id_viber":"ID VIBER сообщения","id_sms":"ID SMS","id_vk":"ID VK сообщения"},
			{"client_id_message":"ID сообщения на стороне клиента","phone":"Номер телефона получателя сообщения","error":"Ошибка в отправке сообщения на указанный номер"}
		],
		[
			{"id_message":"ID сообщения в системе для проверки статуса","client_id_message":"ID сообщения на стороне клиента","phone":"Номер телефона получателя сообщения","count_message":"Количество частей в сообщении","id_viber":"ID VIBER сообщения","id_sms":"ID SMS","id_vk":"ID VK сообщения"}
		],
		{"error":"Текст ошибки"}
	]
}
```
PHP (массив, полученный через php функцию json_decode):
```php
Array(
	[message] => Array(
		[0] => Array ( 
			 [0] => Array ( [id_message] => ID сообщения в системе для проверки статуса [client_id_message] => ID сообщения на стороне клиента [phone] => Номер телефона получателя сообщения [count_message] => Количество сообщений [id_viber] => ID VIBER сообщения [id_sms] => ID SMS [id_vk] => ID VK сообщения ),
			 [1] => Array ( [client_id_message] => ID сообщения на стороне клиента [phone] => Номер телефона получателя сообщения [error] => Ошибка в отправке сообщения на указанный номер )
		),
		[1] => Array ( 
			[0] => Array ( [id_message] => ID сообщения в системе для проверки статуса [client_id_message] => ID сообщения на стороне клиента [phone] => Номер телефона получателя сообщения [count_message] => Количество сообщений [id_viber] => ID VIBER сообщения [id_sms] => ID SMS [id_vk] => ID VK сообщения )
		)
		[2] => Array ( 
			[error] => Текст ошибки
		)
	)
)
```

Где:
* **message** – Сообщения;
* **id_message** - ID сообщения в системе для проверки статуса;
* **client_id_message** - ID сообщения на стороне клиента;
* **phone** – Номер абонента, которому адресовано сообщение;
* **count_message** - Количество частей сообщения. Указано количество частей сообщения в первом указанном направлении (viber, sms);
* **id_viber** - ID VIBER сообщения. 0 - если не было отправлено VIBER сообщение;
* **id_sms** - ID SMS сообщения. 0 - если не было отправлено SMS сообщение;
* **id_vk** - ID VK сообщения. 0 - если не было отправлено VK сообщение;
* **error** - Информация об ошибке, если в процессе отправки сообщения произошла ошибка.

## Получение статуса сообщения
**Адрес сервера:**
```
https://имя_хоста/sendmessagejson.php
```
**JSON-документ:**
```json
{
	"login":"login",
	"password":"password",
	"state":[
		{"id_message":"111"},
		{"id_message":"112"}
	]
}
```
**PHP-данные:**
```php
$param = array(
	'login' => 'login',
	'password' => 'password',
	'state' => array(
		array('id_message' => '111'),
		array('id_message' => '112')
	)
);
```

Где:
* **login** – Логин пользователя;
* **password** – Пароль;
* **state** - Статусы сообщений:
	* **id_message** - ID сообщения в системе.

В ответ может быть выдан один из следующих JSON-документов:
### В случае возникновения ошибки в отправляемом JSON-документе

JSON:
```json
{
	"error":"текст ошибки"
}
```
PHP (массив, полученный через php функцию json_decode):
```php
array ('error' => 'текст ошибки')
```

### В случае получения правильного JSON-документа:

JSON:
```json
{
	"state":[
		{"id_message":"ID сообщения в системе","time_change_state":"Время последней смены состояния","state":"Общий статус сообщения","state_sms":"Статус SMS","state_viber":"Статус VIBER сообщения","state_vk":"Статус VK сообщения","num_parts_sms":"Количество часте SMS сообщения","price_sms":"Цена SMS сообщение","price_viber":"Цена VIBER сообщение","price_vk":"Цена VK сообщение"},
		{"id_message":"ID сообщения в системе","time_change_state":"Время последней смены состояния","state":"Общий статус сообщения","state_sms":"Статус SMS","state_viber":"Статус VIBER сообщения","state_vk":"Статус VK сообщения","num_parts_sms":"Количество часте SMS сообщения","price_sms":"Цена SMS сообщение","price_viber":"Цена VIBER сообщение","price_vk":"Цена VK сообщение"}
	]
}
```
PHP (массив, полученный через php функцию json_decode):
```php
Array(
	[state] => Array(
		[0] => Array ( [id_message] => ID сообщения в системе [time_change_state] => Время последней смены состояния [state] => Общий статус сообщения [state_sms] => Статус SMS [state_viber] => Статус VIBER сообщения [state_vk] => Статус VK сообщения [num_parts_sms] => Количество часте SMS сообщения [price_sms] => Цена SMS сообщение сообщения [price_viber] => Цена VIBER сообщение [price_vk] => Цена VK сообщение ),
		[1] => Array ( [id_message] => ID сообщения в системе [time_change_state] => Время последней смены состояния [state] => Общий статус сообщения [state_sms] => Статус SMS [state_viber] => Статус VIBER сообщения [state_vk] => Статус VK сообщения [num_parts_sms] => Количество часте SMS сообщения [price_sms] => Цена SMS сообщение сообщения [price_viber] => Цена VIBER сообщение [price_vk] => Цена VK сообщение )
	)
)
```

Где:
* **id_message** - ID сообщения в системе;
* **time_change_state** - Время последней смены состояния, в формате: YYYY-MM-DD hh:mm:ss где, YYYY-год, MM-месяц, DD-день, hh-часы, mm-минуты, ss-секунды. Например 2017-11-23 13:15:25. Поле является пустым, если сообщение с указаным ID не обнаружено;
* **state** – Статус сообщения, может принимать следующие значения:
	* **send** - В процессе работы (не профинализировано);
	* **not_deliver** - Сообщение не было доставлено. Конечный статус (не меняется со временем);
	* **expired** - Абонент находился не в сети в те моменты, когда делалась попытка доставки. Конечный Статус (не меняется со временем);
	* **deliver** - Сообщение доставлено. Конечный статус (не меняется со временем);
	* **partly_deliver** - Сообщение было отправлено, но статус так и не был получен. Конечный статус (не меняется со временем). В этом случае для разъяснения причин отсутствия статуса необходимо связаться со службой тех. поддержки;
	* **ДРУГОЕ** - Если статус сообщения не один из указанных выше, статус означает текст ошибки например "Сообщение с таким ID не принималось";
* **state_sms** - Статус SMS, может принимать следующие значения:
	* **send** - Не было отправлено;
	* **not_deliver** - Сообщение не было доставлено. Конечный статус (не меняется со временем);
	* **expired** - Абонент находился не в сети в те моменты, когда делалась попытка доставки. Конечный Статус (не меняется со временем);
	* **deliver** - Сообщение доставлено. Конечный статус (не меняется со временем);
	* **partly_deliver** - Сообщение было отправлено, но статус так и не был получен. Конечный статус (не меняется со временем). В этом случае для разъяснения причин отсутствия статуса необходимо связаться со службой тех. поддержки;
* **state_viber** - Статус VIBER сообщения, может принимать следующие значения:
	* **send** - Не было отправлено;
	* **not_deliver** - Сообщение не было доставлено. Конечный статус (не меняется со временем);
	* **expired** - Абонент находился не в сети в те моменты, когда делалась попытка доставки. Конечный Статус (не меняется со временем);
	* **deliver** - Сообщение доставлено. Конечный статус (не меняется со временем);
	* **partly_deliver** - Сообщение было отправлено, но статус так и не был получен. Конечный статус (не меняется со временем). В этом случае для разъяснения причин отсутствия статуса необходимо связаться со службой тех. поддержки;
* **state_vk** - Статус VK сообщения, может принимать следующие значения:
	* **send** - Не было отправлено;
	* **not_deliver** - Сообщение не было доставлено. Конечный статус (не меняется со временем);
	* **expired** - Абонент находился не в сети в те моменты, когда делалась попытка доставки. Конечный Статус (не меняется со временем);
	* **deliver** - Сообщение доставлено. Конечный статус (не меняется со временем);
	* **partly_deliver** - Сообщение было отправлено, но статус так и не был получен. Конечный статус (не меняется со временем). В этом случае для разъяснения причин отсутствия статуса необходимо связаться со службой тех. поддержки;
* **num_parts_sms** - Количество частей в SMS, в случае если было отправлено SMS;
* **price_sms** - Списанные средства за SMS, в случае если было отправлено SMS.
* **price_viber** - Списанные средства за VIBER сообщение, в случае если было отправлено VIBER сообщение.
* **price_vk** - Списанные средства за VK сообщение, в случае если было отправлено VK сообщение.


# Руководство по взаимодействию с сервисом на основе XML документа, методом POST

# Общие принципы отправки
На определенный адрес сервера отправляются XML документы (описание XML документов, их назначение и адреса сервера приведены ниже). При этом используется POST метод.

Заголовки отправляемых данных должны содержать:
```
Content-type: text/xml; charset=utf-8
```
Кодировка XML документов UTF-8. Передаваемый XML документ не должен содержать переводов строки. Переводы строк в самих данных должны быть заменены на "\n".

## Пример передачи XML документа на php

```php
$src = '<?xml version="1.0" encoding="utf-8"?>
<request>
<security>
<login value="логин" />
<password value="пароль" />
</security>
</request>';
// XML-документ
$href = 'https://server/script.php'; // адрес сервера
$ch = curl_init();
curl_setopt ($ch, CURLOPT_HTTPHEADER, array ('Content-type: text/xml','charset=utf-8','Expect:'));
curl_setopt ($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt ($ch, CURLOPT_SSL_VERIFYPEER, 0);
curl_setopt ($ch, CURLOPT_SSL_VERIFYHOST, 0);
curl_setopt ($ch, CURLOPT_CRLF, true);
curl_setopt ($ch, CURLOPT_POST, true);
curl_setopt ($ch, CURLOPT_POSTFIELDS, $src);
curl_setopt ($ch, CURLOPT_URL, $href);
$result = curl_exec($ch);
curl_close($ch);
echo $result;
```

## Отправка сообщения
**Адрес сервера:**
```
https://имя_хоста/xml/message.php
```
**XML-документ:**
```xml
<?xml version="1.0" encoding="utf-8" ?>
<request>
<security>
	<login value="логин" />
	<password value="пароль" />
</security>
<message>
	<send_viber>1</send_viber>
	<send_vk>2</send_vk>
	<send_sms>3</send_sms>
	<name_delivery>НАЗВАНИЕ_РАССЫЛКИ</name_delivery>
	<time_send>ВРЕМЯ_ОТПРАВКИ</time_send>
	<sender_viber>ИМЯ_ОТПРАВИТЕЛЯ_ВАЙБЕР</sender_viber>
	<text_viber>ТЕКСТ_ВАЙБЕР</text_viber>
	<button_text>ТЕКСТ_КНОПКИ</button_text>
	<button_url>ССЫЛКА_КНОПКИ</button_url>
	<image_url>ИЗОБРАЖЕНИЕ</image_url>
	<validity_period_viber>ВРЕМЯ_ЖИЗНИ_ВАЙБЕР_СООБЩЕНИЯ</validity_period_viber>
	<finale_viber_read>1</finale_viber_read>
	<sender_sms>ИМЯ_ОТПРАВИТЕЛЯ_СМС</sender_sms>
	<text_sms>ТЕКСТ_СМС</text_sms>
	<templateId>100</templateId>
	<templateData>
		<Name>Имя</Name>
		<Where>Москва</Where>
	</templateData>
	<abonent phone="79801234567" client_id_message="111" />
	<abonent phone="79800000001" client_id_message="112" />
</message>
<message>
    <send_viber>1</send_viber>
	<name_delivery>НАЗВАНИЕ_РАССЫЛКИ_2</name_delivery>
	<sender_viber>ИМЯ_ОТПРАВИТЕЛЯ_ВАЙБЕР_2</sender_viber>
	<text_viber>ТЕКСТ_ВАЙБЕР_2</text_viber>
	<abonent phone="79800000002" client_id_message="113" />
</message>
<message>
    <name_delivery>НАЗВАНИЕ_РАССЫЛКИ_3</name_delivery>
	<sender_viber>ИМЯ_ОТПРАВИТЕЛЯ_ВАЙБЕР_3</sender_viber>
	<text_viber>ТЕКСТ_ВАЙБЕР_3</text_viber>
	<abonent phone="79800000003" />
</message>
</request>
```

Где:
* **login** – Логин пользователя;
* **password** – Пароль;
* **message** – Сообщения;
	* **name_delivery** – Название рассылки. Если поле является пустым, по умолчанию - "Шлюз";
	* **time_send** – Желательное время отправки сообщения, в формате: YYYY-MM-DD hh:mm где, YYYY-год, MM-месяц, DD-день, hh-часы, mm-минуты. Например 2017-11-23 13:00. Если поле является пустым, то отправка сообщения происходит сразу;
	* **send_viber** – Отправлять ли VIBER сообщение. Также является порядком сортировки отправки VIBER сообщения (от меньшего к большему). Может принимать значение от 0 до 9, где 0 - не отправлять VIBER сообщение;
	* **sender_viber** – Имя отправителя VIBER. Именно это значение будет выводиться на телефоне абонента в поле от кого сообщение;
	* **text_viber** – Текст VIBER сообщения. Не должен превышать более 1000 символов. Обязательный параметр;
	* **button_text** – Текст кнопки. Не более 19 символов. Необязательный параметр. При добавлении, обязательно чтоб была указана ссылка кнопки в параметре button_url;
	* **button_url** – Ссылка кнопки. Необязательный параметр. При добавлении, обязательно чтоб было указано название кнопки в параметре button_text;
	* **image_url** – Ссылка на изображение. Необязательный параметр. В случае добавления изображения, также необходимо наличие кнопки (button_text и button_url);
	* **validity_period_viber** – Время жизни VIBER сообщения. За этот период, система делает попытки доставить сообщение абоненту. Если за указанный период не будет доставлено сообщение, оно профинализируется со статусом просрочено либо не доставлено. Необязательный параметр. Указывается в минутах, например "60" - что значит 1 час. Если не указано, по умолчанию будет "60";
	* **finale_viber_read** – Считать финальным доставленным VIBER сообщением статус "прочитано". В системе VIBER существуют статусы как доставлено и прочитано. В случае если в данном поле указали "1", то в VIBER сообщении, в котором фигурирует статус доставлено, но не прочитано, по истечению время жизни VIBER сообщения - будет попытка переотправки сообщения по другой системе (например через SMS), если в самом XML запросе фигурирует каскадная отправка (send_viber и send_sms);
	* **send_sms** – Отправлять ли SMS. Также является порядком сортировки отправки SMS (от меньшего к большему). Может принимать значение от 0 до 9, где 0 - не отправлять SMS;
	* **sender_sms** - Отправитель SMS. Именно это значение будет выводиться на телефоне абонента в поле от кого SMS;
	* **text_sms** - Текст SMS;
	* **send_vk** - Отправлять ли VK сообщение. Также является порядком сортировки отправки VK сообщения (от меньшего к большему). Может принимать значение от 0 до 9, где 0 - не отправлять VK сообщение. Для открытия данного направления для вас, свяжитесь с вашим менеджером;
	* **templateId** - Идентификатор шаблона в системе. Можете посмотреть Идентификатор шаблона в личном кабинете;
	* **templateData** - Значения параметров шаблона. Шаблон должен быть согласован VK;
	* **abonent** - Получатели сообщений;
		* **phone** – Номер абонента, которому адресовано сообщение. В международном формате, например, 79000000001 (Для России), 380442589632 (Для Украины) и т.д.;
		* **client_id_message** - ID сообщения на стороне клиента. Число. Необязательный параметр, позволяет избежать повторной отправки. Если раннее с этого аккаунта уже было отправлено сообщение с таким номером, то повторная отправка не производится.
		
В ответ может быть выдан один из следующих XML-документов:
### В случае возникновения ошибки в отправляемом XML-документе

```xml
<?xml version="1.0" encoding="utf-8"?>
<response>
	<error>текст ошибки</error>
</response>
```
**error** - Текст ошибки.

### В случае получения правильного XML-документа

```xml
<?xml version="1.0" encoding="utf-8" ?>
<response>
<message>
	<information id_message="ID сообщения в системе для проверки статуса" client_id_message="ID сообщения на стороне клиента" id_sms="ID SMS" id_viber="ID VIBER сообщения" id_vk="ID VK сообщения" phone="Номер телефона получателя сообщения">Статус/сообщение об ошибке</information>
	<information client_id_message="ID сообщения на стороне клиента" phone="Номер телефона получателя сообщения">Статус/сообщение об ошибке</information>
</message>
<message>
	<information id_message="ID сообщения в системе для проверки статуса" client_id_message="ID сообщения на стороне клиента" id_sms="ID SMS" id_viber="ID VIBER сообщения" id_vk="ID VK сообщения" phone="Номер телефона получателя сообщения">Статус/сообщение об ошибке</information>
</message>
<message>
	<error>Текст ошибки</error>
</message>
</response>
```

Где:
* **message** – Сообщения;
* **id_message** - ID сообщения в системе для проверки статуса;
* **client_id_message** - ID сообщения на стороне клиента;
* **phone** – Номер абонента, которому адресовано сообщение;
* **count_message** - Количество частей сообщения. Указано количество частей сообщения в первом указанном направлении (viber, sms);
* **id_viber** - ID VIBER сообщения. 0 - если не было отправлено VIBER сообщение;
* **id_vk** - ID VK сообщения. 0 - если не было отправлено VK сообщение;
* **id_sms** - ID SMS сообщения. 0 - если не было отправлено SMS сообщение;
* **error** - Информация об ошибке, если в процессе отправки сообщения произошла ошибка.

## Получение статуса сообщения
**Адрес сервера:**
```
https://имя_хоста/xml/state_message.php
```
**XML-документ:**

```xml
<?xml version="1.0" encoding="utf-8" ?>
<request>
<security>
	<login value="логин" />
	<password value="пароль" />
</security>
<state>
	<id_message>111</id_message>
	<id_message>112</id_message>
	<id_message>113</id_message>
</state>
</request>
```

Где
* **login** - ваш логин в системе.
* **password** - ваш пароль в системе.
* **id_message** - ID сообщения в системе.

В ответ может быть выдан один из следующих XML-документов:
### В случае возникновения ошибки в отправляемом XML-документе:

```xml
<?xml version="1.0" encoding="utf-8"?>
<response>
	<error>текст ошибки</error>
</response>
```
**error** - Текст ошибки.

### В случае получения правильного XML-документа:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<response>
	<state id_message="ID сообщения в системе" time_change_state="Время последней смены состояния" state_sms="Статус SMS" state_viber="Статус VIBER сообщения" state_vk="Статус VK сообщения" num_parts_sms="Количество часте SMS сообщения" price_sms="Цена SMS сообщение" price_viber="Цена VIBER сообщение" price_vk="Цена VK сообщение">Статус</state>
	<state id_message="ID сообщения в системе" time_change_state="Время последней смены состояния" state_sms="Статус SMS" state_viber="Статус VIBER сообщения" state_vk="Статус VK сообщения" num_parts_sms="Количество часте SMS сообщения" price_sms="Цена SMS сообщение" price_viber="Цена VIBER сообщение" price_vk="Цена VK сообщение">Статус</state>
	<state id_message="ID сообщения в системе" time_change_state="Время последней смены состояния" state_sms="Статус SMS" state_viber="Статус VIBER сообщения" state_vk="Статус VK сообщения" num_parts_sms="Количество часте SMS сообщения" price_sms="Цена SMS сообщение" price_viber="Цена VIBER сообщение" price_vk="Цена VK сообщение">Статус</state>
</response>
```

Где:
* **id_message** - ID сообщения в системе;
* **time_change_state** - Время последней смены состояния, в формате: YYYY-MM-DD hh:mm:ss где, YYYY-год, MM-месяц, DD-день, hh-часы, mm-минуты, ss-секунды. Например 2017-11-23 13:15:25. Поле является пустым, если сообщение с указаным ID не обнаружено;
* **Статус** – Статус сообщения, может принимать следующие значения:
	* **send** - В процессе работы (не профинализировано);
	* **not_deliver** - Сообщение не было доставлено. Конечный статус (не меняется со временем);
	* **expired** - Абонент находился не в сети в те моменты, когда делалась попытка доставки. Конечный Статус (не меняется со временем);
	* **deliver** - Сообщение доставлено. Конечный статус (не меняется со временем);
	* **partly_deliver** - Сообщение было отправлено, но статус так и не был получен. Конечный статус (не меняется со временем). В этом случае для разъяснения причин отсутствия статуса необходимо связаться со службой тех. поддержки;
	* **ДРУГОЕ** - Если статус сообщения не один из указанных выше, статус означает текст ошибки например "Сообщение с таким ID не принималось";
* **state_sms** - Статус SMS, может принимать следующие значения:
	* **send** - Не было отправлено;
	* **not_deliver** - Сообщение не было доставлено. Конечный статус (не меняется со временем);
	* **expired** - Абонент находился не в сети в те моменты, когда делалась попытка доставки. Конечный Статус (не меняется со временем);
	* **deliver** - Сообщение доставлено. Конечный статус (не меняется со временем);
	* **partly_deliver** - Сообщение было отправлено, но статус так и не был получен. Конечный статус (не меняется со временем). В этом случае для разъяснения причин отсутствия статуса необходимо связаться со службой тех. поддержки;
* **state_viber** - Статус VIBER сообщения, может принимать следующие значения:
	* **send** - Не было отправлено;
	* **not_deliver** - Сообщение не было доставлено. Конечный статус (не меняется со временем);
	* **expired** - Абонент находился не в сети в те моменты, когда делалась попытка доставки. Конечный Статус (не меняется со временем);
	* **deliver** - Сообщение доставлено. Конечный статус (не меняется со временем);
	* **partly_deliver** - Сообщение было отправлено, но статус так и не был получен. Конечный статус (не меняется со временем). В этом случае для разъяснения причин отсутствия статуса необходимо связаться со службой тех. поддержки;
* **state_vk** - Статус VK сообщения, может принимать следующие значения:
	* **send** - Не было отправлено;
	* **not_deliver** - Сообщение не было доставлено. Конечный статус (не меняется со временем);
	* **expired** - Абонент находился не в сети в те моменты, когда делалась попытка доставки. Конечный Статус (не меняется со временем);
	* **deliver** - Сообщение доставлено. Конечный статус (не меняется со временем);
	* **partly_deliver** - Сообщение было отправлено, но статус так и не был получен. Конечный статус (не меняется со временем). В этом случае для разъяснения причин отсутствия статуса необходимо связаться со службой тех. поддержки;
* **num_parts_sms** - Количество частей в SMS, в случае если было отправлено SMS;
* **price_sms** - Списанные средства за SMS, в случае если было отправлено SMS.
* **price_viber** - Списанные средства за VIBER сообщение, в случае если было отправлено VIBER сообщение.
* **price_vk** - Списанные средства за VK сообщение, в случае если было отправлено VK сообщение.
