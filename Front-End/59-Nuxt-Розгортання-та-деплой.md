# Бекенд на Nuxt

## Розгортання та деплой

Розгортання Nuxt додатку у продакшн-середовище — важливий етап розробки, який потребує уваги до деталей та розуміння особливостей різних хостинг-платформ. У цьому розділі розглянемо різні стратегії та підходи до розгортання Nuxt додатків.

### Режими розгортання Nuxt

Nuxt 3 підтримує кілька режимів розгортання:

1. **Server-Side Rendering (SSR)**: повноцінний серверний рендеринг
2. **Static Site Generation (SSG)**: генерація статичних файлів
3. **Client-Side Rendering (CSR)**: рендеринг на стороні клієнта
4. **Hybrid**: комбінація SSR/SSG для різних маршрутів

### Підготовка до розгортання

#### Конфігурація середовища

Перед розгортанням важливо налаштувати змінні середовища для різних середовищ:

```typescript
// nuxt.config.ts
export default defineNuxtConfig({
    runtimeConfig: {
        // Приватні змінні (доступні лише на сервері)
        apiSecret: process.env.API_SECRET,
        databaseUrl: process.env.DATABASE_URL,

        // Публічні змінні (доступні на клієнті та сервері)
        public: {
            apiBase: process.env.API_BASE || "https://api.example.com",
            siteUrl: process.env.SITE_URL || "https://example.com",
        },
    },
});
```

#### Файли середовища

Створіть файли `.env` для різних середовищ:

```bash
# .env.development
NODE_ENV=development
API_SECRET=dev_secret
DATABASE_URL=postgresql://localhost:5432/myapp_dev
API_BASE=http://localhost:3000/api

# .env.production
NODE_ENV=production
API_SECRET=prod_secret_from_vault
DATABASE_URL=postgresql://user:pass@production-db:5432/myapp_prod
API_BASE=https://api.example.com
SITE_URL=https://example.com
```

> **Важливо**: Ніколи не додавайте файли `.env` до системи контролю версій. Додайте їх до `.gitignore` та створіть приклад файлу `.env.example` без реальних даних.

### Збірка проекту

Для підготовки додатку до розгортання використовуйте команду `build`:

```bash
# Збірка для продакшн
npm run build

# Запуск збірки
node .output/server/index.mjs
```

Ця команда створить оптимізовану збірку вашого додатку в директорії `.output`.

### Розгортання на різних платформах

#### Традиційний хостинг (VPS/Dedicated Server)

1. **Підготовка сервера**:

```bash
# Встановлення Node.js та npm
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt-get install -y nodejs

# Встановлення PM2 для керування процесами
npm install -g pm2
```

2. **Розгортання додатку**:

```bash
# Клонування репозиторію
git clone https://github.com/username/your-nuxt-app.git
cd your-nuxt-app

# Встановлення залежностей
npm install

# Створення .env файлу з продакшн-змінними
cp .env.example .env
nano .env  # Редагування змінних середовища

# Збірка додатку
npm run build

# Запуск через PM2
pm2 start ecosystem.config.js
```

3. **Файл конфігурації PM2** (`ecosystem.config.js`):

```javascript
module.exports = {
    apps: [
        {
            name: "nuxt-app",
            exec_mode: "cluster",
            instances: "max", // або конкретне число
            script: "./.output/server/index.mjs",
            env: {
                NODE_ENV: "production",
                PORT: 3000,
            },
        },
    ],
};
```

4. **Налаштування Nginx як проксі**:

```nginx
# /etc/nginx/sites-available/your-nuxt-app
server {
    listen 80;
    server_name example.com www.example.com;

    # Перенаправлення на HTTPS
    location / {
        return 301 https://$host$request_uri;
    }
}

server {
    listen 443 ssl;
    server_name example.com www.example.com;

    ssl_certificate /etc/letsencrypt/live/example.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/example.com/privkey.pem;

    # Оптимізація SSL
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_prefer_server_ciphers on;
    ssl_ciphers ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256;
    ssl_session_cache shared:SSL:10m;

    # Проксіювання запитів до Node.js додатку
    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    # Кешування статичних файлів
    location ~* \.(js|css|png|jpg|jpeg|gif|ico|svg)$ {
        expires 30d;
        add_header Cache-Control "public, no-transform";
    }
}
```

