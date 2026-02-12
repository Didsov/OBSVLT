
### Виртуальное окружение
Виртуальное окружение нужно что бы библиотеки устанавливались конкретно в проект, а не в общую систему
Это позволяет в разных проектах использовать разные версии одной и той же библиотеки

#### Установка виртуального окружения
1. Нужно создать виртуальное окружение в которое нужно установить библиотеки
   `python -m venv .venv`
2. Нужно зайти в окружение
	` .venv\Scripts\activate`
3. Нужно установить библиотеки через pip, пока мы в venv
4. Запускать тоже надо из окружения
5. 
#### Библиотеки
```
import asyncio
from aiogram import Bot, Dispatcher, types
from aiogram.filters.command import Command
from api_token import TOKEN
```

- api_token - файл apy_token.py, созданный вручную и хранящий переменную токен


#### Объявление переменных
```
bot = Bot(TOKEN)
dp = Dispatcher()
```


#### Запуск и настройка
- **dp.start_polling(bot)** - старт опроса бота. По сути непрерывный цикл 
- **bot.delete_webhook(drop_pending_update = True)** - отключение обработки кучи команд, которые были вызваны до запуска бота. То есть запрещает выполнять команды, которые были отправлены боту до его запуска
- 

#### Нулевой  стартовый шаблон
``` python
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

