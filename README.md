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
