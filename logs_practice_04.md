# MicroBlog
## Инфраструктура
#### Backend
Машина `microblog`:
- IP:
- User: devops
- Pass: 0000
#### Database
Машина `blog-mongo-cluster`
- IP:
- User: devops
- Pass: 0000
#### Разработка
Стек:
1) nodejs
2) mongodb

Код бэкенда лежит в /var/www/blog, запущен как systemd-unit - `blog.service`; запуск в ручном режиме - `npm start`; логи пишутся в `journald`\
Демо доступ к админке:
- Логин: admin
- Пароль: admin123
