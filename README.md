### Апи для модераторов:

1. Получение списка пользователей:

  - URL: `/users`

  - Метод: `GET`

  - Описание: Получение списка пользователей с фильтрацией и сортировкой.

2. Получение комментариев пользователя:

  - URL: `/users/{user_id}/comments`

  - Метод: `GET`

  - Описание: Получение всех комментариев определенного пользователя.

3. Получение информации о пользователе:

  - URL: `/users/{user_id}`

  - Метод: `GET`

  - Описание: Подробная информация о пользователе и его комментариях.

4. Удаление комментария:

  - URL: `/comments/{comment_id}`

  - Метод: `DELETE`

  - Описание: Удаление комментария по его ID.

5. Получение всех комментариев с фильтрацией:

  - URL: `/comments`

  - Метод: `GET`

  - Описание: Получение списка комментариев с возможностью фильтрации по различным параметрам.

6. Блокировка пользователя:

  - URL: `/users/{user_id}/block`

  - Метод: `POST`

  - Описание: Блокировка пользователя, предотвращающая его возможность оставлять комментарии.

7. Разблокировка пользователя:

  - URL: `/users/{user_id}/unblock`

  - Метод: `POST`

  - Описание: Разблокировка пользователя, восстанавливающая его возможность оставлять комментарии.

8. Получение списка заблокированных пользователей:

  - URL: `/users/blocked`

  - Метод: `GET`

  - Описание: Получение списка всех заблокированных пользователей.

9. Редактирование комментария:

  - URL: `/comments/{comment_id}`

  - Метод: `PUT` или `PATCH`

  - Описание: Редактирование содержимого комментария.

10. Массовое удаление комментариев:

  - URL: `/comments/bulk_delete`

  - Метод: `DELETE`

  - Описание: Удаление нескольких комментариев одновременно.

11. Массовая блокировка пользователей:

  - URL: `/users/bulk_block`

  - Метод: `POST`

  - Описание: Блокировка нескольких пользователей одновременно.

12. Поиск пользователей:

  - URL: `/users/search`

  - Метод: `GET`

  - Описание: Поиск пользователей по имени, email или другим параметрам.

13. Просмотр истории модерации комментария:

  - URL: `/comments/{comment_id}/history`

  - Метод: `GET`

  - Описание: Получение истории изменений комментария, включая предыдущие версии.

14. Просмотр активности пользователя:

  - URL: `/users/{user_id}/activity`

  - Метод: `GET`

  - Описание: История активности пользователя, включая созданные комментарии и действия по модерации.

15. Массовое редактирование комментариев:

  - URL: `/comments/bulk_edit`

  - Метод: `PATCH`

  - Описание: Изменение нескольких комментариев одновременно.

### Подробное описание эндпоинтов API

1\. Получение списка пользователей

- URL: `/users`

- Метод: `GET`

- Описание: Возвращает список всех пользователей с возможностью фильтрации по активности и сортировке.

- Параметры запроса:

  - `active` (optional, boolean): фильтр по активности пользователя (true - активные, false - неактивные).

  - `sort_by` (optional, string): поле для сортировки (username, created_at).

  - `order` (optional, string): порядок сортировки (asc, desc).

  - `page` (optional, int): номер страницы для пагинации.

  - `per_page` (optional, int): количество пользователей на страницу.

- Пример запроса:

`GET /api/v1/users?active=true&sort_by=created_at&order=desc&page=1&per_page=20`

- Формат ответа:

  ```
  {

  "data": [

    {

      "id": 1,

      "username": "user1",

      "email": "user1@example.com",

      "active": true,

      "created_at": "2024-08-10T12:34:56Z",

      "updated_at": "2024-08-10T12:34:56Z"

    }

    ],

    "pagination": {

      "current_page": 1,

      "per_page": 20,

      "total_pages": 5,

      "total_count": 100

    }

  }
  ```

2\. Получение комментариев пользователя

- URL: `/users/{user_id}/comments`

- Метод: `GET`

- Описание: Возвращает список всех комментариев указанного пользователя.

- Параметры запроса:

  - `page` (optional, int): номер страницы для пагинации.

  - `per_page` (optional, int): количество комментариев на страницу.

- Пример запроса:

`GET /api/v1/users/1/comments?page=1&per_page=10`

- Формат ответа:
  ```
  {

  "data": [

    {

      "comment_id": 101,

      "user_id": 1,

      "content": "This is a comment",

      "created_at": "2024-08-10T13:45:00Z"

    }

    ],

      "pagination": {

      "current_page": 1,

      "per_page": 10,

      "total_pages": 2,

      "total_count": 20

    }

  }
  ```

