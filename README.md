# Rebalance API

Тестовое задание для прохождения летней практики в vl.ru.

Проект представляет собой микросервис на Symfony, который распределяет процессы между машинами с учетом доступных ресурсов (RAM и CPU) и выполняет автоматическую ребалансировку при изменении состава машин или процессов.

## Технологии

* PHP 8.3
* Symfony
* Doctrine ORM
* MySQL
* Docker Compose
* nginx

## Развёртывание

### Запуск

```bash
docker compose up -d

docker compose exec php83-service composer install

docker compose exec php83-service php bin/console make:migration --no-interaction

docker compose exec php83-service php bin/console doctrine:migrations:migrate --no-interaction

docker compose exec php83-service php bin/console doctrine:migrations:migrate --env=test --no-interaction
```

## Запуск тестов

```bash
docker compose run --rm php83-service php vendor/bin/phpunit
```

## API

### Назначения

* `GET /assignments` — список всех назначений процессов на машины

### Машины

* `GET /machines` — список машин
* `POST /machine/add` — добавить машину
* `DELETE /machine/delete/{id}` — удалить машину

### Процессы

* `GET /processes` — список процессов
* `POST /process/add` — добавить процесс
* `DELETE /process/delete/{id}` — удалить процесс
* Распределение выполняется с учетом относительной загрузки машин.
* Проект построен с использованием MVC-подхода и принципов SOLID.
