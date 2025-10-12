# Файловая структура проекта

## 📚 Документация

### Основные документы:
- **[README.md](README.md)** - Главная страница проекта
- **[DEPLOYMENT.md](DEPLOYMENT.md)** - Полное руководство по развертыванию
- **[DEPLOY-QIRIM-ONLINE.md](DEPLOY-QIRIM-ONLINE.md)** - Инструкция для qirim.online
- **[QUICK-START.md](QUICK-START.md)** - Быстрая шпаргалка по командам

### Справочные документы:
- **[README-NAVIDROME-ORIGINAL.md](README-NAVIDROME-ORIGINAL.md)** - Оригинальный README Navidrome
- **[CONTRIBUTING.md](CONTRIBUTING.md)** - Как внести вклад
- **[CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md)** - Кодекс поведения

---

## 🛠 Скрипты

### Развертывание и обновление:
- **[deploy.sh](deploy.sh)** - Полное развертывание на новом домене
- **[update.sh](update.sh)** - Обновление кода (ui/go/full)

### SSL и безопасность:
- **[get-certificate.sh](get-certificate.sh)** - Получение SSL сертификата
- **[apply-ssl.sh](apply-ssl.sh)** - Применение SSL конфигурации
- **[check-ssl-status.sh](check-ssl-status.sh)** - Проверка статуса SSL

### Диагностика:
- **[quick-check.sh](quick-check.sh)** - Быстрая проверка статуса сервера

---

## ⚙️ Конфигурация

### Docker:
- **[docker-compose.yml](docker-compose.yml)** - Конфигурация Docker сервисов
- **[Dockerfile.fixed](Dockerfile.fixed)** - Dockerfile для сборки Navidrome
- **[.dockerignore](.dockerignore)** - Исключения для Docker

### Nginx:
- **[nginx/nginx.conf](nginx/nginx.conf)** - Nginx с SSL и редиректом
- **[nginx/nginx-temp.conf](nginx/nginx-temp.conf)** - Nginx без SSL (временный)

### Переменные:
- **[.env](.env)** - Переменные окружения (создаётся при развертывании)

---

## 🎨 Кастомизация

### Темы:
- **[ui/src/themes/qoDark.js](ui/src/themes/qoDark.js)** - Тёмная тема QO
- **[ui/src/themes/qoLight.js](ui/src/themes/qoLight.js)** - Светлая тема QO
- **[ui/src/themes/index.js](ui/src/themes/index.js)** - Экспорт тем

### UI компоненты:
- **[ui/src/album/AlbumGridView.jsx](ui/src/album/AlbumGridView.jsx)** - Круглые обложки
- **[ui/src/song/SongList.jsx](ui/src/song/SongList.jsx)** - Непрерывное воспроизведение
- **[ui/src/song/useAutoLoadQueue.js](ui/src/song/useAutoLoadQueue.js)** - Автозагрузка очереди

### Логотипы:
- **[ui/public/qo-logo-dark.png](ui/public/qo-logo-dark.png)** - Логотип для тёмной темы
- **[ui/public/qo-logo-light.png](ui/public/qo-logo-light.png)** - Логотип для светлой темы

---

## 📦 Архив

Старые документы и скрипты перемещены в:
- **[archive/old-docs/](archive/old-docs/)** - Устаревшие документы
- **[archive/old-scripts/](archive/old-scripts/)** - Устаревшие скрипты

---

## 🗂 Структура директорий

```
navidrome/
├── 📄 README.md                      # Главная страница
├── 📄 DEPLOYMENT.md                  # Руководство по развертыванию
├── 📄 DEPLOY-QIRIM-ONLINE.md         # Инструкция для qirim.online
├── 📄 QUICK-START.md                 # Шпаргалка
├── 📄 FILES.md                       # Этот файл
│
├── 🔧 deploy.sh                      # Скрипт развертывания
├── 🔧 update.sh                      # Скрипт обновления
├── 🔧 quick-check.sh                 # Проверка статуса
├── 🔧 get-certificate.sh             # Получение SSL
├── 🔧 apply-ssl.sh                   # Применение SSL
├── 🔧 check-ssl-status.sh            # Проверка SSL
│
├── ⚙️  docker-compose.yml             # Docker конфигурация
├── ⚙️  Dockerfile.fixed               # Dockerfile
├── ⚙️  .dockerignore                  # Исключения Docker
│
├── 📁 nginx/                         # Nginx конфигурация
│   ├── nginx.conf                   # С SSL
│   └── nginx-temp.conf              # Без SSL
│
├── 📁 ui/                            # React UI
│   ├── src/
│   │   ├── themes/                  # Кастомные темы
│   │   │   ├── qoDark.js
│   │   │   ├── qoLight.js
│   │   │   └── index.js
│   │   ├── album/
│   │   │   └── AlbumGridView.jsx   # Круглые обложки
│   │   └── song/
│   │       ├── SongList.jsx        # Непрерывное воспроизведение
│   │       └── useAutoLoadQueue.js # Автозагрузка
│   └── public/
│       ├── qo-logo-dark.png        # Логотип тёмной темы
│       └── qo-logo-light.png       # Логотип светлой темы
│
├── 📁 db/                            # Go код и миграции
├── 📁 server/                        # Серверный код
├── 📁 conf/                          # Конфигурационные файлы
│
└── 📁 archive/                       # Архив
    ├── old-docs/                    # Старые документы
    └── old-scripts/                 # Старые скрипты
```

---

**Версия:** v0.58.0-QO
**Последнее обновление:** 2025-10-12
