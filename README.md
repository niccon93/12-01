Домашнее задание к занятию «Базы данных»
Инструкция по выполнению домашнего задания
Сделайте fork репозитория c шаблоном решения к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/gitlab-hw или https://github.com/имя-вашего-репозитория/8-03-hw).
Выполните клонирование этого репозитория к себе на ПК с помощью команды git clone.
Выполните домашнее задание и заполните у себя локально этот файл README.md:
впишите вверху название занятия и ваши фамилию и имя;
в каждом задании добавьте решение в требуемом виде: текст/код/скриншоты/ссылка;
для корректного добавления скриншотов воспользуйтесь инструкцией «Как вставить скриншот в шаблон с решением»;
при оформлении используйте возможности языка разметки md. Коротко об этом можно посмотреть в инструкции по MarkDown.
После завершения работы над домашним заданием сделайте коммит (git commit -m "comment") и отправьте его на Github (git push origin).
Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
Любые вопросы задавайте в чате учебной группы и/или в разделе «Вопросы по заданию» в личном кабинете.
Желаем успехов в выполнении домашнего задания.

Легенда
Заказчик передал вам файл в формате Excel, в котором сформирован отчёт.

На основе этого отчёта нужно выполнить следующие задания.

Задание 1
Опишите не менее семи таблиц, из которых состоит база данных:

какие данные хранятся в этих таблицах;
какой тип данных у столбцов в этих таблицах, если данные хранятся в PostgreSQL.
Приведите решение к следующему виду:

Сотрудники (

 - идентификатор, первичный ключ, serial,
 - фамилия varchar(50),
 - ...
 - идентификатор структурного подразделения, внешний ключ, integer).

### Ответ:

```
Таблица "Сотрудники":

Сотрудники (
    сотрудник_id, первичный ключ, integer,
    фамилия, varchar(50),
    имя, varchar(50),
    отчество, varchar(50),
    дата найма, date,
    должность_id, внешний ключ, integer,
    подразделение_id, внешний ключ, integer
)

Таблица "Структурные подразделения":

Структурные_подразделения (
    подразделение_id, первичный ключ, integer,
    название_подразделения, varchar(100),
    руководитель_подразделения, varchar(100),
    адрес_подразделения, varchar(100)
)

Таблица "Филиалы":

Филиалы (
    филиал_id, первичный ключ, integer,
    название_филиала, varchar(100),
    адрес_филиала, varchar(100)
)

Таблица "Отделы":

Отделы (
    отдел_id, первичный ключ, integer,
    название_отдела, varchar(100),
    подразделение_id, внешний ключ, integer
)

Таблица "Отчеты":

Отчеты (
    отчет_id, первичный ключ, integer,
    название_отчета, varchar(100),
    дата_создания, date,
    ответственный_сотрудник, varchar(100)
)

Таблица "Зарплаты":

Зарплаты (
    зарплата_id, первичный ключ, integer,
    месяц, date,
    сумма_выплаты, numeric(10,2),
    сотрудник_id, внешний ключ, integer
)

Таблица "Адреса":

Адреса (
    адрес_id, первичный ключ, integer,
    адрес, varchar(100),
    филиал_id, внешний ключ, integer
)
```
Приведенные таблицы предполагают некоторую структуру базы данных для хранения информации о сотрудниках, подразделениях, отчетах, зарплатах и адресах филиалов. Указанные типы данных основаны на соответствующих типах данных, используемых в PostgreSQL. Знаки в скобках после типов данных указывают на максимальную длину или точность и масштаб числовых значений, которые можно хранить в столбцах таблицы.


Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале.

Задание 2*
Перечислите, какие, на ваш взгляд, в этой денормализованной таблице встречаются функциональные зависимости и какие правила вывода нужно применить, чтобы нормализовать данные.

### Ответ:

В денормализованной таблице могут встречаться следующие функциональные зависимости:

В таблице "Сотрудники":
Идентификатор -> ФИО сотрудника, Оклад, Должность, Тип подразделения, идентификатор структурного подразделения, Дата найма, Адрес филиала

В таблице "Структурные подразделения":
Идентификатор -> Название подразделения, Руководитель подразделения, Адрес подразделения

В таблице "Отделы":
Идентификатор -> Название отдела, идентификатор структурного подразделения

В таблице "Филиалы":
Идентификатор -> Название филиала, Адрес филиала

В таблице "Отчеты":
Идентификатор -> Название отчета, Дата создания, Сотрудник, ответственный за отчет

В таблице "Зарплаты":
Идентификатор -> Месяц, Сумма выплаты, идентификатор сотрудника

В таблице "Адреса":
Идентификатор -> Адрес, идентификатор филиала

Для нормализации данных можно применить следующие правила вывода:
Первая нормальная форма (1NF): Убедиться, что каждая таблица имеет первичный ключ и все столбцы зависят от целого первичного ключа. Разделить денормализованную таблицу на более мелкие таблицы, чтобы избежать повторения данных.
Вторая нормальная форма (2NF): Убедиться, что все неключевые столбцы в каждой таблице функционально зависят от всего первичного ключа. Если есть частичная зависимость, вынести соответствующие столбцы в отдельные таблицы.
Третья нормальная форма (3NF): Убедиться, что все неключевые столбцы в каждой таблице не зависят от других неключевых столбцов. Если есть транзитивная зависимость, вынести соответствующие столбцы в отдельные таблицы.

Применение этих правил позволит разделить данные на более логически связанные таблицы и устранить аномалии при обновлении, вставке или удалении данных.
