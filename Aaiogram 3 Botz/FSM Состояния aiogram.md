Состояния нужны для того что бы хранить память о текущем пользователи, присвоить ему стейты, значения, переменные и тд...

### Библиотеки
Нужно импортировать `StateGroup, State` из `aiogram.fsm.state`
```python
from aiogram.fsm.state import StatesGroup, State
```

### Создание
Для начала требуется создать класс группы состояния, которая будет хранить состояния пользователя для конкретной процедуры ( по сути шаги )
Это делается путем создания класса, наследуемого от `StatesGroup`. Имя класса нужно называть тем для чего используются состояния

```python
from aiogram.fsm.state import StatesGroup, State


class Registration(StatesGroup):
    #
```


После этого в теле объявляются состояния, которые представляют собой экземляры класса State:

``` python 
from aiogram.fsm.state import StatesGroup, State


class Registration(StatesGroup):
    name = State()
    email = State()
```


### Использование
#### Вход в состояние

Для начала в наш хендлер нам нужно импортировать нашу группу состояний и тип `FSMContext`

```python
from aiogram.fsm.context import FSMContext
from states.state import Registration
```


Затем мы отлавливаем команду запуска процесса и вызываем метод, который принимает сообщение и состояние:
```python
@router.message(F.text == 'Регистрация')
async def reg_start(message: Message, state: FSMContext):
    await message.answer("Регистрация началась:\n Укажите имя")
```

И внутри этой функции нам состояние уже нужно "включить", путем передачи в state.set_state поля из нашей группы состояний:

```python
@router.message(F.text == 'Регистрация')
async def reg_start(message: Message, state: FSMContext):
    await message.answer("Регистрация началась:\n Укажите имя")
    await state.set_state(Registration.name)

```


### Отслеживание состояний
Для отслеживание состояний в @router.message нужно передать Состояние из нашей группы, которое мы хотим словить

```python
@router.message(Registration.name)
async def proccess_name(message: Message, state: FSMContext):
    
```


### Запись значений в состояние
Для записи значение в текущее состояние нужно использовать метод update_data у текущего состояния

```python
@router.message(Registration.name)
async def proccess_name(message: Message, state: FSMContext):
    await state.update_data(name = message.text)
    
    await message.answer("Введите почту: ")
    await state.set_state(Registration.email)
    
```

### Чтение значений состояния
Для чтение значений из состояния нужно вызвать метод get_data(), который вернет словарь.
Для взятия данных из словаря нужно вызывать метод get('поле')
```python 
data = await state.get_data()
name = data.get("name") 
```



### Выход состояния
Что бы выйти состояние нужно использовать метод clear()
```python
await state.clear()
```
