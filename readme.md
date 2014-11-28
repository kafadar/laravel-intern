#InternshipDB [Laravel]

##Отказ от ответственности

 Основой этого проета является [Laravel](https://github.com/laravel/laravel). 

##Рекомендация

For the development you are recommended to use [Laravel Homestead](https://github.com/laravel/homestead). 
>**Homestead** это Vagrant-бокс образ виртуальной машины) специально настроенный для разработки на Laravel. 
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
Но если вы уже локально располагаете готовым боксом выполните данную комманду, указав новое название и нынешнее расположение б:
```
vagrant box add {init_name} {path/file_name.box} 
```

Клонируйте конфигурационные файлы Homestead из репозитария в рабочую папку.
```
git clone https://github.com/laravel/homestead.git
```

Before you proceed further, you must order the structure of folders.
```
code/
 -----projects/

 -----homestead/
```
From this moment you will need ssh-keys.
>If not, generate them:
>```ruby
>ssh-keygen -t rsa -C "your@email.com"
>```

In the cloned folder `homestead` you must configure the `Homestead.yaml` file.

```

---
ip: "192.168.10.10" 
memory: 2048        
cpus: 1             

authorize: /Users/{user_name}/.ssh/id_rsa.pub   --> path to the public ssh_key

keys:
  - /Users/{user_name}/.ssh/id_rsa              --> path to private ssh_key

folders:                        
  - map: {work_path}/code/projects              --> folder on your host_machine (for synchronization)        
    to: /home/vagrant/code/project              --> path to sync_folder on virtual_machine

sites:                                      
  - map: internship.app                                     --> address for accessing from host_machine
    to: /home/vagrant/code/projects/laravel-intern/public  --> path to the entry point on virtual_machine
    
```
Make some adjustments in the `hosts` file(`C:\Windows\System32\drivers\etc\hosts`).
```
127.0.0.1 internship.app
```


>If you have added the Homestead-box locally you must open the `homestead/scripts/homestead.rb`file and change the name of box to be initialised.
>```ruby
>    # Configure The Box
>    config.vm.box = "laravel/homestead"    <---- change this 
>    config.vm.hostname = "homestead"
>```
>To recall the name of box just run the following command:
>```
>vagrant box list
>```

You are ready to go. But first let's clone **this repository** to the `projects` folder. In `projects`folder run this command:
```
git clone https://github.com/kafadar/laravel-intern.git
```

Here the magic happens. To initialise the virtual_machine just run the following command in the `homestead`folder:
```
vagrant up
```
It will take some time, but after you can able to access your machine with `vagrant ssh` command. 
>To make Laravel able to access MySQL you can create `.env.local.php` file in the root of project with following contents:
>```php
>return [
>	'DB_HOST' => 'localhost',
>	'DB_NAME' => {database_name},
>	'DB_USERNAME' => 'homestead',
>	'DB_PASSWORD' => 'secret'];
>```
>Or you can set up database connections in `laravel-intern/app/config/database.php` file.

To initialise the laravel-intern project just run `composer install` command in the root folder on your virtual_machine. Your web project is now accessible by the following address `internship.app:8000` or `127.0.0.1` (if the `hosts` was not changed). 

On you host access the `internship.app:8000`. If everything went fine you will see the following screen:

![You have arrived](https://pbs.twimg.com/media/BLYFfmLCAAEHcZL.png)
