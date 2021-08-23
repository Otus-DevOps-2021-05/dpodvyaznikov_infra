# dpodvyaznikov_infra
dpodvyaznikov Infra repository

=======
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
   HostName 84.252.131.34
   User appuser
   IdentityFile ~/.ssh/appuser

# someinternalhost
Host someinternalhost
   HostName 10.128.0.34
   User appuser
   IdentityFile ~/.ssh/appuser
   ProxyJump bastion

```

3.Подключиться к someinternalhost:

```shell

ssh someinternalhost

```

=======
## Домашнее задание №2: play-travis
* Добавлен pre-commit hook и шаблон для PR
* Добавлена интеграция уведомлений в Slack
* Настроено выполнение тестов в Github Actions
* [Github Actions status](https://github.com/Otus-DevOps-2021-05/dpodvyaznikov_infra/actions/workflows/run-tests.yml) <br>
![Test](https://github.com/Otus-DevOps-2021-05/dpodvyaznikov_infra/actions/workflows/run-tests.yml/badge.svg)<br>
