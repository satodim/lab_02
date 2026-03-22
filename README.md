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

### Создайте пустой репозиторий на сервисе github.com

Создали **этот** репозиторий

### Выполните инструкцию по созданию первого коммита на странице репозитория, созданного на предыдущем шаге.

```sh
git init
git branch -m main
git remote add origin https://github.com/satodim/lab_02
git pull origin main
```

Вывод последней команды:

```
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (3/3), 1.45 KiB | 745.00 KiB/s, done.
From https://github.com/satodim/lab_02
 * branch            main       -> FETCH_HEAD
 * [new branch]      main       -> origin/main
```

### Создайте файл `hello_world.cpp` в локальной копии репозитория (который должен был появиться на шаге 2). Реализуйте программу Hello world на языке C++ используя плохой стиль кода. Например, после заголовочных файлов вставьте строку `using namespace std;`.

Этот файл:
```cpp
#include <iostream>
using namespace std;

int main() {
	cout << "Hello world!" << name << endl;
	return 0;
}
```

### Добавьте этот файл в локальную копию репозитория.
```sh
git add hello_world.cpp
```

### Закоммитьте изменения с осмысленным сообщением.
```sh
git commit -m "hello_world.cpp"
```

```
[main 19baeaf] added hello_world.cpp
 1 file changed, 7 insertions(+)
 create mode 100644 hello_world.cpp
```
### Изменитьте исходный код так, чтобы программа через стандартный поток ввода запрашивалось имя пользователя. А в стандартный поток вывода печаталось сообщение Hello world from @name, где @name имя пользователя.

Новая версия программы
```cpp
#include <iostream>
using namespace std;

int main() {
	string name;
	cin >> name;
	cout << "Hello world from " << name << endl;
	return 0;
}
```

### Закоммитьте новую версию программы. Почему не надо добавлять файл повторно `git add`?

```sh
git commit -a -m "added hello_world.cpp"
```

`-a` означает коммит всех измененных файлов, чтобы этот файл смог закоммититься.

### Запуште изменения в удалёный репозиторий.

```sh
git push origin main
```

```
Username for 'https://github.com': satodim
Password for 'https://satodim@github.com': 
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 2 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 408 bytes | 408.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/satodim/lab_02.git
   ea81e44..b15398a  main -> main
```

### Проверьте, что история коммитов доступна в удалённом репозитории.

```sh
git log
```

```
commit 076186a0e27ecb60e1bcebc2bb46c88470f7d187 (HEAD -> main, origin/main)
Author: satodim <vovkakursk8@gmail.com>
Date:   Fri Mar 6 17:05:21 2026 +0300

     hello_world.cpp

commit b15398ae3b062c765a7264ad83a203a3e54179bc (HEAD -> main, origin/main)
Author: satodim <vovkakursk8@gmail.com>
Date:   Mon Mar 9 13:15:31 2026 +0000

    added hello_world.cpp

commit f776454370e700c28831b42490d171c3bc559b96
Author: Roman Chekrygin <88584860+Mimocake@users.noreply.github.com>
Date:   Fri Mar 6 16:44:28 2026 +0300

    Initial commit
```
## Part II

### В локальной копии репозитория создайте локальную ветку `patch1`.

```sh
git checkout -b patch1
```

### Внесите изменения в ветке `patch1` по исправлению кода и избавления от `using namespace std;`.

Новый код:
```cpp
#include <iostream>

int main() {
	std::string name;
	std::cin >> name;
	std::cout << "Hello world from " << name << std::endl;
	return 0;
}
```

### **commit**, **push** локальную ветку в удалённый репозиторий.

``` sh
git commit -a -m "removed using namespace std"
```

```
[patch1 5faa54d] removed using namespace std
 1 file changed, 3 insertions(+), 4 deletions(-)
```

```sh
git push origin patch1
```

```
Username for 'https://github.com': satodim
Password for 'https://satodim@github.com': 
Enumerating objects: 42, done.
Counting objects: 100% (42/42), done.
Delta compression using up to 2 threads
Compressing objects: 100% (35/35), done.
Writing objects: 100% (42/42), 13.37 KiB | 1.21 MiB/s, done.
Total 42 (delta 6), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (6/6), done.
remote: 
remote: Create a pull request for 'patch1' on GitHub by visiting:
remote:      https://github.com/satodim/lab_02/pull/new/patch1
remote: 
To https://github.com/satodim/lab_02.git
 * [new branch]      patch1 -> patch1
```

### Проверьте, что ветка `patch1` доступна в удалённом репозитории.

```sh
git log
```

