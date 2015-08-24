# Telegram-Webcam-Home-Guard
Telegram Bot for home monitoring (via web-camera)


#Что это такое
Телеграм бот, который присылает вам фотографии с веб-камеры, если кто-то залез к вам в дом или квартиру.<br>

<table><tr><td>
<img width="250" src="https://habrastorage.org/files/ca8/9f0/633/ca89f063376c4fc7aa3377b85a1d89af.jpg"/>
</td><td>

#Вам понадобится
1) Веб-камера<br>
2) Домашний сервер (я использовал Raspberry Pi) с доступом в интернет<br>
<br>
</td></tr></table>

#Подготовка
<br>
1) Установите пакет «<b>motion</b>» (у меня Ubuntu Server: sudo apt-get install motion)<br>
2) Отконфигурируйте <b>/etc/motion/motion.conf</b> (мой конфигурационный файл приложен)<br>
3) Добавьте демона в автозагрузку ОС (допишите в rc.local «motion» перед «exit 0»)<br>
4) Создайте нового Telegram бота
4.1) Добавьте пользователя <b>@BotFather</b>
4.2) Используйте команду «<b>/newbot</b>» для создания нового бота
4.3) Используйте команду «<b>/setcommands</b>» для устанвки выпадающего списка команд. Список команд:

<pre>
start - начать наблюдение
stop - прекратить наблюдение
reboot - перезапустить сервер
</pre>

5) Полученный API Token впишите в файл <b>config.php</b><br>
6) Там же в <b>config.php</b> укажите пароль для доступа к системе (придумайте сами)<br>
7) Корневую папку проекта (заметьте, что при конфигурировании motion вы должны выбрать эту же папку (+/new) для сохранения фотографий. У меня это  «<b>/var/www/sweethome</b>», соответсвенно motion пишет файлы в «<b>/var/www/sweethome/new</b>»<br>
8) Залейте все на сервер<br>
9) Добавьте <b>server.php</b> и <b>monitor.php</b> в crontab на «раз-в-минуту» (на всякий случай, если сервер заглохнет). Единовременно будет работать только одна копия скрипта. <br>

<pre>
* * * * * /usr/bin/php5 /var/www/sweethome/server.php
* * * * * /usr/bin/php5 /var/www/sweethome/monitor.php
</pre>

10) Добавьте бота себе в телеграм. Используйте /start /stop для вкл/выкл режима наблюдения.<br>
11) Как только кто-то попадет в поле камеры - вам в телеграм придет фотка нарушителя<br>
<br><br>

Если совсем ничего не получатеся, но очень хочется - пишите (<a href="https://telegram.me/surzhikov">https://telegram.me/surzhikov</a>).<br>