5. **Активація конфігурації Nginx**:

```bash
sudo ln -s /etc/nginx/sites-available/your-nuxt-app /etc/nginx/sites-enabled/
sudo nginx -t  # Перевірка конфігурації
sudo systemctl restart nginx
```

#### Розгортання на Vercel

Vercel — одна з найпростіших платформ для розгортання Nuxt 3 додатків.

1. **Встановлення Vercel CLI**:

```bash
npm install -g vercel
```

2. **Файл конфігурації `vercel.json`**:

```json
{
    "version": 2,
    "builds": [
        {
            "src": "nuxt.config.ts",
            "use": "@nuxtjs/vercel-builder",
            "config": {
                "serverFiles": ["server/**"]
            }
        }
    ],
    "routes": [
        {
            "src": "/api/(.*)",
            "dest": "/api/$1"
        },
        {
            "src": "/(.*)",
            "dest": "/"
        }
    ],
    "env": {
        "NODE_ENV": "production"
    }
}
```

3. **Деплой на Vercel**:

```bash
# Інтерактивний деплой
vercel

# Продакшн-деплой
vercel --prod
```

Також можна налаштувати автоматичний деплой через GitHub, GitLab або Bitbucket.

#### Розгортання на Netlify

Netlify також добре працює з Nuxt 3, особливо для SSG проєктів.

1. **Файл конфігурації `netlify.toml`**:

```toml
[build]
  command = "npm run build"
  publish = "dist"
  functions = ".output/server"

[dev]
  command = "npm run dev"
  framework = "#custom"
  port = 8888
  targetPort = 3000

[[redirects]]
  from = "/api/*"
  to = "/.netlify/functions/index"
  status = 200

[[redirects]]
  from = "/*"
  to = "/index.html"
  status = 200
```

2. **Деплой на Netlify**:

```bash
# Встановлення Netlify CLI
npm install -g netlify-cli

# Інтерактивний деплой
netlify deploy

# Продакшн-деплой
netlify deploy --prod
```

#### Docker контейнеризація

Для більш складних додатків або мікросервісної архітектури Docker є відмінним рішенням.

1. **Dockerfile**:

```dockerfile
# Етап збірки
FROM node:18-alpine AS build

WORKDIR /app

COPY package*.json ./
RUN npm ci

COPY . .
RUN npm run build

# Етап продакшн
FROM node:18-alpine

WORKDIR /app

# Копіювання лише необхідних файлів зі збірки
COPY --from=build /app/.output /app/.output
COPY --from=build /app/package.json /app/package.json

# Встановлення лише продакшн-залежностей
RUN npm ci --only=production

ENV HOST=0.0.0.0
ENV PORT=3000
ENV NODE_ENV=production

EXPOSE 3000

CMD ["node", ".output/server/index.mjs"]
```

2. **Docker Compose** для локального тестування:

```yaml
# docker-compose.yml
version: "3"

services:
    app:
        build: .
        ports:
            - "3000:3000"
        environment:
            - NODE_ENV=production
            - DATABASE_URL=postgresql://user:pass@db:5432/myapp
        depends_on:
            - db
        restart: unless-stopped

    db:
        image: postgres:14-alpine
        environment:
            - POSTGRES_USER=user
            - POSTGRES_PASSWORD=pass
            - POSTGRES_DB=myapp
        volumes:
            - postgres_data:/var/lib/postgresql/data
        restart: unless-stopped

volumes:
    postgres_data:
```

3. **Запуск через Docker Compose**:

```bash
docker-compose up -d
```

#### Розгортання на Kubernetes

Для великих проектів з високим навантаженням Kubernetes надає потужні можливості оркестрації.

1. **Deployment Manifest** (`deployment.yaml`):

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
    name: nuxt-app
    labels:
        app: nuxt-app
