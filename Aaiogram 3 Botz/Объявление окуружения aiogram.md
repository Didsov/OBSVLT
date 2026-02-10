### Библиотеки
```
import asyncio
from aiogram import Bot, Dispatcher, types
from aiogram.filters.command import Command
from api_token import TOKEN
```

- api_token - файл apy_token.py, созданный вручную и хранящий переменную токен


### Объявление переменных
```
bot = Bot(TOKEN)
dp = Dispatcher()
```


### Запуск и настройка
- **dp.start_polling(bot)** - старт опроса бота. По сути непрерывный цикл 
- **bot.delete_webhook(drop_pending_update = True)** - отключение обработки кучи команд, которые были вызваны до запуска бота. То есть запрещает выполнять команды, которые были отправлены боту до его запуска
- 

### Нулевой  стартовый шаблон
```
import asyncio
from aiogram import Bot, Dispatcher, types
from aiogram.filters.command import Command
from api_token import TOKEN


bot = Bot(TOKEN)
dp = Dispatcher()


@dp.message(Command('start'))
async def start_command(message: types.Message):
    await message.answer('Старт 2218')


async def main():
	await bot.delete_webhook(drop_pending_updates=True)
    await dp.start_polling(bot)


if __name__ == '__main__':
    asyncio.run(main())



```

