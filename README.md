# 1. Цель проекта
Цель проекта — разработать систему для расширения аудитории для брендов, стилистов и удобного поиска готового образа внешнего вида (далее Система). Бренд одежды может загружать свою одежду, которая будет использоваться в генераторе образов. Стилист может вручную создавать образы из одежды, которую загрузил бренд. Образы могут быть бесплатными и платными. Пользователь может выбрать предпочтения и сгенерировать бесплатные образы. Для получения платных образов по своим предпочтениям нужно оформить подписку.

# 2. Описание системы
Система состоит из следующих основных функциональных блоков:
1. Регистрация, аутентификация и авторизация
2. Генератор образов
3. Функционал для бренда
4. Функционал для стилиста
5. Функционал для пользователя без подписки
6. Функционал для пользователя с подпиской
7. Функционал оплаты подписки или разового платежа и главной страницы

## 2.1 Типы пользователей
Система предусматривает три типа пользователей системы: бренд, стилист и подписчик. Бренд выкладывает свою одежду, стилист составляет образы их этой одежды, подписчики в соответствии со своим уровнем подписки получают доступ к разрешённым образам из генератора образов.

## 2.2 Регистрация, аутентификация и авторизация
Бренд:
* email — обязательное поле
* пароль — обязательное поле
* название бренда – обязательное поле

Стилист:
* email — обязательное поле
* пароль — обязательное поле
* Имя и фамилия – обязательное поле

Пользователь:
* email — обязательное поле
* пароль — обязательное поле
* Имя и фамилия – обязательное поле

После отправки формы регистрации на email приходит письмо с ссылкой для активации аккаунта. Аутентификация по Json Web Token. При входе вводится email и пароль.

## 2.3 Генератор образов
В этом блоке пользователь выбирает стиль, сезон, размер, цвет одежды, бренд, стилист. Нажимает кнопку «Сгенерировать образы».

После нажатия пользователю показываются образы:
* Случайные
* Бесплатные
* Платные

### 2.3.1 Случайные образы
Такие образы создаются автоматически. Алгоритм из общего набора одежды создаёт образ – набор одежды, который совпадает с предпочтениями пользователя.

### 2.3.2 Бесплатные образы
Такие образы создают стилисты. При создании он помечает образ как бесплатный. Показывается пользователю с подпиской и без.

### 2.3.3 Платные образы
Такие образы создают стилисты. При создании он помечает образ как платный. Показывается пользователю с подпиской и без. Пользователю без подписки показываются размытые изображения, не показывается бренд, цена, где купить.

## 2.4 Функционал для бренда
После аутентификации открывается функционал:
* Редактирование профиля
* Добавление и редактирование карточек одежды
* Аналитика

### 2.4.1 Редактирование профиля
В этом разделе у бренда есть возможность редактирования данных своего профиля — email, названия, соц сети, контакты. Возможные соц сети:
* YouTube
* Instagram
* Facebook
* VK

Должна быть возможность сменить пароль, подтвердив свой старый пароль.
Если дизайн Системы будет подразумевать какие-то изображения для кастомизации страницы Системы, то эти изображения тоже должны редактироваться из профиля автора.

### 2.4.2 Добавление и редактирование карточек одежды
Каждой карточке задаётся:
* Название
* Категория (футболка, штаны, куртка)
* Основной цвет
* Второй цвет (цвет рисунка)
* Стиль одежды
* Сезон
* Доступна размерная сетка (мы не можем гарантировать доступность определенного размера у бренда, поэтому предлагаю выводить размерную сетку товара)

### 2.4.3 Аналитика
??? ??? ???

## 2.5 Функционал для стилиста
После аутентификации открывается функционал:
* Редактирование профиля
* Создание и редактирование образов одежды
* Аналитика

### 2.5.1 Редактирование профиля
В этом разделе у бренда есть возможность редактирования данных своего профиля — email, названия, соц сети. Возможные соц сети:
* YouTube
* Instagram
* Facebook
* VK

Должна быть возможность сменить пароль, подтвердив свой старый пароль.
Если дизайн Системы будет подразумевать какие-то изображения для кастомизации страницы Системы, то эти изображения тоже должны редактироваться из профиля автора.

### 2.5.2 Создание и редактирование образов одежды
Стилист может составить образ из одежды, которую загрузили бренды. Можно выбрать по 1 элементу на 1 категорию, не может быть 2 куртки в одном образе. Можно выбрать вид образа, бесплатный или платный.

Платный доступен только по подписке на стилиста-автора образа.

### 2.5.3 Аналитика
Абсолютное и относительное количество подписчиков. Возможно, в виде диаграммы pie-chart.

## 2.6 Функционал для пользователя без подписки
После аутентификации открывается функционал:
* Редактирование профиля
* Генератор бесплатных образов
* Оформление подписки

### 2.6.1 Редактирование профиля
см. пункт 2.4.1

### 2.6.2 Генератор бесплатных образов
В этом разделе можно выбрать стиль, сезон, размер, цвет одежды, бренд, стилист. Генератор сгенерирует случайные и бесплатные образы, подходящие по предпочтениям.

Бесплатные образы создает стилист. 

### 2.6.3 Оформление подписки
Пользователь может оформить подписку. У подписок есть уровни. От уровня зависит количество стилистов, которых можно выбрать из общего списка.

## 2.7 Функционал для пользователя с подпиской
После аутентификации открывается функционал:
* Редактирование профиля
* Генератор платных образов
* Отключение подписки

### 2.6.1 Редактирование профиля
см. пункт 2.4.1

### 2.6.2 Генератор платных образов
В этом разделе можно выбрать стиль, сезон, размер, цвет одежды, бренд, стилист. Генератор сгенерирует случайные, бесплатные и платные образы, подходящие по предпочтениям.

Бесплатные и платные образы создает стилист.

### 2.6.3 Отключение подписки
В этом разделе можно отключить продление подписки. После отключения подписка будет дейтвовать до конца оплаченного периода.

## 2.7 Функционал оплаты подписки или разового платежа и главной страницы
На главной странице отображается генератор образов. Пользователь любого уровня может пользоваться генератором.

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

После 5 дней неуспешных попыток списать сумму подписка останавливается и подписчик теряет доступ к платным образам.
# 4. Требования к дизайну
Минимализм, лаконичность, акцент на контент. Белый фон. Должен присутствовать логотип Системы где-то на странице. Логотип надо разработать в рамках этого проекта.

# Вопросы и предложения
1. Как организованы подписки на популярные журналы моды
2. Как организовано получение разрешения на публикацию в журнале моды
3. Модерация образов
4. Сохранить образ в библиотеку/корзину
5. Перейти от подписки на разовые платежи за образы стилистов, а для генератора случайных образов оставить подписку или сделать бесплатным. Чем-то похоже на донат-системы Patreon и Boosty. Там можно покупать единичный контент или пост за разовый платеж (см. скриншот)
<img width="456" alt="Screenshot 2022-11-07 at 13 59 10" src="https://user-images.githubusercontent.com/80126370/200294143-86a70f1f-813b-416c-a85f-28aafa99162c.png">
6. Убрать из Системы бренд. Вместо подписки заключать договор с брендом одежды, который обяжет нас размещать образы с их продукцией на сайте и в генераторе.