spec:
    replicas: 3
    selector:
        matchLabels:
            app: nuxt-app
    template:
        metadata:
            labels:
                app: nuxt-app
        spec:
            containers:
                - name: nuxt-app
                  image: your-registry/nuxt-app:latest
                  ports:
                      - containerPort: 3000
                  env:
                      - name: NODE_ENV
                        value: "production"
                      - name: DATABASE_URL
                        valueFrom:
                            secretKeyRef:
                                name: nuxt-app-secrets
                                key: database-url
                  resources:
                      limits:
                          cpu: "1"
                          memory: "1Gi"
                      requests:
                          cpu: "500m"
                          memory: "512Mi"
                  readinessProbe:
                      httpGet:
                          path: /api/health
                          port: 3000
                      initialDelaySeconds: 10
                      periodSeconds: 5
```

2. **Service Manifest** (`service.yaml`):

```yaml
apiVersion: v1
kind: Service
metadata:
    name: nuxt-app
spec:
    selector:
        app: nuxt-app
    ports:
        - port: 80
          targetPort: 3000
    type: ClusterIP
```

3. **Ingress Manifest** (`ingress.yaml`):

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
    name: nuxt-app-ingress
    annotations:
        kubernetes.io/ingress.class: nginx
        cert-manager.io/cluster-issuer: letsencrypt-prod
spec:
    tls:
        - hosts:
              - example.com
          secretName: example-tls
    rules:
        - host: example.com
          http:
              paths:
                  - path: /
                    pathType: Prefix
                    backend:
                        service:
                            name: nuxt-app
                            port:
                                number: 80
```

4. **Застосування маніфестів**:

```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
kubectl apply -f ingress.yaml
```

### Конфігурація для статичного хостингу (SSG)

Якщо ваш додаток використовує SSG, ви можете розгорнути його на будь-якому статичному хостингу:

1. **Налаштування Nuxt для SSG**:

```typescript
// nuxt.config.ts
export default defineNuxtConfig({
    ssr: true,
    nitro: {
        preset: "static",
    },
});
```

2. **Генерація статичного сайту**:

```bash
npm run generate
```

Ця команда створить статичні файли в директорії `.output/public`, які можна розгорнути на статичному хостингу (GitHub Pages, Netlify, Vercel, Firebase Hosting тощо).

### CI/CD (Безперервна інтеграція та доставка)

Налаштування CI/CD дозволяє автоматизувати процес тестування та розгортання.

#### GitHub Actions

```yaml
# .github/workflows/deploy.yml
name: Deploy Nuxt App

on:
    push:
        branches: [main]

jobs:
    test:
        runs-on: ubuntu-latest
        steps:
            - uses: actions/checkout@v3
            - name: Setup Node.js
              uses: actions/setup-node@v3
              with:
                  node-version: "18"
                  cache: "npm"
            - name: Install dependencies
              run: npm ci
            - name: Lint
              run: npm run lint
            - name: Test
              run: npm run test

    deploy:
        needs: test
        runs-on: ubuntu-latest
        steps:
            - uses: actions/checkout@v3
            - name: Setup Node.js
              uses: actions/setup-node@v3
              with:
                  node-version: "18"
                  cache: "npm"
            - name: Install dependencies
              run: npm ci
            - name: Build
              run: npm run build
              env:
                  NODE_ENV: production
                  # Інші необхідні змінні середовища
            - name: Deploy to Production
              uses: appleboy/ssh-action@master
              with:
                  host: ${{ secrets.SSH_HOST }}
                  username: ${{ secrets.SSH_USERNAME }}
                  key: ${{ secrets.SSH_PRIVATE_KEY }}
                  script: |
                      cd /path/to/app
                      git pull
                      npm ci
                      npm run build
                      pm2 reload ecosystem.config.js
```

#### GitLab CI/CD

```yaml
# .gitlab-ci.yml
stages:
    - test
    - build
    - deploy

variables:
    NODE_ENV: production

test:
    stage: test
    image: node:18-alpine
    script:
        - npm ci
        - npm run lint
        - npm run test

build:
    stage: build
    image: node:18-alpine
    script:
        - npm ci
        - npm run build
    artifacts:
        paths:
            - .output/
        expire_in: 1 hour

deploy:
    stage: deploy
    image: alpine:latest
    before_script:
        - apk add --no-cache openssh-client
        - eval $(ssh-agent -s)
        - echo "$SSH_PRIVATE_KEY" | tr -d '\r' | ssh-add -
        - mkdir -p ~/.ssh
        - chmod 700 ~/.ssh
    script:
        - scp -r -o StrictHostKeyChecking=no .output/* $SSH_USER@$SSH_HOST:/path/to/app/
        - ssh -o StrictHostKeyChecking=no $SSH_USER@$SSH_HOST "cd /path/to/app && pm2 reload ecosystem.config.js"
    only:
        - main
```

