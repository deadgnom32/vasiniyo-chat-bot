# vasiniyo-chat-bot

`vasiniyo-chat-bot` - телеграм бот, написанный на `pyTelegramBotAPI`

## TL;DR
В коренной директории находится файл run.sh, который собирает и запускает контейнер.
Также там лежит файл `.env`, в который нужно определить обязательные переменные окружения:

- `BOT_API_TOKEN` - токен телеграм бота
- `ACCESS_ID_GROUP` - id группы, в который будет работать бот.

   Чтобы указать несколько разрешенных чатов, нужно перечислить их в таком виде: `ACCESS_ID_GROUP=-123;-456`<br>
   Чтобы разрешить бота во всех чатах: `ACCESS_ID_GROUP=*`, `ACCESS_ID_GROUP=`,
   либо не устанавливаете переменную окружения<br>
   Чтобы запретить бота во всех чатах: `ACCESS_ID_GROUP=;`
## Установка
Установите Docker для своей системы: https://docs.docker.com/get-started/get-docker/<br>
Получите последний образ:

```bash
    docker pull ghcr.io/vasiniyo/vasiniyo-bot:latest
```

Также вы можете собрать образ из исходников:<br>
Скачайте репозиторий<br>
Сделать это можно, например, вот так:
```bash
  git clone git@github.com:Vasiniyo/vasiniyo-chat-bot.git
```
```bash
  git clone https://github.com/Vasiniyo/vasiniyo-chat-bot.git
```
Перейдите в директорию с ботом и пропишите команду
```bash
  docker build -t "vasiniyo-bot" --no-cache .
```
После этого создастся образ с именем `vasiniyo-bot`, который можно будет использовать, чтобы поднять контейнер


## Использование
Для использования бота необходимо получить токен (`BOT_API_TOKEN`)<br>
Для его получения можно перейти в следующего бота: https://t.me/BotFather<br>
`/start`<br>
`/newbot`<br>
`Вводим имя вашего бота`<br>
`/setinline`<br>
`@Имя бота`<br>
`выбери нужную команду!`

После этого создастся бот, и вам напишут его токен, который нужно скопировать в переменную окружения `BOT_API_TOKEN`<br>
Чтобы бот мог правильно работать в чате, ему необходимо выдать права администратора.

Чтобы узнать ID комнаты, в котором вы хотите пользоваться ботом, можно воспользоваться следующим ботом: https://t.me/FIND_MY_ID_BOT<br>
Пригласите его в чат и напишите команду `/id@FIND_MY_ID_BOT`<br>
Вставьте этот ID в переменную окружения `ACCESS_ID_GROUP`

Далее нужно создать директорию для базы данных с лайками, которую потом нужно примонтировать к контейнеру.
Допустим, вы хотите, чтобы volume хранился по следующему пути: `/data/my-bot-data`, тогда поднять контейнер можно будет при помощи следующей команды:

```bash
    docker run --env BOT_API_TOKEN="YOUR_API_TOKEN"\
               --env ACCESS_ID_GROUP="YOUR_ACCESS_ID"\
               -v /data/my-bot-data:/data\
               ghcr.io/vasiniyo/vasiniyo-bot:latest
```
Либо просто запустите run.sh в коренной директории, чтобы выполнить сборку образа и поднять контейнер автоматически.
По умолчанию имя контейнера будет `vasiniyo-bot`, а директория с данными создаётся в корне с именем `data`
```bash
    ./run.sh
```

Пример конфигурации находится в файле `config.toml`<br>
Туда можно добавлять свои ответы на сообщения или удалять существующие

Вы прекрасны, бот успешно работает


## Содействие

Вы можете внести свой вклад в бота. Для этого можете открыть имеющиеся `issues`,
либо придумывать свои и отправлять`Pull Request`с соответствующими изменениями.
Обязательно создавайте новый issue, если вы обнаружили баг, либо у вас есть крутые идеи
