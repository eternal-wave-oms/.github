# Eternal wave

![logo](/profile/logo.png)

Экспериментально-учебный проект системы управления заказами для ресторанов и точек быстрого питания. Для использования в реальных условиях может потребоваться "доработка напильником".

# Сценарии использования

Система даёт возможность:

- Администратору: задать доступные для заказа позиции путём ручного набора либо импорта из таблиц.
- Клиенту: оставить заказ на стойке самообслуживания, следить за его статусом по инфопанелям.
- Повару: видеть позиции заказа и их параметры, проставлять статусы готовности заказа.
- Официанту: видеть готовые заказы, проставлять статусы выдачи.

Поскольку проект учебный, никакие средства безналичной оплаты не были учтены в проекте. Для их внедрения необходима модификация кода киоска для внедрения поддержки терминала, модификация сервиса ОЗ для отслеживания статусов оплаты заказов, модификация сервиса БД для хранения информации об оплате и чеков.

# Стек технологий

Все компоненты проекта разработаны на C# под .NET Core 7.

# Компоненты

## Вспомогательные

### [Библиотека](https://github.com/eternal-wave-oms/models)

Требуется для сборки всех компонентов ниже. Содержит общий код, такой как модели и клиенты API.

## Серверные

### [Сервис БД](https://github.com/eternal-wave-oms/db-server)

Предоставляет REST API для авторизации пользователей, чтения/изменения ассортимента, сохранения заказов.
Написан на ASP.NET MVC. Работает с базой данных через EF Core, проверяя права доступа и входящие данные. Используется PostgreSQL, однако для использования другой СУБД не требуется глобальных изменений.

Windows | Linux (headless) | Linux (X / Wayland)
--------|------------------|----------
:heavy_check_mark:|:heavy_check_mark:|:heavy_check_mark:

### [Сервис ОЗ](https://github.com/eternal-wave-oms/order-server)

Предоставляет SignalR сокет для обработки поступающих заказов в реальном времени. Принимает заказы, помещает их в очередь и принимает от дэшей события изменения статусов. Уведомляет инфопанель и дэши об изменении статусов. Написан на ASP.NET. Умеет работать при недоступности сервиса БД.

Windows | Linux (headless) | Linux (X / Wayland)
--------|------------------|----------
:heavy_check_mark:|:heavy_check_mark:|:heavy_check_mark:

## Клиентские

### [Дэшборд](https://github.com/eternal-wave-oms/dashboard)

GUI-приложение для поваров, официантов и администраторов. Имеет раздел заказов и раздел администратора. Раздел заказов показывает все активные заказы и позволяет отчитываться об их готовности / подаче, раздел администратора позволяет модифицировать ассортимент доступный к заказу и работать с историей закрытых заказов. Написано на Avalonia UI с использованием MVVM.

Windows | MacOS | Linux (headless) | Linux (X / Wayland) | Android
--------|-------|------------------|---------------------|--------
:heavy_check_mark:|:heavy_check_mark:|:x:|:heavy_check_mark:|:x:


<!--

**Here are some ideas to get you started:**

🙋‍♀️ A short introduction - what is your organization all about?
🌈 Contribution guidelines - how can the community get involved?
👩‍💻 Useful resources - where can the community find your docs? Is there anything else the community should know?
🍿 Fun facts - what does your team eat for breakfast?
🧙 Remember, you can do mighty things with the power of [Markdown](https://docs.github.com/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
-->
