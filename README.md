# 1. Цель проекта
Цель проекта — разработать систему для расширения аудитории для Брендов, Стилистов и удобного поиска готового образа внешнего вида (далее Система). Бренд одежды может загружать свою одежду, которая будет использоваться в Генераторе образов. Стилист может создать образ из одежды, которую загрузил Бренд. Пользователь может бесплатно воспользоваться генератором образов и оформить платную подписку на Стилистов.

# 2. Описание Cистемы
Система состоит из следующих основных функциональных блоков:
1. Регистрация, аутентификация и авторизация
2. Генератор образов
3. Функционал для Бренда
4. Функционал для Стилиста
5. Функционал для пользователя без подписки
6. Функционал для пользователя с подпиской
7. Функционал оплаты подписки или разового платежа
8. Функционал главной страницы
9. Функционал для админа

## 2.1 Типы пользователей
Система предусматривает три типа пользователей системы: админ, бренд, стилист и пользователь. Бренд загружает свою одежду, Стилист создаёт образы из этой одежды, пользователь может воспользоваться бесплатным генератором образа или оформить платную подписку на Стилиста.

## 2.2 Регистрация, аутентификация и авторизация
Бренд:
* email — обязательное поле
* Пароль — обязательное поле
* Имя – обязательное поле
* Никнейм

Стилист:
* email — обязательное поле
* Пароль — обязательное поле
* Имя – обязательное поле
* Никнейм

Пользователь:
* email — обязательное поле
* Пароль — обязательное поле
* Имя – обязательное поле
* Никнейм

После отправки формы регистрации на email приходит письмо с ссылкой для активации аккаунта. Аутентификация по Json Web Token. При входе вводится email и пароль.

## 2.3 Генератор образов
К генератору есть доступ у всех типов пользователей.

Чтобы сгенерировать образ нужно:
1. Выбрать из каких частей одежды будет состоять образ.
1. Выбрать характеристик: стиль, сезон, размер, цвет, Бренд, Стилист.
2. Нажать кнопку «Сгенерировать»

После нажатия кнопки «Сгенерировать» сервер ищет в БД все вещи, которые совпадают с пользовательскими характеристикам и с частями одежды образа, передаёт Генератору. Из полученного массива вещей создаются все возможные комбинации образов и показываются пользователю.

Например, пользователь выбрал:
* Части одежды: кофта, штаны, обувь
* Стиль: спортивный
* Сезон: лето
* Размер: L
* Цвет: темно-синий
* Бренд: Indiwd
* Стилист: Ярослав Стахира

В ответ от БД получаем двумерный массив `array[n][m]`, где `n` – часть одежды, а `m` – вещь:

```
[[футболка1, футболка2], //верх
[шорты1, шорты2], //штаны
[кроссовки1]] //обувь
```

Генератор создаёт все возможные комбинации образов из этих вещей.

Получаем образы:

```
[[футболка1, шорты1, кроссовки1], //образ 1
[футболка1, шорты2, кроссовки1], //образ 2
[футболка2, шорты1, кроссовки1], //образ 3
[футболка2, шорты2, кроссовки1]] //образ 4
```
Пример объекта одежды:
```
{
  piece: "Штаны",
  name: "Шорты",
  style: "Спортивный",
  season: "Лето",
  size: [XS, S, M, L],
  color: "темно-синий",
  brand: "Indiwd",
  stylist: "Ярослав Стахира"
}
```

## 2.4 Функционал для Бренда
После аутентификации открывается функционал:
* Настройки аккаунта
* Добавление и редактирование карточек одежды
* Аналитика

### 2.4.1 Редактирование страницы
В этом разделе у бренда есть возможность редактирования данных своего аккаунта: 
* Профиль
* Мои соцсети
* Подписки

#### 2.4.1.1 Профиль
Можно изменить:
* Фотография 225x280, размером не более 10 Mb, PNG/JPG
* Имя
* Email
* Платежная информация. Можно привязать или отвязать банковскую карту
* Пароль

#### 2.4.1.2 Мои соцсети
Есть возможность ввести ссылки на свои социальные сети:
* VK
* Telegram
* Instagram
* Twitter
* Facebook
* Youtube
* TikTok

#### 2.4.1.3 Подписки
Здесь показываются оформленные подписки. Есть возможность отменить ненужную подписку.

### 2.4.2 Добавление и редактирование карточек одежды
Бренд может загружать свою одежду в БД со своей страницы.

Каждой карточке задаётся:
* Фотография
* Часть одежды (верх, низ, обувь, кисти, голова)
* Название
* Стиль
* Сезон
* Размерная сетка
* Цвет
* Бренд
* Стилист

## 2.5 Функционал для Стилиста
После аутентификации открывается функционал:
* Редактирование страницы
* Создание и редактирование образов одежды
* Создание уровней подписок
* Аналитика

### 2.5.1 Редактирование страницы
В этом разделе у стилиста есть возможность редактирования данных своего аккаунта: 
* Профиль
* Мои соцсети
* Подписки

