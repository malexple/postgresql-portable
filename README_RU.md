# Как запустить PostgreSQL на Windows без установки

Для начала необходимо скачать zip архив с сайта https://www.enterprisedb.com/download-postgresql-binaries
Данный способ будет работать для 16, 15 и 14 версии PostgreSQL. Может будет работать для других версий, но это я уже не проверял. Скачанный zip нужно распаковать, и в корне новой папки PostgreSQL, создать файл с расширением *.bat.
В данный файл необходимо поместить ниже следующий скрипт:

```bat
@ECHO ON
REM Setting environment variables to run PostgreSQL
@SET PATH="%CD%\bin";%PATH%
@SET PGDATA=%CD%\data
@SET PGDATABASE=postgres
@SET PGUSER=postgres
@SET PGPORT=5432
@SET PGLOCALEDIR=%CD%\share\locale
REM %CD%\bin\initdb -U postgres -A trust
%CD%\bin\pg_ctl -D %CD%/data -l logfile start
ECHO "Press Enter to stop the server"
pause
%CD%\bin\pg_ctl -D %CD%/data stop
Information was taken from here
```

При первом запуске раскомментируйте строку с вызовом initdb. Будет проинициализировано создание БД. При следующих запусках данную строчку нужно закомментировать.  При необходимости можете перенести папку с PostgreSQL  на USB-устройство.  Переменная %CD% возвращает путь к папке, в которой находится командный файл.

Данный способ является лишь одним из вариантов запуска PostgreSQL для экспериментов и тестирования. Надеюсь данная статья будет полезна.

Ну и на последок. Если вам надо сконфигурировать PostgreSQL под определенные возможности железки есть сайт для генерации настроек. Там вы указывает операционную систему. Количество ядер, памяти и другое.

https://www.pgconfig.org/