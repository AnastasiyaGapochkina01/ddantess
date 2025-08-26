1) Написать роль для установки node-exporter НЕ в docker
2) Написать роль для настройки времени и часового пояса с помощью chrony или ntpd
3) Написать роль для установки и настройки auditd; роль должна включать
- настройку основного конфигурационного файла /etc/audit/auditd.conf через шаблон Jinja2 и переменные
  -  log_file
  -  max_log_file
  -  num_logs
  -  space_left_action
  -  admin_space_left
- управление правилами аудита: размещение правил в /etc/audit/rules.d/security.rules с помощью шаблона и переменных
```yaml
auditd_rules:
  - "-a always,exit -F arch=b64 -S open,openat -F success=1"
  - "-w /etc/passwd -p wa -k identity"
  - "-w /etc/sudoers -p wa -k scope"
```
4) Написать роли для развертывания приложения https://gitlab.com/devops201206/visits НЕ в docker
5) Написать роль для установки postgresql НЕ из стандартных репозиториев и его настройки
- замена listen_addresses на 0.0.0.0
- создание БД `ecom_db` с владельцем `ecom` (пароль `secretecom1234`)
6) Написать роль которая будет настраивать сервер после его создания
создание админского пользователя с правами суперпользователя без пароля на sudo с известным публичным ключом
- установка базовых пакетов
	- git
	- curl
	- wget
	- bash-completion
	- ncdu
	- atop
	- iotop
- установка параметра ядра `net.ipv4.ip_forward`
- настройка кастомного баннера при входе с помощью motd

7) Написать роль для полного цикла развертывания WordPress Stack: Nginx, PHP, MySQL
