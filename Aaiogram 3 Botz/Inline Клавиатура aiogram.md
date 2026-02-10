Inline клавиатура добавляет кнопки не под поле ввода, а под сообщение
Для работы с такой клавитурой нужен класс **InlineKeyboardBuilder** и InlineKeyboardButton
Для удобства можно еще импортировать тип **inline_keyboard_button**

```python
from aiogram.utils.keyboard import InlineKeyboardBuilder, InlineKeyboardButton
```



### Добавление inline кнопок
Кнопки добавляются из метода InlineKeyboardButton, который принимает значение text и Обязательные аргументы, которые описывают что делает кнопка
```python
builder = InlineKeyboardBuilder()
builder.row(InlineKeyboardButton(text = "Инлайн 1"))
```

Дополнительные параметры:
- **url** - Переход по URL URL Должен быть в полном формате, c https
- **callback_data** - это Строка, которая отправляется **обратно в бота** при нажатии кнопки.  
Сообщение пользователю не отправляется — бот получает событие `callback_query`.



### CallBack
Для работы с колбеками, нужно имортировать класс **CallbackQuery**
```python
from aiogram.types import CallbackQuery
```


#### Обработка callback
 Для обработки callback-запросов используется декоратор  
`@dp.callback_query`, **вместо** `@dp.message`.

Фильтрация выполняется по значению `callback_data` с помощью `F.data`.

Метод-обработчик принимает аргумент типа `CallbackQuery`,  
через который можно:
- получить данные кнопки
- обратиться к сообщению
- отправить ответ пользователю

#### Пример обработки
``` python
@dp.message(F.text == '/random')
async def random_command(message: types.Message):
    builder = InlineKeyboardBuilder()
    builder.row(InlineKeyboardButton(text="Случайное число", callback_data='random_value'))
    await message.answer('Нажми кнопку', reply_markup=builder.as_markup(resize_keyboard = True))

@dp.callback_query(F.data == "random_value")
async def send_random_value(callback: CallbackQuery):
    await callback.message.answer(str(randint(1, 10)))
    await callback.answer()

```

#### Основные атрибуты `CallbackQuery`

- **callback.data**  
    Содержит строку `callback_data`, переданную кнопкой
- **callback.message**  
    Сообщение, к которому была привязана inline-кнопка
- **callback.from_user**  
    Пользователь, нажавший кнопку

> Рекомендуется **всегда** подтверждать callback-запрос, что бы Телеграм понимал когда обработка окончена

```python 
await callback.answer()
```