```
commit a6505f6297b26b72c249aec334f3d3726b6fc9ff (HEAD -> patch1, origin/patch1)
Author: satodim <vovkakursk8@gmail.com>
Date:   Mon Mar 9 13:31:25 2026 +0000

    removed using namespace std

commit b15398ae3b062c765a7264ad83a203a3e54179bc (origin/main, main)
Author: satodim <vovkakursk8@gmail.com>
Date:   Mon Mar 9 13:15:31 2026 +0000

    added hello_world.cpp

commit ea81e44f304637ee73a489d8f645a0ccc56dbb98
Author: satodim <vovkakursk8@gmail.com>
Date:   Mon Mar 9 12:56:10 2026 +0000

    added sources

commit 1e8920081b14e834d52505ea13c1a46218022eba
Author: satodim <vovkakursk8@gmail.com>
Date:   Mon Mar 9 15:47:47 2026 +0300

    Create .gitignore
```

### Я сделал pull-request удаленно на гитхабе. В этом убедимся с помощью утилиты `gh`.
```sh
gh pr view --json number,title,author
```
вывод:
```
{
  "author": {
    "id": "U_kgDOCjA-pg",
    "is_bot": false,
    "login": "satodim",
    "name": "satodim"
  },
  "number": 1,
  "title": "removed using namespace std"
}
```

### В локальной копии в ветке `patch1` добавьте в исходный код комментарии.

```cpp
// Подключаем библиотеку ввода-вывода
#include <iostream>

int main() {
	// Создаем строку для имени
	std::string name;
	// Принимаем имя
	std::cin >> name;
	// Печатаем
	std::cout << "Hello world from " << name << std::endl;
	return 0;
}
```

### commit, push

```sh
git commit -a -m "added comments"
```

```
[patch1 e87a893] added comments
 1 file changed, 10 insertions(+), 5 deletions(-)
```

```sh
git push origin patch1
```

```
Username for 'https://github.com': satodim
Password for 'https://satodim@github.com': 
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 2 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 488 bytes | 488.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/satodim/lab_02.git
   a6505f6..e87a893  patch1 -> patch1
```

### Проверьте, что новые изменения есть в созданном на шаге 5 pull-request

```sh
gh pr view --json number,title,author,commits
```

```
{
  "author": {
    "id": "U_kgDOCjA-pg",
    "is_bot": false,
    "login": "satodim",
    "name": "satodim"
  },
  "commits": [
    {
      "authoredDate": "2026-03-09T13:31:25Z",
      "authors": [
        {
          "email": "vovkakursk8@gmail.com",
          "id": "U_kgDOCjA-pg",
          "login": "satodim",
          "name": "satodim"
        }
      ],
      "committedDate": "2026-03-09T13:31:25Z",
      "messageBody": "",
      "messageHeadline": "removed using namespace std",
      "oid": "a6505f6297b26b72c249aec334f3d3726b6fc9ff"
    },
    {
      "authoredDate": "2026-03-09T13:40:09Z",
      "authors": [
        {
          "email": "vovkakursk8@gmail.com",
          "id": "U_kgDOCjA-pg",
          "login": "satodim",
          "name": "satodim"
        }
      ],
      "committedDate": "2026-03-09T13:40:09Z",
      "messageBody": "",
      "messageHeadline": "added comments",
      "oid": "e87a8934f708958710a42ab3b99f07d94033dad6"
    }
  ],
  "number": 1,
  "title": "removed using namespace std"
}
```

### В удалённый репозитории выполните слияние PR `patch1 -> master` и удалите ветку `patch1` в удаленном репозитории.

Сделал это на гитхабе

### Локально выполните **pull**.

```sh
git checkout main
git pull origin main
```

```
remote: Enumerating objects: 12, done.
remote: Counting objects: 100% (11/11), done.
remote: Compressing objects: 100% (8/8), done.
remote: Total 8 (delta 4), reused 0 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (8/8), 6.56 KiB | 2.19 MiB/s, done.
From https://github.com/satodim/lab_02
 * branch            main       -> FETCH_HEAD
   b15398a..c56f553  main       -> origin/main
Updating b15398a..c56f553
Fast-forward
 README.md       | 404 ++++++++++++++++++++++++++++++++++++++++++++++++++++++++
 hello_world.cpp |  16 ++-
 2 files changed, 414 insertions(+), 6 deletions(-)
```

### С помощью команды `git log` просмотрите историю в локальной версии ветки **main**.

