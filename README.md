FlexDC.ru docs
---

# Установка Docker Engine и Docker Compose Plugin

Этот документ описывает процесс установки **Docker Engine** и **Docker Compose Plugin** на системы на базе Debian/Ubuntu.

---

## 1. Установка Docker Engine

### Шаг 1. Обновите индекс пакетов

```bash
sudo apt-get update
```

### Шаг 2. Установите необходимые пакеты
```bash
sudo apt-get install ca-certificates curl gnupg
```

### Шаг 3. Добавьте официальный GPG-ключ Docker
```bash
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

### Шаг 4. Настройте репозиторий Docker
```bash echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### Шаг 5. Установите Docker Engine, CLI, containerd и плагин Compose
```bash
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin```
```
### Шаг 6. Проверьте установку
```bash
sudo docker run hello-world
```

## 2. Установка Docker Compose Plugin вручную

Если Docker Engine был установлен без встроенного Compose-плагина, его можно добавить вручную.

### Шаг 1. Скачайте последнюю версию Docker Compose
```bash
DOCKER_CONFIG=${DOCKER_CONFIG:-$HOME/.docker}
mkdir -p $DOCKER_CONFIG/cli-plugins
curl -SL https://github.com/docker/compose/releases/download/v2.23.3/docker-compose-linux-x86_64 \
  -o $DOCKER_CONFIG/cli-plugins/docker-compose
```

💡 Замените v2.23.3 на нужную версию и x86_64 на архитектуру вашей системы (например, aarch64 для ARM).

### Шаг 2. Сделайте файл исполняемым
```bash
chmod +x $DOCKER_CONFIG/cli-plugins/docker-compose
```

### Шаг 3. Проверьте установку
```bash
docker compose version
```
