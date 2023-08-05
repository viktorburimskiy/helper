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

## Отмена слияния
```bash
git checkout master
git log
git reset --hard 72ead1c4c1778c23c277c4f15bbb68f3bb205f54
git push -f
```
или
```bash
git revert HEAD
git push -f origin
```
