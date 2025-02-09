# Blog REST API

REST API для ведения блога с аутентификацией пользователей и CRUD-операциями для постов.

## Требования
- Python 3.7+
- Установленные пакеты из `requirements.txt`

## Установка

1. Клонируйте репозиторий:

```
git clone <URL_репозитория>
cd <папка_проекта>
```
   
2. Установите зависимости:

```
pip install -r requirements.txt
```
   
3. Настройте базу данных:

```
flask db init
flask db migrate
flask db upgrade
```
    
4. Запустите сервер:

```
flask run
```
    
Сервер будет доступен по адресу: http://localhost:5000.

Примеры запросов

1. Регистрация пользователя

```
POST /register
Content-Type: application/json

{
  "username": "john_doe",
  "email": "john@example.com",
  "password": "secret123"
}
```
   
Ответ:

```
{"msg": "User created"}
```

2. Аутентификация (получение токена)

```
POST /login
Content-Type: application/json

{
  "email": "john@example.com",
  "password": "secret123"
}
```
   
Ответ:

```
{"access_token": "ваш_токен"}
```

3. Создание поста

```
POST /posts
Authorization: Bearer ваш_токен
Content-Type: application/json

{
  "title": "Мой первый пост",
  "content": "Привет, мир!"
}
```
   
Ответ:

```
{
  "id": 1,
  "title": "Мой первый пост",
  "content": "Привет, мир!",
  "created_at": "2023-10-05T12:00:00",
  "user_id": 1
}
```

4. Получение всех постов

```
GET /posts
```
   
Ответ:

```
[
  {
    "id": 1,
    "title": "Мой первый пост",
    "content": "Привет, мир!",
    "created_at": "2023-10-05T12:00:00",
    "user_id": 1
  }
]
```

5. Получение конкретного поста

```
GET /posts/1
```
   
Ответ:
   
```
{
  "id": 1,
  "title": "Мой первый пост",
  "content": "Привет, мир!",
  "created_at": "2023-10-05T12:00:00",
  "user_id": 1
}
```

6. Обновление поста
   
```
PUT /posts/1
Authorization: Bearer ваш_токен
Content-Type: application/json

{
  "title": "Новый заголовок",
  "content": "Обновленное содержание"
}
```
   
Ответ:

```
{
  "id": 1,
  "title": "Новый заголовок",
  "content": "Обновленное содержание",
  "created_at": "2023-10-05T12:00:00",
  "user_id": 1
}
```

7. Удаление поста

```
DELETE /posts/1
Authorization: Bearer ваш_токен
```

Ответ:

```
{"msg": "Post deleted"}
```

Тестирование через cURL

Пример создания поста:

```
curl -X POST -H "Content-Type: application/json" -H "Authorization: Bearer ваш_токен" \
-d '{"title":"Тест", "content":"Тестовый пост"}' http://localhost:5000/posts
```

Примечания

Для операций с постами (кроме GET-запросов) требуется заголовок Authorization: Bearer <токен>.
Изменять или удалять посты может только их автор.