### Моніторинг та логування

Для моніторингу продакшн-додатку важливо налаштувати відповідні інструменти.

#### PM2 для моніторингу процесів

```bash
# Перегляд статусу додатків
pm2 status

# Перегляд логів
pm2 logs

# Моніторинг ресурсів
pm2 monit

# Автоматичний перезапуск при збоях
pm2 startup
pm2 save
```

#### Налаштування логування

```typescript
// server/plugins/logger.ts
import { defineNitroPlugin } from "nitropack/runtime";
import winston from "winston";

export default defineNitroPlugin((nitroApp) => {
    // Створення логера
    const logger = winston.createLogger({
        level: process.env.NODE_ENV === "production" ? "info" : "debug",
        format: winston.format.combine(
            winston.format.timestamp(),
            winston.format.json()
        ),
        transports: [
            new winston.transports.File({
                filename: "logs/error.log",
                level: "error",
            }),
            new winston.transports.File({ filename: "logs/combined.log" }),
        ],
    });

    // Додавання консольного транспорту для розробки
    if (process.env.NODE_ENV !== "production") {
        logger.add(
            new winston.transports.Console({
                format: winston.format.combine(
                    winston.format.colorize(),
                    winston.format.simple()
                ),
            })
        );
    }

    // Додавання логера до глобального контексту
    nitroApp.hooks.hook("request", (event) => {
        event.context.logger = logger;
    });

    // Логування помилок
    nitroApp.hooks.hook("error", (error, { event }) => {
        logger.error(`${error.message}`, {
            url: event?.path || "unknown",
            method: event?.method || "unknown",
            stack: error.stack,
        });
    });
});
```

#### Інтеграція з сервісами моніторингу

**Sentry** для відстеження помилок:

```bash
npm install @sentry/node @sentry/vue
```

```typescript
// plugins/sentry.client.ts
import { defineNuxtPlugin } from "#app";
import * as Sentry from "@sentry/vue";

export default defineNuxtPlugin((nuxtApp) => {
    const vueApp = nuxtApp.vueApp;
    const config = useRuntimeConfig();

    Sentry.init({
        app: vueApp,
        dsn: config.public.sentryDsn,
        environment: process.env.NODE_ENV,
        integrations: [
            new Sentry.BrowserTracing({
                routingInstrumentation: Sentry.vueRouterInstrumentation(
                    nuxtApp.$router
                ),
            }),
        ],
        tracesSampleRate: 1.0,
    });
});
```

```typescript
// plugins/sentry.server.ts
import { defineNuxtPlugin } from "#app";
import * as Sentry from "@sentry/node";

export default defineNuxtPlugin((nuxtApp) => {
    const config = useRuntimeConfig();

    Sentry.init({
        dsn: config.public.sentryDsn,
        environment: process.env.NODE_ENV,
        tracesSampleRate: 1.0,
    });

    nuxtApp.hooks.hook("app:error", (error) => {
        Sentry.captureException(error);
    });
});
```

### Діаграми та схеми

#### Архітектура розгортання

```mermaid
graph TD
    A[Розробник] -->|git push| B[Git репозиторій]
    B -->|CI/CD Trigger| C[CI/CD Pipeline]
    C -->|Тестування| D{Тести пройдено?}
    D -->|Так| E[Збірка]
    D -->|Ні| F[Повідомлення про помилку]
    E -->|Деплой| G[Staging/QA]
    G -->|Підтвердження| H[Продакшн]

    subgraph "Продакшн середовище"
    H -->|Балансування навантаження| I[Nuxt Server 1]
    H -->|Балансування навантаження| J[Nuxt Server 2]
    H -->|Балансування навантаження| K[Nuxt Server N]
    I --> L[Бази даних]
    J --> L
    K --> L
    end
```

#### Порівняння режимів розгортання

