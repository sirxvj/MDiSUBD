# Бекман Андрей 253505, E-commerce platform
Субд: PostreSql
## Функциональные требования
- Аутентификация\авторизация с ипользованием access\refresh токенов
- Система ролей: покупатель, продавец, администратор
- CRUD операции для всех сущностей БД
- Возможность просмотра и поиска товаров с помощью категорий
- Просмотр корзины\истории покупок
- Статистика продаж для продавца
- Интеграция платежной системы
## Схема сущностей базы данных
![fixed](https://github.com/user-attachments/assets/d203549c-2eff-4e8b-b0dc-b46ac7f04b93)

## 1. Таблица **`Users`** 
- **`Id`**: UUID PRIMARY KEY - Уникальный идентефикатор
- **`Email`**: VARCHAR(50) Unique NOTNULL - Адрес электронной почты
- **`Phone`**: VARCHAR(30) Unique NOTNULL - Номер телефона
- **`PasswordHash`**: BYTEA NOTNULL - хеш пароля
- **`FirstName`**: VARCHAR(50) NOTNULL - Имя пользователя
- **`LastName`**: VARCHAR(50) NOTNULL - Фамилия пользователя
## 2. Таблица **`Customers`** 
- **`Id`**: UUID PRIMARY KEY - Уникальный 
- **`StripeId`**: VARCHAR(50) - Уникальный идентефикатор в платежной системе
- **`UserId`**: UUID REFERENCES Users(Id) ON DELETE CASCADE - Внешний ключ соответствующий сущности пользователя
## 3. Таблица **`Admins`** 
- **`Id`**: UUID PRIMARY KEY - Уникальный идентефикатор
- **`IsSuper`**: BOOLEAN DEFAULT FALSE NOTNULL - Флаг указывающий на привелегированные возможности администратора
- **`UserId`**: UUID REFERENCES Users(Id) ON DELETE CASCADE - Внешний ключ соответствующий сущности пользователя
## 4. Таблица **`Sellers`** 
- **`Id`**: UUID PRIMARY KEY - Уникальный идентефикатор
- **`ShopName`**: VARCHAR(100) NOTNULL - Имя продавца, показываемое покупателю
- **`UserId`**: UUID REFERENCES Users(Id) ON DELETE CASCADE - Внешний ключ соответствующий сущности пользователя
## 5. Таблица **`RefreshTokens`** 
- **`Id`**: UUID PRIMARY KEY - Уникальный идентефикатор
- **`Token`**: TEXT NOTNULL - Значение токена
- **`ExpiresAt`**: TIMESTAMP WITH TIME ZONE NOTNULL - Время до которого токен валиден
- **`UserId`**: UUID REFERENCES Users(Id) ON DELETE CASCADE - Внешний ключ соответствующий сущности пользователя
## 6. Таблица **`Products`** 
- **`Id`**: UUID PRIMARY KEY - Уникальный идентефикатор
- **`Name`**: VARCHAR(200) NOTNULL - Наименование продукта
- **`Description`**: TEXT NOTNULL - Описание продукта
- **`Price`**: REAL NOTNULL - Цена продукта
- **`Quantity`**: INTEGER  NOTNULL - Количество оставшихся экземпляров у продавца
- **`SellerId`**: UUID REFERENCES Sellers(Id) ON DELETE CASCADE - Внешний ключ, соответствующий сущности продавца товара
## 7. Таблица **`Categories`** 
- **`Id`**: UUID PRIMARY KEY - Уникальный идентефикатор
- **`Name`**: VARCHAR(100) NOTNULL - Уникальный идентефикатор
- **`ParentCategoryId`**: UUID REFERENCES CATEGORIES(Id) ON DELETE CASCADE - Внешний ключ, соответствующий сущности родительской категории
## 8. Таблица **`ProductMedias`** 
- **`Id`**: UUID PRIMARY KEY - Уникальный идентефикатор
- **`ProductId`**: UUID REFERENCES PRODUCT(Id) ON DELETE CASCADE - Внешний ключ, соответствующий сущности продукта
- **`BlobId`**: VARCHAR(50) NOTNULL - Строка идентефицирующая изображение в облачном хранилище
## 9. Таблица **`CartItems`** 
- **`Id`**: UUID PRIMARY KEY - Уникальный идентефикатор
- **`Quantity`**: INTEGER NOTNULL - Количество добавленных в корзину товаров
- **`ProductId`**: UUID REFERENCES PRODUCT(Id) - Внешний ключ, указывающий на ссущность продукта
- **`CustomerId`**: UUID REFERENCES CUSTOMER(Id) - Внешний ключ, указывающий на сущность покупателя, добавившего продукт в корзину
## 10. Таблица **`Orders`** 
- **`Id`**: UUID PRIMARY KEY - Уникальный идентефикатор
- **`Quantity`**: INTEGER NOTNULL - Количество добавленных в корзину товаров
- **`ProductId`**: UUID REFERENCES PRODUCT(Id) - Внешний ключ, указывающий на ссущность продукта
- **`CustomerId`**: UUID REFERENCES CUSTOMER(Id) - Внешний ключ, указывающий на сущность покупателя, заказавшего
- **`OpenAt`**: TIMESTAMP WITH TIME ZONE NOTNULL - Время оформления заказа
## 11. Таблица **`ProductReviews`** 
- **`Id`**: UUID PRIMARY KEY - Уникальный идентефикатор
- **`Raiting`**: INTEGER NOTNULL - Оценка
- **`ProductId`**: UUID REFERENCES PRODUCT(Id) - Внешний ключ, указывающий на ссущность продукта
- **`CustomerId`**: UUID REFERENCES CUSTOMER(Id) - Внешний ключ, указывающий на сущность покупателя, заказавшего
- **`CreatedAt`**: TIMESTAMP WITH TIME ZONE NOTNULL - Время создания отзыва
- **`Comment`**: text - Отзыв
