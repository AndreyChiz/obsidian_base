! не может обрабатывать динамический контент (python app)
#### Конфигурация
`/etc/nginx/nginx.conf`: базовая конфигурация
`include /etc/nginx/conf.d/*.conf`: подключение доп. конфигураций
` server {}`: блок в котором прописывают директивы (listen, server_name)


`sudo nginx -t`:  проверка конфигураций
`nginx -V 2>&1 | grep -o with-openssl[^\ ]*` : Версия openssl


`sudo nginx reload`
`service nginx reload`

```bash
# распаковать и прописать пути к папкам в которые распаковали
wget https://nginx.org/download/nginx-1.25.2.tar.gz
wget https://www.openssl.org/source/openssl-3.0.11.tar.gz
wget https://zlib.net/zlib-1.3.tar.gz
tar xvf nginx-1.25.2.tar.gz 
```


```bash
sudo apt-get install libgd-dev libgd3
sudo apt-get install libgeoip-dev
sudo apt-get install libgoogle-perftools-dev
```




https://si-dev.com/ru/blog/building-nginx-from-sources-on-ubuntu
```shell
./configure --prefix=/home/c2h5oh/.nginx  --with-select_module --with-poll_module --with-threads --with-file-aio --with-http_ssl_module --with-http_v2_module --with-http_v3_module --with-http_realip_module --with-http_addition_module --with-http_xslt_module --with-http_image_filter_module --with-http_geoip_module --with-http_sub_module --with-http_dav_module --with-http_flv_module --with-http_mp4_module --with-http_gunzip_module --with-http_gzip_static_module --with-http_auth_request_module  --with-http_random_index_module --with-http_secure_link_module --with-http_degradation_module --with-http_slice_module --with-http_stub_status_module --with-mail --with-mail_ssl_module --with-stream --with-stream_ssl_module --with-stream_realip_module --with-stream_geoip_module --with-stream_ssl_preread_module --with-google_perftools_module --with-cpp_test_module --with-compat --with-pcre --with-pcre-jit --with-zlib=/home/c2h5oh/server/tmp/zlib/zlib-1.3 --with-pcre=/home/c2h5oh/server/tmp/nginx-1.25.2/pcre-8.45 --with-libatomic --with-openssl=/home/c2h5oh/server/tmp/openssl-3.0.11 --with-debug  --with-libatomic --with-debug
```


