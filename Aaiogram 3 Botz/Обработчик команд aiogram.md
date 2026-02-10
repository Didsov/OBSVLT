Для обработки команд используется метод обололчки 
	**dp.message(Command('*command_Name*'))**

Пример использования:
	```
	@dp.message(Command('start'))
	async def start_command(message: types.Message):
	    await message.answer('Старт 2218')
	```

### Смена символа вызова
По умолчанию символ вызова - **/**. 
То есть Command('start') вызывается при сообщении /start
Для смены префикса нужно передать в атрибут значение префикса:
	@dp.message(Command('start', **prefix = "!"**))

При передачи нескольких символов префиксом будет считаться любой из них


### Передача аргументов
Для использования переданных аргументов нужно добавить параметр у вызываемой обработчиком функции. 
Переданные аргументы будут в .arg
Для того что бы были видны значения в IDE нужно имортировать типы путем
	from aiogram.filters.command import **CommandObject**

Пример использования:
```
@dp.message(Command('reply'))
async def echo(message: types.Message, command: CommandObject):
    await message.reply(command.args)
```


