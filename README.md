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
![asas](https://github.com/user-attachments/assets/ec5b32ad-e9b6-49bc-b3e2-bc3b26570be0)

## 1. Таблица **`Users`** 
- **`Id`**: uuid Primary key - Уникальный идентефикатор
## 2. Таблица **`Customers`** 
- **`Id`**: uuid Primary key - Уникальный идентефикатор
## 3. Таблица **`Admins`** 
- **`Id`**: uuid Primary key - Уникальный идентефикатор
## 4. Таблица **`Sellers`** 
- **`Id`**: uuid Primary key - Уникальный идентефикатор
## 5. Таблица **`RefreshTokens`** 
- **`Id`**: uuid Primary key - Уникальный идентефикатор
## 6. Таблица **`Products`** 
- **`Id`**: uuid Primary key - Уникальный идентефикатор
## 7. Таблица **`Categories`** 
- **`Id`**: uuid Primary key - Уникальный идентефикатор
## 8. Таблица **`ProductMedias`** 
- **`Id`**: uuid Primary key - Уникальный идентефикатор
## 9. Таблица **`CartItems`** 
- **`Id`**: uuid Primary key - Уникальный идентефикатор
## 10. Таблица **`Orders`** 
- **`Id`**: uuid Primary key - Уникальный идентефикатор
