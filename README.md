# Содержание
| Метод                           | Описание                                |
| ------------------------------- | --------------------------------------- |
| [getToken](#gettoken)           | Получение токена для авторизации в API. |
| [getCategories](#getcategories) | Получение списка категорий.             |
| [getItems](#getitems)           | Получение списка товаров.               |
| newCart (В разработке)          | Создание корзины                        |
| cartAdd (В разработке)          | Добавление товара в корзину             |
| cartQuantity (В разработке)     | Изменить количетсов товара в корзине    |
| cartRemove (В разработке)       | Удалить товар из корзины                |
| cartList (В разработке)         | Получить список товаров в корзине       |
| cartOrder (В разработке)        | Оформление заказа                       |



# getToken

## Описание:

Получение токена для авторизации в API. Для получения токена необходимо быть авторизованным на сайте.

## Параметры:

Это действие не требует параметров.

## Примеры кода:

CURL:

```bash
curl -X GET 'https://example.com/path/to/api/?action=getToken'
```

JavaScript

```javascript
fetch('https://example.com/path/to/api/?action=getToken', {
  method: 'GET'
})
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error('Error:', error));
```

# getCategories

## Описание:

Получение списка категорий. При отсутствии параметров выводит верхний уровень категорий. При использовании параметра id, выводятся дочерние категории указанной категории.

## Параметры:

| Имя | Тип     | Значение по умолчанию | Обязательный | Описание                                         |
| --- | ------- | --------------------- | ------------ | ------------------------------------------------ |
| id  | integer | None                  | No           | ID категории для получения её дочерних категорий |

## Примеры кода:

CURL:

```bash
curl -X GET 'https://example.com/path/to/api/?action=getCategories' \
-H 'TOKEN_API: YourApiTokenHere'
# Для получения дочерних категорий
curl -X GET 'https://example.com/path/to/api/?action=getCategories&id=123' \
-H 'TOKEN_API: YourApiTokenHere'
```

JavaScript

```javascript
// Получение верхнего уровня категорий
fetch('https://example.com/path/to/api/?action=getCategories', {
  method: 'GET',
  headers: {
    'TOKEN_API': 'YourApiTokenHere'
  }
})
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error('Error:', error));

// Получение дочерних категорий для категории с ID 123
fetch('https://example.com/path/to/api/?action=getCategories&id=123', {
  method: 'GET',
  headers: {
    'TOKEN_API': 'YourApiTokenHere'
  }
})
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error('Error:', error));
```

## Формат ответа JSON

```json
[
  {
    "id": "ID категории",
    "name": "Имя категории",
    "active": "Статус активности (true/false)",
    "left": "Левая граница",
    "right": "Правая граница",
    "level": "Уровень глубины",
    "parent_id": "ID родительской категории",
    "has_child": "Наличие дочерних категорий (количество)"
  }
]
```

# getItems

## Описание

Получение списка товаров. Позволяет фильтровать товары по категории, включать товары из всех подкатегорий, а также использовать пагинацию для контроля количества и порядка выводимых товаров.

## Параметры

| Имя         | Тип     | Значение по умолчанию | Обязательный | Описание                                                                |
| ----------- | ------- | --------------------- | ------------ | ----------------------------------------------------------------------- |
| id          | integer | None                  | No           | Идентификатор категории. При отсутствии выводятся товары без категории. |
| all         | boolean | false                 | No           | Если true, выводятся товары из всех подкатегорий указанной категории.   |
| page_size   | integer | None                  | No           | Количество товаров на странице для пагинации.                           |
| page_number | integer | None                  | No           | Номер страницы для пагинации.                                           |

## Примеры кода:

CURL:

```bash
curl -X GET 'https://example.com/path/to/api/?action=getItems&id=10&all=true&page_size=50&page_number=2' \
-H 'TOKEN_API: YourApiTokenHere'
```

JavaScript:

```javascript
fetch('https://example.com/path/to/api/?action=getItems&id=10&all=true&page_size=50&page_number=2', {
  method: 'GET',
  headers: {
    'TOKEN_API': 'YourApiTokenHere'
  }
})
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error('Error:', error));
```

## Формат ответа JSON:

```json
[
  {
    "id": "ID товара",
    "name": "Название товара",
    "article": "Артикул",
    "active": "Статус активности (true/false)",
    "quantity": "Количество на складе",
    "price": "Цена товара"
  }
]
```
