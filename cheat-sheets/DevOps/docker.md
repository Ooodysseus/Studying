# DOCKER

Docker — платформа для контейнеризації додатків, що дозволяє ізолювати, запускати, масштабувати та деплоїти сервіси у вигляді контейнерів.

## Категорія: Основні команди CLI

| Команда/метод              | Опис                   | Приклад/Аутпут                 |
| -------------------------- | ---------------------- | ------------------------------ |
| docker --version           | версія Docker          | docker --version               |
| docker pull image          | завантажити образ      | docker pull nginx              |
| docker build -t name .     | зібрати образ          | docker build -t myapp .        |
| docker run image           | запустити контейнер    | docker run nginx               |
| docker run -d -p 80:80 img | у фоні + порт          | docker run -d -p 8080:80 nginx |
| docker ps/-a               | список контейнерів     | docker ps -a                   |
| docker stop/start/rm id    | керування контейнерами | docker stop myid               |
| docker images              | список образів         | docker images                  |
| docker rmi image           | видалити образ         | docker rmi nginx               |
| docker exec -it id bash    | shell у контейнері     | docker exec -it myid bash      |
| docker logs id             | логи контейнера        | docker logs myid               |
| docker cp id:/src dst      | копіювати файли        | docker cp myid:/app/file.txt . |
| docker network ls          | мережі                 | docker network ls              |
| docker volume ls           | томи                   | docker volume ls               |

## Категорія: Dockerfile

| Інструкція/директива     | Опис                     | Приклад/Аутпут                            |
| ------------------------ | ------------------------ | ----------------------------------------- | --- | ------ |
| FROM image               | базовий образ            | FROM python:3.11                          |
| WORKDIR /app             | робоча папка             | WORKDIR /app                              |
| COPY . /app              | копіювати файли          | COPY . /app                               |
| RUN cmd                  | виконати команду         | RUN pip install -r req.txt                |
| CMD ["python", "app.py"] | команда за замовчуванням | CMD ["python", "main.py"]                 |
| EXPOSE 80                | відкрити порт            | EXPOSE 8080                               |
| ENV VAR=val              | змінна середовища        | ENV DEBUG=1                               |
| ENTRYPOINT ["sh"]        | точка входу              | ENTRYPOINT ["sh"]                         |
| ARG build_var            | build-аргумент           | ARG VERSION=1.0                           |
| HEALTHCHECK              | перевірка стану          | HEALTHCHECK CMD curl -f http://localhost/ |     | exit 1 |

## Категорія: docker-compose

| Команда/метод                | Опис              | Приклад/Аутпут               |
| ---------------------------- | ----------------- | ---------------------------- |
| docker-compose up            | запуск сервісів   | docker-compose up -d         |
| docker-compose down          | зупинити все      | docker-compose down          |
| docker-compose build         | зібрати всі       | docker-compose build         |
| docker-compose logs          | логи сервісів     | docker-compose logs          |
| docker-compose exec srv bash | shell у сервісі   | docker-compose exec web bash |
| docker-compose ps            | список сервісів   | docker-compose ps            |
| docker-compose config        | перевірити конфіг | docker-compose config        |

## Категорія: docker-compose.yml

| Ключ/секція  | Опис                | Приклад/Аутпут        |
| ------------ | ------------------- | --------------------- |
| version: '3' | версія формату      | version: '3.8'        |
| services:    | сервіси             | services: web: ...    |
| build: .     | збірка з Dockerfile | build: .              |
| image: name  | ім'я образу         | image: myapp:latest   |
| ports:       | проброс портів      | ports: [8080:80]      |
| environment: | змінні середовища   | environment: DEBUG=1  |
| volumes:     | монтування томів    | volumes: ./data:/data |
| depends_on:  | залежності          | depends_on: [db]      |
| networks:    | мережі              | networks: [default]   |

## Категорія: Робота з реєстрами, best practices

| Команда/метод           | Опис                | Приклад/Аутпут                    |
| ----------------------- | ------------------- | --------------------------------- |
| docker login            | логін у реєстр      | docker login                      |
| docker tag img repo/img | тегування           | docker tag myapp repo/myapp:1.0   |
| docker push repo/img    | пуш у реєстр        | docker push repo/myapp:1.0        |
| docker pull repo/img    | витягнути з реєстру | docker pull repo/myapp:1.0        |
| .dockerignore           | ігнорування файлів  | .dockerignore: node_modules       |
| multi-stage build       | оптимізація         | FROM node AS build ... FROM nginx |
| secrets                 | секрети             | secrets: [db_password]            |
| restart: always         | автозапуск          | restart: always                   |
| resource limits         | обмеження ресурсів  | mem_limit: 512m, cpus: 0.5        |
| healthcheck             | перевірка стану     | healthcheck: ...                  |
| Документація            | офіційна            | docs.docker.com                   |

---

> Шпаргалка складена за інструкціями: компактно, категоріями, з короткими прикладами та описами.
