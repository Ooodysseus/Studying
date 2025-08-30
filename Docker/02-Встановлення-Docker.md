# 02. Встановлення Docker

## Інсталяція Docker Engine і Docker Desktop

Docker пропонує два основні продукти для використання:

-   **Docker Engine**: серверна частина (демон) і клієнтські інструменти командного рядка
-   **Docker Desktop**: графічний інтерфейс, який включає Docker Engine та додаткові інструменти

### Встановлення на Windows

#### Вимоги до системи:

-   Windows 10 64-bit: Pro, Enterprise, або Education (збірка 18362 або новіша)
-   Увімкнений WSL 2 (Windows Subsystem for Linux 2)
-   Увімкнена віртуалізація у BIOS

#### Кроки встановлення Docker Desktop:

1. Завантажте інсталятор з офіційного сайту: [Docker Desktop для Windows](https://www.docker.com/products/docker-desktop)
2. Запустіть завантажений файл `.exe` і слідуйте інструкціям
3. Під час встановлення оберіть опцію "Use WSL 2 instead of Hyper-V"
4. Після завершення інсталяції перезавантажте комп'ютер
5. Docker Desktop запуститься автоматично після перезавантаження

> **Важливо!** Якщо у вас Windows Home, вам потрібно спочатку встановити WSL 2 і оновити систему до останньої версії.

### Встановлення на macOS

#### Вимоги до системи:

-   macOS 10.15 або новіша (Catalina, Big Sur, Monterey, Ventura)
-   Для Apple Silicon (M1/M2) або Intel процесорів є окремі інсталятори

#### Кроки встановлення:

1. Завантажте інсталятор з офіційного сайту: [Docker Desktop для Mac](https://www.docker.com/products/docker-desktop)
2. Перетягніть Docker.app у папку Applications
3. Запустіть Docker Desktop з папки Applications
4. Слідуйте підказкам для надання необхідних дозволів

### Встановлення на Linux

Для Linux доступний тільки Docker Engine, який встановлюється через командний рядок:

#### Ubuntu/Debian:

```bash
# Видалення старих версій (якщо є)
sudo apt-get remove docker docker-engine docker.io containerd runc

# Встановлення залежностей
sudo apt-get update
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

# Додавання офіційного GPG ключа Docker
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

# Додавання репозиторію Docker
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Встановлення Docker Engine
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io

# Додавання поточного користувача до групи docker (щоб не використовувати sudo)
sudo usermod -aG docker $USER
newgrp docker
```

#### CentOS/RHEL:

```bash
# Видалення старих версій
sudo yum remove docker \
                docker-client \
                docker-client-latest \
                docker-common \
                docker-latest \
                docker-latest-logrotate \
                docker-logrotate \
                docker-engine

# Встановлення залежностей
sudo yum install -y yum-utils
sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo

# Встановлення Docker Engine
sudo yum install docker-ce docker-ce-cli containerd.io

# Запуск і активація Docker
sudo systemctl start docker
sudo systemctl enable docker

# Додавання поточного користувача до групи docker
sudo usermod -aG docker $USER
newgrp docker
```

> **Порада:** На Linux рекомендується додати свого користувача до групи `docker`, щоб не використовувати `sudo` при кожній команді.

## Перевірка роботи Docker

Після встановлення Docker важливо перевірити, чи коректно він працює:

### Перевірка версії

```bash
docker --version
```

Приклад виводу:

```
Docker version 24.0.6, build ed223bc
```

### Запуск тестового контейнера

```bash
docker run hello-world
```

Якщо все працює правильно, ви побачите наступне повідомлення:

```
Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.
...
```

### Діагностика типових проблем при встановленні

1. **Docker демон не запускається**

    - Windows: Перевірте, чи увімкнено WSL 2 та віртуалізацію
    - Linux: Перевірте статус сервісу `sudo systemctl status docker`
    - Mac: Перевірте системні вимоги та перезапустіть Docker Desktop

2. **Помилка доступу до сокету Docker**

    - Linux: Додайте користувача до групи docker і перелогіньтеся

    ```bash
    sudo usermod -aG docker $USER
    newgrp docker # або перезавантажте систему
    ```

3. **Конфлікт портів**
    - Перевірте, чи порти 2375 та 2376 не зайняті іншими програмами

> **Важливо!** Після встановлення Docker на Windows чи Mac може знадобитися перезавантаження системи.

## Найкращі практики

1. **Регулярно оновлюйте Docker** до останньої версії для отримання виправлень безпеки та нових функцій.
2. **Налаштуйте ресурси Docker Desktop** відповідно до потужності вашої системи (пам'ять, CPU, диск).
3. **Використовуйте офіційні інсталятори** з сайту Docker, а не сторонні пакети.
4. **Розгляньте використання Docker в WSL 2** на Windows для кращої продуктивності.
5. **Перевірте фаєрвол** і мережеві налаштування, якщо виникають проблеми з підключенням.
