Для быстрого создания больших клавиатур разумнее использовать сборщик, чем [[Кнопки aiogram|ручное создание кнопок]]

### Импорт
```python
from aiogram.utils.keyboard import ReplyKeyboardBuilder
```


### Создание
Для начала нужно объявить экземпляр класса ReplyKeyboardBuilder
После этого с помощью метода add добавить в него кнопки KeyboardButton
Что бы указать сколько кнопок в ряду нужно применить метод adjust
Для вывода клавиатуры в переменную reply_markup применить метод as_markup()




### Пример
```python
@dp.message(Command('keyboard'))
async def keyboard_command(message: types.Message):
    builder = ReplyKeyboardBuilder()
    for i in range(1, 21):
        builder.add(KeyboardButton(text=str(i)))
    builder.adjust(5)
    await message.answer("Выберите число: ", reply_markup=builder.as_markup())
```

Метод as_markup может принимать те же параметры что и ReplyKeyboardMarkup. Через запятую


### Создание рядов
Вместо автоматического разбития рядов, можно указывать кнопки в рядах вручную. 
Для этого следует использовать метод row(), в который мы передаем кнопки:
