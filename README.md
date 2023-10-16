#  Kittygram
Проект Kittygram позволяет пользователям поделиться своими домашними любимцами и рассказать о их достижениях.
### 1. Создание и развертка контейнеров проекта:
Форкнуть репозиторий, сконировать и перейти в корневую папку `kittygram_final`
Создать файл .env и заполнить его переменными:
```
POSTGRES_DB=...
POSTGRES_USER=...
POSTGRES_PASSWORD=...
POSTGRES_HOST=...
POSTGRES_PORT=...

SECRET_KEY=...
DEBUG=False
ALLOWED_HOSTS=...
```
Убедиться, что сервис Docker активен в системе:
```
sudo systemctl status docker
```
Собрать контейнеры:
```
sudo docker compose -f docker-compose.production.yml pull
sudo docker compose -f docker-compose.production.yml down
sudo docker compose -f docker-compose.production.yml up -d
```
Выполнить миграции, собрать статику:
```
sudo docker compose -f docker-compose.production.yml exec backend python manage.py migrate
sudo docker compose -f docker-compose.production.yml exec backend python manage.py collectstatic
sudo docker compose -f docker-compose.production.yml exec backend cp -r /app/collected_static/. /static/
```
Установить nginx:
```
sudo apt install nginx -y
sudo systemctl start nginx
```
Настроить фаерволл:
```
sudo ufw allow 'Nginx Full'
sudo ufw allow OpenSSH
sudo ufw enable
```
Настроить nginx:
```
sudo nano /etc/nginx/sites-enabled/default
```
Заменяем содержимое файла на:
```
server {
    listen 80;
    server_name example.com;
    
    location / {
        proxy_set_header HOST $host;
        proxy_pass http://127.0.0.1:9000;

    }
}
```
Проверяем и перезагружаем nginx:
```
sudo nginx -t
sudo systemctl reload nginx
```
### 2. Стек технологий
* #### Django REST
* #### Python 3.9
* #### Gunicorn
* #### Nginx
* #### JS
* #### Node.js
* #### PostgreSQL
* #### Docker

### 3. Автор проекта
#### [Дмитрий К.](https://github.com/777777k)