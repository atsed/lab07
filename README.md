[![Build Status](https://travis-ci.org/desta-study/lab05.svg?branch=master)](https://travis-ci.org/desta-study/lab05)
## Laboratory work V

Данная лабораторная работа посвещена изучению систем непрерывной интеграции на примере сервиса **Travis CI**

```ShellSession
$ open https://travis-ci.org
```

## Tasks

- [x] 1. Авторизоваться на сервисе **Travis CI** с использованием **GitHub** аккаунта
- [x] 2. Создать публичный репозиторий с названием **lab05** на сервисе **GitHub**
- [x] 3. Ознакомиться со ссылками учебного материала
- [x] 4. Включить интеграцию сервиса **Travis CI** с созданным репозиторием
- [x] 5. Получить токен для **Travis CLI** с правами **repo** и **user**
- [x] 6. Получить фрагмент вставки значка сервиса **Travis CI** в формате **Markdown**
- [x] 7. Установить [**Travis CLI**](https://github.com/travis-ci/travis.rb#installation)
- [x] 8. Выполнить инструкцию учебного материала
- [x] 9. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```ShellSession
$ export GITHUB_USERNAME=<имя_пользователя>  # Устанавливаем значение переменной окружения GITHUB_USERNAME
$ export GITHUB_TOKEN=<полученный_токен>   # Устанавливаем значение переменной окружения GITHUB_TOKEN
```
### Инициализация директории lab04

```ShellSession
$ git clone https://github.com/${GITHUB_USERNAME}/lab04 lab05
https://github.com/${GITHUB_USERNAME}/lab04 lab05
Клонирование в «lab05»…
remote: Counting objects: 29, done.
remote: Compressing objects: 100% (21/21), done.
remote: Total 29 (delta 7), reused 21 (delta 3), pack-reused 0
Распаковка объектов: 100% (29/29), готово.
Проверка соединения… готово.
$ cd lab05
$ git remote remove origin
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab05
```
### Работа с файлом .travis.yml

```ShellSession
$ cat > .travis.yml <<EOF
language: cpp
EOF
```

```ShellSession
$ cat >> .travis.yml <<EOF

script:
- cmake -H. -B_build -DCMAKE_INSTALL_PREFIX=_install
- cmake --build _build
- cmake --build _build --target install
EOF
```

```ShellSession
$ cat >> .travis.yml <<EOF

addons:
  apt:
    sources:
      - george-edison55-precise-backports
    packages:
      - cmake
      - cmake-data
EOF
```
### Заходим в аккаунт на сервисе Travis с помощью github token

```ShellSession
$ travis login --github-token ${GITHUB_TOKEN}
Successfully logged in as desta-study!
```

```ShellSession
$ travis lint
Warnings for .travis.yml:
[x] value for addons section is empty, dropping
[x] in addons section: unexpected key apt, dropping
```

```ShellSession
$ ex -sc '1i|[![Build Status](https://travis-ci.org/desta-study/lab05.svg?branch=master)](https://travis-ci.org/desta-study/lab05)' -cx README.md
```
### Отправляем последние изменения на GitHub сервер

```ShellSession
$ git add .travis.yml   # Отследить изменения .travis.yml
$ git add README.md     # Отследить изменения README.md
$ git commit -m"added CI"    # Сохранить изменения
$ git push origin master     # Загрузка файлов на сервер
```

```ShellSession
$ travis lint     # display warnings for a .travis.yml
Warnings for .travis.yml:
[x] value for addons section is empty, dropping
[x] in addons section: unexpected key apt, dropping
$ travis accounts   # displays accounts and their subscription status
desta-study (desta-study): subscribed, 6 repositories
$ travis sync    # triggers a new sync with GitHub
synchronizing: .. done
$ travis repos     # list of my repos
desta-study/lab03 (active: no, admin: yes, push: yes, pull: yes)
Description: ???

desta-study/lab03-1 (active: no, admin: yes, push: yes, pull: yes)
Description: ???

desta-study/lab04 (active: no, admin: yes, push: yes, pull: yes)
Description: laba04

desta-study/lab04-1 (active: no, admin: yes, push: yes, pull: yes)
Description: Изучение систем автоматизации сборки проекта на примере CMake

desta-study/lab05 (active: yes, admin: yes, push: yes, pull: yes)
Description: ???

desta-study/stack2 (active: no, admin: yes, push: yes, pull: yes)
Description: Homework-2
$ travis enable      # enables a project
Detected repository as desta-study/lab05, is this correct? |yes| yes
desta-study/lab05: enabled :)
$ travis whatsup    # lists most recent builds
desta-study/lab05 passed: #1
$ travis branches    # most recent build for each branch
master: #1 passed added CI
$ travis history    # project history
travi#1 passed: master added CI
$ travis show   # displays a build 
Job #1.1: added CI
State: passed
Type: push
Branch: master
Compare URL: https://github.com/desta-study/lab05/compare/70611972..^...d64728e06ec8
Duration: 36 sec
Started: 2017-10-04 13:24:40
Finished: 2017-10-04 13:25:16
Allow Failure: false
Config: os: linux
```

## Report

```ShellSession
$ cd ~/workspace/labs/
$ export LAB_NUMBER=05
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gistup -m "lab${LAB_NUMBER}"
```

## Links

- [Travis Client](https://github.com/travis-ci/travis.rb)
- [AppVeyour](https://www.appveyor.com/)
- [GitLab CI](https://about.gitlab.com/gitlab-ci/)

```
Copyright (c) 2017 Братья Вершинины
```

