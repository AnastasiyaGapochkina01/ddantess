# Troubleshooting Stand Flask Application
## Описание
Простое Flask-приложение - REST API для управления пользователями (добавление, получение по имени). Логирует запросы в файл; для проверки "здоровья" использует эндпоинт `/health`. В качестве БД используется postgresql

## Инфраструктура
### Хост (users-vm)
- **IP:** 89.169.174.128
- **User:** devops
- **Pass:** 0000

### Сервис
- Корневая директория - `/opt/users-app/`
- Сервис - `users-backend.service`

## Примеры запросов
#### Добавить пользователя
```bash
curl -X POST http://localhost/user -H "Content-Type: application/json" -d '{"username":"alice"}'
```
#### Получить пользователя по имени
```bash
curl http://localhost/user/alice
```
#### healthcheck
```bash
curl http://localhost/health
```
