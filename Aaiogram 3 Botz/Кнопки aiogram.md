Для использование Кнопок понадобтся  методы KeyboardButton и ReplyKeyboardMarkup из aiogram.types
```python 
from aiogram.types import KeyboardButton, ReplyKeyboardMarkup
```


### Создание списка кнопок
Для кнопок удобно создавать двойные массивы, где каждый подмассив это кнопка
```python
kb = [
        [KeyboardButton(text='Кнопка request_chat', request_chat=True)],
        [KeyboardButton(text='Кнопка request_location', request_location=True)],
        [KeyboardButton(text='Кнопка request_contact', request_contact=True)],
        [KeyboardButton(text='Кнопка request_poll', request_poll=True)],
        [KeyboardButton(text='Кнопка request_user', request_user=True)],
        [KeyboardButton(text='Просто Кнопка')]
    ]
```

Метод KeyboardButton принимает текст кнопки и в качестве до параметра позволяет принять реквест, который отправляет из телеграма системный диалог.

- request_chat: Открывает список чатов (Для групп)
- request_location: Запрос геолокации пользователя
- request_contact: Запрос номера телефона
- request_poll: Запрос создания опроса (Для групп)
- request_user: Запрос выбора пользователя ( для групп )
### Создание клавиатуры
После того как мы обозначили какие кнопкки будут в клавитуре их нужно добавить в ReplyKeyboardMarkup, для этого создадим переменную клавиатуры:
``` python
    keyboard = ReplyKeyboardMarkup(keyboard=kb)
```
`ReplyKeyboardMarkup` может принимать дополнительные параметры:
- **resize_keyboard**  
    Если `True`, клавиатура автоматически подстраивается под размер кнопок  
    (становится компактнее и удобнее для пользователя).
- **is_persistent**  
    Если `True`, клавиатура остаётся открытой после нажатия кнопки  
    (по умолчанию клавиатура может скрываться).
- **one_time_keyboard**  
    Если `True`, клавиатура скрывается сразу после нажатия любой кнопки  
    (удобно для одноразовых действий, например подтверждения).
- **selective**  
    Если `True`, клавиатура будет показана только определённым пользователям  
    (используется редко, в основном для ответов в группах).
- **input_field_placeholder**  
    Принимает строковое значение, которое отображается как подсказка  
    в поле ввода сообщения, пока пользователь ничего не ввёл

### Вывод клавиатуры
Созданную переменную keyboard нужно прикрепить к ответу
Для этого в метода ответа в атрибут reply_markup нужно добавить нашу созданную клавиатуру
```python
    await message.answer('Старт', reply_markup=keyboard)
```


### Пример вывода
```python
@dp.message(Command('start'))
async def start_command(message: types.Message):
    kb = [
        [KeyboardButton(text='Кнопка request_location', request_location=True)],
        [KeyboardButton(text='Кнопка request_contact', request_contact=True)],
        [KeyboardButton(text='Просто кнопка')]
    ]
    keyboard = ReplyKeyboardMarkup(keyboard=kb, resize_keyboard=True, input_field_placeholder="Выберите действие")
    await message.answer('Старт', reply_markup=keyboard)
```


### Обработка нажатия
Для того что бы бот реагировал на нажатие кнопок, нужно добавить хендлер, который ищет кнопки
Для этого создадим обработку конкретно под текст каждой кнопки

```python
@dp.message(F.text.lower() == 'просто кнопка')
async def just_button(message: types.Message):
    await message.answer("Была нажата просто кнопка")
```

Здесь F это фильтр, который который вызывает хендлер, только если он текст и текст в нижнем регистре совпадает с условием
