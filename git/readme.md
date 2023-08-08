## Конфигурация Git

##### Отобразить глобальные переменные:
```bash
git config --list
```
##### Создание глобальных переменных:
```bash
git config --global user.name vik
git config --global user.email vik1988kms@gmail.com
```
##### Изменить редактор по умолчанию 
По умолчанию используется vi:
```bash
git config --global core.editor emacs
```
##### Добавление алиасов
```bash
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr)%C(bold blue)<%an>%Creset' --abbrev-commit"
```
После этой команды можно использовать git lg вместо стандартного git log.

##### Создаем глобальный `.gitignore`
Cоздаем файл ~/.gitignore_global с содержанием (например):
```
# Файлы редакторов Emacs или Vim
*~
.*.swp
# Игнорирует файлы .DS_Store
.DS_Store
# Игнорирует директорию .vscode/
.vscode/
# Игнорирует директорию .idea/
.idea/
# Не игнорируем указанный файл в директории .vscode
!.vscode/settings.json
```
и выполните команду 

```bash
git config --global core.excludesfile ~/.gitignore_global
```
то Git больше не потревожит на счёт этих файлов.

## Git command

[git init](https://git-scm.com/docs/git-init) - инициализация репозитория. <br>
[git add](https://git-scm.com/docs/git-add) - добавление файлов в состояние staged. <br>
  * `git add <список файлов>` - git add file1 file2
  * `git add . ` - добавить все файлы в текущей папке
  * `git add *.py` - добавить все файлы в текущей папке с расширением .py
  * `git add *.py` - добавить все файлы в текущей папке с расширением .py
  * `git add folder/*.py` - добавить все файлы в папке folder с расширением .py
  * `git add folder/` - добавить все файлы в папке folder
  * `git add "*.py"` - добавить все файлы в проекте с расширением .py

[git commit -m "message"](https://git-scm.com/docs/git-commit) - сделать коммит с сообщением message. Файлы в состоянии "committed"
  * `git commit -a -m "message"` - добавить все модифицированные файлы (за исключением новых или не отслеживаемых) и делает коммит с сообщением message
  * `git commit --amend -m "message"` - добавляет изменения, изменяет сообщение message у последнего коммита.

[git diﬀ](https://git-scm.com/docs/git-diff) - Показывает разницу между текущим неотслеживаемым состоянием репозитория и последним снимком репозитория
  * `git diﬀ --staged` -  показывает разницу между текущим отслеживаемым состоянием репозитория и последним снимком репозитория
  * `git diﬀ commit_id` - показывает разницу между текущим состоянием репозитория и указанным снимком репозитория

[git reset](https://git-scm.com/docs/git-reset) - для отмены каких-либо изменений в проекте, откату проекта к какому-то снимку <br>
`git reset [--soft | --mixed | --hard] [COMMIT]`
![image](https://github.com/viktorburimskiy/helper/assets/62743337/37d0e5f1-f717-4c60-88f4-3d287e68c108)

  * `--soft`  - возвращает на указанный коммит и переводит все коммиты после указанного в отслеживаемую зону (staged)
  * `--mixed` - возвращает на указанный коммит и переводит все коммиты после указанного в неотслеживаемую зону (unstaged)
  * `--hard`  - возвращает на указанный коммит и УДАЛЯЕТ ВСЕ коммиты после указанного.
  * `COMMIT` - указатель на коммит или на HEAD.
    * `HEAD^` - откатиться на 1 коммит.
      ![image](https://github.com/viktorburimskiy/helper/assets/62743337/e8a2a703-5199-4498-bc89-bcdbd2bdaeec)

    * `HEAD^^ или HEAD~2` - откатиться на 2 коммита.
      ![image](https://github.com/viktorburimskiy/helper/assets/62743337/e1450244-c32c-420c-8cb5-45764db7f3fe)

    * `HASH` - указатель на HASH коммита.
      ![image](https://github.com/viktorburimskiy/helper/assets/62743337/2ceac5b7-be21-46bb-b67f-638011fe2223)

[git checkout](https://git-scm.com/docs/git-checkout) - используется для перемещения, между коммитами, версиями отдельных файлов и ветками.
  * `git checkout <BRANCH>` - переключиться на ветку `<BRANCH>`
  * `git checkout [COMMIT | BRANCH]` - `COMMIT` - указатель на коммит, `BRANCH` - указатель на ветку
  * `git checkout [COMMIT | BRANCH] -- [FILES]` - `--` - указатель, что дальше нет команд, только текст FILES - путь до фала(ов)
  * `git checkout -b <BRANCH>` - создать и переключиться на ветку `<BRANCH>`

[git clean](https://git-scm.com/docs/git-clean) `-n` - выведет список не отслеживаемых файлов которые можно удалить `git clean -f` - удаляет файлы из репозитория

[git remote](https://git-scm.com/docs/git-remote) - управляет набором отслеживаемых репозиториев
  * `git remote -v` - список удалённых репозиториев
  * `git remote show <NAME>` - показать информацию об удалённом репозитории `<NAME>`
  * `git remote add <NAME> <URL>` - добавление репозитория `<NAME>` - название репозитория `<URL>` - ссылка, путь к репозиторию

[git push](https://git-scm.com/docs/git-push) `<NAME> <BRANCH>` - отправить изменения в репозиторий по ссылке `<NAME>` ветку `<BRANCH>`. Push первого изменения на сервер осуществляется командой: `git push --set-upstream <NAME> <BRANCH>`

[git pull](https://git-scm.com/docs/git-pull) `<NAME> <BRANCH>` - забрать изменения из репозиторий по ссылке `<NAME>` ветку `<BRANCH>` 

[git branch](https://git-scm.com/docs/git-branch) - получить список всех имеющихся веток и показывает на текущий HEAD
  * `git branch -d <BRANCH>` - удалить ветку `<BRANCH>`
    * `-d` - простое удаление
    * `-D` - --force удаление. Удаление ветки `<BRANCH>` не смотря ни на что.
  * `git branch -r` - получить список всех веток которые находятся на удалённом репозитории
  * `git branch --merged` - список всех веток, соединённых с текущей
  * `git branch --no-merged` - список всех не соединённых с текущей веток.

[git merge](https://git-scm.com/docs/git-merge) `<BRANCH>` - влить в текущую ветку (куда указывает HEAD) с веткой `<BRANCH>`

[git fetch](https://git-scm.com/docs/git-fetch) - получить информацию об изменениях в удалённом репозитории. `git pull = git fetch && git merge <name> <BRANCH>`

[git rebase](https://git-scm.com/docs/git-rebase) `<BRANCH> `- сделать перебазирование текущей ветки поверх ветки `<BRANCH>`. Нежелательно использовать в публичных ветвях: он изменяет историю коммитов. Поэтому после rebase’а может возникнуть проблема с push’ем.

[git cherry-pick](https://git-scm.com/docs/git-cherry-pick) `[COMMAND] <hash>` - взять коммит и скопировать его в текущую ветку
  * `--edit` - и поменять сообщение коммита
  * `--no-commit` - и помещаем в отслеживаемую зону без коммита в нашу ветку
  * `-x` - и указать в сообщение hash того коммита, из которого мы сделали cherry-pick
  * `--signoff` - и указать в сообщении коммита имя того пользователя, кто совершил cherry-pick

[git log](https://git-scm.com/docs/git-log) - получить историю коммитов в репозитории
  * `git log --oneline` - каждый коммит в одной строке. Кроме того, она показывает лишь префикс ID коммита.
  * `git log --oneline --decorate` - Печатает все относительные имена показанных коммитов.
  * `git log --oneline --graph` - тоже самое, но в виде дерева (графа)
  * `git log --color --pretty=format:"%C(yellow)%h%C(reset) %s%C(bold red)%d%C(reset) %C(green)%ad%C(reset) %C(blue)[%an]%C(reset)" --relative-date --decorate` - можем узнать дату и автора коммита.

[git show](https://git-scm.com/docs/git-show) `<hash>` - показать содержимое коммита



## Отмена слияния
```bash
# опасная операция тк затирает историю предыдущих комитов
git checkout master
git log
git reset --hard 72ead1c4c1778c23c277c4f15bbb68f3bb205f54
git push -f
```
или
```bash
# безопасный способ - создает новый комит с отмененными изменениями
git revert HEAD
git push -f origin
```
