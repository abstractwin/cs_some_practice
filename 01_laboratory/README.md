# Использование Docker в качестве средства виртуализации.
﻿
Docker - программное обеспечение для автоматизации развёртывания и управления приложениями в средах с поддержкой контейнеризации. Позволяет «упаковать» приложение со всем его окружением и зависимостями в контейнер, который может быть перенесён на любую Linux-систему с поддержкой cgroups в ядре, а также предоставляет среду по управлению контейнерами. Изначально использовал возможности LXC, с 2015 года применял собственную библиотеку, абстрагирующую виртуализационные возможности ядра Linux - libcontainer. С появлением Open Container Initiative начался переход от монолитной к модульной архитектуре. [wiki](https://ru.wikipedia.org/wiki/Docker)

Docker является относительно новым и быстро развивающимся проектом, который позволяет создавать очень легкие «виртуальные машины». То что Docker позволяет создавать, в действительности не является виртуальной машиной. Docker решает многие из тех же проблем, что решают виртуальные машины, плюс некоторые другие, которые виртуальные машины могли бы решить в случае, если бы они не потребляли так много ресурсов. Docker можно использовать для следующего:
* изоляции зависимостей приложения;
* создания образа приложения и его тиражирования;
* создания готового для запуска приложения, которое легко распространять;
* возможности легкого и быстрого масштабирования отдельных экземпляров приложения;
* тестирования приложения и освобождения затраченных ресурсов после завершения тестирования.

Идея, стоящая за Docker, представляет собой создание переносимых легких контейнеров, применяемых для программ, которые могут быть запущены на любом компьютере с установленным Docker, причем, независимо от основной ОС, что напоминает грузовые контейнеры, используемые на суднах. Довольно амбициозно и успешно.

Двумя наиболее важными сущностями в Docker являются образы (images) и контейнеры (containers). 


## Образы

Образ в Docker похож на снимок виртуальной машины, но он более легковесен.

Есть несколько способов создания образов в Docker, большинство из них основывается на создании нового образа на базе уже существующего образа, и поскольку есть общедоступные образы почти для всего, что вам может потребоваться, в том числе для основных дистрибутивов Linux, поэтому маловероятно, что вы не найдете то, что вам нужно. Однако, если вы посчитаете, что нужно создать образ с нуля, то это можно сделать несколькими способами.

Чтобы создать образ, вы берете некоторый образ и изменяете его таким образом, чтобы получился образ-потомок. Это можно сделать либо с помощью файла, в котором определяется базовый образ и изменения, которые должны быть выполнены, либо в живую "запускаете" образ, изменяете его и сохраняете в нем изменения. У каждого способа есть свои преимущества, но обычно для внесения изменений предпочитают использовать файл.

У образов есть уникальный идентификатор и уникальная пара параметров - уникальное удобочитаемое название и тег. Образы могут назваться, например, ubuntu:latest, ubuntu:precise, django:1.6, django:1.7 и т.д. [rus-linux](rus-linux.net/MyLDP/vm/docker/docker-tutorial.html)

Для управления образами используется команды **docker image ...**, доступные для образов команды:
* **build** - собирает образ из Dockerfile;
* **history** - отображает историю образа;
* **import** - импортировать содержимое из архива, чтобы создать образ файловой системы;
* **inspect** - возвращает информацию низкого уровня о одного или нескольких образов;
* **load** - загрузить образ из архива или STDIN;
* **ls** - отображает список образов;
* **prune** - удаляет неиспользуемые образы;
* **pull** - загрузить (pull) образ или репозиторий из реестра Docker registry;
* **push** - выгрузить (push) образ или репозиторий в реестр Docker;
* **rm** - удаляет один или несколько образов;
* **save** - сохраняет образ в архив;
* **tag** - указать тег для образа. [dker](https://dker.ru/docs/docker-engine/engine-reference/command-line-reference/docker-commands/)



## Контейнеры

Вы можете из образов создавать контейнеры, что эквивалентно созданию виртуальной машины из моментального снимка, но способ, с помощью которого это делается, менее ресурсоемкий. Контейнеры являются именно тем, что запускается и функционирует. [rus-linux](rus-linux.net/MyLDP/vm/docker/docker-tutorial.html)

Для управления контейнерами используется команды **docker container ...**, доступные для контейнеров команды:
* **attach** - подключиться к запущенному контейнеру;
* **commit** - cоздает новый образ из измененного контейнера;
* **cp** - копирует файлы/каталоги из контейнера в HOSTDIR или STDOUT;
* **create** - создает новый контейнер;
* **diff** - проверяет изменения в файловой системе контейнера;
* **exec** - выполняет команду в запущенном контейнере;
* **export** - экспортирует файловую систему контейнера в tar архив;
* **inspect** - возвращает информацию низкого уровня о контейнере;
* **kill** - грубое завершение запущенного контейнера;
* **logs** - отображает логи контейнера;
* **ls** - список контейнеров;
* **pause** - ставит на паузу все процессы контейнера;
* **port** - отображение общего списка портов или для конкретного контейнера;
* **prune** - удаляет неиспользуемые контейнеры;
* **rename** - переименовать контейнер;
* **restart** - перезапускает запущенный контейнер;
* **rm** - удаляет один или несколько контейнеров;
* **run** - выполняет команду в новом контейнере;
* **start** - запускает один или несколько остановленных контейнеров;
* **stats** - выводит в реальном времени информацию о потребляемых контейнером ресурсах;
* **stop** - останавливает контейнер;
* **top** - отображает запущенные в контейнере процессы;
* **unpause** - снимает с паузы все процессы контейнера;
* **update** - обновляет конфигурацию одного или нескольких контейнеров;
* **wait** - блокирует контейнер до его остановки, а затем выводит код завершения. [dker](https://dker.ru/docs/docker-engine/engine-reference/command-line-reference/docker-commands/)


## Установка Docker

Вне зависимости от выбранной операционной системы для работы с docker изображениями и контейнерами следует использовать PowerShell на Windows и Terminal на Linux.


### Установка Docker Desktop на Windows

Согласно инструкции [docs.docker](docs.docker.com/docker-for-windows/install/)  Docker Desktop устанавливается следующим образом:

1. По адресу [docs.docker](docs.docker.com/docker-for-windows/install/) нажать на кнопку "Download from Docker Hub".

![Страница руководства по установки Docker Desktop на Windows](/data/docker_install_windows_0.png)

2. В результате чего мы будем перенаправленны на [id.docker.com/login/](id.docker.com/login/), где следует ввести логин и пароль для входа в систему.

![Страница авторизации в Docker Hub](/data/docker_install_windows_1.png)

3. Оказавшись на [hub.docker](hub.docker.com/), осуществляется скачивание "Docker for Window installer.exe" посредством выбора сооствествующей кнопки загрузки.

![Страница Docker Hub, на которой предлагается сказать Docker Desktop](/data/docker_install_windows_2.png)

4. Запустить установочных исполняемый файл.

![Изображение установочного файла "Docker for Window installer.exe"](/data/docker_install_windows_3.png)

5. Из предложенного: добавление ярлыка на рабочий стол; использование контейнеров Windows, вместо контейнеров Linux, - выбирается необходимое.

![Диалоговое окно инстолятора docker](/data/docker_install_windows_4.png)

6. После установки следует выйти из текущей рабочей сессии пользователя.

![Преложение выйти, следующее за завершением установки](/data/docker_install_windows_5.png)

7. После входа в систему, docker предложит активизировать функции Hyper-V и Containers (для этого потребуется перезагрузка компьютера).

![Сообщение предлагающее активизировать дополнительные функции](/data/docker_install_windows_6.png)

8. После перезагрузки docker будет запущен в фоновом режиме, и доступен в области уведомлений.

![Docker в области уведомлений](/data/docker_install_windows_7.png)

9. Для открытия свойств docker следует: выбрать плитку программы в области уведомлений, нажать правой кнопкой мыши, и выбрать пункт "Settings".

![Окно настроек docker](/data/docker_install_windows_8.png)


### Установка Docker на Ubuntu

Для установки Docker на Ubuntu, в терминале достаточно выполнить следующую комманду:
```bash
sudo apt install docker docker.io
```

Для запуска команды docker без использования sudo, требуется добавить пользователя (обладающего правами root) в группу docker. Для этого следует выполнить следующую комманду:
```
sudo usermod -aG docker USER_NAME
```

## Пример использования

Пусть стоит следующая задача: на операционной системе ubuntu, надо создать программу на С, выводящую привественное сообщение "Hello World!".	


### Ручное создание контейнера

1. Запустить контейнер ubuntu в интерактивном режиме (сразу предоставлен доступ к терминалу контейнера).
```
(base) user@pc:/# docker run -it ubuntu
Unable to find image 'ubuntu:latest' locally
latest: Pulling from library/ubuntu
35c102085707: Pull complete 
251f5509d51d: Pull complete
8e829fe70a46: Pull complete 
6001e1789921: Pull complete 
Digest: sha256:d1d454df0f579c6be4d8161d227462d69e163a8ff9d20a847533989cf0c94d90
Status: Downloaded newer image for ubuntu:latest
```
В выводе видно то, что образ ubuntu найден небыл, в результате чего он был загружен из репозитория образов (https://hub.docker.com/). В другом терминале можно просмотреть список образов.
```
(base) user@pc:/# docker image ls -a
REPOSITORY  TAG     IMAGE ID      CREATED      SIZE 
ubuntu      latest  a2a15febcdf3  2 weeks ago  64.2MB
```
Так же как и список контейнеров.
```
(base) user@pc:/# docker container ls -a
CONTAINER ID  IMAGE   COMMAND  CREATED  STATUS  PORTS  NAMES
291017b927bc  ubuntu  "bash"   min ago  min            abba_tim
```
Мы видим созданный контейрер ubuntu, к которому можно обращаться (запускать, останавливать, присоединяться к нему) по имени **abba_tim** или по ID контейнера "291017b927bc".

2. В результате выполнения предыдущего шага был создан контейнер ubuntu, и нам предоставлена консоль этого контейнера. Осуществляем обновление репозитория программного обеспечения.
```
root@ca3d1f7a77d2:/# apt update
Reading package lists... Done
Building dependency tree       
Reading state information... Done
15 packages can be upgraded.
```

3. Осуществляем обновление программного обеспечения.
```
root@ca3d1f7a77d2:/# apt upgrade
15 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
Need to get 3544 kB of archives.
After this operation, 1024 B disk space will be freed.
Do you want to continue? [Y/n] y
```

4. Устанавливаем необходимые приложения: **gcc** - содержащий компилятор языка C, **nano** - консольный текстовый редактор для UNIX-подобных операционных систем.
```
root@ca3d1f7a77d2:/# apt install gcc nano
0 upgraded, 30 newly installed, 0 to remove and 0 not upgraded.
Need to get 28.7 MB of archives.
After this operation, 118 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
```

5. Запускае текстовый редактор: создаем новый файл **main.c** и указываем флаг **-i** для автоотступа.
```
root@ca3d1f7a77d2:/# nano main.c -i
```
![Текстовых редактор nano](/data/docker_example_nano.png)

6. В открывшемся редакторе, набираем следующий код:
```C
#include <stdio.h>
int main(int argc, char* argv[]) {
	printf("Hello World!\n");
	return 0;
}
```
После чего нажимаем **Ctrl+O** для сохранения изменений и **Ctrl+X** для закрытия редактора.

7.Компилируем и запускаем программу.
```
root@ca3d1f7a77d2:/# gcc main.c -o main
root@ca3d1f7a77d2:/# ./main
Hello World!
```


### Создание контейрена с помощью Dockerfile'а

1. Создаём копию существующего репозитория **cs_some_practice** ползователя **abstractwin** c **git**'а на компьютере.
```
(base) user@pc:/# git clone https://github.com/abstractwin/cs_some_practice.git
Cloning into 'cs_some_practice'...
Unpacking objects: 100%, done.
```

2. Переходим в папку **01_laboratory**. Здесь мы создаем образ на основе папки **way_02** (в ней содержится файл Dockerfile, строки которого определяют шаги создания контейнера) и даём ему имя **ubuntu_way_02**.
```
(base) user@pc:/# cd cs_some_practice/01_laboratory/
(base) user@pc: ... /# docker build way_02 -t ubuntu_way_02
Step 1/7 : FROM ubuntu:latest
Step 2/7 : RUN apt-get update
Step 3/7 : RUN apt-get -y upgrade
Step 4/7 : RUN apt-get install -y gcc
Step 5/7 : RUN apt-get install -y nano
Step 6/7 : ADD main.c main.c
Step 7/7 : RUN gcc main.c -o main
Successfully tagged ubuntu_way_02:latest
```

3. Далее следует запустить контейнер на основе образа **ubuntu_way_02** в интерактивном режиме. Выполняем программу **./main**.
```
(base) user@pc: ... /# docker run -it ubuntu_way_02
root@2d9572a62d09:/# ./main
Hello World!
```


### Использование готового образа из репозитория

Здесь мы используем уже готовый образ **01_laboratory** из репозитория пользователя **abstractwin**, для создания и запуска контейнера в интерактивном режиме.
```
(base) user@pc:/# docker run -it abstractwin/01_laboratory
Unable to find image 'abstractwin/01_laboratory:latest' locally
latest: Pulling from abstractwin/01_laboratory
35c102085707: Pull complete
251f5509d51d: Pull complete
8e829fe70a46: Pull complete
6001e1789921: Pull complete
f4e4810b9ea5: Pull complete
e8c49370e684: Pull complete
ab2ac79cbb62: Pull complete
fe303933ee84: Pull complete
bd0cfae87d8d: Pull complete
b76eff8b5ff4: Pull complete
5eb2f1fd4651: Pull complete
Digest: sha256:be9c64fe7c2ec3b2ddc90e0253bfdb90386c8114fd8e85aa845a6b1dd3623ddb
Status: Downloaded newer image for abstractwin/01_laboratory:latest

root@c1b5b698730a:/# ./main
Hello World!
```


### Загрузка образа из архива

1. Создаём копию существующего репозитория **cs_some_practice** ползователя **abstractwin** c **git**'а на компьютере.
```
(base) user@pc:/# git clone https://github.com/abstractwin/cs_some_practice.git
\end{bashcommand}
\begin{bashout}
Cloning into 'cs_some_practice'...
Unpacking objects: 100%, done.
```

2. Переходим в папку **01_laboratory**. Здесь мы загружаем образ из архива **ubuntu_way_04.tar** находящегося в папке **way_04**.
```
(base) user@pc:/# cd cs_some_practice/laboratory_01/
(base) user@pc: ... /# docker load -i way_04/ubuntu_way_04.tar
6cebf3abed5f: Loading layer [=====>]  65.56MB/65.56MB
f7eae43028b3: Loading layer [=====>]  991.2kB/991.2kB
7beb13bce073: Loading layer [=====>]  15.87kB/15.87kB
122be11ab4a2: Loading layer [=====>]  3.072kB/3.072kB
af339871ce2d: Loading layer [=====>]  27.12MB/27.12MB
107805e0bbd2: Loading layer [=====>]  9.142MB/9.142MB
562210c3a6c7: Loading layer [=====>]  111.1MB/111.1MB
fc77f6059e4a: Loading layer [=====>]  1.347MB/1.347MB
70797d3c4b57: Loading layer [=====>]  2.048kB/2.048kB
db8122bfeafe: Loading layer [=====>]  10.75kB/10.75kB
5a2c9d7d7e54: Loading layer [=====>]   2.56kB/2.56kB
Loaded image: ubuntu_way_04:latest
```

3. Далее следует запустить контейнер на основе образа **ubuntu_way_04** в интерактивном режиме. Выполняем программу **./main**.
```
(base) user@pc: ... /# docker run -it ubuntu_way_04
root@ee1cc5d7b1b0:/# ./main 
Hello World!
```

