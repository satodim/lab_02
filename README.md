# lab_02

## Tutorial

### Проинициализируем нужные для работы переменные, перейдем в рабочее пространство и активируем ранее подготовленные скрипты.
```sh
export GITHUB_USERNAME=satodim
export GITHUB_EMAIL=<адрес_почтового_ящика>
export GITHUB_TOKEN=<сгенирированный_токен>
alias edit=nano

cd ${GITHUB_USERNAME}/workspace
source scripts/activate
```
### Cоздадим папку `.config`, в ней файл конфигурации `hub` с необходимыми переменными и установим протокол https для работы с гитхабом:

```sh
mkdir ~/.config
cat > ~/.config/hub <<EOF
github.com:
- user: ${GITHUB_USERNAME}
  oauth_token: ${GITHUB_TOKEN}
  protocol: https
EOF
git config --global hub.protocol https
```
### Создаём папку для второй лабы и переходим туда
```sh
mkdir projects/lab02 && cd projects/lab02t
```
### Создаем новый репозиторий
```sh
git init
```

Предупреждает, что текущая ветка `master`:
```
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint: 
hint: 	git config --global init.defaultBranch <name>
hint: 
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint: 
hint: 	git branch -m <name>
Initialized empty Git repository in /home/univer/Desktop/timp/satodim/workspace/projects/lab02t/.git/
```
На гитхабе главная ветка называется `main`, поэтому, чтобы не создавать новую ветку, переименуем локальную ветку `master` в `main`

```sh
git branch -m main
```

### Установим имя и почту для гита:
```sh
git config --global user.name ${GITHUB_USERNAME}
git config --global user.email ${GITHUB_EMAIL}
```

### И проверим, что все пошло успешно:
```sh
git config -e --global
```

```
[hub]
        protocol = https
[user]
        name = satodim
        email = ...@gmail.ru
```
### Все установилось правильно, поэтому следующей командой привяжем локальную директорию с созданным удаленно репозиторием:
```sh
git remote add origin https://github.com/${GITHUB_USERNAME}/lab02.git
```

### И загрузим все, что есть в этом репозитории, на наш компьютер
```sh
git pull origin main
```
Выше сказанно, что главная ветка в гитхабе наз-ся `main`, поэтому команда чуть чуть отличеается.

### Вывод предыдущей команды:
```sh
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (3/3), 1.45 KiB | 744.00 KiB/s, done.
From https://github.com/satodim/lab02
 * branch            main       -> FETCH_HEAD
 * [new branch]      main       -> origin/main
```
 
### Создадим `README.md`
```sh
touch README.md
```
 
### Посмотрим на статусы файлов в папке
```sh
git status
```
 
```
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	README.md

nothing added to commit but untracked files present (use "git add" to track)
```
### Созданный README пока что никак не участвует в репозитории, поэтому мы можем его добавить и сделать новый коммит:
```sh
git add README.md
git commit -m "added README.md"
```

```
[main 19701b1] added README.md
 1 file changed, 1 insertion(+)
 create mode 100644 README.md
```

### Пушим локальный коммит на удаленный репозиторий
```sh
git push origin main
```

```
Username for 'https://github.com': satodim
Password for 'https://satodim@github.com': 
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 4 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 307 bytes | 307.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/Mimocake/lab02t.git
   2b5f135..19701b1  main -> main
```
### Теперь удаленно создадим `.gitignore` и загрузим к нам.
```sh
git remote pull origin
```

```
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (3/3), 993 bytes | 496.00 KiB/s, done.
From https://github.com/satodim/lab02
 * branch            main       -> FETCH_HEAD
   19701b1..4fc5ac2  main       -> origin/main
Updating 19701b1..4fc5ac2
Fast-forward
 .gitignore | 4 ++++
 1 file changed, 4 insertions(+)
 create mode 100644 .gitignore
```

### На всякий случай убедимся, что все действительно загрузилось:
```sh
ls -a
```

```
.  ..  .git  .gitignore  LICENSE  README.md
```
### Посмотрим на историю репозитория 
```sh
git log
```

```
commit 4fc5ac20c9dc9ecc8fb5493645726145eed30953 (HEAD -> main, origin/main)
Author: satodim <88584860+satodim@users.noreply.github.com>
Date:   Thu Mar 6 12:56:58 2026 +0300

    Create .gitignore

commit 19701b13454bd7a64edbd07011e16323424d3f8f
Author: satodim <vovkakursk8@gmail.com>
Date:   Thu Mar 6 12:37:38 2026 +0300

    added README.md

commit 2b5f1353c2c0a8d60a8d693bb0a9bebecfc874c3
Author: saatodim <88584860+satodim@users.noreply.github.com>
Date:   Thu Mar 6 12:15:22 2026 +0300

    Initial commit
```
Видно, что первый коммит был сделан мною на гитхабе, второй тоже мною в консоли, и третий опять на гитхабе

### Ну и теперь создадим несколько `cpp` файлов

```sh
mkdir sources
mkdir include
mkdir examples

cat > sources/print.cpp <<EOF
#include <print.hpp>

void print(const std::string& text, std::ostream& out)
{
  out << text;
}

void print(const std::string& text, std::ofstream& out)
{
  out << text;
}
EOF

cat > include/print.hpp <<EOF
#include <fstream>
#include <iostream>
#include <string>

void print(const std::string& text, std::ofstream& out);
void print(const std::string& text, std::ostream& out = std::cout);
EOF

cat > examples/example1.cpp <<EOF
#include <print.hpp>

int main(int argc, char** argv)
{
  print("hello");
}
EOF

cat > examples/example2.cpp <<EOF
#include <print.hpp>

#include <fstream>

int main(int argc, char** argv)
{
  std::ofstream file("log.txt");
  print(std::string("hello"), file);
}
EOF
```

### Коммитим и пушим их:
```sh
git add .
git commit -m"added sources"
git push origin master
```

### Введем `git log` для проверки

```
Author: satodim <vovkakursk8@gmail.com>
Date:   Thu Mar 6 13:20:32 2026 +0300

    added sources

commit 4fc5ac20c9dc9ecc8fb5493645726145eed30953
Author: satodim <88584860+satodim@users.noreply.github.com>
Date:   Thu Mar 6 12:56:58 2026 +0300

    Create .gitignore

commit 19701b13454bd7a64edbd07011e16323424d3f8f
Author: satodim <vovkakursk8@gmail.com>
Date:   Thu Mar 6 12:37:38 2026 +0300

    added README.md

commit 2b5f1353c2c0a8d60a8d693bb0a9bebecfc874c3
Author: satodim <88584860+satodim@users.noreply.github.com>
Date:   Thu Mar 6 12:15:22 2026 +0300

    Initial commit
```