3\. Получение информации о конкретном пользователе

- URL: `/users/{user_id}`

- Метод: `GET`

- Описание: Возвращает подробную информацию о пользователе по его ID, включая все его комментарии.

- Пример запроса:

`GET /api/v1/users/1`

- Формат ответа:
  ```
  {

    "id": 1,

    "username": "user1",

    "email": "user1@example.com",

    "active": true,

    "created_at": "2024-08-10T12:34:56Z",

    "updated_at": "2024-08-10T12:34:56Z"

  }
  ```

4\. Удаление комментария

- URL: `/comments/{comment_id}`

- Метод: `DELETE`

- Описание: Удаляет комментарий по его ID.

- Пример запроса:

`DELETE /api/v1/comments/101`

- Формат ответа:
  ```
    {

      "message": "Comment deleted successfully."

    }
  ```

5\. Получение всех комментариев с возможностью фильтрации

- URL: `/comments`

- Метод: `GET`

- Описание: Возвращает список всех комментариев с возможностью фильтрации по пользователю, дате создания или содержимому.

- Параметры запроса:

  - `user_id` (optional, int): фильтр по ID пользователя.

  - `date_from` (optional, string): фильтр по дате создания, начиная с указанной даты (формат: YYYY-MM-DD).

  - `date_to` (optional, string): фильтр по дате создания, заканчивая указанной датой (формат: YYYY-MM-DD).

  - `content` (optional, string): фильтр по содержимому комментария (например, поиск по ключевому слову).

  - `page` (optional, int): номер страницы для пагинации.

  - `per_page` (optional, int): количество комментариев на страницу.

- Пример запроса:

`GET /api/v1/comments?user_id=1&date_from=2024-08-01&content=spam&page=1&per_page=20`

- Формат ответа:
  ```
  {

  "data": [

      {

        "comment_id": 101,

        "user_id": 1,

        "content": "This is a spam comment",

        "created_at": "2024-08-10T13:45:00Z"

      }

    ],

      "pagination": {

      "current_page": 1,

      "per_page": 20,

      "total_pages": 5,

      "total_count": 100

    }

  }
  ```
6\. Блокировка пользователя

- URL: `/users/{user_id}/block`

- Метод: `POST`

- Описание: Блокирует пользователя, предотвращая его возможность оставлять комментарии.

- Пример запроса:

`POST /api/v1/users/1/block`

- Формат ответа:
  ```
  {

    "message": "User blocked successfully.",

    "user": {

      "id": 1,

      "username": "user1",

      "active": false,

      "blocked_at": "2024-08-12T14:30:00Z"

    }

  }
  ```
7\. Разблокировка пользователя

- URL: `/users/{user_id}/unblock`

- Метод: `POST`

- Описание: Разблокировка пользователя, восстанавливающая его возможность оставлять комментарии.

- Пример запроса:

```POST /api/v1/users/1/unblock```

- Формат ответа:
  ```
  {

    "message": "User unblocked successfully.",

    "user": {

      "id": 1,

      "username": "user1",

      "active": true,

      "unblocked_at": "2024-08-12T15:00:00Z"

      }

  }
  ```
8\. Получение списка заблокированных пользователей

- URL: `/users/blocked`

- Метод: `GET`

- Описание: Возвращает список всех заблокированных пользователей.

- Пример запроса:

`GET /api/v1/users/blocked`

- Формат ответа:
  ```
  {

    "data": [

      {

        "id": 2,

        "username": "user2",

        "email": "user2@example.com",

        "blocked_at": "2024-08-10T16:00:00Z"

      }

    ]

  }
  ```
9\. Редактирование комментария

- URL: `/comments/{comment_id}`

- Метод: `PUT` или `PATCH`

- Описание: Позволяет модератору отредактировать содержимое комментария по его ID.

- Тело запроса:
  ```
  {

    "content": "Updated comment content"

  }
  ```
- Пример запроса:

`PUT /api/v1/comments/101
`
- Формат ответа:
  ```
  {

    "comment_id": 101,

    "user_id": 1,

    "content": "Updated comment content",

    "created_at": "2024-08-10T13:45:00Z",

    "updated_at": "2024-08-12T15:30:00Z"

  }
  ```
10\. Массовое удаление комментариев

- URL: `/comments/bulk_delete`

- Метод: `DELETE`

- Описание: Позволяет модератору удалить несколько комментариев одновременно.

