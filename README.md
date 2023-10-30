# Kittygram

Kittygram — социальная сеть для обмена фотографиями любимых питомцев.

В проекте Kittygram доступны следующие возможности: регистрация/авторизация пользователя, добавление нового питомца (также дополнительной информации о нем- фото, год рождения, цвет и достижения), просмотр других питомцев.

---

# Запуск проекта на виртуальном сервере из репозитория GitHub
## Клонирование проекта с GitHub на сервер
	git clone https://github.com/kamilisx/infra_sprint1
 
# Backend-приложение
Создаем и активируем виртуальное окружение, устанавливаем зависимости:

 	python3 -m venv venv
	source venv/bin/activate
 	pip install -r requirements.txt

Из директории с файлом manage.py выполняем миграции и создаем суперюзера:

	python3 manage.py migrate
 	python3 manage.py createsuperuser
  
Корректируем файл .env: добавляем в ALLOWED_HOSTS внешний IP сервера, 127.0.0.1, localhost и домен, DEBUG = 'False'

Собираем статику backend-приложения и копируем в директорию var/www/kittygram/:

	python3 manage.py collectstatic
 	sudo cp -r /путь_к_директории_backend/static_backend/ /var/www/kittygram/

# Frontend-приложение

Из директории с frontend-приложением выполнить команды:
	
 	npm i
	npm run build 
Копируем статику фронтенд-приложения в директорию /var/www/kittygram/:

	sudo cp -r /путь_к_директории_frontend/build. /var/www/kittygram/

# Установка и настройка Gunicorn

При активированном виртуальном окружении backend-приложения устанавливаем пакет gunicorn:

	pip install gunicorn==20.1.0
 
Из директории с файлом manage.py запускаем gunicorn:

	gunicorn --bind 0.0.0.0:8080 backend.wsgi

Создаем файл конфигурации юнита для gunicorn в директории /etc/systemd/system/ и следующим кодом:

	[Unit]
	Description=gunicorn daemon
	After=network.target
	[Service]
	User=имя_пользователя_в_системе
	WorkingDirectory=/home/имя_пользователя/папка_с_проектом/папка_с_файлом_manage.py/
	ExecStart=/.../venv/bin/gunicorn --bind 0.0.0.0:8080 backend.wsgi:application
	[Install]
	WantedBy=multi-user.target

Для запуска и отслеживания работы демона Gunicorn выполняем следующие команды:
	
 	sudo systemctl start gunicorn_kittygram
	sudo systemctl enable gunicorn_kittygram
Проверка работоспособности запущенного демона:

	sudo systemctl status gunicorn_kittygram

# Установка и настройка Nginx

Для установки и запуска Nginx выполняем:

 	sudo apt install nginx -y
  	sudo systemctl start nginx

Для изменения настроек Nginx, редактором Nano открывается файл конфигурации:

	sudo nano /etc/nginx/sites-enabled/default

Перезагружаем конфигурацию Nginx:

	sudo systemctl reload nginx

# Настройка файрвола ufw

Последовательно выполняем команды для настроек файрвола и его включения:

	sudo ufw allow 'Nginx Full'
 	sudo ufw allow OpenSSH
  	sudo ufw enable
Проверка файрвола:

	sudo ufw status




# Технологии:

	• Python 3.9
	• Django 3.2.3
	• gunicorn 20.1.0
	• Доменное имя: https://www.noip.com

Автор: Backend/Frontend - Яндекс Практикум; Деплой - Исхаков Камиль
