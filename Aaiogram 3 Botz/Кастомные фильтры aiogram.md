Использование кастомных фильтров наступает когда нужно делать двойные условия, например разделение по ролям

Так фильтр представляет собой класс, наследуемый от Filter. 
Внутри этого класса должен быть метод `__call__`, который принимает self и message: Message
Метод возвращает булевое значение true, если фильтр применяется и false если нет

```python
```python
ADMINS = [12345, 67890]

class AdminProtect(Filter):
    def __init__(self):
        self.admins = ADMINS

    async def __call__(self, message: types.Message):
        return message.from_user.id in self.admins
```
```


