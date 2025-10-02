# Metrics Dashboard App
Простая система мониторинга серверов
## Компоненты
1) Агент на Go: запущен на каждом мониторируемом сервере, собирает метрики CPU, памяти и диска и отправляет их в очередь RabbitMQ.
2) Backend на Node.js: подписывается на очередь RabbitMQ, принимает метрики, записывает их в InfluxDB и предоставляет API для фронтенда.
3) База данных InfluxDB: хранит временные ряды метрик для анализа и визуализации.
4) Фронтенд на React: отображает графики метрик на дашборде, запрашивая данные с backend API.
5) RabbitMQ: брокер сообщений для асинхронной передачи метрик от агентов к backend.

InfluxDB и RabbitMQ запущены через docker compose; dashboard-frontend и dashboard-backend запущены как systemd юниты

<img width="586" height="304" alt="image" src="https://github.com/user-attachments/assets/e53e8427-e30a-4066-80fd-42b0580dc368" />

## Машины
#### dash-rabbit
IP: `89.169.191.150`\
Login/Pass: `devops/0000`
#### dash-back
IP: `84.201.167.53`\
Login/Pass: `devops/0000`
#### dash-front
IP: `158.160.9.223`\
Login/Pass: `devops/0000`
## Запуск агента
Скомпилируйте Go-агент:

```bash
go build -o agent agent.go
./agent
```
Агент начинает собирать и отправлять метрики в RabbitMQ.
