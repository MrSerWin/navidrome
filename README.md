# Navidrome QO - Custom Music Streaming Server

Кастомная версия Navidrome с темами QO Dark/Light, круглыми обложками альбомов, непрерывным воспроизведением и автоматической загрузкой очереди.

![Version](https://img.shields.io/badge/version-0.58.0--QO-blue)
![Navidrome](https://img.shields.io/badge/based%20on-Navidrome%200.58.0-green)

---

## 🚀 Быстрый старт

### Развертывание на новом домене

```bash
./deploy.sh your-domain.com root@vps-ip
```

**Пример для qirim.online:**

```bash
./deploy.sh qirim.online root@93.127.197.163
```

Скрипт автоматически:
- ✅ Проверит DNS
- ✅ Загрузит код на VPS
- ✅ Соберёт Docker образ
- ✅ Запустит Navidrome
- ✅ Настроит SSL сертификат
- ✅ Настроит редирект HTTP → HTTPS

**Время:** ~5-7 минут

---

## 📚 Документация

### Основные документы:

- **[DEPLOYMENT.md](DEPLOYMENT.md)** - Полное руководство по развертыванию
- **[DEPLOY-QIRIM-ONLINE.md](DEPLOY-QIRIM-ONLINE.md)** - Специфичная инструкция для qirim.online
- **[CHEATSHEET.md](CHEATSHEET.md)** - Шпаргалка по командам Docker

### Дополнительные документы:

- **[README-NAVIDROME-ORIGINAL.md](README-NAVIDROME-ORIGINAL.md)** - Оригинальный README Navidrome
- **[CONTRIBUTING.md](CONTRIBUTING.md)** - Как внести вклад в Navidrome
- **[CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md)** - Кодекс поведения

---

## ✨ Кастомные функции

### 1. Темы QO Dark/Light

Две новые темы разработанные специально для QO Music:

- **QO Dark** (по умолчанию) - Тёмная тема на основе Nord Theme
- **QO Light** - Светлая тема с цветовой схемой Light Theme

**Файлы:**
- [ui/src/themes/qoDark.js](ui/src/themes/qoDark.js)
- [ui/src/themes/qoLight.js](ui/src/themes/qoLight.js)

### 2. Круглые обложки альбомов

Обложки альбомов отображаются круглыми (70% размера, по центру).

**Файл:** [ui/src/album/AlbumGridView.jsx](ui/src/album/AlbumGridView.jsx)

### 3. Непрерывное воспроизведение

При клике на песню в очередь добавляются ВСЕ песни из текущего списка, а не только одна.

**Файл:** [ui/src/song/SongList.jsx](ui/src/song/SongList.jsx)

### 4. Автоматическая загрузка очереди

Когда в очереди остаётся меньше 10 песен, автоматически загружается следующая страница.

**Файл:** [ui/src/song/useAutoLoadQueue.js](ui/src/song/useAutoLoadQueue.js)

### 5. Кастомные логотипы

- Логотип QO для тёмной темы
- Логотип QO для светлой темы

**Файлы:**
- [ui/public/qo-logo-dark.png](ui/public/qo-logo-dark.png)
- [ui/public/qo-logo-light.png](ui/public/qo-logo-light.png)

---

## 🛠 Полезные скрипты

### Развертывание и обновление:

- **`deploy.sh`** - Полное развертывание на новом домене/VPS
- **`update.sh`** - Обновление кода (ui/go/full)
- **`get-certificate.sh`** - Получение SSL сертификата
- **`apply-ssl.sh`** - Применение SSL конфигурации

### Диагностика:

- **`quick-check.sh`** - Быстрая проверка статуса
- **`check-ssl-status.sh`** - Проверка SSL сертификата

### Примеры использования:

```bash
# Полное развертывание
./deploy.sh qirim.online root@93.127.197.163

# Обновить только UI
./update.sh ui

# Обновить только Go код
./update.sh go

# Полное обновление
./update.sh full

# Проверить статус
./quick-check.sh

# Получить SSL сертификат вручную
./get-certificate.sh
```

---

## 📦 Структура проекта

```
navidrome/
├── deploy.sh                 # Главный скрипт развертывания
├── update.sh                 # Скрипт обновления
├── quick-check.sh            # Проверка статуса
├── get-certificate.sh        # Получение SSL
├── apply-ssl.sh              # Применение SSL
├── check-ssl-status.sh       # Проверка SSL
│
├── DEPLOYMENT.md             # Полное руководство
├── DEPLOY-QIRIM-ONLINE.md    # Инструкция для qirim.online
├── CHEATSHEET.md             # Шпаргалка
│
├── docker-compose.yml        # Конфигурация Docker
├── Dockerfile.fixed          # Dockerfile (рабочий)
├── .dockerignore             # Исключения Docker
│
├── nginx/
│   ├── nginx.conf            # Nginx с SSL
│   └── nginx-temp.conf       # Nginx без SSL (временный)
│
├── ui/                       # React UI
│   ├── src/
│   │   ├── themes/
│   │   │   ├── qoDark.js     # Тёмная тема QO
│   │   │   ├── qoLight.js    # Светлая тема QO
│   │   │   └── index.js      # Экспорт тем
│   │   ├── album/
│   │   │   └── AlbumGridView.jsx  # Круглые обложки
│   │   └── song/
│   │       ├── SongList.jsx       # Непрерывное воспроизведение
│   │       └── useAutoLoadQueue.js # Автозагрузка очереди
│   └── public/
│       ├── qo-logo-dark.png  # Логотип для тёмной темы
│       └── qo-logo-light.png # Логотип для светлой темы
│
├── db/                       # Go код и миграции
├── server/                   # Серверный код
└── archive/                  # Старые скрипты и документы
    ├── old-docs/             # Устаревшие документы
    └── old-scripts/          # Устаревшие скрипты
```

---

## 🔧 Требования

### На Mac (разработка):

- Git
- SSH доступ к VPS

### На VPS (production):

- Ubuntu 20.04+
- Docker и Docker Compose (установится автоматически)
- Открытые порты: 80, 443
- DNS A-запись на IP VPS

---

## 🌐 Текущие развертывания

- **qirim.cloud** - `https://qirim.cloud` (93.127.197.163)
- **qirim.online** - (готово к развертыванию)

---

## 📝 Обновление кода

### После изменений в UI:

```bash
./update.sh ui root@93.127.197.163
```

⏱ **Время:** ~1-2 минуты

### После изменений в Go коде:

```bash
./update.sh go root@93.127.197.163
```

⏱ **Время:** ~2-3 минуты

### Полное обновление:

```bash
./update.sh full root@93.127.197.163
```

⏱ **Время:** ~3-5 минут

---

## 🐛 Troubleshooting

### Сайт недоступен

```bash
# Проверить DNS
dig +short your-domain.com

# Проверить статус
./quick-check.sh

# Просмотреть логи (на VPS)
ssh root@vps-ip 'cd /opt/navidrome && docker compose logs navidrome'
```

### SSL не работает

```bash
# Получить сертификат вручную
./get-certificate.sh

# Применить SSL конфигурацию
./apply-ssl.sh
```

### Ошибки сборки

```bash
# Полная пересборка (на VPS)
ssh root@vps-ip
cd /opt/navidrome
docker compose down
docker system prune -a
docker compose build --no-cache navidrome
docker compose up -d
```

Подробнее: [DEPLOYMENT.md - Troubleshooting](DEPLOYMENT.md#troubleshooting)

---

## 🤝 Вклад в проект

Этот проект основан на [Navidrome](https://github.com/navidrome/navidrome).

Для вклада в оригинальный Navidrome, смотрите [CONTRIBUTING.md](CONTRIBUTING.md).

---

## 📄 Лицензия

Как и оригинальный Navidrome, этот проект распространяется под лицензией GPL v3.

---

## 🔗 Полезные ссылки

- [Navidrome Official Site](https://www.navidrome.org)
- [Navidrome Documentation](https://www.navidrome.org/docs/)
- [Navidrome GitHub](https://github.com/navidrome/navidrome)
- [Docker Documentation](https://docs.docker.com/)
- [Let's Encrypt](https://letsencrypt.org/)

---

## 📞 Поддержка

При проблемах:

1. Проверьте [DEPLOYMENT.md - Troubleshooting](DEPLOYMENT.md#troubleshooting)
2. Запустите `./quick-check.sh` для диагностики
3. Проверьте логи: `docker compose logs navidrome` (на VPS)

---

**Версия:** v0.58.0-QO
**Базируется на:** Navidrome v0.58.0
**Последнее обновление:** 2025-10-12
