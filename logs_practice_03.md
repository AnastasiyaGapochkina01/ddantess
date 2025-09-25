# Dragons App
## Описание
Веб-приложение для каталогизации различных видов драконов с системой аутентификации пользователей:
- backend: Go
- frontend: HTML/CSS шаблоны (render by server)
- база данных: PostgreSQL
- веб-сервер: Nginx
- логирование: Journald + Rsyslog
## Инфраструктура

<img width="652" height="334" alt="image" src="https://github.com/user-attachments/assets/848e5ee7-ddbd-40f3-9a57-cc2d9021bb7e" />

#### balancer
ВМ с nginx (reverse proxy)

IP: 89.169.185.126\
User: devops\
Pass: 0000

##### dragons
ВМ с базой даннх и бэкендом. Бэкенд запущен как systemd-unit `dragon-catalog.service`

IP: 89.169.185.126\
User: devops\
Pass: 0000

## Взаимодействие с сервисом
1) Через браузер по домену https://dragons.anestesia.fun/
2) Из консоли с помощью `curl`:
```bash
export BASE_URL="https://dragons.anestesia.fun"
export COOKIE_FILE="dragons"

# регистрация
curl -X POST "$BASE_URL/register" \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -d "username=curluser_$(date +%s)&password=curlpass123" \
  -c $COOKIE_FILE -b $COOKIE_FILE -L -s -o /dev/null -w "Регистрация: %{http_code}\n"

# вход
curl -X POST "$BASE_URL/login" \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -d "username=curluser&password=curlpass123" \
  -c $COOKIE_FILE -b $COOKIE_FILE -L -s -o /dev/null -w "Вход: %{http_code}\n"

# главная страница
curl -X GET "$BASE_URL/main" \
  -c $COOKIE_FILE -b $COOKIE_FILE -L -s -o main_page.html -w "Главная: %{http_code}\n"
```
### Эндпоинты
- `/` - Страница входа/регистрации
- `/main` - Главная страница с категориями драконов
- `/about?category=<id>` - Драконы выбранной категории
- `/dragon?id=<id>` - Детальная информация о драконе
