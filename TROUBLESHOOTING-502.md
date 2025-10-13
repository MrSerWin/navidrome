# 🔴 Решение проблемы 502 Bad Gateway

## Что означает ошибка 502?

Nginx не может подключиться к контейнеру Navidrome. Это означает, что либо контейнер не запущен, либо упал при старте.

---

## 🚀 Быстрое решение

### Шаг 1: Проверить статус сервера
```bash
./check-server.sh
```

Скрипт проверит:
- ✅ Доступность сервера
- ✅ Статус Docker
- ✅ Состояние контейнера Navidrome
- ✅ Логи контейнера
- ✅ Порты

### Шаг 2: Перезапустить контейнер
```bash
./restart-server.sh
```

Скрипт:
- 🛑 Остановит контейнер
- 🚀 Запустит его заново
- 📊 Покажет статус
- 📝 Выведет логи

---

## 🔍 Возможные причины

| Проблема | Решение |
|----------|---------|
| Контейнер остановлен | `./restart-server.sh` |
| Контейнер падает при старте | Проверить логи: `ssh root@93.127.197.163 "cd /opt/navidrome && docker compose logs navidrome"` |
| Неправильная конфигурация | Проверить docker-compose.yml на сервере |
| Docker демон не запущен | `ssh root@93.127.197.163 "systemctl start docker"` |
| Nginx неправильно настроен | `ssh root@93.127.197.163 "nginx -t"` |

---

## 🛠️ Ручная диагностика

Если скрипты не помогли, подключитесь к серверу вручную:

```bash
ssh root@93.127.197.163
```

### Проверить статус контейнера
```bash
cd /opt/navidrome
docker compose ps
```

### Посмотреть логи
```bash
docker compose logs --tail=50 navidrome
```

### Проверить, работает ли Docker
```bash
systemctl status docker
docker ps
```

### Проверить порт 4533
```bash
netstat -tlnp | grep 4533
# или
ss -tlnp | grep 4533
```

### Проверить Nginx
```bash
systemctl status nginx
nginx -t
```

### Перезапустить все
```bash
cd /opt/navidrome
docker compose down
docker compose up -d
docker compose logs -f navidrome
```

---

## 📋 Типичные ошибки в логах

### "Permission denied" в логах
```bash
# Проверить права на директории
ssh root@93.127.197.163 "ls -la /opt/navidrome/data"
```

### "Cannot bind to port"
```bash
# Проверить, не занят ли порт
ssh root@93.127.197.163 "lsof -i :4533"
```

### "Database locked"
```bash
# Перезапустить контейнер
./restart-server.sh
```

---

## ✅ После исправления

1. Откройте https://qirim.cloud
2. Нажмите **Cmd+Shift+R** (или Ctrl+Shift+R) для очистки кэша
3. Проверьте, что сайт загружается

---

## 💡 Профилактика

Чтобы избежать проблем в будущем:

1. **Регулярные проверки**
   ```bash
   ./check-server.sh
   ```

2. **Мониторинг логов**
   ```bash
   ssh root@93.127.197.163 "cd /opt/navidrome && docker compose logs -f navidrome"
   ```

3. **Автоматический перезапуск** (настроить на сервере)
   ```yaml
   # В docker-compose.yml добавить:
   restart: unless-stopped
   ```

---

## 🆘 Если ничего не помогло

Соберите диагностическую информацию и отправьте:

```bash
./check-server.sh > diagnostics.txt 2>&1
```

Затем отправьте файл `diagnostics.txt` для анализа.
