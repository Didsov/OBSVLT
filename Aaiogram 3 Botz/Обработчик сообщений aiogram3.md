Для вызова обратки всех сообщений нужно обернуть желаемый метод в модификатор @dp.message без передачи ему параметров.


### Пример Эхо бота:
```
@dp.message()
async def echo(message: types.Message):
    await message.reply(message.text)
```

