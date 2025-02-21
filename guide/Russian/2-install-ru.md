﻿# Установка Windows

### Перезапустите режим восстановления для начала установки Windows

```cmd
fastboot boot <recovery.img>
```

### Скопируйте скрипт msc в /sbin

```cmd
adb push msc.sh /sbin/
```

### Выполните скрипт msc

```cmd
adb shell sh /sbin/msc.sh
```

## Привязка букв к разделам
  

#### Запустите Менеджер дисков Windows
> Как только планшет определился как диск

```cmd
diskpart
```


### Привязка буквы `X` к разделу Windows

#### Выберите Windows раздел планшета 
> Используйте команду `list volume` чтобы найти разделы "WINNABU" и "ESPNABU"

```diskpart
select volume <number>
```

#### Привяжите букву X
```diskpart
assign letter=x
```

### Привязка буквы `Y` к разделу ESP

#### Выберите ESP раздел планшета
> Используйте команду `list volume` чтобы найти его, обычно это последний раздел

```diskpart
select volume <number>
```

#### Привяжите букву Y

```diskpart
assign letter=y
```

### Закройте diskpart
```diskpart
exit
```

  
  

## Установка

> Замените `<path/to/install.wim>` действительным путём к файлу install.wim,
> `install.wim` расположен в папке sources внутри вашего ISO
> Вы можете получить его, смонтировав образ или разархивировав его

```cmd
dism /apply-image /ImageFile:<path/to/install.wim> /index:1 /ApplyDir:X:\
```

# Установка драйверов

> Замените `<nabudriversfolder>` расположением папки с драйверами

```cmd
driverupdater.exe -d <nabudriversfolder>\definitions\Desktop\ARM64\Internal\nabu.txt -r <nabudriversfolder> -p X:
```

  

# Создайте файлы загрузчика Windows

```cmd
bcdboot X:\Windows /s Y: /f UEFI
```

  
  

# Разрешите использование неподписанных драйверов

> Если вы не сделаете этого, вы получите BSOD
```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set {default} testsigning on
```

# Запуск Windows

### Создайте резервную копию текущего ядра Android

```cmd
adb shell "dd if=/dev/block/bootdevice/by-name/boot$(getprop ro.boot.slot_suffix) of=/tmp/boot.img"
```

##### Скопируйте на компьютер

```cmd
adb pull /tmp/boot.img
```

### Перезапустите планшет в режим загрузки 

```cmd
adb reboot bootloader
```

### Прошейте образ uefi 

```cmd
fastboot flash boot boot-nabu.img
```

# Загрузка в Android
> Прошейте скопированное ранее ядро в режиме загрузки

```cmd
fastboot flash boot boot.img
```

# Готово!