#### 2.5.1.1 Профиль
Можно изменить:
* Фотография 225x280, размером не более 10 Mb, PNG/JPG
* Имя
* Email
* Платежная информация. Можно привязать или отвязать банковскую карту
* Пароль

#### 2.5.1.2 Мои соцсети
Есть возможность ввести ссылки на свои социальные сети:
* VK
* Telegram
* Instagram
* Twitter
* Facebook
* Youtube
* TikTok

#### 2.5.1.3 Подписки
Здесь показываются оформленные подписки. Есть возможность отменить ненужную подписку.

### 2.5.2 Создание и редактирование образов одежды
Стилист может создавать образы у себя на **странице**.

#### 2.5.2.1 Страница Стилиста
Состав:

<img width="400" alt="Screenshot 2022-11-11 at 01 32 58" src="https://user-images.githubusercontent.com/80126370/201220812-a41ec184-50e5-463b-9df9-62c24e779987.png">

* Фото профиля
* Имя
* Соцсети
* Кнопка «Создать образ»: открывает страницу создания образа
* Уровни подписки: созданные уровни подписки. Отображается количество подписчиков с каждым уровнем подписки.
* Кнопка «Добавить подписку»: можно создать уровень (тир/tier) подписки с индивидуальной ценой руб/мес.
  - Поля ввода: название подписки, описание, стоимость.


##### 2.5.2.1.1 Страница создания образа

<img width="400" alt="Screenshot 2022-11-11 at 01 40 07" src="https://user-images.githubusercontent.com/80126370/201222659-0c8e81b0-4168-4163-82e3-124a52e276d6.png">

* Нужно ввести название образа и текст тизера
* Загрузить обложку тизера
* Выбрать, кто может смотреть образ

После нажатия кнопки «Опубликовать» образ появляется на странице Стилиста. Те, кто не имеет доступа, видят только тизер образа.

##### Блок создания образа:

<img width="760" alt="Screenshot 2022-11-11 at 01 59 18" src="https://user-images.githubusercontent.com/80126370/201225649-8f5cdef8-c58e-4aa3-a0c4-4fdd45d20916.png">

Здесь можно выбрать части образа, характеристики одежды. Для каждой части образа нужно выбрать вещь из общего набора, подходящего по характеристикам.

### 2.5.3 Аналитика
* Абсолютное и относительное количество подписчиков. Возможно, в виде диаграммы pie-chart.
* Сколько денег поступило на счёт
* Вывод средств на банковскую карту


## 2.6 Функционал для пользователя
После аутентификации открывается функционал:
* Редактирование профиля
* Оформление подписки на Стилиста

### 2.6.1 Редактирование страницы
В этом разделе у бренда есть возможность редактирования данных своего аккаунта: 
* Профиль
* Мои соцсети
* Подписки

#### 2.6.1.1 Профиль
Можно изменить:
* Фотография 225x280, размером не более 10 Mb, PNG/JPG
* Имя
* Email
* Платежная информация. Можно привязать или отвязать банковскую карту
* Пароль

#### 2.6.1.2 Мои соцсети
Есть возможность ввести ссылки на свои социальные сети:
* VK
* Telegram
* Instagram
* Twitter
* Facebook
* Youtube
* TikTok

#### 2.6.1.3 Подписки
Здесь показываются оформленные подписки. Есть возможность отменить ненужную подписку.

### 2.6.3 Оформление подписки
Пользователь может оформить подписку на Стилиста. На странице Стилиста справа показаны виды подписок на него. При нажатии на одну из них появляется окно оплаты:

<img width="400" alt="Screenshot 2022-11-11 at 02 27 27" src="https://user-images.githubusercontent.com/80126370/201228019-c3311e71-0ec7-4996-8d32-2127919040e0.png">

* Пользователь видит название описание подписки
* Может выбрать подходящий срок подписки
* Стоимость. Она меняется в зависимости от срока.
* Кнопка «Купить подписку»

## 2.7 Функционал для админа
После аутентификации открывается функционал:
* Блокировка и удаление аккаунтов всех пользователей, образов Стилистов, одежды Брендов

# 3. Предлагаемый стек технологий
Back-end:
* Node JS
* Express
* Mongo/PostgreSQL

Front-end:
* React
* Typesript

Интернет-эквайринг:
* Тинькофф
* CloudPayments
* ~Apple Pay~, ~Google Pay~, Sber Pay
* Рекуррентные платежи

Хранение изображений:
* S3 хранилище

## 3.1 Рекуррентные платежи
Рекуррентные платежи должны списываться через 30 дней после предыдущей оплаты. Если снять платёж не удалось — в течение ближайших 5 дней должна осуществляться ежедневная попытка списать сумму. В течение этих 5 дней доступ сохраняется, а подписчик получает после каждой неуспешной попытки письмо на email. После успешного снятия суммы за подписку подписчик также получает письмо на email.

После 5 дней неуспешных попыток списать сумму подписка останавливается и подписчик теряет доступ к платным образам Стилиста.

# 4. Требования к дизайну
Минимализм, лаконичность, акцент на контент Стилистов.

# 5. Вопросы и предложения
1. Модерация образов
2. Сохранить образ из генератора в библиотеку/корзину/любимые

