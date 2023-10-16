```shell
#---------------------------------------------------------------
# базовые
sudo systemctl set-default multi-user.target
echo "%sudo   ALL=(ALL:ALL) NOPASSWD: ALL" | sudo tee -a /etc/sudoers
source ~/.bashrc
df -h 
#---------------------------------------------------------------
#Проверка системы
sudo systemctl status #проверка состояния
sudo apt update
sudo apt upgrade
sudo journalctl -b -p err #посмотреть какие ошибки есть при загрузке

#----------------------------------------------------------------

# Настройка локали
sudo localedef ru_RU.UTF-8 -i ru_RU -fUTF-8; export LANGUAGE=ru_RU.UTF-8; \
export LANGUAGE=ru_RU.UTF-8; \
export LANG=ru_RU.UTF-8; \
export LC_ALL=ru_RU.UTF-8; \
sudo dpkg-reconfigure locales
# убираем всё галочки кроме ru_RU.UTF-8 UTF-8
# на втором экране выбираем то-же
#-------------------------------------------------------------
# Настройка openssh-server
sudo nano /etc/ssh/sshd_config
    #Include /etc/ssh/sshd_config.d/*.conf
	PermitRootLogin no
	PubkeyAuthentication yes
	PasswordAuthentication yes
	Match User c2h5oh
	PasswordAuthentication yes
	PasswordAuthentication no

# Настройки админа
# выйти из ssh и со своей машины выполнить 
ssh-copy-id -p 050286 c2h5oh@192.168.1.68
#-------------------------------------------------------------
Внутренний пользователь сервера
# Настройка пользователя
sudo useradd -m -s /bin/bash www
sudo passwd www #ast10273
sudo usermod -aG cdrom www 
sudo usermod -aG sudo www 
sudo usermod -aG dip www 
sudo usermod -aG plugdev www 
sudo usermod -aG lxd www 
sudo passwd www
# ---------------------------------------------------
# Установка настройка timeshift
sudo apt install timeshift
timeshift --create --comments "install"
sudo nano /etc/timeshift.json
{
  "backup_device_uuid" : "f2296b99-6525-49b7-8426-024ae6840199",
  "parent_device_uuid" : "",
  "do_first_run" : "false",
  "btrfs_mode" : "false",
  "include_btrfs_home_for_backup" : "false",
  "include_btrfs_home_for_restore" : "false",
  "stop_cron_emails" : "true",
  "btrfs_use_qgroup" : "true",
  "schedule_monthly" : "false",
  "schedule_weekly" : "false",
  "schedule_daily" : "true",
  "schedule_hourly" : "false",
  "schedule_boot" : "false",
  "count_monthly" : "2",
  "count_weekly" : "3",
  "count_daily" : "5",
  "count_hourly" : "6",
  "count_boot" : "5",
  "snapshot_size" : "4982275706",
  "snapshot_count" : "96430",
  "date_format" : "%Y-%m-%d %H:%M:%S",
  "exclude" : [
        "/swap.img",
        "swap.img"      
  ],
  "exclude-apps" : [
        "swap.img"
  ]
}
#--------------------------------------------------
#Настройка часовог пояса
sudo timedatectl set-timezone Europe/Astrakhan
timedatectl
sudo systemctl restart systemd-timesyncd
#--------------------------------------------------
# Установка NGINX
wget https://nginx.org/download/nginx-1.25.2.tar.gz
cd ng*
tar xvf nginx-*
wget https://www.cpan.org/src/5.0/perl-5.38.0.tar.gz
tar xvf per*
cd per*
wget https://sourceforge.net/projects/pcre/files/pcre/8.45/pcre-8.45.tar.gz/download
tar xvf pcr*
cd pcre-8.45/
pwd
wget https://zlib.net/zlib-1.3.tar.gz
tar xvf zl*
wget https://www.openssl.org/source/openssl-3.1.3.tar.gz

sudo apt-get install gcc
sudo apt-get install libxml2 libxslt1-dev
sudo apt-get install libgd-dev
sudo apt-get install libperl-dev
sudo apt-get install libgeoip-dev
sudo apt-get install libgoogle-perftools-dev
sudo apt-get install libpcre3 libpcre3-dev
sudo apt-get install g++
libx11-dev libxau-dev libxcb1-dev libxdmcp-dev libxml2-dev libxpm-dev libxslt1-dev libzstd-dev m4 po-debconf quilt uuid-dev x11proto-dev xorg-sgml-doctools xtrans-dev libtool libvpx-dev libwebp-dev libpcrecpp0v5 libperl-dev libpng-dev libpthread-stubs0-dev libssl-dev libsub-override-perl libtiff-dev autoconf automake autopoint autotools-dev debhelper debugedit dh-autorecon dh-strip-nondeterminism diffstat dwz geoip-bin gettext icu-devtools intltool-debian libarchive-zip-perl libbrotli-dev libdebhelper-per libdeflate-dev libfile-stripnondeterminism-perl libfontconfig-de libfreetype-dev libgd-dev libgeoip-dev libgeoip1 libhiredis-de libhiredis0.14 libicu-dev libjbig-dev libjpeg-dev libjpeg-turbo8-de libjpeg8-dev liblerc-dev liblzma-dev libmaxminddb-dev libmhash-de libnetaddr-ip-perl libpam0g-dev libpcre16-3 libpcre3 libpcre3-dev libpcre32-3  libtiffxx6 

sudo apt install make

./configure --sbin-path=/usr/sbin/nginx --conf-path=/etc/nginx/nginx.conf --pid-path=/var/run/nginx.pid --user=www-data --group=www-data --with-select_module --with-poll_module --with-threads --with-file-aio --with-http_ssl_module --with-http_v2_module --with-http_v3_module --with-http_realip_module --with-http_addition_module --with-http_xslt_module --with-http_image_filter_module --with-http_geoip_module --with-http_sub_module --with-http_dav_module --with-http_flv_module --with-http_mp4_module --with-http_gunzip_module --with-http_gzip_static_module --with-http_auth_request_module --with-http_random_index_module --with-http_secure_link_module --with-http_degradation_module --with-http_slice_module --with-http_stub_status_module --with-mail --with-mail_ssl_module --with-stream --with-stream_ssl_module --with-stream_realip_module --with-stream_geoip_module --with-stream_ssl_preread_module --with-google_perftools_module --with-cpp_test_module --with-compat --with-pcre --with-pcre=/home/www/install_distributives/nginx/nginx-1.25.2/pcre-8.45 --with-pcre-jit --with-zlib=/home/www/install_distributives/nginx/zlib-1.3 --with-openssl=/home/www/install_distributives/nginx/openssl-3.1.3 --with-debug


sudo make
sudo make install 

sudo mkdir /etc/nginx/sites-available
sudo mkdir /etc/nginx/sites-enabled
sudo nginx -V
sudo nano /lib/systemd/system/nginx.service

	[Unit]
	Description=The NGINX HTTP and reverse proxy server
	After=syslog.target network-online.target remote-fs.target nss-lookup.target
	Wants=network-online.target
	
	[Service]
	Type=forking
	PIDFile=/var/run/nginx.pid
	ExecStartPre=/usr/sbin/nginx -t
	ExecStart=/usr/sbin/nginx
	ExecReload=/usr/sbin/nginx -s reload
	ExecStop=/bin/kill -s QUIT $MAINPID
	PrivateTmp=true
	
	[Install]
	WantedBy=multi-user.target

#--------------------------------------------------------------
#Установка python из исходников
mkdir ~install/python
cd python
wget https://www.python.org/ftp/python/3.12.0/Python-3.12.0.tgz
tar xvf Python-*
cd Python*
mkdir ~/python3.12
./configure --enable-optimizations --prefix=/home/www/.python3.12
sudo make -j8
cd ~
nano .bashrc
	export VIRTUALENVWRAPPER_PYTHON="/home/www/python3.12/bin/python3.12"
	export PATH=$PATH:/home/www/python3.12/bin
source .bashrc











 # переключем в режим командной строки
sudo systemctl status #проверка состояния
sudo apt update
sudo apt upgrade
sudo journalctl -b -p err #посмотреть какие ошибки есть при загрузке
#(ошибка флопи) окт 11 16:27:19 astmark10274 kernel: blk_update_request: I/O error, dev fd0, sector 0 op 0x0:(READ) flags 0x0 phys_seg 1 prio class 0
# (решение) 
# sudo su
# sudo echo "blacklist floppy" >> /etc/modprobe.d/blacklist-floppy.conf
# sudo modprobe -r floppy
# echo 'KERNEL=="fd0", ENV{UDISKS_IGNORE}="1"' | sudo tee /etc/udev/rules.d/10-local.rules
#KERNEL=="fd0", ENV{UDISKS_IGNORE}="1"
# exit
# sudo reboot
echo "%adm ALL=(ALL:ALL) NOPASSWD:ALL" | sudo tee -a /etc/sudoers %adm ALL (ALL:ALL) NOPASSWD:ALL # отменить ввод пароля для пользователей группы adm при действии от sudo

#Настройка WOL
sudo apt install ethtool
sudo nano /etc/systemd/system/wol.service
#Вставить в файл следующий текст:
#[Unit]
#Description=Enable Wake-on-LAN

#[Service]
#Type=oneshot
#ExecStart=/sbin/ethtool -s enp3s0 wol g

#[Install]
#WantedBy=basic.target
sudo systemctl daemon-reload
sudo systemctl enable wol.service



#Настроить UFW


```