```
Merge: 95b1f20 e87a893
Author: satodim <vovkakursk8@gmail.com>
Date:   Mon Mar 9 16:42:19 2026 +0300

    Merge pull request #1 from satodim/patch1
    
    removed using namespace std

commit e87a8934f708958710a42ab3b99f07d94033dad6 (origin/patch1, patch1)
Author: satodim <vovkakursk8@gmail.com>
Date:   Mon Mar 9 13:40:09 2026 +0000

    added comments

commit 95b1f2004178644144245fbf06225d419b6ace96
Author: satodim <vovkakursk8@gmail.com>
Date:   Mon Mar 9 16:35:25 2026 +0300

    README.md

commit a6505f6297b26b72c249aec334f3d3726b6fc9ff
Author: satodim <vovkakursk8@gmail.com>
```

### Удалите локальную ветку `patch1`.

```sh
git branch -d patch1
```

```
Deleted branch patch1 (was e87a893).
```
## Part III

### Создайте новую локальную ветку `patch2`.

```sh
git checkout -b patch2
```

### Измените code style с помощью утилиты `clang-format`. Например, используя опцию `-style=Mozilla`.

```sh
clang-format -style=Mozilla -i hello_world.cpp 
```

код:
```cpp
// Подключаем библиотеку ввода-вывода
#include <iostream>

int
main()
{
  // Создаем строку для имени
  std::string name;
  // Принимаем имя
  std::cin >> name;
  // Печатаем
  std::cout << "Hello world from " << name << std::endl;
  return 0;
}
```

### commit, push, создайте pull-request `patch2 -> master`

```sh
git commit -a -m "changed code style"
```

```
[patch2 0c61fbe] changed code style
 1 file changed, 10 insertions(+), 8 deletions(-)
```

```sh
git push origin patch2
```

```
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 4 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 399 bytes | 399.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
remote: 
remote: Create a pull request for 'patch2' on GitHub by visiting:
remote:      https://github.com/satodim/lab_02/pull/new/patch2
remote: 
To https://github.com/satodim/lab_02
 * [new branch]      patch2 -> patch2
```

Также сделаем pull-request и, как и в прошлый раз, проверим его создание с помощью утилиты `gh`:

```sh
gh pr view --json number,title,author,commits
```

```
{
  "author": {
    "id": "U_kgDOCjA-pg",
    "is_bot": false,
    "login": "satodim",
    "name": "satodim"
  },
  "commits": [
    {
      "authoredDate": "2026-03-09T13:55:47Z",
      "authors": [
        {
          "email": "vovkakursk8@gmail.com",
          "id": "U_kgDOCjA-pg",
          "login": "satodim",
          "name": "satodim"
        }
      ],
      "committedDate": "2026-03-09T13:55:47Z",
      "messageBody": "",
      "messageHeadline": "changed code style",
      "oid": "f86f70b391d8b886cd99073695d57d6df6cae7a3"
    }
  ],
  "number": 2,
  "title": "changed code style"
}
```

### В ветке `main` в удаленном репозитории измените комментарии, например, расставьте знаки препинания, переведите комментарии на другой язык.

Переключимся на векту `main`

```sh
git checkout main
```

И переведем комментарии на английский:
```cpp
// including standard IO library
#include <iostream>

int main() {
	// creating string for name
	std::string name;
	// recieving name
	std::cin >> name;
	// printing "hello world from name"
	std::cout << "Hello world from " << name << std::endl;
	return 0;
}
```

Ну и по классике:

```sh
git commit -a -m "translated comments"
```

```
[main a053462] translated comments
 1 file changed, 4 insertions(+), 4 deletions(-)
```

```sh
git push origin main
```

```
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 4 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 443 bytes | 443.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/satodim/lab_02
   e122c12..a053462  main -> main
```

### Теперь переключимся на ветку `patch2`
```sh
git checkout patch2
```

И проверим наш pull-request, в этот раз посмотрим в том числе и на параметр `mergeable`
```sh
gh pr view --json number,title,author,commits,mergeable
```

```
{
  "author": {
    "login": "satodim"
  },
  "commits": [
    {
      "authoredDate": "2026-03-07T16:31:41Z",
      "authors": [
        {
          "email": "vovkakursk8@gmail.com",
          "id": "U_kgDOCjA-pg",
          "login": "satodim",
          "name": "satodim"
        }
      ],
      "committedDate": "2026-03-07T16:31:41Z",
      "messageBody": "",
      "messageHeadline": "changed code style",
      "oid": "0c61fbe7eda89afec7299c556e6f3c4f32d4af45"
    }
  ],
  "mergeable": "CONFLICTING",
  "number": 2,
  "title": "part 3"
}
```

