# DummyAPI & Gorest

В данном проекте описаны процессы тестирования API на открытых сервисах в веб-приложении Postman, добавлены коллекции и окружения.

## Оглавление

## GOREST

## Описание проекта

https://gorest.co.in/ - данный сайт представляет собой сервис для тестирования API. Для выполнения запросов необходим получить token, который будет доступен после регистрации.
В качестве объектов тестирования были взяты объекты **User** и **Comments**.

### Важная информация

- Для постраничных результатов параметры "page" и "per_page" должны быть переданы в URL, например: GET /public/v2/users?page=1&per_page=20 (максимально 100 результатов)
- Для выполнения запросов с методами PUT, POST, PATCH, DELETE необходим токен, необходимо передать через вкладку "Authorization" в header как Bearer token.
- Доступны API версии /public-api/*, /public/v1/* and /public/v2/*

### USER
-----
#### Resources

https://gorest.co.in/public/v2/users

#### Trying it Out

POST /public/v2/users	Create a new user
GET /public/v2/users/6942253	Get user details
PUT|PATCH /public/v2/users/6942253	Update user details
DELETE /public/v2/users/6942253	Delete user

#### Nested Resources
GET /public/v2/users/6942253/posts	Retrieves user posts

#### Запросы

#### 1. GET OneUser

Выводит одного пользователя по его id, которое передается в URL запроса.

#### 2. POST CreateUser

Создание пользователя, данные которого передаются в Request body:

```javascript
{  
    "name": "Bhushit Menon DDS",
    "email": "menon_bhushit_dds@cruickshank111.test",
    "gender": "female",
    "status": "active"
}
```
**Response body**
```javascript
{
    "id": 7494004,
    "name": "Bhushit Menon DDS",
    "email": "menon_bhushit_dds@cruickshank111.test",
    "gender": "female",
    "status": "active"
}
```

#### 3. PUT ChangeUser

Изменение пользователя по его id. Данные, которые будут изменены, передаются в Request body:

```javascript
{  
    "name": "11111"
}
```
**Response body**
```javascript
{
    "name": "11111",
    "id": 7494004,
    "email": "menon_bhushit_dds@cruickshank111.test",
    "gender": "female",
    "status": "active"
}
```

#### 4. DEL DeleteUser

Удаление пользователя по его id, которое передается в URL запроса.
----
