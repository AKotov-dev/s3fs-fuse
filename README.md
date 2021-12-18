# s3fs-fuse
s3fs is a utility that lets Linux and macOS mount an Object Storage bucket via FUSE. Mageia Linux rpm-package.

**Настройка**  
Для настройки s3fs сохраните идентификатор ключа и секретный ключ в файле ~/.passwd-s3fs в формате <идентификатор ключа>:<секретный ключ>, а также ограничьте доступ к файлу ~/.passwd-s3fs следующим образом:
```
echo <идентификатор ключа>:<секретный ключ> >  ~/.passwd-s3fs
chmod 600  ~/.passwd-s3fs
```
**Монтирование бакета**  
Выберите каталог, в который вы будете монтировать бакет, и убедитесь, что у вас достаточно прав для операции монтирования. Выполните команду вида:
```
s3fs <имя бакета> /mount/<путь к папке> -o passwd_file=$HOME/.passwd-s3fs \
    -o url=http://storage.yandexcloud.net -o use_path_request_style
```
Можно настроить монтирование бакета при запуске системы, для этого добавьте в файл /etc/fstab строку вида:
```
s3fs#<имя бакета> /mount/<путь к папке> fuse _netdev,allow_other,use_path_request_style,url=http://storage.yandexcloud.net,passwd_file=/home/<имя пользователя>/.passwd-s3fs 0 0
```
Материал заимствован YandexCloud: https://cloud.yandex.ru/docs/storage/tools/s3fs
