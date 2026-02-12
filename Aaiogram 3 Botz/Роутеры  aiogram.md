Роутеры нужны что бы разбивать хендлеры ( Обработчики сообщений ) по разным файлам и делать приложение модульным

### Создание роутера
Для создание роутера нужно создать новый python файл и импортировать туда роутер
```python 
from aiogram import Router
```

Затем мы создаем экземляр роутера:
```python
router = Router()
```

И к этому экземляру уже вешаем наши обработчики 

```python
@router.message(F.text == 'Регистрация')
async def reg_start(message: Message, state: FSMContext):
    await message.answer("Регистрация началась:\n Укажите имя", reply_markup=cancel_kb())
    await state.set_state(Registration.name)
```


### Использование роутера

Что бы использовать роутер в наш main файл мы должны импортировать созданный экземпляр роутера

```
from handlers import handle_start
```

После импорта роутер нужно подключить к диспетчеру:
```python
    dp.include_router(handle_start.router)
```


