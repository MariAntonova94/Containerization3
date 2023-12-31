Урок 3. Введение в Docker
Задание:
1) запустить контейнер с БД, отличной от mariaDB, используя инструкции на сайте: https://hub.docker.com/
2) добавить в контейнер hostname такой же, как hostname системы через переменную
3) заполнить БД данными через консоль
4) запустить phpmyadmin (в контейнере) и через веб проверить, что все введенные данные доступны

Формат сдачи ДЗ: предоставить доказательства выполнения задания посредством ссылки на google-документ с правами на комментирование/редактирование.
Результатом работы будет: текст объяснения, логи выполнения, история команд и скриншоты (важно придерживаться такой последовательности).
В названии работы должны быть указаны ФИ, номер группы и номер урока.

1) Для запуска контейнера с БД другого типа, отличного от MariaDB, нам потребуется найти образ данной БД на сайте https://hub.docker.com/. Предположим, мы хотим использовать PostgreSQL. Для этого мы можем найти Docker-образ PostgreSQL в репозитории Docker Hub, используя запрос "PostgreSQL" в строке поиска.

![lxc version](https://github.com/MariAntonova94/Containerization3/blob/main/file/1.png)

2) При запуске контейнера мы можем передать переменную окружения с желаемым hostname из командной строки или через Dockerfile. Для примера, для передачи hostname=mysystemhostname, мы можем использовать команду запуска контейнера следующим образом:

```
docker run -e "hostname=mysystemhostname" --name mydatabase -d postgres
```
В этом случае, при запуске контейнера с образом PostgreSQL, мы передаем значение переменной окружения "hostname" в контейнер.

![lxc version](https://github.com/MariAntonova94/Containerization3/blob/main/file/2.png)

3) Для заполнения БД данными через консоль, мы можем использовать команду `psql` внутри контейнера, которая предоставляет доступ к консоли PostgreSQL. Например, мы можем использовать следующую команду, чтобы подключиться к нашей БД и выполнить SQL-запрос:

```
docker exec -it mydatabase psql -U postgres -d mydatabase
```

Эта команда позволит нам войти в контейнер (с именем "mydatabase"), выполнить команду `psql` и соединиться с БД "mydatabase" под пользователем "postgres".

После подключения к консоли PostgreSQL, мы можем выполнять необходимые SQL-запросы для заполнения БД данными.

4) Чтобы запустить phpMyAdmin в контейнере и проверить доступность введенных данных через веб-интерфейс, мы можем использовать образ phpMyAdmin:

```
docker run --name myphpmyadmin -d --link mydatabase:db -p 8080:80 phpmyadmin/phpmyadmin
```

Эта команда запускает контейнер с образом phpMyAdmin, связывая его с контейнером БД (с именем "mydatabase"), который был ранее создан, и пробрасывая порт 8080 контейнера на порт 80 хост-системы.

Теперь мы можем открыть веб-браузер и перейти по адресу http://localhost:8080, где будет доступен phpMyAdmin. Мы можем войти в phpMyAdmin, используя учетные данные доступа к БД (например, имя пользователя и пароль), и проверить, что все ранее введенные данные доступны.

*Подготовила студентка GeekBrains* [*`Антонова Мария`*]
