> [!IMPORTANT]  
> Все приложения запускаются без дополнительных контейнеров. Нужно написать Dockerfile, собрать image и запустить из него контейнер. Обязательно проверить что приложение внутри контейнера живо

1) Запустить в docker приложение
```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def home():
    return "Hello, Dockerized World!"

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```
2) Запустить в docker приложение 
```js
const http = require('http');
const port = process.env.PORT || 3000;
const message = process.env.MESSAGE || "Hello, default!";

const server = http.createServer((req, res) => {
  res.end(message);
});

server.listen(port, () => {
  console.log(`Server running on port ${port}`);
});
```
3) Запустить в docker приложение https://gitlab.com/dos-26/cmdb/frontend
4) Запустить в docker приложение https://gitlab.com/devops201206/nuxt
