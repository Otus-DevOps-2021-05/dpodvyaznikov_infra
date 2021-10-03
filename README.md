# dpodvyaznikov_infra
dpodvyaznikov Infra repository

-------------

## Домашнее задание №6: terraform-1

* Созданы ветка `terraform-1`, в ней каталог **terraform** с **main.tf** внутри и обновлены исключения в **.gitignore**
* Отредактирован **main.tf** и создан инстанс с помощью **terraform**
*Для корректной работы необходимо изменить в **main.tf** количество ядер с 1 на 2:*
```
...
  resources {
    cores  = 2
    ...
  }
  ...
```
* Создан **outputs.tf** для сохранения параметров полученного инстанса.
* Созданы файлы для запуска приложения в директории **files**; настроены провижионеры, дополнен **main.tf**
* Запущен инстанс с автозапуском приложения

## Домашнее задание №5: packer

* Заполнен шаблон **ubuntu16.json**

*Для корректной работы шаблона необходимо добавить в шаблон строки:*
```json
{
   "use_ipv4_nat": true,
   "zone": "ru-central1-a",
   "subnet_id": "my_subnet_id"
}
```

* Проверен и собиран образ
```bash
>>> packer validate ./ubuntu16.json
>>> packer build ./ubuntu16.json
```
*Для корректной работы необходимо добавить в скрипты **install_ruby.sh** и **install_mongodb.sh**, строчку:*
```bash
echo "sleep 3m for install updates"; sleep 5m; echo "start install ..."
```
* Созданы файлы с переменными **variables.json** и **variables.json.example**, первый добавлен в **.gitignore**
```json
{
  "key": "key.json",
  "fid": "qwe",
  "image": "ubuntu-1604-lts"
}
```

* Для валидации в travis создан **key.json.example** идентичный рабочему
```json
{
   "id": "qwe",
   "service_account_id": "rty",
   "created_at": "2021-10-03T09:09:29Z",
   "key_algorithm": "RSA_2048",
   "public_key": "-----BEGIN PUBLIC KEY-----\n",
   "private_key": "-----BEGIN PRIVATE KEY-----\n"
}
```

## Домашнее задание №4: bastion

Адреса хостов:

```shell

testapp_IP = 62.84.118.84
testapp_port = 9292
```

Команда CLI для запуска тестового приложения:

yc compute instance create
--name reddit-app
--hostname reddit-app
--memory=4
--create-boot-disk image-folder-id=standard-images,image-family=ubuntu-1604-lts,size=10GB
--network-interface subnet-name=default-ru-central1-a,nat-ip-version=ipv4
--metadata serial-port-enable=1 --zone=ru-central1-a
--metadata-from-file user-data=startup_script.yml

## Домашнее задание №3: bastion

Адреса хостов:

```shell

bastion_IP = 130.193.38.163
someinternalhost_IP = 10.128.0.29
```
#### Для подключения к someinternalhost_IP напярмую с локальной машины необходимо:

1.Создать на локальном хосте файл *config* в каталоге ~/.ssh

2.Добавить в него следующую конфигурацию:

```shell

# bastion
Host bastion
   HostName 130.193.38.163
   User appuser
   IdentityFile ~/.ssh/appuser

# someinternalhost
Host someinternalhost
   HostName 10.128.0.29
   User appuser
   IdentityFile ~/.ssh/appuser
   ProxyJump bastion

```

3.Подключиться к someinternalhost:

```shell

ssh someinternalhost

```

-------------
## Домашнее задание №2: play-travis
* Добавлен pre-commit hook и шаблон для PR
* Добавлена интеграция уведомлений в Slack
* Настроено выполнение тестов в Github Actions
* [Github Actions status](https://github.com/Otus-DevOps-2021-05/dpodvyaznikov_infra/actions/workflows/run-tests.yml) <br>
![Test](https://github.com/Otus-DevOps-2021-05/dpodvyaznikov_infra/actions/workflows/run-tests.yml/badge.svg)<br>
