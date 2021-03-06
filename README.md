# dpodvyaznikov_infra
dpodvyaznikov Infra repository

-------------

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
