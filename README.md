## Laboratory work XI

Данная лабораторная работа посвещена изучению процесса создания сеансов совместной разработки с использованием инструмента **ngrok**

```sh
$ open https://ngrok.com/
```

## Tasks

- [x] 1. Ознакомиться со ссылками учебного материала
- [x] 2. Выполнить инструкцию учебного материала
- [x] 3. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```sh
$ cd ~
$ mkdir install - создает папку инстал
$ mkdir tmp - создает папку тмп
$ export HOME_PREFIX=`pwd`/install
$ echo $HOME_PREFIX
$ export USERNAME=`whoami`
```

```sh
$ cd tmp
```

```sh
$ wget https://github.com/libevent/libevent/releases/download/release-2.1.8-stable/libevent-2.1.8-stable.tar.gz - скачать libevent 2.1.8 (это асинхронная библиотека уведомлений о событиях)
$ tar -xvzf libevent-2.1.8-stable.tar.gz - разархивируем
$ cd libevent-2.1.8-stable - открываем папку либевент
$ ./configure --prefix=${HOME_PREFIX} - установка компонентов программы в (print working directory) install, то есть папку инсталл
$ make && make install - сборка и компиляция папки инсталл
$ cd ..
```

```sh
$ wget http://invisible-island.net/datafiles/release/ncurses.tar.gz - скачать библиотеку (ncurses), предназначенную для управления ввода-вывода на терминал, позволяет задавать экранные координаты
$ tar -xvzf ncurses.tar.gz - разархивировать эту библиотеку
$ cd ncurses-5.9 - открыть установленную папку с файлами
$ ./configure --prefix=${HOME_PREFIX} - установка компонентов библиотеки в папку инсталл
$ make && make install - сборка и компиляция папки инсталл
$ cd ..
```


```sh
$ wget https://github.com/tmux/tmux/releases/download/2.5/tmux-2.5.tar.gz - скачать тмукс - терминальный мультиплексор (он позволяет создавать несколько терминалов, получать к ним доступ и !управлять с одного экрана!)
$ tar -xvzf tmux-2.5.tar.gz - разархивировать тмукс
$ cd tmux-2.5 - открыть папку тмукс
$ ./configure --prefix=${HOME_PREFIX} CFLAGS="-I${HOME_PREFIX}/include -I${HOME_PREFIX}/include/ncurses" LDFLAGS="-L${HOME_PREFIX}/lib" - установка компонентов  папки тмукс в папку инсталл
$ make && make install - сборка и компиляция инсталла
$ cd ..
```

```sh
$ wget https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-linux-amd64.zip - скачать нгрок (это сервис)
$ unizp ngrok-stable-linux-amd64.zip - разархивировать нгрок 
$ mv ngrok ${HOME_PREFIX}/bin - переместить папку нгрок в папку бин
```

```sh
$ export LD_LIBRARY_PATH=${HOME_PREFIX}/lib
$ export PATH="${HOME_PREFIX}/bin:${PATH}"
$ tmux - открыть отдельный терминал
```

```sh
$ cd ~
$ rm -rf tmp install - удалить папку тмп и инсталл
```

```sh
$ brew install tmux ngrok # or use linuxbrew 🎉- brew устанавливает тмукс и нгрок
```

```sh
$ tmux new -s session_with_group - создание новой сессии
```

```sh
# Alisa:
$ open https://ngrok.com/signup - открыть сайт нгрок, узнать токен оттуда
$ export NGROK_TOKEN=<токен>
$ ngrok authtoken ${NGROK_TOKEN} - авторизоваться
$ ngrok tcp 22 - создает туннель с протоколом tcp с портом 22
<порт_ngrok_сервера>
```

```sh
# Bob:
$ ssh ${USERNAME}@0.tcp.ngrok.io -p<порт_ngrok_сервера> - через протокол ssh установить соединение с открытой сессий в нгрок
<пароль_от_учетной_записи>
$ tmux a -t session_with_group - присоединиться к сессии
$ <C-B>" - разделить экран по горизонтали
```

## Report

```sh
$ cd ~/workspace/
$ export LAB_NUMBER=11
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER}.git tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gist REPORT.md
```

## Links

- [Tmux](https://raw.githubusercontent.com/tmux/tmux/master/README)
- [Libevent](http://libevent.org)
- [Ncurses](http://invisible-island.net/ncurses/)

```
Copyright (c) 2015-2021 The ISC Authors
```
