# DummyAPI & Gorest

В данном проекте описаны процессы тестирования API на открытых сервисах в веб-приложении Postman, добавлены коллекции и окружения.

## Оглавление
1. [GOREST](#gorest)
   1. [Описание проекта](#описание-проекта)
   2. [Важная информация](#важная-информация)
   3. [USER](#user)
      1. [Resources](#resources)
      2. [Trying it Out](#trying-it-out)
      3. [Nested Resources](#nested-resources)
      4. [Запросы](#запросы)
    4. [COMMENTS](#comments)
       1. [Resources](#resources-1)
       2. [Nested Resources](#nested-resources-1)
       3. [Запросы](#запросы-1)
2. [DummyAPI](#dummyapi)
   1. [Описание проекта](#описание-проекта-1)
   2. [POST](#post)
      1. [GET /post (Get List)](#get-post-get-list)
      2. [POST /post/create](#post-postcreate)
   3. [Майнд-карта](#майнд-карта)
   4. [Автотесты](#автотесты)
   5. [Quest](#quest)
3. [Коллекции POSTMAN](#коллекции-postman)

## GOREST

### Описание проекта

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

##### 1. GET OneUser

Выводит одного пользователя по его id, которое передается в URL запроса.

##### 2. POST CreateUser

Создание пользователя, данные которого передаются в Request body:

```javascript
{  
    "name": "Bhushit Menon DDS",
    "email": "menon_bhushit_dds@cruickshank111.test",
    "gender": "female",
    "status": "active"
}
```
***Response body***
```javascript
{
    "id": 7494004,
    "name": "Bhushit Menon DDS",
    "email": "menon_bhushit_dds@cruickshank111.test",
    "gender": "female",
    "status": "active"
}
```

##### 3. PUT ChangeUser

Изменение пользователя по его id. Данные, которые будут изменены, передаются в Request body:

```javascript
{  
    "name": "11111"
}
```
***Response body***
```javascript
{
    "name": "11111",
    "id": 7494004,
    "email": "menon_bhushit_dds@cruickshank111.test",
    "gender": "female",
    "status": "active"
}
```

##### 4. DEL DeleteUser

Удаление пользователя по его id, которое передается в URL запроса.

----
### COMMENTS
----

#### Resources

https://gorest.co.in/public/v2/comments

#### Nested Resources

GET /public/v2/posts/6942264/comments

#### Запросы

##### 1. GET AllComments

Возвращает все комментарии

##### 2. GET OneComment

Возвращает один комментарий по его id, который передается в URL запроса

##### 3. POST CreateComment

Создание комментария к посту. Данные комментария передаются в Request body:

```javascript
{
    "post_id": 164883,
    "name": "Sergey",
    "email": "ruuuuu@ru.ru",
    "body": "Ty zahodi, esli che"
}
```
***Response body***
```javascript
{
    "id": 127639,
    "post_id": 164883,
    "name": "Sergey",
    "email": "ruuuuu@ru.ru",
    "body": "Ty zahodi, esli che"
}
```

##### 4. PUT ChangeComment

Изменение существующего комментария. Новые данные также передаются в Request body:
```javascript
{
"body": "111111"
}
```
***Response body***
```javascript
{
    "body": "111111",
    "id": 127583,
    "post_id": 164883,
    "name": "Sergey",
    "email": "ruuuuu@ru.ru"
}
```

##### 5. DEL DeleteComment

Удаление существующего комментария по его id, который передается в URL запроса

##### 6. GET FilterCommentsByPost_NR

Возвращает комментарии по определенному посту через Nested Resources. ID поста задается в URL запроса

##### 7. POST CreateComment_NR

Cоздание комментария к определенному посту через Nested Resources. ID поста передается в URL запроса, а данные комментария в Request body:
```javascript
{    
    "name": "Bhushit Menon DDS",
    "email": "menon_bhushit_dds@cruickshank.test",
    "body": "Yeeeee"
}
```
***Response body***
```javascript
{
    "id": 127640,
    "post_id": 164883,
    "name": "Bhushit Menon DDS",
    "email": "menon_bhushit_dds@cruickshank.test",
    "body": "Yeeeee"
}
```
----

## DummyAPI

### Описание проекта

https://dummyapi.io/ - это сайт, представляющий собой тоже сервис для тестирования API. Для выполнения запросов необходим app-id, который можно получить автоматически после регистрации на сайте. Для тестирования взят объект **Post**.
В коллекции **Post** тестировались 2 метода: Get List и Create Post. 
Запросы коллекции были созданы на основании специально созданной майнд-карты.

### POST
----

#### GET /post (Get List)

Возвращает список постов, отсортированных по дате создания.
Доступен query params для вывода определенной страницы
Доступен query params для отображения числа пользователей на странице.

**Response body**

**List**
```javascript
{
data: Array(Model)
total: number(total items in DB)
page: number(current page)
limit: number(number of items on page)
}
```
**Post Preview**
```javascript
{
id: string(autogenerated)
text: string(length: 6-50, preview only)
image: string(url)
likes: number(init value: 0)
tags: array(string)
publishDate: string(autogenerated)
owner: object(User Preview)
}
```
#### POST /post/create

Создает новый пост. Возвращает данные поста.

**Request body**

**Post Create**
```javascript
{
text: string(length: 6-50, preview only)
image: string(url)
likes: number(init value: 0)
tags: array(string)
owner: string(User id)
}
```
**Response body**
```javascript
{
id: string(autogenerated)
text: string(length: 6-1000)
image: string(url)
likes: number(init value: 0)
link: string(url, length: 6-200)
tags: array(string)
publishDate: string(autogenerated)
owner: object(User Preview)
}
```

### Майнд-карта 
Данная МК представляет собой набор тестов для тестирования объекта **Post**. Подробная проверка расписана для методов **Get List** и **Create Post**

[![DummiAPI-Map 1.png](https://s.iimg.su/s/27/XDR6LgDdh3S5Cdkdwwru71x2JgMfYWHQ65TadEAH.png)](https://iimg.su/i/J8v9I)

Также майнд-карту можно [скачать](https://github.com/Zhan30/DummyAPI/blob/main/DummiAPI.xmind)

### Автотесты

Для объекта Post, 7 запросов (GetPostList, GetListByUser, GetListByTag, CreatePost, GetPostById, UpdatePost, DeletePost), были созданы скрипты автотестов, проверяющие код статуса ответа каждого запроса, получен ли OK по каждому запросу, время выполнения запроса (меньше ли оно 5000 мс). 

Также автотесты проверяют данные полученные в Response body запросов, например, соответствие полей объектам String, Number, Array, Object или undefined.

В конце автотесты методов GET проверяют параметры page, limit и total.

### Quest

В данном проекте также приложена коллекция запросов, созданных в рамках прохождения небольшого квеста. В рамках него необходимо было найти ID багов, скрытых в запросах API по объектам Author, Book и Review.

Проверялись запросы на правильность и неправильность методов, на наличие параметров в запросах. Методы POST, PUT и PATCH проверялись на корректные, некорректные значения в полях, значения разного типа. Отправлялись запросы к различным версиям API. 

----

## Коллекции POSTMAN

1. Окружение проекта DummyAPI: [скачать](https://github.com/Zhan30/DummyAPI/blob/main/DummyAPI.postman_environment.json)
2. Окружение для коллекции Quest: [скачать](https://github.com/Zhan30/DummyAPI/blob/main/Quest.postman_environment.json)
3. Коллекция запросов по объекту Post: [скачать](https://github.com/Zhan30/DummyAPI/blob/main/Post.postman_collection.json)
4. Коллекция запросов обхекта Post с автотестами: [скачать](https://github.com/Zhan30/DummyAPI/blob/main/Post_Lesson_4.postman_collection.json)
5. Коллекция запросов для квеста: [скачать](https://github.com/Zhan30/DummyAPI/blob/main/Quest.postman_collection.json)
