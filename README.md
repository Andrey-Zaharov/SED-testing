1. Основные понятия в тестировании
===================================
Тестирование программного обеспечения (Software Testing) – это проверка соответствия между реальным и ожидаемым поведением программы, осуществляемая на конечном наборе тестов, выбранном определенным образом [IEEE Guide to Software Engineering Body of Knowledge, SWEBOK, 2004].
В более широком смысле, тестирование – это одна из техник контроля качества, включающая в себя действия по планированию работ (Test Management), проектированию тестов (Test Design), выполнению тестирования (Test Execution) и анализу полученных результатов (Test Analysis).
Верификация (Verification) – это процесс оценки системы или её компонента с целью определения соответствия результатов текущего этапа разработки условиям, сформированным в начале этого этапа [IEEE].
Валидация (Validation) – это определение соответствия разрабатываемого ПО ожиданиям и потребностям пользователя, требованиям к системе [BS7925-1].
План Тестирования (Test Plan) – это документ, описывающий весь объем работ по тестированию, начиная с описания объекта, стратегии, расписания, критериев начала и окончания тестирования, до необходимого в процессе работы оборудования, специальных знаний, а также оценки рисков с вариантами их разрешения.
Тестовый случай (Test Case) – это алгоритм, описывающий совокупность шагов, конкретных условий и параметров, необходимых для проверки реализации тестируемой функции или её части.
Тестовый набор (Test Suite) – это совокупность тест-кейсов, объединенных по некоторому общему признаку. Например, тест-кейсы для проверки функционала компоненты, используемой в разных формах приложения.
Баг / Дефект Репорт (Bug Report) – это документ, описывающий ситуацию или последовательность действий приведшую к некорректной работе объекта тестирования, с указанием причин и ожидаемого результата. Порядок оформления багов описан в документе «Форма оформления заявок.doc».
Объект тестирования – это отдельная логическая единица (форма, подсистема) со всеми элементами управления и диалогами.

