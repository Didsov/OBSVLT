Разметка может быть в формате HTML и markDownV2

Для использования разметки нужно импортировать:
```python
from aiogram.enums import ParseMode
from aiogram import F
```

Что бы примнить разметку нужно в методе ответа добавить атрибут parse_mode и дать ему значение разметки.
Значения разметки:
- HTML: parse_mode=ParseMode.HTML
- MDv2: parse_mode=ParseMode.MARKDOWN_V2


Пример использования:
```python
@dp.message(F.text, Command('text'))
async def text_command(message: types.Message):
    await message.reply(("<h1>HTML разметка<\h1>\n"
                        "<i>курсив</i>"
                        "<b>жирный</b>"), parse_mode=ParseMode.HTML
                        )
    await message.reply("||Спойлер||\n~Зачеркнутый~", parse_mode=ParseMode.MARKDOWN_V2)

```

### MarkDownV2
- *Жирный*
	`*текст*`
- _Курсив_
	`_текст_`
- __Подчёркнутый__
	`__текст__`
-  ~Зачёркнутый~
	`~текст~`
- ||Спойлер||
	`||текст||`
- __Комбинирование__
	`*_жирный курсив_*`
	`*__жирный подчёркнутый__*`

- __Однострочный Код__ ( копируется по клику)
	``` ` adasd ` ``` 
- **Многострочный код**
`
	` ``` ` Многострочный текст, который скопируется, еще можно указать в начале язык программирования ` ``` ` 
- **Ссылка**  
	`[текст](https://example.com)`
- **Упоминание**  
	`[имя](tg://user?id=123456789)`