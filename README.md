## Деплой и настройка удалённого сервера.

### Стек:
- Django
- PostgreSQL
- Docker + Docker Compose
- Nginx
- CI/CD через GitHub Actions

### CI/CD через GitHub Actions
Workflow запускается автоматически при пуше в репозиторий.

#### Включает этапы:

- Линтинг кода с помощью flake8

- Юнит-тесты

- Сборка Docker-образов

- Деплой на удалённый сервер через SSH

###  Секреты в GitHub (в Settings > Secrets and variables > Actions)
#### Создайте переменные:

- DOCKER_HUB_USERNAME — имя пользователя Docker Hub

- DOCKER_HUB_ACCESS_TOKEN — токен Docker Hub

- SERVER_IP — IP-адрес сервера

- SSH_USER — пользователь на сервере

- SSH_KEY — приватный SSH-ключ

- DEPLOY_DIR — директория на сервере, где будет размещён проект

### Настройка удалённого сервера (Ubuntu)
1. Установите Docker и Docker Compose:
```commandline
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL <https://download.docker.com/linux/ubuntu/gpg> -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] <https://download.docker.com/linux/ubuntu> \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt install docker-compose -y
```
2. Подключитесь к серверу по SSH, установите Git и склонируйте проект:
```
sudo apt install git
```
```
ssh ubuntu@158.160.133.231
```
```
git clone https://github.com/VasiliySochnev/SkyproLibraryProject.git
```
3. Перейдите в директорию с проектом
```
cd SkyproLibraryProject
```
4. Запустите проект:
```
sudo docker-compose up -d
```