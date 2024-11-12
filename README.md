# Переход с монолита на микрофронтенды

## Работа 1

## Что есть в проекте

## Компоненты монолитного фронта

- AddPlacePopup - компонент ответственный за добавление новой картинки.
- App - компонент точка входа.
- Card - компонент карточки со снимком.
- EditAvatarPopup - компонент отвечающий за изменение аватарки.
- EditProfilePopup - компонент описывающий меню в котором можно редактировать профиль.
- Footer - компонент описывающий раздел, который размещается внизу страницы сайта.
- Header - компонент описывающий раздел, который размещается вверху страницы сайта.
- ImagePopup - компонент которые показывает загруженную картинку в открытом состоянии.
- InfoTooltip. - компонент показывающий разную информацию. Например уведомляющий о успешной регистрации или ошибках при регистрации или о успешном входе.
- Login - компонент для отрисовки окна входа.
- Main - компонент который рисует профиль и набор картинок.
- PopupWithForm - содержит шаблон для popup компонентов AddPlacePopup, EditAvatarPopup, EditProfilePopup.
- ProtectedRoute - компонент для защиты маршрутов, если пользователь не авторизован.
- Register - компонент для отрисовки окна регистрации.

## Потенциальные микрофронт

### Основной микрофронт (host)

Точка входа в приложение.
Служит агрегатором для всех остальных микрофронтов.
Содержит следующие компоненты:

- Footer
- Header
- Main
- ProtectedRoute

### Микрофронт аутентификация и регистрации (authentication)

Микрофронт ответственный за регистрацию и вход пользователя.
Позволит не подгружать другие микрофронты, пока пользователь не авторизуется.
Содержит следующие компоненты:

- InfoTooltip
- Login
- Register

### Микрофронт пользователя (user-profile)

Микрофронт ответственный за работу с профилем пользователя.
Содержит следующие компоненты:

- EditAvatarPopup
- EditProfilePopup
- PopupWithForm - продублировал этот компонент в данный микрофронт, так как так будет меньше связанности между микрофронтами.
- Profile - новый компонент вырезанный из компонента Main. Отвечает за отображения профиля пользователя.

### Микрофронт галереи (gallery)

Микрофронт ответственный за работку с галерей. Содержит все необходимое для работы с нею.
Содержит следующие компоненты:

- AddPlacePopup
- Card
- ImagePopup
- Places - новый компонент вырезанный из компонента Main. Отвечает за представление галерии.
- PopupWithForm - продублировал этот компонент в данный микрофронт, так как так будет меньше связанности между микрофронтами.

## Инструмент для создания микрофронтендов

В качестве фреймворка был выбран Webpack Module Federation.
Он поддерживает возможность использовать общие зависимости и ленивую загрузку.
Также на него есть не мало гайдов, которые позволили в нем разобраться.

_В том числе лабораторная работа перед практикой 1._

## Метод интеграции

Как я понимаю WMF автоматически делает интеграцию микрофронтов runtime.

## Метод композиции

В данной работе используется клиентская композиция.
Так как все компоненты подгружаются через lazy, а для отрисовки используется suspend.

## Межмодульное взаимодействие

Микрофронты общаются через dispatchEvent, то есть по сути реализован механизм общения pub/sub.
Такой подход позволяет использовать разные фреймворки в микрофронтах, в отличии от UserContext.
Я отказался от использования UserContext специально, так как предполагал, что в будущем микрофронты могут быть переписаны на другие фреймворки.

## Примечания к работе

Как я понял тут при работе с бэком используется статический токен.
Можно было отказаться и переписать работу api через jwt однако это выходит за рамки задания.

Проект можно запустить, надо прописать в каждом микрофронте `npm install && npm start`

## Работа 2

[Ссылка на работу](./arch_template_task2.drawio)