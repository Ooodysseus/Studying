# 05. Docker Compose

## Навіщо потрібен Docker Compose

Docker Compose - це інструмент для визначення та запуску багатоконтейнерних Docker-додатків. З Compose ви використовуєте YAML-файл для налаштування сервісів вашого додатку. Потім одним командою ви створюєте та запускаєте всі сервіси з вашої конфігурації.

### Основні переваги Docker Compose:

1. **Спрощене управління середовищем** - один файл конфігурації замість множини команд
2. **Ізоляція середовищ** - кожен проект може мати власну ізольовану мережу
3. **Повторне використання контейнерів** - збереження даних між запусками
4. **Змінні середовища та масштабування** - просте налаштування різних середовищ
5. **Оркестрація запуску** - контроль залежностей між сервісами

> **Порада:** Docker Compose ідеально підходить для розробки, тестування та CI/CD сценаріїв. Для промислових середовищ з високим навантаженням розгляньте Kubernetes або Docker Swarm.

## Структура docker-compose.yml

Файл `docker-compose.yml` - це YAML-файл, який визначає сервіси, мережі та томи для вашого додатку:

```yaml
version: "3.8" # Версія формату Compose

services: # Визначення сервісів
    web: # Назва першого сервісу
        image: nginx:latest # Образ з Docker Hub
        ports:
            - "80:80" # Проброс портів (хост:контейнер)
        volumes:
            - ./website:/usr/share/nginx/html # Монтування тому
        depends_on:
            - api # Залежність від іншого сервісу

    api: # Назва другого сервісу
        build: ./api # Шлях до Dockerfile
        environment:
            - DB_HOST=database
            - DB_PORT=5432
        ports:
            - "3000:3000"
        depends_on:
            - database

    database: # Назва третього сервісу
        image: postgres:13
        volumes:
            - postgres_data:/var/lib/postgresql/data
        environment:
            - POSTGRES_PASSWORD=secret
            - POSTGRES_USER=myuser
            - POSTGRES_DB=mydb

volumes: # Визначення томів
    postgres_data: # Персистентне збереження даних

networks: # Визначення мереж (опціонально)
    default:
        driver: bridge
```

### Основні секції docker-compose.yml:

1. **version** - версія формату Compose файлу
2. **services** - конфігурація сервісів (контейнерів)
3. **volumes** - визначення іменованих томів
4. **networks** - налаштування мереж

### Ключові параметри для сервісів:

| Параметр         | Опис                                                          |
| ---------------- | ------------------------------------------------------------- |
| `image`          | Образ для контейнера                                          |
| `build`          | Шлях до Dockerfile або об'єкт з опціями                       |
| `ports`          | Проброс портів (HOST:CONTAINER)                               |
| `volumes`        | Монтування томів                                              |
| `environment`    | Змінні середовища                                             |
| `env_file`       | Файл зі змінними середовища                                   |
| `depends_on`     | Залежності запуску                                            |
| `restart`        | Політика перезапуску (no, always, on-failure, unless-stopped) |
| `networks`       | Мережі для підключення                                        |
| `command`        | Перевизначення команди за замовчуванням                       |
| `container_name` | Кастомне ім'я контейнера                                      |
| `healthcheck`    | Перевірка стану сервісу                                       |

## Запуск кількох сервісів разом

Docker Compose дозволяє легко керувати життєвим циклом всіх сервісів вашого додатку.

### Основні команди Docker Compose:

```bash
# Запуск всіх сервісів (створення та запуск)
docker-compose up

# Запуск у фоновому режимі
docker-compose up -d

# Зупинка сервісів
docker-compose stop

# Зупинка та видалення контейнерів
docker-compose down

# Зупинка, видалення контейнерів та томів
docker-compose down -v

# Перегляд статусу сервісів
docker-compose ps

# Перегляд логів
docker-compose logs

# Перегляд логів конкретного сервісу
docker-compose logs api

# Відстеження логів у реальному часі
docker-compose logs -f

# Запуск команди в сервісі
docker-compose exec api npm test

# Збірка або перезбірка сервісів
docker-compose build

# Перезапуск одного сервісу
docker-compose restart api
```

> **Важливо!** За замовчуванням `docker-compose` шукає файл `docker-compose.yml` у поточній директорії. Ви можете вказати інший файл за допомогою параметра `-f`: `docker-compose -f production.yml up`

## Приклади типових конфігурацій

### 1. Веб-додаток з базою даних і кешем

```yaml
version: "3.8"

services:
    web:
        build: ./frontend
        ports:
            - "80:80"
        depends_on:
            - api

    api:
        build: ./backend
        ports:
            - "3000:3000"
        environment:
            - NODE_ENV=development
            - DB_HOST=db
            - DB_USER=postgres
            - DB_PASSWORD=secret
            - DB_NAME=myapp
            - REDIS_HOST=redis
        depends_on:
            - db
            - redis

    db:
        image: postgres:13-alpine
        volumes:
            - postgres_data:/var/lib/postgresql/data
        environment:
            - POSTGRES_USER=postgres
            - POSTGRES_PASSWORD=secret
            - POSTGRES_DB=myapp

    redis:
        image: redis:6-alpine
        volumes:
            - redis_data:/data

volumes:
    postgres_data:
    redis_data:
```

