# cloud_wordpress

# CloudPayments модуль для Wordpress eCommerce
Модуль позволит с легкостью добавить на ваш сайт оплату банковскими картами через платежный сервис CloudPayments. 
Для корректной работы модуля необходима регистрация в сервисе и установленный плагин WP eCommerce


### Возможности:  
• Одностадийная схема оплаты;   
• Возврат платежей из ЛК CMS;    
• Отправка чеков по email;

### Ручная установка

1.	Копируем архив с github
2.	В папку плагинов Wordpress /wp-content/plugins копируем все содержимое из архивной папки wordpress_cloudpayments 
3.	Итого в /wp-content/plugins должна быть папка cloudpayments_pay со всем содержимым.
4.	Далее переходим в раздел установки плагинов в административной части Wordpress и активируем наш плагин
![0](http://cloud2.web-sputnik.com/git/img1.png)
5. Чтобы модуль корректно работал, нужно внести ряд изменений в настройки модуля, а также настроить работу вебхуков в личном кабинете - https://merchant.cloudpayments.ru/Account/Login. Настройки модуля и настройки вебхуков описаны ниже.


### Настройка модуля

1.	Все настройки платежной системы находятся в модуле ECommerce. По адресу /wp-admin/options-general.php?page=wpsc-settings. "Настройки -> Магазин -> Платежи".
![0](http://cloud2.web-sputnik.com/git/img2.png)
2.	Далее выбираем из списка платежную систему "Cloudpayments" и переходим в настройки
![0](http://cloud2.web-sputnik.com/git/img3.png)
Заполняем:
- «Public ID»
- «Пароль для API», и выбираем «Тип схемы проведения платежей»
- Указываем корректный ИНН
Остальные параметры заполняем на свое усмотрение. 


### Описание параметров модуля:
- **Отображаемое имя** - имя платежной системы на сайте. То имя, что будет отображаться в оформление заказа.
- **Тестовый режим** - включение режима тестирования. Напоминаю, что он также должен быть включен на стороне Cloudpayments.
- **Transaction url** - Url успешного оформления заказа, с session_id в параметрах, где sessionid=#SESSION_ID# обязательный GET параметр
- **Кодировка текста** - кодировка всего текста модуля. По умолчанию стоит utf-8, можно сменить на CP1251.
- **Использовать функционал формирования чеков** - формирование и отправка чеков оплаты на email. 
- **Статус возврата платежа** - в этом пункте выбирается какой статус заказа, отвечает за возврат платежа. Т.е. выбрав указанный в этом пункте статус, в заказе, будет выполнена функция возврата платежа через API cloudpayments.
- **Success URL** - url на который будет переадресован пользователь после успешной оплаты заказа.
- **Fail URL** - url на который будет переадресован пользователь после неудачно оплаты заказа.
- **Язык модуля** - язык отображения текста в данных настройках
- **Язык виджета** - список доступных языков виджета оплаты заказа, который появляется когда пользователь нажимает кнопку "оплатить".


### Настройка вебхуков:

Для корректной работы модуля, а именно подтверждения оплаты и прочих действий, нужно прописать правильные url в настройках вебхуков. 
Так как  настройка ЧПУ(Семантический URL) может быть отличной от параметра по умолчаню, то для корректной настройки вебхуков лучше всего будет использовать след. способ:
Для настройки вебхуков:
1) Авторизуемся в личном кабинете по ссылке https://merchant.cloudpayments.ru/Account/Login
2) Переходим в "Сайты"  
![0](http://cloud.websputnik.su/git/img4.png)
3) Добавляем свой сайт, если еще не добавили и переходим в настройки
![0](http://cloud.websputnik.su/git/img5.png)
3) Далее жмем еще раз настройки
![0](http://cloud.websputnik.su/git/img6.png)

Напротив каждого хука копируем линк ниже для соответсвующего вебхука:

* (Check) 		#SITE_URL#h?action=check
* (Fail) 		#SITE_URL#?action=fail
* (Pay) 		#SITE_URL#?action=pay
* (Refund)		#SITE_URL#?action=refund

Где #SITE_URL# - адрес сайта. Например: http://domain.ru

### Отмена оплаченного заказа

Чтобы отменить оплаченный заказ. Нужно перейти в редактирование заказа и в статусе заказа выбрать статус выбранный в настройках модуля
![0](http://cloud.websputnik.su/git/img7.png)

После чего будет отправлен refund запрос на отмену оплаты. Также отмена оплаты будет произведена автоматически, если будет отменен или удален заказ в ЛК сайта или в редактирование заказа. 
