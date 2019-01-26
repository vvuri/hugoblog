---
categories: ["Linux"]
tags: ["DevOps","Linux","Debian"]
description: ""
menu: 
    main:
        parent: "DevOps"
date: "2017-11-20T23:27:56+03:00"
title: "Debian"
---

#### Архитектура и компоненты ПК
```bash
$ less /proc/cpuinfo 
$ lscpu
$ free 
$ dpkg --print-architecture - архитектура ПК
```

#### мониторинг всего:
```bash
# netstat -lnp 
# dmsetup ls 
# lvdisplay 
# lsblk
$ uptime        - время работы и загрузка за последние 3 часа
$ strace uptime - что вызывает вообще - можно ковырять софт
# strace uptime 2>&1 | grep open     - все открываемые файлы
$ pstree        - дерево процессов но без ID
$ du -h -s /var/cache/apt/archives/  - SIZE dir
```

#### htop
*R* — [running or runnable] запущенные или находятся в очереди на запуск <br>
*S* — [interruptible sleep] прерываемый сон <br>
*D* — [uninterruptible sleep] непрерываемый сон (в основном IO) <br>
*Z* — [zombie] процесс зомби, прекращенный, но не забранный родителем <br> 
*T* — Остановленный сигналом управления заданиями <br>
*t* — Остановленный отладчиком <br>
*X* — Мёртвый (не должен показываться) <br>
[детальней тут](https://habrahabr.ru/post/316806/)

#### RDP client
```bash
$ sudo apt-add-repository ppa:remmina-ppa-team/remmina-next 
$ sudo apt-get update 
$ sudo apt-get install remmina remmina-plugin-rdp 
```

#### Рабочие компнды
> Extract tar gz  
```bash
$ tar -zxvf {file.tar.gz}
```
> Dump  
```bash
$ tcpdump -nq -s 0 -i eth0 -w /tmp/dump.pcap
``` 
> показать как дерево  
```bash
tree -d /var/log/
или  
$ ls -R | grep ":$" | sed -e 's/:$//' -e 's/[^-][^\/]*\//--/g' -e 's/^/   /' -e 's/-/|/'
```
> переход в домашний каталог | ```$ cd ~``` <br>

#### Конфигурирование 
> перечитать .profile ```sh   $ . ~/.profile ``` <br>
> тут прописываются dns nameserver ```sh   # cat /etc/resolv.conf ``` <br>
> Добавляем в репозиторий ```# vi /etc/apt/sources.list ``` <br>
> Имя системы это hostname 	```$ hostname jenkins``` <br>
> тут можно указать на постоянной основе ```$ cat /etc/hostname ``` <br>

#### Создание образа диска:
> 
```bash
# dd if=/dev/cdrom of=image.iso
```
> попробовать его прочитать, игнорируя ошбки чтения:
```bash
# dd if=/dev/cdrom of=image.iso conv=noerror
```
> смонтировать данный образ
```bash
# mount -o loop image.iso /mnt/image
```
> 	
> не оптимальное решение клонирования жесткого диска:
```bash
# dd if=/dev/sda of=/dev/sdb bs=4096
```
>
>	бекап раздела по сети<br>
```bash
# dd if=/dev/DEVICE | ssh user@host «dd of=/home/user/DEVICE.img».
```
>
> MBR расположена в первых 512 байтах жесткого диска, и состоит из таблицы разделов, загрузчика и пары доп. байт. Иногда, ее приходится бекапить, восстанавливать и т.д. Бекап выполняется так:<br>
```bash
# dd if=/dev/sda of=mbr.img bs=512 count=1
```
> Восстановить можно проще:<br>
```bash
# dd if=mbr.img of=/dev/sda
# dd if=/dev/urandom of=/dev/null bs=100M count=5
```
> if: 	указывает на источник, т.е. на то, откуда копируем.<br> 
> of: 	указывает на файл назначения. То же самое, писать можем как в обычный файл, так и напрямую в устройство.<br>
> bs: 	количество байт, которые будут записаны за раз.<br> 
> count: 	как раз то число, которое указывает: сколько кусочков будет скопировано.<br>
> Описанная команда читает 5*100 мегабайт из устройства /dev/urandom в устройство /dev/null. - система сгенерирует 500 мегабайт случайных значений и запишет их в null устройство.<br>

#### Копирование SCP
> Команда копирования локального SourceFile на удалённый хост:
```bash
# scp SourceFile user@host:/directory/TargetFile
```
> Команда копирования SourceFile с удалённого хоста:
```bash
# scp user@host:/directory/SourceFile TargetFile
$ scp nin@zoom:/home/bigeye/l_ipp_8.1.tgz ~/
```
> Рекурсивно с подкаталогами -r
```bash
$ scp -r root@ux:/home/da/test ~/ 
```

#### ставим Хром:
> качаем с google.com/chrome
```bash
sudo apt-get install libappindicator1
sudo dpkg -i google-chrome-stable_current_amd64_2.deb
```

#### проверка на взлом
> 
```bash
$ lastlog
$ history
$ sudo vi /var/log/auth.log
с какого IP подключались:
$ zgrep sshd /var/log/auth.log* | grep rhost | sed -re 's/.*rhost=([^ ]+).*/\1/' | sort –u
Проверьте журналы Apache:
$ sudo less /var/log/apache2/access.log
$ sudo less /var/log/apache2/error.log
$ ps aux | less
$ crontab -l | grep -v ‘^#’
Запрет входа root-пользователей по SSH
$ sudo vi /etc/ssh/sshd_config
PermitRootLogin no
```

#### Sound
> [pulseaudio](https://wiki.archlinux.org/index.php/PulseAudio/Examples_%28%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9%29)
> что бы сделать звук с наушников по-умолчанию:
```bash
sudo vi /etc/pulse/daemon.conf
default-sample-channels = 2
sudo pulseaudio -k
sudo pulseaudio --check
```