2. Инструментарий 
================================
Для автоматизации тестирования рекомендуется использовать:
•	Selenium IDE - инструменты для создания наборов функциональных тестовых скриптов для проверки web-приложений. (Используем как аддон для Firefox)
http://habrahabr.ru/post/208638/ - Видео материал, который расставляет все точки над и.
http://habrahabr.ru/post/152653/ - Что такое Selenium.
•	Apache JMeter - инструмент для проведения нагрузочного тестирования и снятия количественных показателей нагрузки на сервер.(не обязательно)
•	ZeNmap, XSpider, Metasploit - сканеры безопасности для исследования топологии сети, поиска уязвимостей в сетевой инфраструктуре приложения и их эксплуатации.(не обязательно)
•	Acunetics WVS, инструментарий OWASP LiveCD - сканер и анализатор логики работы web-приложений, поиска уязвимостей в приложении, и инструменты для тестирования web-приложений.(не обязательно)
При ручном тестировании приложений рекомендуется использовать вспомогательные инструменты для исследования приложения:
•	PicPick - для снятия скриншотов и записи действий на экране.
•	FireBug - плагин для Firefox, который позволяет отслеживать ошибки приложения на стороне клиента и исследовать (http://firebug.ru/). (желательно)
•	Intercepter-NG, WinDump и др. – снифферы для перехвата и анализа сетевого траффика.(необязательно)

3. Категории тестов
================================
•	Init-тесты инициализации и авторизации (init / login / logout).
Обязательные действия в данной категории:
- для основного Init-теста в тестовом наборе добавить проверку корректности формы авторизации (все элементы формы присутствуют и доступны);
- для основного Init-теста в тестовом наборе добавить проверку того, что все обязательные элементы интерфейса главной формы приложения присутствуют и доступны;
- Init-тесты (шаблоны) для всех остальных тестов, разрабатываемые перед непосредственной реализацией основных проверок, должны содержать блок команд для корректного входа и выхода из приложения.
•	Функциональные CRUD-тесты (Create, Read, Update, Delete) для тестирования интерфейса стандартных операций по созданию, чтению, изменению, удалению элементов web-формы, добавляются в соответствующие Init-тесты.
Обязательные действия в данной категории:
- добавить проверки возможности добавления нескольких разнотипных элементов, из различных классов тестовых данных;
- добавить проверки возможности редактирования добавленных данных;
- добавить проверки возможности удаления данных;
- добавить проверки успешного обновления данных.
•	Функциональные регрессионные тесты для проверки корректности решенных в  системе bug/task-трекинга задач и отсутствия ранее имеющихся ошибок.
Обязательные действия в данной категории:
- добавить проверки важных задач task-ов (имеющих критичный функционал или влияющих на логику работы приложения (Например не возможность создавать документы, или отсутствие возможности изменять уже существующие));
•	Функциональные позитивные тесты для проверки корректности завершения разрешенных (валидных) операций, входящих в CRUD-тесты (например, проверка того, что после сохранения корректно введенной информации выводится сообщение об успехе операции), добавляются в соответствующие Init-тесты. Обязательные действия в данной категории:
- добавить проверки наличия ключевых элементов формы (все кнопки и надписи на своих местах);- добавить проверки фактического выполнения операций CRUD: добавляемые элементы действительно добавились, после редактирования данные изменились, после удаления данные действительно удалены, после обновления имеющиеся на форме данные остаются неизменными и т.п.;
- добавить проверки наличия сообщений об успехе операций CRUD.
•	Функциональные негативные тесты для проверки корректной обработки неправильно введенных данных (например, проверка того, что при попытке ввода в текстовое поле слишком длинной строки выводится сообщение об ошибке), добавляются в соответствующие Init-тесты.
Обязательные действия в данной категории:
- добавить проверки корректности обработки недопустимых или некорректных данных для операций CRUD: при таких данных программа не должна допускать их сохранения (например это одинарные\двойные кавычки, и остальные спецсимволы), редактирования или обновления в БД, а также не допускать удаления данных, с которыми имеются связи, без предварительной обработки этих связей и т.п.;
- добавить проверки наличия сообщений о некорректных действиях пользователя или неверных исходных данных.
•	Функциональные end-to-end сценарии, имитирующие конкретную последовательность действий реального пользователя (например, проверка корректного выполнения последовательности действий по входу в систему, открытию нужной формы, вводу данных в поля этой форму, сохранению данных и выходу из системы), добавляются в соответствующие Init-тесты.
Обязательные действия в данной категории:
- добавить несколько различных вариантов завершенных и логичных действий пользователя при работе с приложением.
•	Нагрузочные тесты(пока не используем), для проверки возможности "нормальной" и корректной работы в системе определенного числа пользователей выполняющих типичные действия (для имитации работы пользователей возможно использовать, например, уже имеющиеся CRUD-тесты или end-to-end сценарии).
Количественные показатели измеряются для случаев:
a) работы приложения без нагрузки (для определения сравнительных характеристик);
b) работы приложения под равномерно увеличивающейся нагрузкой (с различным числом виртуальных пользователей или различным числом подключений к узлам приложения);
c) работы приложения под пиковой нагрузкой (с различным числом виртуальных пользователей или различным числом подключений к узлам приложения).
Обязательные действия в данной категории:
- определить цели и объекты нагрузки;
- выбрать подходы и методики тестирования нагрузки;
- определить количественные и качественные показатели для нагрузочного тестирования (например, измерить среднее время доступа к приложению, данным и основным подсистемам приложения, степень загрузки процессоров, сетевых адаптеров, файла подкачки, памяти серверов приложений и БД).
•	Тесты информационной безопасности, которые должны включать в себя проверки безопасного (с точки зрения ИБ) функционирования приложения с точки зрения бизнес-логики работы приложения, даже при работе под нагрузкой или попытках анализа приложения на наличие уязвимостей или взлома.

