```bash
# настройка резервного копирования
# Создание скрипта резервного копирования с именем, основанным на дате
sudo bash -c 'echo "#!/bin/bash" > /usr/local/bin/backup_system.sh'
sudo bash -c 'echo "SOURCE_DIR=\"/home\"  # Если вы хотите скопировать всю систему, оставьте так" >> /usr/local/bin/backup_system.sh'
sudo bash -c 'echo "BACKUP_ROOT=\"/backup_hdd\"" >> /usr/local/bin/backup_system.sh'
sudo bash -c 'echo "DATE=\$(date +\"%Y-%m-%d_%H-%M-%S\")" >> /usr/local/bin/backup_system.sh'
sudo bash -c 'echo "BACKUP_DIR=\"\$BACKUP_ROOT/backup_\$DATE\"" >> /usr/local/bin/backup_system.sh'
sudo bash -c 'echo "EXCLUDE_DIRS=\"/backup_hdd /some_hdd\"" >> /usr/local/bin/backup_system.sh'
sudo bash -c 'echo "mkdir -p \$BACKUP_DIR" >> /usr/local/bin/backup_system.sh'
sudo bash -c 'echo "rsync -av --delete --compress --info=progress2 -v --exclude 'swap.img' --exclude 'proc/kcore' --exclude \$EXCLUDE_DIRS \$SOURCE_DIR/ \$BACKUP_DIR/" >> /usr/local/bin/backup_system.sh'
sudo chmod +x /usr/local/bin/backup_system.sh
# Создание скрипта восстановления
sudo bash -c 'echo "#!/bin/bash" > /usr/local/bin/restore_system.sh'
sudo bash -c 'echo "BACKUP_DIR=\"/backup_hdd/"" >> /usr/local/bin/restore_system.sh'
sudo bash -c 'echo "TARGET_DIR=\"/\"  # Восстанавливайте в нужное место" >> /usr/local/bin/restore_system.sh'
sudo bash -c 'echo "rsync -av --info=progress2 \$BACKUP_DIR \$TARGET_DIR" >> /usr/local/bin/restore_system.sh'
sudo chmod +x /usr/local/bin/restore_system.sh
# Добавление алиасов в ~/.bashrc
sudo bash -c 'echo "alias backup_system=\"sudo backup_system.sh\"" >> ~/.bashrc'
sudo bash -c 'echo "alias restore_system=\"sudo restore_system.sh"" >> ~/.bashrc'
source ~/.bashrc
#----------------------------------------------------------
```