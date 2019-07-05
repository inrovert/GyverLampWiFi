![PROJECT_PHOTO](https://github.com/vvip-68/GyverLampWiFi/blob/master/proj_img.jpg)
# Крутая WiFi лампа на esp8266 своими руками
* [Описание проекта](#chapter-0)
* [Папки проекта](#chapter-1)
* [Схемы подключения](#chapter-2)
* [Материалы и компоненты](#chapter-3)
* [Как скачать и прошить](#chapter-4)
* [FAQ](#chapter-5)
* [Полезная информация](#chapter-6)

<a id="chapter-0"></a>
## Описание проекта
Этот проект основан на проекте AlexGyver ["Матрица на адресных светодиодах с управлением по Bluetooth"](https://github.com/AlexGyver/GyverMatrixBT)
с реализацией функционала проекта ["Крутая WiFi лампа на esp8266 своими руками"](https://github.com/AlexGyver/GyverLamp)
и его дальнейшем развитии.

## Описание проекта
Представляю вашему вниманию светильник на адресных светодиодах с кучей эффектов, управлением по Wi-Fi и функцией будильник-рассвет!
### Железо
- Проект собран на базе микроконтроллера ESP8266 в лице платы NodeMCU или Wemos D1 mini (неважно, какую из этих плат использовать!).
- Вместо адресной ленты используется гибкая адресная матрица 16×16, что выходит дешевле ленты (матрица 16×16 стоит 1500р, она состоит из 256 диодов с плотностью 100 штук на метр. 
  Лента такой же плотности стоит 1000р за метр (за 100 светодиодов). Для склейки матрицы размером 16×16 понадобится 2.5 метра ленты, то есть 2500р. А готовая матрица стоит на 1000р дешевле!).
- Система управляется со смартфона по Wi-Fi, а также “оффлайн” с кнопки на корпусе (сенсорная кнопка на TTP223).

### Фишки
- 23 крутых эффектов
- Настройка скорости и “масштаба” для каждого эффекта со смартфона
- Работа системы как в локальной сети, так и в режиме “точки доступа”
- Система получает точное время из Интернета
- Управление кнопкой: смена режима, настройка яркости, вкл/выкл, отображение текущего
- Режим будильник-рассвет: менеджер будильников на неделю в приложении

### Корпус
- Корпус выглядит очень презентабельно, несмотря на простоту и доступность материалов
- Рассеиватель – матовый плафон из Леруа Мерлен
- Остальные элементы корпуса – канализационные трубы, в лучших традициях жанра!
- Страница проекта на сайте: https://alexgyver.ru/GyverLamp/

### Изменения функционала лампы по справнению с исходным пректом:
 - Адаптированная программа управления лампой на Andrioid
 - Настройка сервера синхронизации времени из программы на смартфоне 
 - Установка текущего времени со смартфона фручную, если не удалось подключиться к серверу времени NTP
 - Поддержка звука будильника / звука рассвета звуковой платой MP3 DFPlayer
 - Отображение текущего времени на индикаторе TM1637
 - Два режима работы индикатора времени TM1637 - светится постоянно или выключается вместе с лампой
 - Настройки сетевого подключения (SSID и пароль, статический IP) задаются в программе и сохраняются в EEPROM
 - Если не удается подключиться к сети (неверный пароль или имя сети) - создается точка подключения
   с именем LampAP, пароль 12341234, IP 192.168.4.1. Подключившись к точке доступа из приложения
   можно настроить параметры сети. Если после задания параметиров сети WiFi соединение установлено - 
   в приложении на смартфоне виден IP адрес подключения к сети WiFi.  
 - Отображение текущего IP адреса лампы на индикаторе TM1637
 - Быстрое включение популярных режимов лампы из приложения
 - Два программируемых по времени режима, позволяющие, например, настроить автоматическое выключение лампы в ночное время и автоматическое же включение вечером.

#### Эффекты:
 - Лампа белого или другого заданного цвета
 - Снегопад
 - Блуждающий кубик
 - Радуга (горизонтальная, вертикальная, диагональная)
 - Огонь
 - The Matrix
 - Конфетти
 - Звездопад
 - Шумовые эффекты с разными цветовыми палитрами
 - Плавная смена цвета лампы
 - Светлячки

#### Возможности:
- Автоподключение к лампе при запуске
- Настройки яркости лампы из программы или сенсорной кнопкой

### Кнопка управления режимами, последовательность переключения:
#### Будильник сработал, идет рассвет или мелодия пробуждения
- Любое нажатие кнопки отключает будильник
#### Долгое удержание кнопки 
- Плавное изменение яркости
#### Однократное нажатие кнопки
- Включение / выключение лампы
#### Двухкратное нажатие кнопки
- Ручной переход к следующему режиму
#### Трехкратное нажатие кнопки
- Включается демо-режим с автоматической сменой режима по циклу
#### Четырехкратное нажатие кнопки
- На индикаторе TM1637 отображается IP адрес лампы, если подключение к локальной WiFi сети установлено

<a id="chapter-1"></a>
## Папки
**ВНИМАНИЕ! Если это твой первый опыт работы с Arduino, читай [инструкцию](#chapter-4)**
- **libraries** - библиотеки проекта.
- **firmware** - прошивки
- **schemes** - схемы подключения компонентов
- **sounds** - звуковые файлы будильника для размещения на SD-карте
- **Android** - файлы с приложениями, примерами для Android и Thunkable
- **3D_print** - файлы для печати корпуса лампы на 3D принтере

<a id="chapter-2"></a>
## Схемы
![SCHEME](https://github.com/vvip-68/GyverMatrixWiFi/blob/master/schemes/scheme.jpg)

<a id="chapter-3"></a>
## Материалы и компоненты
### Ссылки оставлены на магазины
Полный список компонентов есть в статье https://alexgyver.ru/matrix_guide/
- NodeMCU http://ali.ski/RgD5P  http://ali.ski/_1FJZ
- Wemos D1 mini http://ali.ski/FuTgbO  http://ali.ski/Z9feWU
- Матрица 16x16 http://ali.ski/BCKQT  http://ali.ski/bRW14  http://ali.ski/X-tBrQ
- Адресная лента (для DIY матрицы) http://ali.ski/2dmOe_  http://ali.ski/rqgqdq  http://ali.ski/4Ma9iH
- Сенсорная кнопка http://ali.ski/aWQBAa  http://ali.ski/rsOrSB
- Резисторы http://ali.ski/UEez2
- БП 5V (брать 3A минимум) http://ali.ski/K-CThT  http://ali.ski/3UWXJ
- MP3 DFPlayer http://ali.onl/1gY1 http://ali.onl/1gY3
- Динамики http://ali.onl/1h3u http://ali.onl/1h3v
- Проводочки http://ali.ski/JQRler  http://ali.ski/_SuCF
- Плафон https://leroymerlin.ru/product/plafon-cilindr-18212968/

## Вам скорее всего пригодится
* [Всё для пайки (паяльники и примочки)](http://alexgyver.ru/all-for-soldering/)
* [Недорогие инструменты](http://alexgyver.ru/my_instruments/)
* [Все существующие модули и сенсоры Arduino](http://alexgyver.ru/arduino_shop/)
* [Электронные компоненты](http://alexgyver.ru/electronics/)
* [Аккумуляторы и зарядные модули](http://alexgyver.ru/18650/)

<a id="chapter-4"></a>
## Как скачать и прошить
* [Первые шаги с Arduino](http://alexgyver.ru/arduino-first/) - ультра подробная статья по началу работы с Ардуино, ознакомиться первым делом!
* Скачать архив с проектом
> На главной странице проекта (где ты читаешь этот текст) вверху справа зелёная кнопка **Clone or download**, вот её жми, там будет **Download ZIP**
* Установить библиотеки в  
`C:\Program Files (x86)\Arduino\libraries\` (Windows x64)  
`C:\Program Files\Arduino\libraries\` (Windows x86)
* **Подключить внешнее питание 5 Вольт**
* Подключить Ардуино к компьютеру
* Запустить файл прошивки (который имеет расширение .ino)
* Настроить IDE (COM порт, модель Arduino, как в статье выше)
* Настроить что нужно по проекту
* Нажать загрузить
* Скачать и установить на смартфон GyverMatrix
* Пользоваться  

## Важно
Если проект не собирается (ошибки компиляции) или собирается, но работает неправильно (например вся матрица светится белым и ничего не происходит) - проверьте версии библиотек. Данный проект рассчитан на работу с версииями библиотек поддержки плат ESP версии 2.5.2 и библиотеки FastLED версии 3.2.9;

<a id="chapter-5"></a>
## FAQ
### Основные вопросы
В: Как скачать с этого грёбаного сайта?  
О: На главной странице проекта (где ты читаешь этот текст) вверху справа зелёная кнопка **Clone or download**, вот её жми, там будет **Download ZIP**

В: Скачался какой то файл .zip, куда его теперь?  
О: Это архив. Можно открыть стандартными средствами Windows, но думаю у всех на компьютере установлен WinRAR, архив нужно правой кнопкой и извлечь.

В: Я совсем новичок! Что мне делать с Ардуиной, где взять все программы?  
О: Читай и смотри видос http://alexgyver.ru/arduino-first/

В: Вылетает ошибка загрузки / компиляции!   
О: Читай тут: https://alexgyver.ru/arduino-first/#step-5

### Вопросы по этому проекту

В: Эй чувак! У тебя проект не компилится. Ты файл DFRobotDFPlayerMini.h в проект забыл включить. Выложи!   
О: Это стандартная библиотека для MP3 DFPlayer. Идите в менеджер библиотек и установите ее. Или скачайте с [сайта производителя](https://github.com/DFRobot/DFRobotDFPlayerMini)

В: Собрал, использую NodeMCU. Ничего не работает! Мигает один или несколько светодиодов в начале матрицы. И всё.   
О: NodeMCU v3 чрезвычайно требователен к источнику питания. Ему на вход VIN нужно подавать напряжение в диапазоне 4.7-5 вольт. И не более. Описанные эффекты возникают даже при питании в 5.25 (а тем более - 5.45) вольт. Для проверки - не подключайте +5 вольт от блока питания к NodeMCU совсем, питание подавайте на матрицу непосредственно. Землю NodeMCU и ленты соедините. Подключите сигнальный пин NodeMCU ко входу DIN ленты. Подключите NodeMCU к компьютеру через USB (питание будет поступать отсюда). Должно заработать. Далее регулируйте выходное напряжение своего блока питания.

В: Не компилируется. Выбрана плата "голая ESP8266-12E". Сообщение об ошибке: "D4 was not declared in this scope."   
О: Очевидно производители библиотеки для "голой ESP8266-12E" не определили данную константу. Используйте всесто константы D4 числовое определение пина для вашей платы или выполните компиляцию проекта для плат NodeMCU или WeMos D1 R2.

В: Не компилируется. В сообщении об ошибке содержатся сведения о дублирующихся библиотеках.    
О: В вашей среде установлено две версии одной и той же библиотеки. Обычно это библиотека FastLED - одна версия находится в папке установки среды Ардуино (например в "C:\Program Files (x86)\Arduino\libraries\"), другая - в папке документов пользователя (например "C:\Users\vvip-68\Documents\Arduino\libraries\"). Удалите одну из версий библиотек и попробуйте скомпилировать снова.

В: Не компилируется. В сообщении об ошибке что-то про несоответствие типов.   
О: Обычно такая ситуация возникает в двух случаях:
- выбрана неверная плата. Используйте NodeMCU 1.0 (ESP-12E Module) или Wemos D1 R1. Под эти платы проект собирается, под другие, возможно, нужна модификация кода.
- установлена устаревшая версия библиотек поддержки плат - например для ESP8266 версия библиотеки 2.4.2. Данный проект использует библиотеки для плат ESP8266 версии 2.5. Обновите библиотеки поддержки плат.

<a id="chapter-6"></a>
## Полезная информация
* [Cайт Alex Gyver](http://alexgyver.ru/)
* [Канал Alex Gyver на YouTube](https://www.youtube.com/channel/UCgtAOyEQdAyjvm9ATCi_Aig?sub_confirmation=1)
* [YouTube канал про Arduino](https://www.youtube.com/channel/UC4axiS76D784-ofoTdo5zOA?sub_confirmation=1)
* [Видеоуроки по пайке](https://www.youtube.com/playlist?list=PLOT_HeyBraBuMIwfSYu7kCKXxQGsUKcqR)
* [Видеоуроки по Arduino](http://alexgyver.ru/arduino_lessons/)