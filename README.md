# Kittygram

Kittygram — социальная сеть для обмена фотографиями любимых питомцев.

В проекте Kittygram доступны следующие возможности: регистрация/авторизация пользователя, добавление нового питомца (также дополнительной информации о нем- фото, год рождения, цвет и достижения), просмотр других питомцев.

---

# Запуск проекта на виртуальном сервере из репозитория GitHub:
Клонируем проект из репозитория на GitHub:

	git clone https://github.com/kamilisx/infra_sprint1

# Backend-приложение:

Создаем и активируем виртуальное окружение

Устанавливаем необходимые зависимости:
	
 	pip install -r requirements.txt
В settings.py отключаем режим debug: 
	
 	DEBUG = False
 
# Frontend-приложение:

Для запуска сборки frontend-приложения выполняем команды: 

	npm i
 	npm run build

# Перезапуск gunicorn  и Nginx:

	sudo systemctl daemon-reload
	sudo systemctl reload nginx

#Технологии:

	• Python 3.9
	• Django 3.2.3
	• gunicorn 20.1.0
	• Доменное имя: https://www.noip.com

Автор: Backend/Frontend - Яндекс Практикум; Деплой - Исхаков Камиль
