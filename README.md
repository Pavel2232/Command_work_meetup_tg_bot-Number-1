#  Коммандный проект meetup_bot
Командный проект по реализации телеграм-ботов выполняющие полный спектр
необходимых для автоматизации проведения meetup-мероприятия


# Задачи бота
Пользователь:
Пришёл на мероприятие, увидел рекламу бота → хочу узнать что это такое, любопытно → бот кратко описал свой функционал
Слушаю доклад → хочу задать докладчику вопрос → смог найти нужного докладчика и написать ему
Дослушал доклад, начался новый доклад → хочу задать вопрос докладчику → вопрос ушёл докладчику, который выступает сейчас, а не тому, который уже выступил
Докладчик немного задержался и выступает дольше, чем должен был → хочу задать ему вопрос → вопрос ушёл этому докладчику, а не следующему
Слушаю доклад → захотелось узнать, какой доклад будет дальше → получил программу мероприятия
Пришёл на мероприятие → хочу пообщаться с другими разрабами, но стесняюсь подойти сам → бот предложил познакомить меня с кем-нибудь
Бот предложил познакомить меня с кем-нибудь → хочу узнать, как он это сделает. страшно, что будет неловко → бот кратко описал как всё работает
Бот предложил познакомиться с другими разрабами → хочу познакомиться → бот выдал анкету, чтобы опросить кто я такой
Заполнил анкету о себе → хочу уже знакомиться → бот предложил анкету другого человека и его контакт в тг.
Заполнил анкету о себе самым первым → хочу познакомиться с кем-нибудь → бот предупреждает, что остальные пока не заполнили анкеты. когда кто-нибудь заполнил анкету – бот напомнил мне о себе
Заполнил анкету, пообщался → хочу задать вопрос заказчику → могу вернуться, задать вопрос, а затем продолжить поиск собеседника
Бот предложил мне анкету другого разраба → не хочу общаться с этим человеком → бот даёт мне возможность “отступить” и написать другому
Увидел предложение задонатить организатору → не хочу → бот не настаивает
Увидел предложение задонатить организатору → хочу поддержать → бот принял платёж

Докладчик:
Выступаю с докладом → хочу ответить на вопросы → открыл приложение, вижу контакты
Выступил с докладом → хочу послушать другие доклады и пообщаться, как и другие → могу пользоваться приложением как остальные пользователи

Организатор:
Организую выступления докладчиков → хочу внести в бота докладчиков, которые будут выступать → внёс список людей, которые будут выступать. они видят, что они теперь помечены как докладчики
Организую мероприятие → хочу поменять программу дня → поменял
Поменял программу выступления → хочу оповестить других пользователей, что она поменялась → оповестил
Что-либо случилось → хочу всем массово сообщить о чём-то → могу организовать рассылку
Прошло мероприятие → хочу провести ещё одно → могу воспользоваться ботом ещё раз
Идёт мероприятие → хочу узнать, кто донатил → получил список поддержавших и суммы, которые они пожертвовали


## Требования к использованию

Требуется [Python](https://www.python.org/downloads/) версии 3.7 или выше и установленный [pip](https://pip.pypa.io/en/stable/getting-started/). Для установки необходимых зависимостей используйте команду:  
1.
```commandline
poetry init
```

## Установка

1. Выполнить миграцию: `python3 manage.py migrate`
2. Создать файл `.env`, заполнить его по образцу:
```comandline
TELEGRAM_SPEECHERS_BOT_API_TOKEN=ваш токен бота для спикера
TG_USER_BOT_TOKEN=ваш токен бота для пользователей
TG_ORGANIZER_BOT_TOKEN=ваш токен бота для организатора
ID_CHAT_CHANEL=id телеграмм канала #-тут13цифр
SECRET_KEY=ThisIsSoMuchSecretKey
DEBUG=True
ALLOWED_HOSTS=localhost,127.0.0.1
DATABASE=sqlite:///db.sqlite3
PAYMENT_TOKEN=токен для оплаты в тг боте(выдаёт при подключении оплаты BOT_FATHER)
```

3. Переместить скрипт со своим ботом в главную директорию.
4. Добавить в него следующее (в начало, до импорта моделей):
```python
os.environ['DJANGO_SETTINGS_MODULE'] = 'storage.settings'
django.setup()

from db.models import User, Donation, Event

```
    тут основной код

5. Вызывать его простой командой `python3 bot_organizer.py`.
