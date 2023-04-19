# Возможности плейбука:
1. Настройка репозитория для Ubuntu 18.04 - `ansible-playbook run-repo.yml --tags=setup`
2. Сборка из исходных кодов https://github.com/peervpn/peervpn `ansible-playbook run-peervpn.yml --tags=build`
3. Упаковка в .deb `ansible-playbook run-peervpn.yml --tags=deb`
4. Публикация получившегося deb в репо `ansible-playbook run-repo.yml --tags=add`
5. Установка peervpn из репозитория `ansible-playbook run-peervpn.yml --tags=install`



# Переменные:
### roles/repository/vars/main.yml
**repo_server_name** - имя виртуального хоста репозитория. По-умолчанию localhost.servapp.ru (dummy-домен, резолвится в 127.0.0.1)



### roles/peervpn/vars/main.yml
**repo_url** - url по которому скрипт ожидает http доступ к репозиторию. По-умолчанию По-умолчанию localhost.servapp.ru (dummy-домен, резолвится в 127.0.0.1)

**deb_revision** - переменная используется для сборки .deb подставляется в значение номера ревизии пакета. По-умолчанию 1

**build_deb_path** - Путь, куда будут складываться собранные .deb пакеты. Должен указывать на папку files роли repository. На случай нестаддартного расположения ролей



# Использование
0. Указать в `inventory/dev/inventory` сервер(а)
1. В `run-peervpn.yml` и `run-repo.yml` указать соответствующие хосты (для репо и для сборки)
2. Указать  `repo_url` и `repo_server_name` (если тестируется на одном сервере, то можно оставить умолчания)
3. Настроить репо `ansible-playbook run-repo.yml --tags=setup`
4. Собрать бинарный пакет из исходного кода и упаковать его в .deb `ansible-playbook run-peervpn.yml --tags=build,deb`
5. Добавить .deb в репо `ansible-playbook run-repo.yml --tags=add`
6. Установить (при необходимости добавить хосты в run-peervpn.yml) `ansible-playbook run-peervpn.yml --tags=install`
