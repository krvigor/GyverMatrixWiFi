![PROJECT_PHOTO](https://github.com/vvip-68/GyverMatrixWiFi/blob/master/proj_img.jpg)

# Адресная матрица на NodeMCU с управлением по WiFi
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
#### Изменения по справнению с исходным проектом:
 - Поддержка только контроллера с большим объемом памятии наличием WiFi на борту - NodeMCU, Wemos D1 
 - Другие типы контроллеров (типа Arduino Mega + WiFi) - не тестировались.
 - Удалена поддержка управления с кнопок
 - Оставлена одна кнопка управления для переключения режимов, отключения работающего будильника
 - Удалена поддержка управления по Bluetooth
 - Удалена поддержка платы часов реального времени
 - Управление матрицей - через WiFi (локальная сеть)
 - Синхронизация времени с NTP сервером через интернет
 - Адаптированная программа управления матрицей на Andrioid
 - Изменены настройки режимов воспроизведения эффектов
 - Настройки режимов можно изменять из программы со смартфона
   - Яркость матрицы - единая для всех режимов
   - Скорость эффектов - индивидуально для каждого режима
   - Наличие наложения часов на эффекты - индивидуально для каждого режима
   - Включение/исключение режима из списка любимых режимов
 - Настройки сохраняются в энергонезависимой памяти EEPROM
 - К режиму часов добавлен календарь - кратковременное отображение текущей даты поверх эффекта
 - Настройка сервера синхронизации времени
 - Будильник "рассвет", настройки через программу на смартфоне, 7 будильников на каждый день
 - Поддержка звука будильника  / звука рассвета звуковой платой MP3 DFPlayer
 - Настройки сетевого подключения (SSID и пароль, статический IP) задаются в программе и сохраняются в EEPROM
 - Если не удается подключиться к сети (неверный пароль или имя сети) - создается точка подключения
   с именем MatrixAP, пароль 12341234, IP 192.168.4.1. Подключившись к точке доступа из приложения
   можно настроить параметры сети. Если после задания параметиров сети WiFi соединение установлено - 
   в приложении на смартфоне виден IP адрес подключения к сети WiFi.  
 - Быстрое включение режимов лампы белого или заданного цвета из приложения (вся панель светится), 
   выключение панели, комбинация лампы с отображением часов, ночные часы (пониженная яркость).
 - Автоматическая установка яркости матрицы в зависимости от уровня внешней освещенности.
 - Два программируемых по времени режима, позволяющие, например, настроить автоматическое выключение экрана матрицы в ночное время и автоматическое же включение матрицы утром.

## От исходного проекта сохранены следующие возможности:
#### Режимы:
 - Рисование
 - Загрузка картинок
 - Бегущая строка  
#### Эффекты:
 - Снегопад
 - Блуждающий кубик
 - Радуга
 - Огонь
 - The Matrix
 - Летающие частицы
 - Звездопад
 - Пейнтбол
 - Водоворот
 - Шумовые эффекты с разными цветовыми палитрами
 - Анимация
 - Часы  
#### Игры:
 - Змейка
 - Tетриc
 - Лабиринт  
 - Арканоид
 - Runner
#### Возможности:
- Автоподключение к матрице при запуске
- Настройки яркости и скорости отображения
- Использование акселерометра в играх

### Кнопка управления режимами, последовательность переключения:
#### Будильник сработал, идет рассвет или мелодия пробуждения
- Любое нажатие кнопки отключает будильник
#### Долгое удержание кнопки (более 3 секунд)
- Если матрица включена, она будет выключена (черный экран)
- Если матрица выключена (черный экран) - включается режим часов
#### Однократное нажатие кнопки
- Если матрица включена в режиме часов, происходит переключение часов по циклу:
  - Часы на черном фоне
  - Часы на фоне огня (камин)
  - Ночные часы
- Если матрица включена в режим лампы (белый экран) - вкл / выкл отображения часов.
- Если работают демо-режимы -  переход к следующему режиму
#### Двухкратное нажатие кнопки
- Из любого режима включается режим часов на черном фоне
- Из режима часов переключается в режим лампы
#### Трехкратное нажатие кнопки
- Включается демо-режим
#### Четырехкратное нажатие кнопки
- На экране матрицы в режиме бегущей строки отображается IP адрес матрицы, если подключение к локальной WiFi сети установлено

<a id="chapter-1"></a>
## Папки
**ВНИМАНИЕ! Если это твой первый опыт работы с Arduino, читай [инструкцию](#chapter-4)**
- **libraries** - библиотеки проекта.
- **firmware** - прошивки для NodeMCU
- **schemes** - схемы подключения компонентов
- **sounds** - звуковые файлы будильника для размещения на SD-карте
- **Android** - файлы с приложениями, примерами для Android и Thunkable
- **image decoding** - папка с инструментами для загрузки картинок и гифок

<a id="chapter-2"></a>
## Схемы
![SCHEME](https://github.com/vvip-68/GyverMatrixWiFi/blob/master/schemes/scheme.jpg)

<a id="chapter-3"></a>
## Материалы и компоненты
### Ссылки оставлены на магазины
Полный список компонентов есть в статье https://alexgyver.ru/matrix_guide/
- NodeMCU http://ali.onl/1dVU http://ali.onl/1dVV
- Матрицы разные http://ali.ski/pw2ic
- Лента http://ali.ski/YdfMN
- Модульная гирлянда http://ali.ski/0h35RR
- Резисторы http://ali.ski/UEez2
- БП 5 Вольт http://ali.ski/3cNyj  http://ali.ski/qSKFK
- MP3 DFPlayer http://ali.onl/1gY1 http://ali.onl/1gY3
- Динамики http://ali.onl/1h3u http://ali.onl/1h3v

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

**Подробная инструкция [тут](https://github.com/vvip-68/GyverMatrixWiFi/wiki/%D0%9F%D0%BE%D0%B4%D0%B3%D0%BE%D1%82%D0%BE%D0%B2%D0%BA%D0%B0-%D1%81%D1%80%D0%B5%D0%B4%D1%8B-%D0%B4%D0%BB%D1%8F-%D1%81%D0%B1%D0%BE%D1%80%D0%BA%D0%B8-%D0%BF%D1%80%D0%BE%D0%B5%D0%BA%D1%82%D0%B0)**

## Важно
Если проект не собирается (ошибки компиляции) или собирается, но работает неправильно (например вся матрица светится белым и ничего не происходит) - проверьте версии библиотек. Данный проект рассчитан на работу с версииями библиотек поддержки плат ESP версии 2.5.2 и библиотеки FastLED версии 3.2.9 или более новую;

Если в качестве микроконтроллера вы используете Wemos D1 - в менеджере плат для компиляции все равно выбирайте **"NodeMCU v1.0 (ESP-12E)"**, в противном случае, если выберете плату Wemos D1 (xxxx), - будет работать нестабильно, настройки не будут сохраняться в EEPROM, параметры подключения к локальной сети будут сбрасываться каждый раз при перезагрузке, плата вместо подключения к локальной сети будет каждый раз создавать точку доступа.

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

В: Эй чувак! У тебя проект не компилится. Ты файл FastLed.h в проект забыл включить. Выложи!   
О: Это стандартная библиотека для FastLed для управления адресными светодиодами. Идите в менеджер библиотек и установите ее. Или скачайте с [сайта производителя](https://github.com/FastLED/FastLED)

В: Собрал, использую NodeMCU/Wemos. Ничего не работает! Мигает один или несколько светодиодов в начале матрицы. И всё.   
О: Производители разных плат (NodeMCU, Wemos) могут использовать различные схемы соединения контактов микроконтроллера ESP8266 к выводам макетной платы. Обычно используемый в проекте пин вывода на ленту приходится или на пин D2 или на пин D4. Для проверки не подключайте сигнальный провод матрицы к микроконтроллеру, вместо этого через резистор коснитесь вывода D2 или D4 пина микроконтроллера. Большая вероятность что матрица заработает с тем или иным вариантом подключения.

В: Собрал, использую NodeMCU. Эффекты работают, но нестабильно. Случайные вспышки на матрице. Буквы бегущей строки прыгают.   
О: NodeMCU v3 чрезвычайно требователен к источнику питания. Ему на вход VIN нужно подавать напряжение в диапазоне 4.7-5 вольт. И не более. Описанные эффекты возникают даже при питании в 5.25 (а тем более - 5.45) вольт. Для проверки - не подключайте +5 вольт от блока питания к NodeMCU совсем, питание подавайте на матрицу непосредственно. Землю NodeMCU и ленты соедините. Подключите сигнальный пин NodeMCU ко входу DIN ленты. Подключите NodeMCU к компьютеру через USB (питание будет поступать отсюда). Должно заработать. Далее регулируйте выходное напряжение своего блока питания.  
В особо тяжелых случаях, когда понижение напряжения питания системы не приводит к желаемым результатам и артефакты, вспышки, дрожание текста бегущей строки продолжается, можно использовать дополнительно схему преобразования уровня от 3.3 вольта с выхода NodeMCU к 5 вольтам входа адресной ленты:  
![SCHEME](https://github.com/vvip-68/GyverMatrixWiFi/blob/master/schemes/convertor.png)

В: Не компилируется. Выбрана плата "голая ESP8266-12E". Сообщение об ошибке: "D4 was not declared in this scope."   
О: Очевидно производители библиотеки для "голой ESP8266-12E" не определили данную константу. Используйте всесто константы D4 числовое определение пина для вашей платы или выполните компиляцию проекта для плат NodeMCU или WeMos D1 R2.

В: Не компилируется. В сообщении об ошибке содержатся сведения о дублирующихся библиотеках.    
О: В вашей среде установлено две версии одной и той же библиотеки. Обычно это библиотека FastLED - одна версия находится в папке установки среды Ардуино (например в "C:\Program Files (x86)\Arduino\libraries\"), другая - в папке документов пользователя (например "C:\Users\vvip-68\Documents\Arduino\libraries\"). Удалите одну из версий библиотек и попробуйте скомпилировать снова.

В: Не компилируется. В сообщении об ошибке что-то про несоответствие типов.   
О: Обычно такая ситуация возникает в двух случаях:
- выбрана неверная плата. Используйте NodeMCU 1.0 (ESP-12E Module) или Wemos D1 R1. Под эти платы проект собирается, под другие, возможно, нужна модификация кода.
- установлена устаревшая версия библиотек поддержки плат - например для ESP8266 версия библиотеки 2.4.2. Данный проект использует библиотеки для плат ESP8266 версии 2.5. Обновите библиотеки поддержки плат.

В: Подскажите, что не так... C подключением через точку доступа всё исправно работает, а при попытке подключиться к локальной сети не могу законнектиться через приложение. В чем может быть проблема?  
О: Проблема может быть в неправильно указанном статическом адресе / параметрах сети в прошивке. В сектче по умолчанию используется адрес в сети 192.168.**0**.xxx. Ваш WiFi роутер в зависимости от настроек может создавать сеть в другом диапазоне. Чаще всего это 192.168.**1**.xxx или 192.168.**100**.xxx; Проверьте какую сеть создает ваш роутер и укажите в скетче и при подключении приложения к сети именно эту сеть.

В: Автор неверно указал IP адрес матрицы 192.168.4.1 в режиме точки доступа. На самом деле он 192.168.4.2 - указываю его, приложение на смартфоне подключается. Правда управлять матрицей не получается все равно - она не реагирует на изменения.     
О: Нет, все правильно. IP матрицы - 192.168.4.1; Адрес 192.168.4.2 получает ваш смартфон при подключении к точке доступа. Когда в приложении для подключения вы указываете адрес 192.168.4.2 - вы подключаете ваш смартфон с самому себе, а не к матрице. Естественно никакое управление матрицей работать не будет.   

В: Матрица создает точку доступа, телефон к ней подключается. В приложении ввожу IP адрес матрицы 192.168.4.1, но соединение не происходит. Что я делаю не так?     
О: Некоторые телефоны не могут передавать данные через точку доступа, пока в них активен мобильный интернет. Все передаваемые данные отправляются в интернет, вместо передачи их в точку доступа. В настройках телефона выключите мобильный интернет ("Мобильные данные"). После этого телефон из приложения должен подключиться к матрице.  

В: В скетче есть настройки который задают имя и пароль к локальной сети. Указываю, но к сети даже не пытается подключиться В чем дело?     
#define NETWORK_SSID ""                      // Имя WiFi сети - пропишите здесь или задайте из программы на смартфоне    
#define NETWORK_PASS ""                      // Пароль для подключения к WiFi сети - пропишите здесь или задайте из программы на смартфоне      
О: Эти настройки определяют параметры доступа к сети по умолчанию, которые используются при ПЕРВОЙ загрузке прошивки в матрицу. В этот момент они сохраняются в EEPROM и при последующих запусках имя сети и пароль извлекаются из энергонезависимой памяти и используются уже извлеченные значения, а не те, что прописаны в #define. Если вы уже запускали матрицу и ПОСЛЕ этого изменили в скетче имя и пароль сети, вам нужно также изменить значение флага, указывающее было ли уже сохранение параметров в EEPROM или еще нет. Этот флаг находится в файле eeprom.ino в первой строке  
#define EEPROM_OK 0x5A                     // Флаг, показывающий, что EEPROM инициализирована корректными данными 
Измените его на любое другое значение, например 0xA5

### Всё собрал строго по инструкции, ничего не работает.

1. Разбираем всё обратно.
2. Берем платку, смотрим чтобы к ней НИЧЕГО не было подключено.
3. Плату в таком состоянии подключаем кабелем USB к компьютеру.
4. Берем последнюю версию [прошивки](https://github.com/vvip-68/GyverMatrixWiFi/) и загружаем ее в микроконтроллер.
5. Смотрим в сообщениях, что загрузка успешно выполнена и осуществлен перезапуск микроконтроллера, а в мониторе порта, что скетч старотовал, вывел версию прошивки, создал точку доступа MatrixAP
6. Устанавливаем на смартфон приложение из этого проекта
7. Подключаемся телефоном к точке доступа, приложение подключаем к матрице, пробуем тыкать на кнопки.
8. Отключаем микроконтроллер от компьютера
9. Подключаем блок питания +5 вольт и минусовой провод к матрице. Минусовой провод подключаем также к пину GND микроконтроллера.
Контроллер подключаем USB кабелем к компьютеру, блок питания включаем в сеть.
10. Проверяем, что напряжение питания с блока не превышает +5.25 вольт. Если больше - регулируем его до уровня 4.8 вольта.
11. Сигнальным проводом с матрицы с подключенным резистором 200 Ом тыкаемся поочередно в пины D4 и D2 микроконтроллера. В каком-то из этих двух вариантов на иматрице должно сформироваться осмысленное отображение эффекта, игры или бегущего текста. Что из этого конкретно должно в данный момент отображаться написано в мониторе порта. Запоминаем подключение к какому пину дало результат.
12. Отключаем микроконтроллер и блок питания. Провод +5V с блока питания подключаем к микроконтроллеру на пин его входного напряжения питания (у разных плат обозначен по разному - Vin, Vcc или +5). Сигнальный провод матрицы припаеваем к пину, который определили шагом выше. Очень желательно между пинами Vin и GND микроконтроллера припаять электролитический конденсатор номиналом 1000-4700 мкф, и параллельно ему керамический конденсатор на 33-100 нф.
13. Включаем блок питания в розетку. Матрица должна заработать.
14. Собираем всю конструкцию в корпус. Если матрица это гирлянда - развешиваем ее.


<a id="chapter-6"></a>
## Полезная информация
* [Cайт Alex Gyver](http://alexgyver.ru/)
* [Канал Alex Gyver на YouTube](https://www.youtube.com/channel/UCgtAOyEQdAyjvm9ATCi_Aig?sub_confirmation=1)
* [YouTube канал про Arduino](https://www.youtube.com/channel/UC4axiS76D784-ofoTdo5zOA?sub_confirmation=1)
* [Видеоуроки по пайке](https://www.youtube.com/playlist?list=PLOT_HeyBraBuMIwfSYu7kCKXxQGsUKcqR)
* [Видеоуроки по Arduino](http://alexgyver.ru/arduino_lessons/)