```
┌─────────────────────────────────────────────────────┐
│ Режим         │ Переваги            │ Недоліки      │
├───────────────┼─────────────────────┼───────────────┤
│ SSR           │ SEO                 │ Серверне      │
│               │ Швидке перше        │ навантаження  │
│               │ відображення        │ Складніший    │
│               │ Єдиний код          │ деплой        │
├───────────────┼─────────────────────┼───────────────┤
│ SSG           │ Продуктивність      │ Обмеження для │
│               │ Простий деплой      │ динамічного   │
│               │ Безпека             │ контенту      │
│               │ Низька вартість     │ Час збірки    │
├───────────────┼─────────────────────┼───────────────┤
│ CSR           │ Простий деплой      │ SEO проблеми  │
│               │ Низьке серверне     │ Повільне перше│
│               │ навантаження        │ завантаження  │
├───────────────┼─────────────────────┼───────────────┤
│ Hybrid        │ Гнучкість           │ Складність    │
│               │ Оптимізація per-    │ розробки      │
│               │ route               │ Складніший    │
│               │                     │ деплой        │
└───────────────┴─────────────────────┴───────────────┘
```

#### Порівняння платформ для розгортання

```
┌─────────────────────────────────────────────────────┐
│ Платформа     │ Переваги            │ Недоліки      │
├───────────────┼─────────────────────┼───────────────┤
│ VPS/Dedicated │ Повний контроль     │ Ручне         │
│ Server        │ Кастомізація        │ налаштування  │
│               │ Гнучкість           │ Підтримка     │
├───────────────┼─────────────────────┼───────────────┤
│ Vercel        │ Простота            │ Обмеження     │
│               │ Глобальна CDN       │ функціоналу у │
│               │ Serverless          │ безкоштовному │
│               │ Інтеграція з Git    │ плані         │
├───────────────┼─────────────────────┼───────────────┤
│ Netlify       │ Простота            │ Менш гнучкий  │
│               │ Глобальна CDN       │ для складних  │
│               │ Форми, Auth         │ серверних     │
│               │                     │ додатків      │
├───────────────┼─────────────────────┼───────────────┤
│ Docker        │ Ізоляція            │ Складніше     │
│               │ Відтворюваність     │ для           │
│               │ Масштабованість     │ початківців   │
├───────────────┼─────────────────────┼───────────────┤
│ Kubernetes    │ Автоматичне         │ Висока        │
│               │ масштабування       │ складність    │
│               │ Відмовостійкість    │ Крута крива   │
│               │ Оркестрація         │ навчання      │
└───────────────┴─────────────────────┴───────────────┘
```

### Найкращі практики

1. **Автоматизуйте деплой** через CI/CD для зменшення помилок
2. **Використовуйте змінні середовища** для конфігурації
3. **Впровадьте моніторинг** для своєчасного виявлення проблем
4. **Налаштуйте логування** для відстеження помилок
5. **Використовуйте стратегію Zero-Downtime Deployment**:
    - Blue-Green deployment
    - Canary releases
    - Rolling updates
6. **Налаштуйте резервне копіювання** даних
7. **Проводьте навантажувальне тестування** перед релізами
8. **Слідкуйте за безпекою** (регулярні оновлення залежностей)

### Приклад: Повний процес деплою на VPS

```bash
#!/bin/bash
# deploy.sh

# Змінні
APP_DIR="/var/www/nuxt-app"
GIT_REPO="git@github.com:username/nuxt-app.git"
BRANCH="main"

# Оновлення коду
echo "Pulling latest code..."
if [ -d "$APP_DIR" ]; then
    cd "$APP_DIR"
    git pull origin "$BRANCH"
else
    git clone -b "$BRANCH" "$GIT_REPO" "$APP_DIR"
    cd "$APP_DIR"
fi

# Встановлення залежностей
echo "Installing dependencies..."
npm ci

# Збірка додатку
echo "Building app..."
npm run build

# Перезапуск додатку
echo "Restarting app..."
pm2 reload ecosystem.config.js --update-env

# Перевірка статусу
echo "Checking app status..."
pm2 status

echo "Deployment completed successfully!"
```

### Висновок

Розгортання Nuxt додатку вимагає розуміння архітектури проекту та вибору відповідної стратегії деплою. Вибір платформи розгортання залежить від вимог проекту, бюджету та необхідного рівня контролю. Сучасні CI/CD інструменти дозволяють автоматизувати процес розгортання та зробити його надійним і безпечним.
