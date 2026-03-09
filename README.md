# lab_02

## Tutorial

### Проинициализируем нужные для работы переменные, перейдем в рабочее пространство и активируем ранее подготовленные скрипты.
```sh
export GITHUB_USERNAME=Mimocake
export GITHUB_EMAIL=<адрес_почтового_ящика>
export GITHUB_TOKEN=<сгенирированный_токен>
alias edit=nano

cd ${GITHUB_USERNAME}/workspace
source scripts/activate
```

### Теперь создадим папку `.config`, в ней файл конфигурации `hub` с необходимыми переменными:

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
последней командой установим протокол `https` для работы с гитхабом.

Создаём папку для второй лабы и переходим туда
```sh
mkdir projects/lab02t && cd projects/lab02t
```
Создаем новый репозиторий
```sh
git init
```

Вывод предупреждает о том, что текущая ветка называется `master`:
```
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint: 
hint:  git config --global init.defaultBranch <name>
hint: 
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint: 
hint:  git branch -m <name>
Initialized empty Git repository in /home/vboxuser/satodim/workspace/workspace/projects/lab_02/.git/
```
На гитхабе главная ветка называется `main`, поэтому  переименуем локальную ветку `master` в `main`

```sh
git branch -m main
```

### Установим юзернейм и почту для гита:
```sh
git config --global user.name ${GITHUB_USERNAME}
git config --global user.email ${GITHUB_EMAIL}
```

И проверим, что все пошло по плану:
```sh
git config -e --global
```

```
[hub]
        protocol = https
[user]
        name = satodim
        email = ...@gmail.com
```
### Все установилось правильно, привяжем локальную директорию с созданным удаленно репозиторием:
```sh
git remote add origin https://github.com/${GITHUB_USERNAME}/lab_02.git
```

И загрузим все, что есть в этом репозитории, на наш компьютер
```sh
git pull origin main
```

Вывод предыдущей команды:
```sh
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (3/3), 1.45 KiB | 744.00 KiB/s, done.
From https://github.com/satodim/lab_02
 * branch            main       -> FETCH_HEAD
 * [new branch]      main       -> origin/main
```
 
### Создадим `README.md`
```sh
touch README.md
```
 
### Теперь посмотрим на статусы файлов в папке
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

### Видно, что новосозданный README пока что никак не участвует в репозитории, поэтому мы можем его добавить и сделать новый коммит:
```sh
git add README.md
git commit -m "added README.md"
```

```
[main 19701b1] added README.md
 1 file changed, 1 insertion(+)
 create mode 100644 README.md
```

### Запушим локальный коммит на удаленный репозиторий
```sh
git push origin main
```

```
Username for 'https://github.com': satodim
Password for 'https://satodim@github.com': 
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 2 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 282 bytes | 282.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/satodim/lab_02.git
   9a76e6f..200709d  main -> main
```

На гитхабе появился README.

### Теперь удаленно создадим `.gitignore` и загрузим к нам.

На всякий случай убедимся, что все действительно загрузилось:
```sh
ls -a
```

```
.  ..  .git  .gitignore  LICENSE  README.md
```
Действительно, `.gitignore` загрузился

### Посмотрим на историю репозитория 
```sh
git log
```

```
commit 200709d7a92d037a88536bc7a7a90098b6454b9b
Author: satodim <vovkakursk8@gmail.com>
Date:   Mon Mar 9 12:28:51 2026 +0000

    added README.md

commit 9a76e6fe6a744e4719f80516c50cad66c2548745
Author: satodim <vovkakursk8@gmail.com>
Date:   Mon Mar 9 15:27:09 2026 +0300

    README.md

commit 6148f015c1dae95e609cb536b20910e8ef5f2b90
Author: satodim <vovkakursk8@gmail.com>
Date:   Sun Mar 8 19:06:25 2026 +0300

    README.md

commit 9d052f6a354185bbd51f8602cc906497f5526ba9
Author: satodim <vovkakursk8@gmail.com>
Date:   Sun Mar 8 18:51:09 2026 +0300

    README.md

commit 140f77de6eca12ff3a800da82f7bfbd175beb6ac
Author: satodim <vovkakursk8@gmail.com>
Date:   Sun Mar 8 15:02:32 2026 +0300

    README.md

commit 85a2f1437b1c88f0c22a43e32c9c3a095e635340
Author: satodim <vovkakursk8@gmail.com>
Date:   Sun Mar 8 14:16:18 2026 +0300

    README.md

commit 4099f5370e7fed6af83fc36dd30da700bb249e8e
Author: satodim <vovkakursk8@gmail.com>
Date:   Sun Mar 8 13:56:19 2026 +0300

    .gitignore

commit 908ae0168b9e4a4010670320dddfebf55bd40e2a
Author: satodim <vovkakursk8@gmail.com>
Date:   Sun Mar 8 12:41:36 2026 +0300

    Initial commit
```
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
# Homework
## Part I

