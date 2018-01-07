[![Build Status](https://travis-ci.org/desta-study/lab07.svg?branch=master)](https://travis-ci.org/desta-study/lab07)



## Laboratory work VII

Данная лабораторная работа посвещена изучению систем документирования исходного кода на примере **Doxygen**

```ShellSession
$ open https://www.stack.nl/~dimitri/doxygen/manual/index.html
```

## Tasks

- [x] 1. Создать публичный репозиторий с названием **lab07** на сервисе **GitHub**
- [x] 2. Выполнить инструкцию учебного материала
- [x] 3. Ознакомиться со ссылками учебного материала
- [x] 4. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

Делаем первоначальные настройки
```ShellSession
$ export GITHUB_USERNAME=desta-study # Устанавливаем значение переменной окружения GITHUB_USERNAME
$ alias edit=vi # Команде edit задаём значение команды vi
$ alias gsed=sed
$ cd ${GITHUB_USERNAME}/workspace
$ pushd .
~/desta-study/workspace ~/desta-study/workspace
$ source scripts/activate #Выполняем скрипт внутренней сессии
$ wget https://redirector.gvt1.com/edgedl/go/go1.9.2.linux-amd64.tar.gz #Загружаем файл
--2018-01-05 17:42:47--  https://redirector.gvt1.com/edgedl/go/go1.9.2.linux-amd64.tar.gz
Resolving redirector.gvt1.com (redirector.gvt1.com)... 209.85.233.139, 209.85.233.100, 209.85.233.102, ...
Connecting to redirector.gvt1.com (redirector.gvt1.com)|209.85.233.139|:443... connected.
HTTP request sent, awaiting response... 302 Found
Location: https://r8---sn-n8v7kn7l.gvt1.com/edgedl/go/go1.9.2.linux-amd64.tar.gz?cms_redirect=yes&expire=1515177767&ip=2.92.215.106&ipbits=0&mm=28&mn=sn-n8v7kn7l&ms=nvh&mt=1515163279&mv=m&nh=IgpwcjAyLnN2bzA1KgkxMjcuMC4wLjE&pl=17&shardbypass=yes&sparams=expire,ip,ipbits,mm,mn,ms,mv,nh,pl,shardbypass&signature=54F0991C0C21A27D6AE94BDC46AD1F9FA3321CEB.1ED19A9C17FEB2594F9A3447773CCE4C8D4FC3DE&key=cms1 [following]
--2018-01-05 17:42:47--  https://r8---sn-n8v7kn7l.gvt1.com/edgedl/go/go1.9.2.linux-amd64.tar.gz?cms_redirect=yes&expire=1515177767&ip=2.92.215.106&ipbits=0&mm=28&mn=sn-n8v7kn7l&ms=nvh&mt=1515163279&mv=m&nh=IgpwcjAyLnN2bzA1KgkxMjcuMC4wLjE&pl=17&shardbypass=yes&sparams=expire,ip,ipbits,mm,mn,ms,mv,nh,pl,shardbypass&signature=54F0991C0C21A27D6AE94BDC46AD1F9FA3321CEB.1ED19A9C17FEB2594F9A3447773CCE4C8D4FC3DE&key=cms1
Resolving r8---sn-n8v7kn7l.gvt1.com (r8---sn-n8v7kn7l.gvt1.com)... 173.194.163.218, 2a00:1450:4011:3d::1a
Connecting to r8---sn-n8v7kn7l.gvt1.com (r8---sn-n8v7kn7l.gvt1.com)|173.194.163.218|:443... connected.
HTTP request sent, awaiting response... 302 Found
Location: https://r1---sn-4g5e6nl6.gvt1.com/edgedl/go/go1.9.2.linux-amd64.tar.gz?expire=1515177767&ip=2.92.215.106&ipbits=0&pl=17&shardbypass=yes&sparams=expire,mm,mn,ms,mv,pl,shardbypass&signature=24A543278C1FA0F18D81B324C6672F6ADC35074D.79E927DBB1A471BB0D44487707316FA89C3497F3&key=cms1&redirect_counter=1&cm2rm=sn-n8vky7r&req_id=9876e74d86180caa&cms_redirect=yes&mm=34&mn=sn-4g5e6nl6&ms=ltu&mt=1515163288&mv=m [following]
--2018-01-05 17:42:47--  https://r1---sn-4g5e6nl6.gvt1.com/edgedl/go/go1.9.2.linux-amd64.tar.gz?expire=1515177767&ip=2.92.215.106&ipbits=0&pl=17&shardbypass=yes&sparams=expire,mm,mn,ms,mv,pl,shardbypass&signature=24A543278C1FA0F18D81B324C6672F6ADC35074D.79E927DBB1A471BB0D44487707316FA89C3497F3&key=cms1&redirect_counter=1&cm2rm=sn-n8vky7r&req_id=9876e74d86180caa&cms_redirect=yes&mm=34&mn=sn-4g5e6nl6&ms=ltu&mt=1515163288&mv=m
Resolving r1---sn-4g5e6nl6.gvt1.com (r1---sn-4g5e6nl6.gvt1.com)... 74.125.104.71, 2a00:1450:4001:56::7
Connecting to r1---sn-4g5e6nl6.gvt1.com (r1---sn-4g5e6nl6.gvt1.com)|74.125.104.71|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 104247844 (99M) [application/octet-stream]
Saving to: ‘go1.9.2.linux-amd64.tar.gz’

go1.9.2.linux-amd64.tar.gz         100%[===============================================================>]  99,42M  8,55MB/s    in 11s     

2018-01-05 17:42:58 (9,41 MB/s) - ‘go1.9.2.linux-amd64.tar.gz’ saved [104247844/104247844]

$ tar -C . -xzf go1.9.2.linux-amd64.tar.gz #Используем архиватор
$ rm -rf go1.9.2.linux-amd64.tar.gz
$ echo "export GOROOT=`pwd`/go" >> scripts/activate #Помещаем строку в ковычках в конец файла
$ echo "export GOPATH=`pwd`/go_modules" >> scripts/activate #Помещаем строку в ковычках в конец файла
$ echo "export PATH=\${PATH}:\${GOROOT}/bin" >> scripts/activate #Помещаем строку в ковычках в конец файла
$ echo "export PATH=\${PATH}:\${GOPATH}/bin" >> scripts/activate #Помещаем строку в ковычках в конец файла
$ source scripts/activate #Активация скрипта
$ go get github.com/prasmussen/gdrive #Установка необходимых пакетов
```

Работаем с репозиторием
```ShellSession
$ git clone https://github.com/${GITHUB_USERNAME}/lab06 lab07 # Копируем репозиторий lab06 в локальный lab07
$ cd lab07 # Входим в lab07
$ git remote remove origin # Отключаемся от удалённого репозитория lab06
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab07 # Подключаемся у удалённому репозиторию lab07
```

Работаем с doxygen
```ShellSession
$ mkdir docs # Создаём дирректорию docs
$ doxygen -g docs/doxygen.conf # Создаём файл с настройками
$ cat docs/doxygen.conf # Смотрим содержимое файла
```

Вносим изменения в файл
```ShellSession
$ sed -i '' 's/\(PROJECT_NAME.*=\).*$/\1 print/g' docs/doxygen.conf # Вносим изменения в docs/doxygen.conf
$ sed -i '' 's/\(EXAMPLE_PATH.*=\).*$/\1 examples/g' docs/doxygen.conf # Вносим изменения в docs/doxygen.conf
$ sed -i '' 's/\(INCLUDE_PATH.*=\).*$/\1 examples/g' docs/doxygen.conf # Вносим изменения в docs/doxygen.conf
$ sed -i '' 's/\(INPUT *=\).*$/\1 README.md include/g' docs/doxygen.conf # Вносим изменения в docs/doxygen.conf
$ sed -i '' 's/\(USE_MDFILE_AS_MAINPAGE.*=\).*$/\1 README.md/g' docs/doxygen.conf # Вносим изменения в docs/doxygen.conf
$ sed -i '' 's/\(OUTPUT_DIRECTORY.*=\).*$/\1 docs/g' docs/doxygen.conf # Вносим изменения в docs/doxygen.conf
```

Вносим изменения в файл README.md
```ShellSession
$ sed -i '' 's/lab06/lab07/g' README.md # Вносим изменения в файл README.md
```

Документируем файл print.hpp
```ShellSession
# документируем функции print 
$ edit include/print.hpp
```

Делаем последние настройки и загружаем репозиторий на сайт
```ShellSession
$ git add . # Добавляем все отредактированные файлы в подтвержденные
$ git commit -m"added doxygen.conf" # Создаем коммит
$ git push origin master # Выгружаем локальную репозиторий в удаленный репозиторий lab07
```

Авторизируемся в travis и "включаем" репозиторий
```ShellSession
$ travis login --auto # Входим в travis
$ travis enable # Активируем в travis наш репозиторий
```

Продолжаем работать с doxygen
```
$ doxygen docs/doxygen.conf # Запускаем программу Doxygen, указав ей в качестве параметра путь к файлу с настройками

Searching for include files...
Searching for files in directory /home/desta-study/desta-study/workspace/projects/lab07/examples
Searching for example files...
Searching for files in directory /home/desta-study/desta-study/workspace/projects/lab07/examples
Searching for images...
Searching for dot files...
Searching for msc files...
Searching for dia files...
Searching for files to exclude
Searching INPUT for files to process...
Searching for files in directory /home/desta-study/desta-study/workspace/projects/lab07/include
Reading and parsing tag files
Parsing files
Reading /home/desta-study/desta-study/workspace/projects/lab07/README.md...
Preprocessing /home/desta-study/desta-study/workspace/projects/lab07/include/print.hpp...
Parsing file /home/desta-study/desta-study/workspace/projects/lab07/include/print.hpp...
Building group list...
Building directory list...
Building namespace list...
Building file list...
Building class list...
Associating documentation with classes...
Computing nesting relations for classes...
Building example list...
Searching for enumerations...
Searching for documented typedefs...
Searching for members imported via using declarations...
Searching for included using directives...
Searching for documented variables...
Building interface member list...
Building member list...
Searching for friends...
Searching for documented defines...
Computing class inheritance relations...
Computing class usage relations...
Flushing cached template relations that have become invalid...
Creating members for template instances...
Computing class relations...
Add enum values to enums...
Searching for member function documentation...
Building page list...
Search for main page...
Computing page relations...
Determining the scope of groups...
Sorting lists...
Freeing entry tree
Determining which enums are documented
Computing member relations...
Building full member lists recursively...
Adding members to member groups.
Computing member references...
Inheriting documentation...
Generating disk names...
Adding source references...
Adding xrefitems...
Sorting member lists...
Computing dependencies between directories...
Generating citations page...
Counting data structures...
Resolving user defined references...
Finding anchors and sections in the documentation...
Transferring function references...
Combining using relations...
Adding members to index pages...
Generating style sheet...
Generating search indices...
Generating example documentation...
Generating file sources...
Generating code for file include/print.hpp...
Generating file documentation...
Generating docs for file include/print.hpp...
Generating docs for file README.md...
Generating page documentation...
Generating group documentation...
Generating class documentation...
Generating namespace index...
Generating graph info page...
Generating directory documentation...
Generating index page...

/home/desta-study/desta-study/workspace/projects/lab07/README.md:2: warning: Unexpected html tag <img> found within <a href=...> context
/home/desta-study/desta-study/workspace/projects/lab07/README.md:2: warning: Unexpected html tag <img> found within <a href=...> context

Generating page index...
Generating module index...
Generating namespace index...
Generating namespace member index...
Generating annotated compound index...
Generating alphabetical compound index...
Generating hierarchical class index...
Generating graphical class hierarchy...
Generating member index...
Generating file index...
Generating file member index...
Generating example index...
finalizing index lists...
writing tag file...
Running dot...
Generating dot graphs using 5 parallel threads...
sh: 1: dot: not found
error: Problems running dot: exit code=127, command='dot', arguments='"/home/desta-study/desta-study/workspace/projects/lab07/docs/html/print_8hpp__incl.dot" -Tpng -o "/home/desta-study/desta-study/workspace/projects/lab07/docs/html/print_8hpp__incl.png"'
sh: 1: dot: not found
error: Problems running dot: exit code=127, command='dot', arguments='"/home/desta-study/desta-study/workspace/projects/lab07/docs/html/graph_legend.dot" -Tpng -o "/home/desta-study/desta-study/workspace/projects/lab07/docs/html/graph_legend.png"'
sh: 1: dot: not found
error: Problems running dot: exit code=127, command='dot', arguments='"/home/desta-study/desta-study/workspace/projects/lab07/docs/latex/print_8hpp__incl.dot" -Tpdf -o "/home/desta-study/desta-study/workspace/projects/lab07/docs/latex/print_8hpp__incl.pdf"'
Running dot for graph 1/3
Running dot for graph 2/3
Running dot for graph 3/3
Patching output file 1/2
error: problems opening map file /home/desta-study/desta-study/workspace/projects/lab07/docs/html/print_8hpp__incl.map for inclusion in the docs!
If you installed Graphviz/dot after a previous failing run, 
try deleting the output directory and rerun doxygen.
Patching output file 2/2
error: problem writing FIG 0 figure!
lookup cache used 1/65536 hits=2 misses=1
finished...

$ ls | grep "[^docs]" | xargs rm -rf # Просматриваем или удаляем
$ mv docs/html/* . && rm -rf docs # Перемещаем и удаляем
$ git checkout -b gh-pages # Копируем файлы в рабочую дирректорию

D	CMakeLists.txt
D	LICENSE
D	README.md
D	artifacts/screenshot.png
D	docs/doxygen.conf
D	examples/example1.cpp
D	examples/example2.cpp
D	file.txt
D	include/print.hpp
D	sources/print.cpp
D	tests/catch.hpp
D	tests/main.cpp
D	tests/test1.cpp
Switched to a new branch 'gh-pages'

$ git add . # Добавляем все отредактированные файлы в подтвержденные
$ git commit -m"added documentation" # Создаем коммит

[gh-pages c8baf63] added documentation
 69 files changed, 3960 insertions(+), 14015 deletions(-)
 delete mode 100644 CMakeLists.txt
 delete mode 100644 LICENSE
 delete mode 100644 README.md
 create mode 100644 README_8md.html
 create mode 100644 arrowdown.png
 create mode 100644 arrowright.png
 delete mode 100644 artifacts/screenshot.png
 create mode 100644 bc_s.png
 create mode 100644 bdwn.png
 create mode 100644 closed.png
 create mode 100644 dir_d44c64559bbebec7f509842c48db8b23.html
 create mode 100644 doc.png
 delete mode 100644 docs/doxygen.conf
 create mode 100644 doxygen.css
 create mode 100644 doxygen.png
 create mode 100644 dynsections.js
 delete mode 100644 examples/example1.cpp
 delete mode 100644 examples/example2.cpp
 delete mode 100644 file.txt
 create mode 100644 files.html
 create mode 100644 folderclosed.png
 create mode 100644 folderopen.png
 create mode 100644 globals.html
 create mode 100644 globals_func.html
 create mode 100644 graph_legend.dot
 create mode 100644 graph_legend.html
 create mode 100644 graph_legend.md5
 delete mode 100644 include/print.hpp
 create mode 100644 index.html
 create mode 100644 jquery.js
 create mode 100644 nav_f.png
 create mode 100644 nav_g.png
 create mode 100644 nav_h.png
 create mode 100644 open.png
 create mode 100644 print_8hpp.html
 create mode 100644 print_8hpp__incl.dot
 create mode 100644 print_8hpp__incl.md5
 create mode 100644 print_8hpp_source.html
 create mode 100644 search/all_0.html
 create mode 100644 search/all_0.js
 create mode 100644 search/all_1.html
 create mode 100644 search/all_1.js
 create mode 100644 search/close.png
 create mode 100644 search/files_0.html
 create mode 100644 search/files_0.js
 create mode 100644 search/files_1.html
 create mode 100644 search/files_1.js
 create mode 100644 search/functions_0.html
 create mode 100644 search/functions_0.js
 create mode 100644 search/mag_sel.png
 create mode 100644 search/nomatches.html
 create mode 100644 search/search.css
 create mode 100644 search/search.js
 create mode 100644 search/search_l.png
 create mode 100644 search/search_m.png
 create mode 100644 search/search_r.png
 create mode 100644 search/searchdata.js
 delete mode 100644 sources/print.cpp
 create mode 100644 splitbar.png
 create mode 100644 sync_off.png
 create mode 100644 sync_on.png
 create mode 100644 tab_a.png
 create mode 100644 tab_b.png
 create mode 100644 tab_h.png
 create mode 100644 tab_s.png
 create mode 100644 tabs.css
 delete mode 100644 tests/catch.hpp
 delete mode 100644 tests/main.cpp
 delete mode 100644 tests/test1.cpp
 
$ git push origin gh-pages # Выгружаем локальную репозиторий в удаленный репозиторий lab07
$ git checkout master # Копируем файлы в master
```

Создаём дирректорию и работаем со скриншотом
```ShellSession
$ mkdir artifacts && cd artifacts # Создаём дирректорию и входим в неё
$ sleep 3s && gnome-screenshot --file artifacts/screenshot.png #Делаем скриншот
$ gdrive upload screenshot.png # Выгружаем скриншот
$ SCREENSHOT_ID=`gdrive list | grep screenshot | awk '{ print $1; }'` # Взаимодействуем с google disk
$ gdrive share ${SCREENSHOT_ID} --role reader --type user --email rusdevops@gmail.com # Отправляем на емаил
$ echo https://drive.google.com/open?id=${SCREENSHOT_ID} # Показать скриншот на сайте
```

## Report

```ShellSession
$ cd ~/workspace/labs/
$ export LAB_NUMBER=07
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gistup -m "lab${LAB_NUMBER}"
```

## Links

- [HTML](https://ru.wikipedia.org/wiki/HTML)
- [LAΤΕΧ](https://ru.wikipedia.org/wiki/LaTeX)
- [man](https://ru.wikipedia.org/wiki/Man_(%D0%BA%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D0%B0_Unix))
- [CHM](https://ru.wikipedia.org/wiki/HTMLHelp)
- [PostScript](https://ru.wikipedia.org/wiki/PostScript)

```
Copyright (c) 2017 Братья Вершинины
```
