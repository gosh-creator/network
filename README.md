# network
Fast and Secure Messenger

# Network — Android Social Messenger

Android-приложение для общения в реальном времени с поддержкой личных чатов, новостной ленты и профиля пользователя. Построено на Firebase.

## Возможности

- Регистрация и вход через Firebase Authentication (email + пароль)
- Список всех зарегистрированных пользователей для создания нового чата
- Личные чаты в реальном времени через Firebase Realtime Database
- Профиль пользователя с именем и аватаром (загрузка фото через Firebase Storage)
- Редактирование биографии в настройках профиля
- Новостная лента

## Структура приложения

Навигация по четырём разделам через нижнюю панель:

| Раздел | Описание |
|---|---|
| Chats | Список активных чатов текущего пользователя |
| New Chat | Список всех пользователей для начала диалога |
| Profile | Информация пользователя, смена аватара, настройки |
| Feed | Новостная лента |

## Технологии

- **Java**, Android SDK (minSdk 24, targetSdk 33)
- **Firebase Authentication** — авторизация
- **Firebase Realtime Database** — хранение пользователей, чатов и сообщений
- **Firebase Storage** — хранение аватаров
- **Glide** — загрузка и кэширование изображений
- **CircleImageView** — круглые аватары
- **ViewBinding** — работа с UI-компонентами
- **AndroidX Navigation** — навигация между фрагментами

## Структура базы данных (Firebase Realtime Database)

```
Users/
  {uid}/
    email, username, password, profileImage, chats (через запятую)

ChatsId/
  {chatId}/
    userId1, userId2
    messages/
      {messageId}/
        ownerId, text, date
```

## Сборка и запуск

1. Клонируйте репозиторий.
2. Откройте проект в Android Studio.
3. Подключите собственный проект Firebase: замените `app/google-services.json` на свой файл из Firebase Console.
4. Включите в Firebase Console: Authentication (Email/Password), Realtime Database, Storage.
5. Запустите приложение на эмуляторе или устройстве через `Run > Run 'app'`.

## Структура проекта

```
app/src/main/
├── AndroidManifest.xml
├── java/com/example/network/
│   ├── ChatActivity.java               # Экран переписки (отправка и загрузка сообщений)
│   ├── NewsFragment.java               # Фрагмент новостной ленты
│   ├── SettingsFragment.java           # Фрагмент настроек (редактирование биографии)
│   │
│   ├── Log_Reg_in/
│   │   ├── Login.java                  # Экран входа
│   │   └── Registration.java           # Экран регистрации
│   │
│   ├── The_Main/
│   │   ├── MainOne.java                # Главный экран с нижней навигацией
│   │   └── Settings.java
│   │
│   ├── For_Chats/
│   │   ├── Chat.java                   # Модель чата
│   │   ├── ChatAdapter.java            # Адаптер списка чатов
│   │   ├── ChatViewHolder.java
│   │   ├── Fragment_menu_chats.java    # Фрагмент списка чатов пользователя
│   │   └── Fragment_new_chat.java      # Фрагмент выбора пользователя для нового чата
│   │
│   ├── Profile/
│   │   └── Fragment_profile.java       # Фрагмент профиля (аватар, имя, биография)
│   │
│   ├── chatUtils/
│   │   └── ChatUtil.java               # Утилита создания чата и генерации chatId
│   │
│   ├── message/
│   │   ├── Message.java                # Модель сообщения
│   │   └── MessagesAdapter.java        # Адаптер сообщений (входящие / исходящие)
│   │
│   ├── users/
│   │   ├── User.java                   # Модель пользователя
│   │   ├── UsersAdapter.java           # Адаптер списка пользователей
│   │   └── UserViewHolder.java
│   │
│   ├── news/
│   │   ├── News.java                   # Модель новости
│   │   ├── NewsAdapter.java
│   │   ├── NewsViewHolder.java
│   │   ├── adapter_recycler/           # Интерфейс и адаптер RecyclerView для новостей
│   │   ├── interfaces/IApiService.java # Retrofit-интерфейс API
│   │   ├── main_rep/MainRepository.java
│   │   ├── models/                     # RSS-модели (Rss, Channel, Item, Content, MainViewModel)
│   │   └── retclient/RetrofitClient.java
│   │
│   └── feed/
│       ├── FeedAdapter.java
│       ├── ItemFragmentFeed.java
│       └── placeholder/PlaceholderContent.java
│
└── res/
    ├── layout/                         # XML-разметки экранов и элементов списков
    ├── drawable/                       # Иконки и фигуры (формы сообщений, кнопки)
    ├── menu/bottom_navigation_menu.xml # Меню нижней навигации
    ├── navigation/nav_graph.xml        # Граф навигации
    ├── font/                           # Шрифты Ubuntu Light / Medium
    └── values/                         # Цвета, строки, темы, размеры
```

## Требования

- Android Studio Hedgehog или новее
- JDK 8
- Gradle 8.x
- Устройство или эмулятор с Android 7.0+ (API 24)