И как можно заметить, этот параметр равен `CONFLICTING`, то есть действительно присутствуют конфликты.

### Для этого локально выполните `pull` + `rebase` (точную последовательность команд, следует узнать самостоятельно). Исправьте конфликты.

Для начала на всякий случай подтянем ветку `main`, чтобы она была синхронизированна с удалённым репозиторием.

```sh
git checkout main
git pull origin main
```

У меня оно и так уже было up-to-date, поэтому я получил следующий вывод:

```
From https://github.com/satodim/lab_02
 * branch            main       -> FETCH_HEAD
Already up to date.
```

Дальше переключаемся на другую ветку и пытаемся ее перебазировать:

```sh
git checkout patch2
git rebase main
```

На что гит выведет следующее сообщение:
```
Auto-merging hello_world.cpp
CONFLICT (content): Merge conflict in hello_world.cpp
error: could not apply 0c61fbe... changed code style
hint: Resolve all conflicts manually, mark them as resolved with
hint: "git add/rm <conflicted_files>", then run "git rebase --continue".
hint: You can instead skip this commit: run "git rebase --skip".
hint: To abort and get back to the state before "git rebase", run "git rebase --abort".
Could not apply 0c61fbe... changed code style
```

А `hello_world.cpp` стал вот таким:

```cpp
// including standard IO library
#include <iostream>

<<<<<<< HEAD
int main() {
	// creating string for name
	std::string name;
	// recieving name
	std::cin >> name;
	// printing "hello world from name"
	std::cout << "Hello world from " << name << std::endl;
	return 0;
=======
int
main()
{
  // Создаем строку для имени
  std::string name;
  // Принимаем имя
  std::cin >> name;
  // Печатаем
  std::cout << "Hello world from " << name << std::endl;
  return 0;
>>>>>>> 0c61fbe (changed code style)
}
```

Исправим конфликт, совместив английские комментарии с другим стилем кода:
```sh
// including standard IO library
#include <iostream>

int
main()
{
  // creating string for name
  std::string name;
  // recieving name
  std::cin >> name;
  // printing "hello world from name"
  std::cout << "Hello world from " << name << std::endl;
  return 0;
}
```

Теперь пометим этот файл как переделанный с помощью команды 
```sh
git add hello_world.cpp
```

И продолжим перебазирование:
```sh
git rebase --continue
```

Других конфликтов не возникло. Гит предложил ввести название этого перебазирования и потом вывел это:
```
[detached HEAD cceff5a] changed code style and translated comments
 1 file changed, 10 insertions(+), 8 deletions(-)
Successfully rebased and updated refs/heads/patch2.
```

### Сделайте force push в ветку `patch2`

```sh
git push --force origin patch2
```

```
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 4 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 466 bytes | 466.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/satodim/lab_02
 + 0c61fbe...cceff5a patch2 -> patch2 (forced update)
```

### Убедитесь, что в pull-request пропали конфликтны.

Делаем это уже привычным для нас образом

```sh
gh pr view --json number,title,author,commits,mergeable
```

```
{
  "author": {
    "login": "satodim"
  },
  "commits": [
    {
      "authoredDate": "2026-03-07T16:31:41Z",
      "authors": [
        {
          "email": "vovkakursk8@gmail.com",
          "id": "U_kgDOCjA-pg",
          "login": "satodim",
          "name": "satodim"
        }
      ],
      "committedDate": "2026-03-07T18:10:13Z",
      "messageBody": "",
      "messageHeadline": "changed code style and translated comments",
      "oid": "cceff5a8b18ac71a7e12a995b186f2048bc4ff5a"
    }
  ],
  "mergeable": "MERGEABLE",
  "number": 2,
  "title": "part 3"
}
```

Теперь переменная `mergeable` равна `MERGEABLE`.

### Вмержите pull-request `patch2` -> `master`.

Сделал это на гитхабе.

Теперь можно посмотреть последние 2 коммита и убедиться, что слияние прошло успешно:
```sh
git checkout main
git log -2
```

```
commit a37547d1e626f4f6e41e9f77499c67655d1522b5 (HEAD -> main, origin/main)
Merge: a053462 cceff5a
Author: satodim <88584860+satodim@users.noreply.github.com>
Date:   Sat Mar 9 21:27:39 2026 +0300

    Merge pull request #2 from satodim/patch2
    
    part 3 step 9

commit cceff5a8b18ac71a7e12a995b186f2048bc4ff5a (origin/patch2, patch2)
Author: satodim <vovkakursk8@gmail.com>
Date:   Sat Mar 9 19:31:41 2026 +0300

