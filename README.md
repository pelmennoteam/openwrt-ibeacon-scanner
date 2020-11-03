# Настройка iBeacon Scanner на OpenWRT

1. Устанавливаем пакеты
```
opkg update
opkg install kmod-bluetooth bluez-libs bluez-utils kmod-usb-core kmod-usb-uhci kmod-usb2
```

1. Копируем содержимое репозитория в корень устройства

1. Выставляем права на запуск
```
chmod +x /etc/init.d/{ibeacon-ifup,ibeacon-scan}
chmod +x /usr/bin/{ibeacon-ifup,ibeacon-scan}
```

1. Включаем автозапуск сервисов
```
/etc/init.d/dbus enable
/etc/init.d/ibeacon-ifup enable
/etc/init.d/ibeacon-scan enable
```

1. Перезагружаем устройство

## Настройки скрипта

Конфиг файл `/etc/ibeacon.conf`

```
remote_addr= # http://site.com/path/to/handler/
interface=hci0
```

`remote_addr` - адрес ресурса на который будут отправляться данные (формат: `{"uuid": "", "major": "", "minor": "", "power": "", "rssi": "", "device": ""}`)
`interface` - интерфейс usb bluetooth устройства
`device` - имя устройства (подставляется в тело запроса к `remote_addr`)
