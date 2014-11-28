#InternshipDB [Laravel]

##Отказ от ответственности

 Основой этого проета является [Laravel](https://github.com/laravel/laravel). 

##Рекомендация

For the development you are recommended to use [Laravel Homestead](https://github.com/laravel/homestead). 
>**Homestead** это Vagrant-бокс образ виртуальной машины специально настроенный для разработки на Laravel. 
>
>Homestead включает в себя:
>  * Ubuntu 14.04 LTS
>  * PHP 5.5
>  * Ngnix
>  * MySQL
>  * Postgres
>  * и прочее

Перед использванием Homestead вам следует установить [Vagrant](https://www.vagrantup.com/) и [VirtualBox](https://www.virtualbox.org). 

##Настройка окружения [Homestead]
Прежде всего, Homestead-бокс должен быть добавлен в Vagrant. Откройте терминал (Windows: [GitBash](http://git-scm.com/download)) и выполните следующую команду:
```
vagrant box add laravel/homestead
```
Эта комманда скачивать готовый бокс с облачного хранилища [VagrantCloud](https://vagrantcloud.com/).
Но если вы уже локально располагаете заранее загруженным Homestead-боксом выполните данную комманду, указав новое название и нынешнее расположение загруженного бокса:
```
vagrant box add {init_name} {path/file_name.box} 
```

Клонируйте конфигурационные файлы Homestead из репозитария в рабочую папку.
```
git clone https://github.com/laravel/homestead.git
```

Перед тем как продолжить, вы должны определиться со структурой проекта.
```
code/
 -----projects/

 -----homestead/
```
Вам также понадобятся ssh-ключи.
>Если у вас их нет можете их сгенерировать:
>```ruby
>ssh-keygen -t rsa -C "your@email.com"
>```

В скопированной папке `homestead` необходимо редактировать файл `Homestead.yaml`.

```

---
ip: "192.168.10.10" 
memory: 2048        
cpus: 1             

authorize: /Users/{user_name}/.ssh/id_rsa.pub   --> путь к публичному ssh_key

keys:
  - /Users/{user_name}/.ssh/id_rsa              --> путь к приватному ssh_key

folders:                        
  - map: {work_path}/code/projects              --> путь к папке с проктом на гостевой машине (для синхронизации)        
    to: /home/vagrant/code/project              --> путь к папке на виртиальной машине

sites:                                      
  - map: internship.app                                     --> address for accessing from host_machine
    to: /home/vagrant/code/projects/laravel-intern/public  --> path to the entry point on virtual_machine
    
```
Внесите некоторые изменения в `hosts` file(`C:\Windows\System32\drivers\etc\hosts`).
```
127.0.0.1 internship.app
```


>Если вы добавили Homestead-бокс локально, то вам следует изменить название используемого бокса в файле `homestead/scripts/homestead.rb`.
>```ruby
>    # Configure The Box
>    config.vm.box = "laravel/homestead"    <---- укажите имя бокса 
>    config.vm.hostname = "homestead"
>```
>Этой коммандой можно вывести весь список доступных Vagrant-боксов:
>```
>vagrant box list
>```

Вы уже готовы клонировать этот проект в папку `projects`:
```
git clone https://github.com/kafadar/laravel-intern.git
```

Теперь осталось лишь инициализировать виртуальную машину. В папке `homestead` выполните данную комманду:
```
vagrant up
```
Спустя некоторое время, вы можете получить доступ к созданной виртуальной машине через комманду `vagrant ssh`.

>Or you can set up database connections in `laravel-intern/app/config/database.php`.

