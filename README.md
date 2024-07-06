# Tasks API

API для управления задачами с использованием Laravel и Sanctum.

## Описание

Этот API позволяет пользователям регистрироваться, входить в систему и управлять своими задачами. Пользователи могут создавать, обновлять, просматривать и удалять задачи, а также искать задачи по статусу и крайнему сроку.

## Требования

- PHP >= 8.2
- Composer
- Laravel 10.x
- Laravel Sanctum

## Установка

1. Клонируйте репозиторий:
    ```bash
    git clone https://github.com/Huldul/kvok.git
    cd tasks-api
    ```

2. Установите зависимости:
    ```bash
    composer install
    ```

3. Скопируйте файл окружения:
    ```bash
    cp .env.example .env
    ```

4. Сгенерируйте ключ приложения:
    ```bash
    php artisan key:generate
    ```

5. Настройте файл `.env` с данными для подключения к базе данных.

6. Запустите миграции:
    ```bash
    php artisan migrate
    ```

## Использование

Запустите локальный сервер:
```bash
php artisan serve
```

## Документация

Полная документация API доступна на [Swagger](https://app.swaggerhub.com/apis/KIRIUNCHIK/Kvok/1.0.0#/User).

## Эндпоинты

### Регистрация пользователя

**URL:** `/api/register`  
**Метод:** `POST`  
**Описание:** Регистрация нового пользователя.

**Запрос:**
```json
{
    "name": "Имя Пользователя",
    "email": "email@example.com",
    "password": "password123",
    "password_confirmation": "password123"
}
```

**Ответ:**
```json
{
    "token": "your-auth-token"
}
```

### Вход пользователя

**URL:** `/api/login`  
**Метод:** `POST`  
**Описание:** Вход пользователя и получение токена авторизации.

**Запрос:**
```json
{
    "email": "email@example.com",
    "password": "password123"
}
```

**Ответ:**
```json
{
    "token": "your-auth-token"
}
```

### Получение списка задач

**URL:** `/api/tasks`  
**Метод:** `GET`  
**Описание:** Получение списка задач пользователя. Поддерживается фильтрация по статусу и крайнему сроку.

**Заголовки:**
```http
Authorization: Bearer your-auth-token
```

**Параметры запроса (опционально):**
- `status`: Статус задачи (например, `completed`, `pending`).
- `due_date`: Крайний срок задачи в формате `YYYY-MM-DD`.

**Ответ:**
```json
[
    {
        "id": 1,
        "title": "Задача 1",
        "description": "Описание задачи 1",
        "status": "pending",
        "created_at": "2024-07-07T00:00:00.000000Z",
        "due_date": "2024-07-10T00:00:00.000000Z"
    },
    {
        "id": 2,
        "title": "Задача 2",
        "description": "Описание задачи 2",
        "status": "completed",
        "created_at": "2024-07-07T00:00:00.000000Z",
        "due_date": "2024-07-08T00:00:00.000000Z"
    }
]
```

### Создание задачи

**URL:** `/api/tasks`  
**Метод:** `POST`  
**Описание:** Создание новой задачи для пользователя.

**Заголовки:**
```http
Authorization: Bearer your-auth-token
```

**Запрос:**
```json
{
    "title": "Новая задача",
    "description": "Описание новой задачи",
    "status": "pending",
    "due_date": "2024-07-15"
}
```

**Ответ:**
```json
{
    "id": 3,
    "title": "Новая задача",
    "description": "Описание новой задачи",
    "status": "pending",
    "created_at": "2024-07-07T00:00:00.000000Z",
    "due_date": "2024-07-15T00:00:00.000000Z"
}
```

### Получение задачи

**URL:** `/api/tasks/{id}`  
**Метод:** `GET`  
**Описание:** Получение информации о задаче по её ID.

**Заголовки:**
```http
Authorization: Bearer your-auth-token
```

**Ответ:**
```json
{
    "id": 1,
    "title": "Задача 1",
    "description": "Описание задачи 1",
    "status": "pending",
    "created_at": "2024-07-07T00:00:00.000000Z",
    "due_date": "2024-07-10T00:00:00.000000Z"
}
```

### Обновление задачи

**URL:** `/api/tasks/{id}`  
**Метод:** `PUT`  
**Описание:** Обновление информации о задаче по её ID.

**Заголовки:**
```http
Authorization: Bearer your-auth-token
```

**Запрос:**
```json
{
    "title": "Обновленная задача",
    "description": "Описание обновленной задачи",
    "status": "completed",
    "due_date": "2024-07-20"
}
```

**Ответ:**
```json
{
    "id": 1,
    "title": "Обновленная задача",
    "description": "Описание обновленной задачи",
    "status": "completed",
    "created_at": "2024-07-07T00:00:00.000000Z",
    "due_date": "2024-07-20T00:00:00.000000Z"
}
```

### Удаление задачи

**URL:** `/api/tasks/{id}`  
**Метод:** `DELETE`  
**Описание:** Удаление задачи по её ID.

**Заголовки:**
```http
Authorization: Bearer your-auth-token
```

**Ответ:**
```json
{
    "message": "Task deleted successfully"
}
```

Этот README содержит основную информацию о проекте, инструкцию по установке и использованию, а также описание основных эндпоинтов. Ссылка на Swagger документацию также включена.
