# 🚀 Инструкция по деплою Navidrome

## Быстрый старт

### 1. Собрать Docker образ
```bash
./build-image.sh
```

### 2. Задеплоить на сервер

**Вариант A: С вводом пароля (самый простой)**
```bash
./deploy-manual.sh
```
Вы будете несколько раз запрошены ввести SSH пароль.

**Вариант B: Настроить SSH ключ (один раз, потом автоматически)**
```bash
# 1. Создать SSH ключ (если еще нет)
ssh-keygen -t ed25519 -C "your_email@example.com"

# 2. Скопировать на сервер
ssh-copy-id root@SERVER_IP

# 3. Проверить доступ (должен зайти без пароля)
ssh root@SERVER_IP "echo 'SSH key works!'"

# 4. Теперь можно использовать автоматический деплой
./deploy-full.sh
```

### 3. Проверить результат
1. Откройте https://qirim.cloud
2. Очистите кэш браузера (Ctrl+Shift+R или Cmd+Shift+R)
3. Проверьте, что ошибка Service Worker исчезла

---

## Управление на сервере

### Перезапуск контейнера
```bash
ssh root@SERVER_IP
cd /opt/navidrome
docker compose restart navidrome
```

### Просмотр логов
```bash
ssh root@SERVER_IP
cd /opt/navidrome
docker compose logs -f navidrome
```

### Проверка статуса
```bash
ssh root@SERVER_IP
cd /opt/navidrome
docker compose ps
```

---

## Структура скриптов

- `build-image.sh` - сборка Docker образа локально
- `deploy-manual.sh` - деплой с вводом пароля
- `deploy-full.sh` - автоматический деплой (требует SSH ключ)
- `push-to-server.sh` - только отправка образа на сервер
- `restart.sh` - перезапуск контейнера (запускать на сервере)

---

## Решение проблем

### SSH не подключается
```bash
# Проверить доступ к серверу
ping SERVER_IP

# Проверить SSH порт
nc -zv SERVER_IP 22

# Проверить SSH конфиг
ssh -v root@SERVER_IP
```

### Docker образ не собирается
```bash
# Очистить кэш Docker
docker builder prune -a

# Попробовать снова
./build-image.sh
```

### Контейнер не стартует
```bash
# Посмотреть логи
ssh root@SERVER_IP "cd /opt/navidrome && docker compose logs --tail=100 navidrome"

# Проверить docker-compose.yml
ssh root@SERVER_IP "cd /opt/navidrome && cat docker-compose.yml"
```

---

## Что было исправлено

1. ✅ **Service Worker ошибка** - добавлен недостающий файл `workbox-expiration.prod.js`
2. ✅ **DSF библиотека** - добавлена поддержка DSF через pre-built TagLib
3. ✅ **Сборка образа** - исправлены все зависимости (zlib, taglib)
4. ✅ **Скрипты деплоя** - созданы удобные скрипты для управления

---

## Версия

Текущая версия: `v0.58.0-QO`
Образ: `navidrome-qo:latest`
