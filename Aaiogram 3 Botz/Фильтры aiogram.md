### Импорт
Все фильтры импортируются из 
```python
from aiogram.filters import CommandStart, Command
```

Или из aiogram в случае магического фильтра F
```python
from aiogrom import F
```

### F фильтр
F фильтр это универсальный фильтр, который может фильтровать множество типов данных
Среди них:
- F.text - Получает текст сообщения
	- Получение данных: message.text
- F.data - полученный callback из Inline кнопки
- F.data.startswith('smth_')
	- Получение данных: callback.message.data / text
- F.photo - Получает фото из сообщения
	- Получение данных: message.photo[-1].file_id
- F.Video - Получение видео
	- Получение данных: message.video.file_id
- F.auido
- F.voice
- F.document
- F.stiker
	- Для всего этого аналогично
- from_user.id - Фильтр по пользователю
- 

