Учебный проект на Spring Boot: управление пользователями и отправка email-уведомлений. Система разворачивается через Docker Compose.

Компонент-описание-порт<br>

API Gateway - единая точка входа для HTTP-запросов - 8080<br>
user-service - REST API пользователей, работа с PostgreSQL, публикация событий Kafka - 8081<br>
notification - service-Получение событий Kafka и отправка email-уведомлений - 8082<br>
discovery-server - регистрация и обнаружение сервисов через Eureka - 8761<br>
PostgreSQL - хранение пользователей - 5432<br>
Kafka - обмен событиями между микросервисами - 9092<br>

Реализованные паттерны

API Gateway — маршрутизация запросов к микросервисам.<br>
Service Discovery — регистрация приложений в Eureka.<br>
Circuit Breaker — защита HTTP-вызова notification-service с помощью Resilience4j.<br>
External Configuration — внешний файл `config/application.properties` и переменные окружения Docker Compose.<br>

Взаимодействие сервисов

1. Клиент отправляет запрос через API Gateway.<br>
2. Gateway направляет запрос в user-service.<br>
3. user-service сохраняет изменения пользователей в PostgreSQL и публикует события в топик `user-events`.<br>
4. notification-service получает события и отправляет email через настроенный SMTP-сервер.<br>

Запуск

Установите и запустите Docker Desktop<br>
Из корневой папки проекта выполните в bash:<br>
docker compose up --build -d<br>