4. Предполагаемый набор проверок для автотестов
============================================
•	CRUD-тесты: 
- добавление. Добавляем в цикле 3-4 элемента.
- редактирование. Редактируем один из созданных элементов.
- обновление. Обновляем данные.
- удаление. Удаляем в цикле все созданные элементы.
- проверка на отсутствие ошибок. После каждого из вышеперечисленных действий, а так же при открытии новых форм и диалогов проверять на отсутствие ошибок. 
В CRUD-тестах используем для этого наборы команд assert*.(для Selenium IDE)
•	Позитивные тесты:
- длина полей. Проверяем, что в поля ввода вводится строка максимально допустимой длины.
- ОДЗ полей. Проверяем область допустимого значения полей. Актуально, например, для математических функций (cos x и тд) или конкретные ограничения (количество вариантов не больше 50 и т.д.)
- открытие выпадающих списков. Проверяем, что комбобоксы и выпадающие списки при нажатии открываются. 
- выбор флажков, переключателей. Проверяем, что чекбоксы и радиобатоны выбираются.
- орфография. Попутно проверяем орфографию. В частности, названия полей и столбцов. Для этого, при обращении к элементу можно использовать заголовок таблицы.
- сортировка. Если нет возможности проверить корректность сортировки, то проверить, что после сортировки по всем имеющимся столбцам не выходит ошибка. В позитивных тестах для проверок используем блок команд verify*. (для Selenium IDE)
- модальность. Проверяем на модальность все открывающиеся окна, диалоги, запросы на удаление, выход и т.д.
- активность кнопок. Проверяем, что при заполненных обязательных полях или других необходимых условиях, кнопки активны.
- всплывающие подсказки на кнопках. Проверяем, что при наведении на кнопки и, возможно, другие элементы появляются правильные тултипы (tooltip - подсказка).
- добавление, редактирование, удаление. В дополнение к CRUD-тесту, проверяем что эти операции действительно выполняются. То есть, что элемент после сохранения - появляется, на редактирование - открывается, после удаления - пропадает.
•	Негативные тесты:
- недоступность кнопок. Проверяем, что при невыполнении обязательных условиий, кнопки неактивны.
- длина полей. Проверяем, что в поля ввода не вводятся строки меньше и больше минимальной и максимальной допустимой длины.
- ОДЗ (область допустимых значений) полей. Проверяем, что в поля не вводятся значения, не входящие в область допустимых (см. аналогичный пункт в позитивных тестах).
- ошибки. После ввода некорректных данных проверяем, что выходит ошибка. Это может быть выделение поля красным цветом (проверяем свойства поля), всплывающая подсказка (наводим курсор на требуемое поле), сообщение или объединение нескольких уведомлений об ошибке.
В негативных тестах для проверок используем блок команд verify*. (для Selenium IDE)
- допустимые символы. Проверяем, что в поля с ограниченным набором допустимых символов не вводятся остальные.
- доступность дублирования. Проверяем, что не добавляются дублирующие элементы (если это недопустимо).
- тримминг(trim функция). Проверяем, что после сохранения убираются пробелы и табы до первого значащего символа и после последнего значащего символа.
- ограничение полей даты. Проверяем, что не вводятся некорректные даты, в частности пятизначное число года, не выбирается прошедшая дата, если это недопустимо.
- недоступость полей. Проверяем, что в недоступные поля ничего нельзя вбить. Для этого проверяем свойства полей.
•	End-to-end сценарии:
- проверка ролей. Проверяем отдельным тестом каждую роль, участвующую в бизнес-процессе.(заходим под пользователями с различными правами доступа).