### 2. Мікросервісна архітектура

```yaml
version: "3.8"

services:
    gateway:
        build: ./gateway
        ports:
            - "80:80"
        depends_on:
            - auth-service
            - user-service
            - product-service

    auth-service:
        build: ./auth-service
        environment:
            - DB_HOST=auth-db
        depends_on:
            - auth-db

    user-service:
        build: ./user-service
        environment:
            - DB_HOST=user-db
        depends_on:
            - user-db

    product-service:
        build: ./product-service
        environment:
            - DB_HOST=product-db
        depends_on:
            - product-db

    auth-db:
        image: mongo:4
        volumes:
            - auth_data:/data/db

    user-db:
        image: postgres:13
        volumes:
            - user_data:/var/lib/postgresql/data

    product-db:
        image: mysql:8
        volumes:
            - product_data:/var/lib/mysql

volumes:
    auth_data:
    user_data:
    product_data:
```

### 3. Локальне середовище розробки

```yaml
version: "3.8"

services:
    app:
        build:
            context: .
            dockerfile: Dockerfile.dev
        volumes:
            - .:/app # Монтування коду для live-reload
            - /app/node_modules # Запобігання перезапису node_modules
        ports:
            - "3000:3000"
        environment:
            - CHOKIDAR_USEPOLLING=true # Для hot-reload у Docker
        command: npm run dev

    test:
        build:
            context: .
            dockerfile: Dockerfile.dev
        volumes:
            - .:/app
            - /app/node_modules
        command: npm run test:watch

    db:
        image: postgres:13-alpine
        volumes:
            - dev_db:/var/lib/postgresql/data
        environment:
            - POSTGRES_PASSWORD=password
            - POSTGRES_USER=developer
            - POSTGRES_DB=devdb

volumes:
    dev_db:
```

### 4. Використання змінних середовища

Створіть файл `.env` в тій же директорії, що й `docker-compose.yml`:

```
POSTGRES_USER=myuser
POSTGRES_PASSWORD=mypassword
POSTGRES_DB=mydb
EXTERNAL_PORT=8080
```

Потім використайте змінні в `docker-compose.yml`:

```yaml
version: "3.8"

services:
    web:
        image: nginx
        ports:
            - "${EXTERNAL_PORT}:80"

    db:
        image: postgres
        environment:
            - POSTGRES_USER=${POSTGRES_USER}
            - POSTGRES_PASSWORD=${POSTGRES_PASSWORD}
            - POSTGRES_DB=${POSTGRES_DB}
```

## Типові проблеми та їх вирішення

1. **Проблема**: Контейнери не можуть "бачити" один одного.
   **Рішення**: Переконайтеся, що вони знаходяться в одній мережі. За замовчуванням Compose створює одну мережу для всіх сервісів.

2. **Проблема**: Зміни в коді не відображаються в контейнері.
   **Рішення**: Правильно налаштуйте томи для монтування коду з хоста.

3. **Проблема**: Сервіси запускаються в неправильному порядку.
   **Рішення**: Використовуйте `depends_on` і перевірки стану (healthcheck).

4. **Проблема**: Дані в томах зникають після `docker-compose down`.
   **Рішення**: Уникайте використання `-v` з `down`, якщо не хочете видаляти томи.

5. **Проблема**: Змінні оточення не підхоплюються з `.env` файлу.
   **Рішення**: Перевірте розташування файлу і використовуйте повне ім'я змінних в `docker-compose.yml`.

## Найкращі практики

1. **Розділяйте конфігурації для різних середовищ**:

    ```bash
    docker-compose -f docker-compose.yml -f docker-compose.prod.yml up -d
    ```

2. **Використовуйте змінні середовища** для налаштування без зміни самого файлу docker-compose.yml.

3. **Називайте томи відповідно до їх призначення** для легкої ідентифікації.

4. **Версіонуйте docker-compose.yml** разом з кодом проекту для забезпечення відтворюваності.

5. **Документуйте налаштування** кожного сервісу за допомогою коментарів.

6. **Використовуйте healthcheck** для переконання, що сервіси дійсно запущені та працюють:

    ```yaml
    services:
        api:
            image: my-api
            healthcheck:
                test: ["CMD", "curl", "-f", "http://localhost:3000/health"]
                interval: 30s
                timeout: 10s
                retries: 3
    ```

7. **Для продакшн середовища** розгляньте використання Docker Swarm або Kubernetes замість Compose.

8. **Обмежуйте ресурси для контейнерів**:

    ```yaml
    services:
        api:
            image: my-api
            deploy:
                resources:
                    limits:
                        cpus: "0.5"
                        memory: 512M
                    reservations:
                        cpus: "0.1"
                        memory: 128M
    ```

9. **Не зберігайте секрети у файлі docker-compose.yml**. Використовуйте змінні оточення або Docker secrets.

10. **Регулярно оновлюйте образи** для отримання виправлень безпеки.
