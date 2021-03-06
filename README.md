# proxmox-autostart-check
Возникла необходимость отключать автозапуск VM в кластере во время проведения регламентных работ.

Вызвано тем, что штатно выключенные VM после перезагрузки ноды начнут включаться. Если требуется несколько перезагрузок, то их включение и последующее выключение каждой VM может потребовать значительного времени.

Скрипт подключается к ноде по Proxmox VE API через https. 

Для работы скрипта должен быть установлен pip.

# Как пользоватся:

1. Указать IP, имя пользователя и пароль для подключения к любой ноде кластера на строке 27:

```bash
proxmox = ProxmoxAPI("xxx.xxx.xxx.xxx", user="user@pam", password="xxxxxxxxxxxxxx", verify_ssl=False)
```

2). Вывести текущие настройки автостарта для VM:

```bash
python3 proxmox-backup-check.py
```

3) Сохранить текущую настройку параметров автостарта VM в файл (если имя файла не указано, то будет использовано имя по умолчанию - startonboot.conf):

```bash
python3 proxmox-backup-check.py -export <filename.conf>
```

4) ООтключить автостарт на VM и сохранить текущую настройку параметров автостарта VM в файл (если имя файла не указано, то будет использовано имя по умолчанию - startonboot.conf):

```bash
python3 proxmox-backup-check.py -disable <filename.conf>
```

5) Применить сохраненные настройки автостарта VM в кластере из файла:

```bash
python3 proxmox-backup-check.py --import <filename.conf>
```