- Тело запроса:
  ```
  {

    "comment_ids": [101, 102, 103]

  }
  ```
- Формат ответа:
  ```
  {

    "message": "Comments deleted successfully.",

    "deleted_count": 3

  }
  ```
11\. Массовая блокировка пользователей

- URL: `/users/bulk_block`

- Метод: `POST`

- Описание: Позволяет модератору заблокировать нескольких пользователей одновременно.

- Тело запроса:
  ```
  {

    "user_ids": [1, 2, 3]

  }
  ```
- Формат ответа:
  ```
  {

    "message": "Users blocked successfully.",

    "blocked_count": 3

  }
  ```
12\. Поиск пользователей

- URL: `/users/search`

- Метод: `GET`

- Описание: Позволяет искать пользователей по имени, email или другим параметрам.

- Параметры запроса:

  - `username` (optional, string): поиск по имени пользователя.

  - `email` (optional, string): поиск по email.

  - `active` (optional, boolean): фильтр по активности пользователя.

- Пример запроса:

`GET /api/v1/users/search?username=johndoe&active=true`

- Формат ответа:
  ```
  {

  "data": [

      {

        "id": 1,

        "username": "johndoe",

        "email": "johndoe@example.com",

        "active": true

      }

    ]

  }
  ```
13\. Просмотр истории модерации комментария

- URL: `/comments/{comment_id}/history`

- Метод: `GET`

- Описание: Позволяет получить историю изменений комментария, включая предыдущие версии и действия модераторов.

- Пример запроса:

`GET /api/v1/comments/101/history`

- Формат ответа:
  ```
  {

    "comment_id": 101,

    "history": [

      {

        "version": 1,

        "content": "Original content",

        "modified_at": "2024-08-10T13:45:00Z",

        "modified_by": "moderator1"

      },

      {

        "version": 2,

        "content": "Edited content",

        "modified_at": "2024-08-11T15:30:00Z",

        "modified_by": "moderator2"

      }

    ]

  }
  ```
14\. Просмотр активности пользователя

- URL: `/users/{user_id}/activity`

- Метод: `GET`

- Описание: Возвращает историю активности пользователя, включая созданные комментарии и действия по модерации.

- Пример запроса:

`GET /api/v1/users/1/activity`

- Формат ответа:
  ```
  {

    "user_id": 1,

    "activity": [

      {

        "action": "comment_created",

        "comment_id": 101,

        "content": "This is a comment",

        "created_at": "2024-08-10T13:45:00Z"

      },

      {

        "action": "comment_deleted",

        "comment_id": 102,

        "deleted_at": "2024-08-11T15:00:00Z"

      }

    ]

  }
  ```
15\. Массовое редактирование комментариев

- URL: `/comments/bulk_edit`

- Метод: `PATCH`

- Описание: Позволяет модератору изменить несколько комментариев одновременно, например, для замены определенных слов или фраз.

- Тело запроса:
    ```
    {

      "comment_ids": [101, 102],

      "new_content": "Updated content for multiple comments"

    }
    ```
- Формат ответа:
    ```
    {

      "message": "Comments updated successfully.",

      "updated_count": 2

    }
    ```

### Обработка ошибок

Для всех эндпоинтов API предусмотрена стандартная обработка ошибок с использованием HTTP-статусов и сообщений об ошибках.

1.	400 Bad Request:
  - Описание: Возникает, когда запрос содержит неверные параметры или тело запроса.
  - Формат ответа:
    ```
    {
      “error”: “Bad Request”,
      “message”: “Invalid parameters”
    }
    ```
2.	401 Unauthorized:
  - Описание: Возникает, когда пользователь не аутентифицирован.
  - Формат ответа:
    ```
    {
      “error”: “Unauthorized”,
      “message”: “Authentication required”
    }
    ```
3.	403 Forbidden:
  - Описание: Возникает, когда у пользователя нет прав на выполнение действия.
  - Формат ответа:
    ```
    {
      “error”: “Forbidden”,
      “message”: “You do not have permission to access this resource”
    }
    ```
4.	404 Not Found:
- Описание: Возникает, когда запрашиваемый ресурс не найден.
- Формат ответа:
  ```
  {
    “error”: “Not Found”,
    “message”: “Resource not found”
  }
  ```
5.	500 Internal Server Error:
- Описание: Возникает в случае внутренней ошибки сервера.
- Формат ответа:
  ```
  {
    “error”: “Internal Server Error”,
    “message”: “An unexpected error occurred. Please try again later.”
  }
  ```
 