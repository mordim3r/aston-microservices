Учебный проект на Spring Boot: управление пользователями и отправка email-уведомлений. Система разворачивается через Docker Compose.

Компонент-описание-порт

API Gateway - единая точка входа для HTTP-запросов - 8080
user-service - REST API пользователей, работа с PostgreSQL, публикация событий Kafka - 8081
notification - service-Получение событий Kafka и отправка email-уведомлений - 8082
discovery-server - регистрация и обнаружение сервисов через Eureka - 8761
PostgreSQL - хранение пользователей - 5432
Kafka - обмен событиями между микросервисами - 9092

Реализованные паттерны

API Gateway — маршрутизация запросов к микросервисам.
Service Discovery — регистрация приложений в Eureka.
Circuit Breaker — защита HTTP-вызова notification-service с помощью Resilience4j.
External Configuration — внешний файл `config/application.properties` и переменные окружения Docker Compose.

Взаимодействие сервисов

1. Клиент отправляет запрос через API Gateway.
2. Gateway направляет запрос в user-service.
3. user-service сохраняет изменения пользователей в PostgreSQL и публикует события в топик `user-events`.
4. notification-service получает события и отправляет email через настроенный SMTP-сервер.

Запуск

Установите и запустите Docker Desktop
Из корневой папки проекта выполните в bash:
docker compose up --build -d
