

``./config --prefix=/usr --libdir=/usr/lib/x86_64-linux-gnu`

после обновления до 3 падвет ошибка 
/snap/snapd/11107/usr/lib/snapd/snap-confine: error while loading shared libraries: libudev.so.1: failed to map segment from shared object
```sh
ldconfig /lib/x86_64-linux-gnu/
```