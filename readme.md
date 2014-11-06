#InternshipDB [Laravel]

##Disclaimer

 This project is based on [Laravel](https://github.com/laravel/laravel). 

##Recommendations

For the development you are recommended to use [Laravel Homestead](https://github.com/laravel/homestead). 
>**Homestead** is the Vagrant-Box specially tuned for the efficient Laravel development. 
>
>Homestead includes:
>  * Ubuntu 14.04 LTS
>  * PHP 5.5
>  * Ngnix
>  * MySQL
>  * Postgres
>  * etc

Before using Homestead you must install [Vagrant](https://www.vagrantup.com/) and [VirtualBox](https://www.virtualbox.org). 

##Enviroment setup [Homestead]
First of all, the Homestead-box must be added to Vagrant. Open your terminal (Windows: [GitBash](http://git-scm.com/download)) and type in:
```
vagrant box add laravel/homestead
```
This command downloads the Homestead-box from the [VagrantCloud](https://vagrantcloud.com/).
But if you want to add predownloaded box, then run this command in your terminal:
```
vagrant box add {init_name} {path/file_name.box} 
```

Clone the Homestead configuration from the repository to the project directory.
```
git clone https://github.com/laravel/homestead.git
```

Before you proceed further, you must order the structure of folders.
```xml
code/
 -----projects/

 -----homestead/
```
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
  - map: homestead.app                                     --> address for accessing from host_machine
    to: /home/vagrant/code/projects/laravel-intern/public  --> path to the entry point on virtual_machine
    
```

>If you have added the Homestead-box locally you must open the `homestead/scripts/homestead.rb`file and change the name of box >to be initialised.
>```ruby
>    # Configure The Box
>    config.vm.box = "laravel/homestead"    <---- change this 
>    config.vm.hostname = "homestead"
>```
>To recall the name of box just run the following command:
>```
>vagrant box list
>```
