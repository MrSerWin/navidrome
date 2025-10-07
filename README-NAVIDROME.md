# Navidrome - Локальная Установка с Кастомной Темой

## 🎵 Установка завершена!

Navidrome собран из исходников с кастомной темой **"Custom Dark (myQO)"** и поддержкой 4 дополнительных языков.

> 📖 **Быстрый старт:** См. [NAVIDROME-QUICKSTART.md](NAVIDROME-QUICKSTART.md) для подробных инструкций по запуску и управлению
>
> 🌍 **Локализация:** См. [NAVIDROME-LOCALIZATION.md](NAVIDROME-LOCALIZATION.md) для информации о языках интерфейса

## 🚀 Запуск

```bash
cd navidrome
./start.sh
```

Или прямо из корня проекта:
```bash
navidrome/start.sh
```

Доступ: **http://localhost:4533**

## 🎨 Кастомная Тема

Создана новая тема **"Custom Dark (myQO)"** с цветовой схемой:
- Основной цвет: `#e94560` (красно-розовый)
- Фон: `#1a1a2e` (темно-синий)
- Панели: `#16213e` (синий)
- Акценты: `#0f3460` (темно-голубой)

Файлы темы:
- [ui/src/themes/customDark.js](navidrome/ui/src/themes/customDark.js)
- [ui/src/themes/customDark.css.js](navidrome/ui/src/themes/customDark.css.js)

## ⚙️ Конфигурация

Конфиг: [navidrome/navidrome.toml](navidrome/navidrome.toml)

Основные настройки:
- **Порт**: 4533
- **Музыка**: `./music/`
- **Данные**: `./navidrome-data/`
- **Тема по умолчанию**: Custom Dark (myQO)
- **Сессия**: 24 часа

## 📁 Структура Проекта

```
myQO/
├── navidrome/              # Исходники и бинарный файл
│   ├── navidrome          # Скомпилированный бинарник (65MB)
│   ├── start.sh           # Скрипт запуска
│   ├── navidrome.toml     # Конфигурация
│   └── ui/src/themes/     # Кастомные темы
├── music/                 # Ваша музыкальная библиотека
└── navidrome-data/        # База данных и кеш
```

## 🎵 Добавление Музыки

1. Добавьте музыкальные файлы в папку `music/`
2. Убедитесь, что файлы имеют правильные **ID3 теги**:
   - ARTIST - исполнитель
   - ALBUM - альбом
   - TITLE - название трека
   - ALBUMARTIST - исполнитель альбома

3. Navidrome автоматически просканирует файлы

## 🛠️ Редактирование Темы

Чтобы изменить тему:

1. Отредактируйте файлы:
   - `navidrome/ui/src/themes/customDark.js` - основные настройки темы
   - `navidrome/ui/src/themes/customDark.css.js` - CSS стили плеера

2. Пересоберите UI:
```bash
cd navidrome
make build
```

3. Перезапустите сервер

## 📦 Сборка

Использованные технологии:
- **Go 1.25.1** - бэкенд
- **Node 20.19.3** - фронтенд
- **ffmpeg 7.1.1** - транскодинг
- **taglib 2.1.1** - чтение метаданных

Команда сборки:
```bash
cd navidrome
make build
```

## 🔄 Переключение на Docker

Если хотите вернуться к Docker версии:

```bash
# Остановить локальный сервер
pkill -f navidrome

# Запустить Docker
docker-compose up -d
```


# Сначала пересоберите UI
cd ui
npm run build

# Затем соберите Go-сервер
cd ..
make build
2. Перезапустить сервер:
Если сервер уже запущен, остановите его и запустите снова:
# Остановите текущий сервер (Ctrl+C)
# Затем запустите снова:
./navidrome


## 🌐 Первый Запуск

При первом запуске:
1. Откройте http://localhost:4533
2. Увидите форму "Create Admin"
3. Создайте администратора с желаемым логином/паролем
4. Первый пользователь = админ с полными правами

## 🎨 Выбор Темы в UI

После входа:
1. Нажмите на свой аватар (правый верхний угол)
2. Settings → Theme
3. Выберите **"Custom Dark (myQO)"**

Доступные темы:
- Light
- Dark
- **Custom Dark (myQO)** ⭐
- Extra Dark
- Green
- Spotify
- Nord
- Monokai
- И другие...


команда для запуска в режиме разработки:
Терминал 1 (Backend с автоперезапуском):
cd /Volumes/T9/1_dev/1_QO/myQO/navidrome
air
Терминал 2 (Frontend с hot reload):
cd /Volumes/T9/1_dev/1_QO/myQO/navidrome/ui
npm start
Браузер:
http://localhost:4533


Самый простой способ - используйте make dev:
cd /Volumes/T9/1_dev/1_QO/myQO/navidrome
make dev
Эта команда автоматически запустит:
✅ Frontend (Vite) на порту 4533 с hot reload
✅ Backend (Go) на порту 4633 с автоперезапуском при изменениях
Все в одном терминале! 🚀
📝 Если нужны отдельные терминалы:
Терминал 1 - Frontend:
cd ui
npm start
Терминал 2 - Backend:
make server
🛑 Остановить все:
make stop
Или просто Ctrl+C в терминале с make dev