Проверка типичных ошибок
•	Отображение понятных пользователю сообщений об ошибке при обработке исключений (вместо непонятных системных).
•	Допустимость ввода отрицательных, нулевых, пустых значений по каждому полю.
•	Наличие сортировки по умолчанию в списках. (по алфавиту, по значимости и т.д)
•	Корректность сортировки после добавления новой записи к уже отсортированным.
•	Допустимость добавления дублирующих записей.
•	Ограничение поля год (от 0 до 9999 или по договоренности с РП, но не отрицательные).
•	Возможность удаления изображений и записей с загруженными изображениями.
•	Корректность скроллинга при большом количестве данных (комбобоксы, таблицы).
•	Орфографию заголовков полей.
•	Корректность отображения данных после ухода со вкладки и возвращения на неё (в т.ч. после обновления данных).
•	Правильную нумерации строк и полей записей.
•	Допустимые значения для налоговых/финансовых/банковских номеров и сокращений (например, ИНН - не более 12 символов, КПП - не более 9, для остальных - см. википедию).
•	Проверка на то, что все строки тримятся (после сохранения должны убираться пробелы и табы до первого значащего символа и после последнего значащего символа: "   Татарстан     "    =>    "Татарстан").
•	Модальность диалоговых окон.
•	Блокировку кнопок редактирования/удаления в процессе открытия диалогов редактирования или удаления соответствующих элементов (с целью предотвращения повторного открытия диалогов или удаления).
•	Если все поля КЛАДРа обязательны к заполнению, то после выбора любого варианта в одном комбобоксе, должен заполняться адресами комбобокс ниже (хотя бы одним значением по умолчанию - прочерком).
•	Более подробно об остальных типичных ошибках, информацию можно получить в багтрекере (redmine.e-kazan.ru) в соответствующем проекте, в разделе задачи.

5. Процесс тестирования
=======================
5.1. Процесс разработки GUI-тестов для проверки логики работы приложения целиком
1.	Составить функциональную схему логики работы приложения: выделить основные типичные формы и сгруппировать их по реализуемому функционалу (справочники, админка, формы ввода данных, формы для выгрузки данных и т.п.).
2.	Создать комплекты шаблонов для тестов требуемых категорий (файлы "пустышки", содержащими заголовки и основную структуру теста).
3.	Разработчик теста выбирает для тестируемой формы соответствующий ей шаблон и заполняет его проверками, требуемыми для конкретной категории теста.
4.	Отдельные тест-кейсы можно объединить в тест-сьюты, исходя из проверяемого ими функционала.
5.	Написать скрипты для запуска тестов.
5.2. Процесс разработки GUI-тестов для отдельных задач, поставленных программистам
1.	Начать ручное тестирование задачи, поставленной в системе bug/task-трекинга и имеющей статус Resolved (решена).
2.	Открыть имеющийся или создать новый шаблон теста для проверки функционала элементов приложения, разработанных в рамках этой задачи.
3.	Выполнять ручное тестирование элементов и если они рабочие, то сразу заносить команды для проверки их работоспособности в тест.
4.	Если найдена ошибка, зафиксировать ее в системе bug/task-трекинга (можно приложить скриншот ошибки) и переоткрыть задачу для разработчика.
5.	Ждать исправления ошибок разработчиками и приостановить разработку теста.
6.	После исправления ошибок запустить тест в IDE для тестирования до места ошибки, убедиться в её отсутствии и продолжить разработку теста, дополнять его новыми проверками и т.д.
5.3. Правила расстановки приоритетов для задач-багов
1. Приоритеты задач выставляют менеджеры, тестировщики создают задачи со статусом «новая»

6. Подготовка и ведение тестплана
=============================
Тест-план в самом простом случае можно формировать в табличном виде в Excel. Этот документ отражает анализ логики работы приложения и содержит его структуру и описание объектов, для которых будут разрабатываться тесты. Табличная организация тест-плана позволяет представить функционал сложного приложения более наглядно, по отдельным логическим модулям, а также упрощает слежение за разработкой тестов, для чего достаточно построить простые гистограммы готовности тестов.
В тест-плане указываются следующие данные:
•	имя тестового-набора, например, "CRUD-тесты для проверки базового функционала СЭД на Минстрое РФ";
•	рабочий идентификатор, например, sed_minstroy_Test_suite_CRUD;
•	тип тестов в наборе, например, CRUD-тесты;
•	комментарий к тестовому набору;
•	общая готовность тестового набора в %;
•	разбиение приложения на логические модули и подсистемы, например, тесты для подсистемы безопасности и администрирования, тесты для справочников, тесты для различных форм, при необходимости, даже тесты для отдельных подвкладок;

