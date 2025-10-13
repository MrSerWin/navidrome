# 🚀 Быстрая справка - Navidrome

## Проблема 502 - СРОЧНО

```bash
# 1. Проверить что не так
./check-server.sh

# 2. Перезапустить
./restart-server.sh

# 3. Если не помогло - читать
cat TROUBLESHOOTING-502.md
```

---

## Деплой нового образа

```bash
# Полный процесс
./build-image.sh        # Собрать образ
./deploy-manual.sh      # Задеплоить (с паролем)

# После деплоя
# 1. Открыть https://qirim.cloud
# 2. Нажать Cmd+Shift+R (очистить кэш)
```

---

## Проверка статуса

```bash
# Локально
docker images | grep navidrome-qo

# На сервере
./check-server.sh
```

---

## Управление на сервере

```bash
# Перезапуск
./restart-server.sh

# Вручную через SSH
ssh root@93.127.197.163
cd /opt/navidrome

# Команды
docker compose ps              # статус
docker compose logs navidrome  # логи
docker compose restart         # перезапуск
docker compose up -d           # запуск
docker compose down            # остановка
```

---

## Локальная разработка

```bash
# Пересобрать UI
cd ui
npm run build

# Пересобрать образ
./build-image.sh

# Проверить образ
docker run -p 4533:4533 navidrome-qo:latest
```

---

## Документация

- `DEPLOY-INSTRUCTIONS.md` - инструкция по деплою
- `TROUBLESHOOTING-502.md` - решение 502 ошибки
- `README.md` - общая информация

---

## Скрипты

| Скрипт | Описание |
|--------|----------|
| `build-image.sh` | Собрать Docker образ |
| `deploy-manual.sh` | Деплой с вводом пароля |
| `deploy-full.sh` | Автоматический деплой (SSH ключ) |
| `check-server.sh` | Диагностика сервера |
| `restart-server.sh` | Перезапуск на сервере |

---

## Частые проблемы

### Ошибка Service Worker
✅ Уже исправлено в текущем образе

### 502 Bad Gateway
```bash
./check-server.sh
./restart-server.sh
```

### SSH не подключается
```bash
# Проверить доступ
ping 93.127.197.163
ssh -v root@93.127.197.163
```

### Docker образ не собирается
```bash
docker builder prune -a
./build-image.sh
```
