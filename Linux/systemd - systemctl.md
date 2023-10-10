

/run/systemd/   - каталог для файлов юнитов  созданных при установке системы
/usr/lib/systemd/ - файлы юнитов служб которые были установлены из пакетов
/etc/systemd/system - файлы юнитов от администратора

`systemctl list-units --type=target`: список возможных целей для загрузки


/etc/systemd/system/.#dooucoffe.ru.serviceef81a545707fd102    
```sh

[Unit]
Description=DOOUCOFFE.RU gunicorn instance
After=network.target #цель после которой будет загружаться этот сервис

[Service]
User=c2h5oh  #пользователь     
Group=www-data #группа которая создается для nginx

```






















##### Err-fix
w83627ehf - ml
После того как сделали sensors-detect, программа выдает что необходимо загрузить модуль w83627ehf.
При попытке его загрузить выдается ошибка такого плана: `modprobe w83627ehf   FATAL: Error inserting w83627ehf (/lib/modules/2.6.31-14-generic/kernel/drivers/hwmon/w83627ehf.ko): Device or resource busy`
Решается все просто, в файл /etc/default/grub вместо: GRUB_CMDLINE_LINUX=" "
Необходимо вставить: GRUB_CMDLINE_LINUX="acpi_enforce_resources=lax"
И дать команду обновления груба: sudo update-grub2