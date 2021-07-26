# Lab10
## Изучение процесса создания и конфигурирования виртуальной среды разработки с использованием **Vagrant**
### Tutorial

Создаём переменные окружения
```sh
$ export GITHUB_USERNAME=Solomatin-Sergey
$ export PACKAGE_MANAGER=apt
```
Переходим в рабочий каталог и устанавливаем туда vagrant
```sh
$ cd ${GITHUB_USERNAME}/workspace
$ ${PACKAGE_MANAGER} install vagrant
```

```sh
Узнаём версию vagrant
$ vagrant version
Создаётся Vagrantfile
$ vagrant init bento/ubuntu-19.10
Открываем Vagrantfile
$ less Vagrantfile
Перезаписать существующий Vagrantfile и использовать минимальный шаблон файла Vagrantfile (без комментариев в справке)
$ vagrant init -f -m bento/ubuntu-19.10
```

```sh
$ mkdir shared
```
>> Записываем в Vagrantfile всю необходимую информацию (с комментариями), этот файл можно посмотреть выше.
```sh
Проверяем файл Vagrantfile
$ vagrant validate
Определяем состояние vagrant машины
$ vagrant status
Запускается vagrant среда
$ vagrant up # --provider virtualbox
Отображается информацию о сопоставлениях гостевых портов
$ vagrant port
$ vagrant status
Подключается к виртуальной машине по SSH
$ vagrant ssh
Перечисляются все snapshot, сделанные для машины
$ vagrant snapshot list
Делается снимок текущего состояния машины и "вставляется" в стек состояний.
$ vagrant snapshot push
$ vagrant snapshot list
Останавливает vagrant машину
$ vagrant halt
Восстанавливается состояние, которое было помещено в стек snapshots с помощью "vagrant snapshot push".
$ vagrant snapshot pop
```

```ruby
Для работы с VMware EXSI 
(это аппаратный гипервизор, который удобно устанавливается на сервер и дает возможность запускать на нем несколько виртуальных машин) 
используются следующие настройки:
  config.vm.provider :vmware_esxi do |esxi|
Имя, которое присваивается компьютеру, подключенному к сети
    esxi.esxi_hostname = '<exsi_hostname>'
Имя пользователя
    esxi.esxi_username = 'root'
Это будет запрашивать у вас пароль esxi каждый раз, когда вы
выполните команду vagrant. Это значение по умолчанию.
    esxi.esxi_password = 'prompt:'
SSH port. Default port 22.
    esxi.esxi_hostport = 22
Имя виртуальной машины
    esxi.guest_name = '${GITHUB_USERNAME}'
Имя пользователя гостевой машины. The default is 'vagrant'.
    esxi.guest_username = 'vagrant'
Количество памяти для гостевой машины в мб.
Переопределение размера памяти.
По умолчанию используется размер памяти, указанный в файле .vmx, однако здесь вы можете указать новое значение.
    esxi.guest_memsize = '2048'
Переопределение виртуальных процессоров
По умолчанию используется указанное количество виртуальных процессоров в файле vmx, однако здесь вы можете указать новое значение.   
    esxi.guest_numvcpus = '2'
Указывается тип диска. В данном случае по умолчанию.   
    esxi.guest_disk_type = 'thin'
  end
```

```sh
Устанавливаем плагин vagrant-vmware-esxi 
$ vagrant plugin install vagrant-vmware-esxi 
Список плагинов
$ vagrant plugin list
Создаётся машина с provider под названием vmware_esxi
$ vagrant up --provider=vmware_esxi
```
