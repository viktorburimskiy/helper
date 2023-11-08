## SSH

##### Проверить статус службы:
```bash
service ssh status
```
##### Установка:
```bash
sudo apt-get install openssh-server
```
##### Генерация ключей:
```bash
ssh-keygen
# Generating public/private rsa key pair.
# Enter file in which to save the key (/home/vik/.ssh/id_rsa): -можем задать свое имя (по умолчанию id_rsa)
```
Проверяем пары:
```bash
ls -l ~/.ssh 
#total 8
#-rw-------. 1 vik vik 1743 Oct 23 12:07 id_rsa
#-rw-r--r--. 1 vik vik  397 Oct 23 12:07 id_rsa.pub
```

ls -l ~/.ssh


##### Подключение с заданным пользователем (без указания юзера будет браться текущий):
```bash
ssh remote_user@host 
```
##### Подключение с использованием файла ключей
1. Копируем значение нашего публичного ключа `id_rsa.pub`.
2. Подключаемся к серверу по паролю
3. Переходим в каталог ssh `cd .ssh/`
4. Создаем файл: `nano authorized_keys`
5. Вставляем наш публичный ключ. Можно добавлять несколько ключей (1 строка = 1 ключ)
6. Меняем пермишен, чтобы доступ был к ключю только у владельца: ` chmod 0600 authorized_keys` 

```bash
# если имя файла приватного ключа отличный от имени id_rsa, то необходимо явно указать его через параметр -i
ssh -i ~/.ssh/my_private_key remote_user@host
```


##### Множества SSH ключей для подключения на разные Linux (ssh config)
  * Глобальный файл конфигурации SSH 

    `/etc/ssh/ssh_config`
  * Пользовательский файл конфигурации SSH

    `~/.ssh/config`


1. Создаем config файл:
    ```bash
    cd .ssh
    nano config
    
    # заполняем файл:
    Host my_ubuntu
         HostName 192.168.0.1 #можно так же dns имя
         User vik
         Port 22
    ```
2. Меняем пермишен
    ```bash
    chmod 0600 config
    ```
3. Подключаемся
    ```bash
    ssh my_ubuntu
    ```
##### Если хотим убрать вывод fingerprint при подключении
В файл config дописываем
```bash
    nano config
    # дописываем файл:
    ...
         
    Host *
         StrictHostKeyChecking no #чтобы не выводил fingerprint
         UserKnownHostsFile /dev/null #чтобы не создавал файл known_host
```

##### Дополнение (подключение с помощью *.pem файлов)
1. В файл config редактируем
```bash
    nano config
    # заполняем файл:
    #---------------------------------------------------------------------------------
    Host my_ubuntu
         HostName 192.168.0.1 #можно так же dns имя
         User vik
         Port 22
    #---------------------------------------------------------------------------------
    # ко всем хостам которые оканчиваются на node1.newprolab.com    
    Host *node1.newprolab.com
         User vb-user1
         IdentityFile ~/.ssh/newprolab1.pem
    #---------------------------------------------------------------------------------     
    # ко всем хостам которые оканчиваются на node2.newprolab.com
    Host *node2.newprolab.com
         User vb-user2
         IdentityFile ~/.ssh/newprolab2.pem
    #---------------------------------------------------------------------------------
    Host *
         StrictHostKeyChecking no #чтобы не выводил fingerprint
         UserKnownHostsFile /dev/null #чтобы не создавал файл known_host
    #---------------------------------------------------------------------------------
```
2. Подключаемся:
```bash
ssh spark-node1.newprolab.com
```