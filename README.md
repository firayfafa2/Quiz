# Quiz
Quiz

# Руководство пользователя:

**1.Начало работы:**

Найти бота в Telegram: @MomentQuizBot.

Отправить команду /start для регистрации.

**2.Прохождение викторины:**

Выбрать тему: /quiz история.

Отвечать на вопросы, нажимая кнопки с вариантами.

После 10 вопросов увидеть результат и поделиться им.

**3.Команды:**

/score — текущий счёт.

/top — таблица лидеров.

/feedback — оставить отзыв.

**4.Частые вопросы:**

Как сменить тему? → Используйте /quiz новая_тема.

Где моя статистика? → Нажмите /stats.




# Документация разработчика для Telegram-бота моментального квиза
Описание проекта
Telegram-бот моментального квиза — это приложение, которое позволяет пользователям участвовать в викторинах через Telegram. Бот предоставляет вопросы, принимает ответы и оценивает результаты. Основная цель — автоматизация взаимодействия с пользователями и упрощение процесса проведения викторин.

Основные компоненты
Язык программирования: Python.

Библиотека для работы с Telegram API: python-telegram-bot (версия 20.x).

Функционал:

Команда /start для приветствия.

Команда /quiz для начала викторины.

Обработка ответов пользователей.

Подсчет результатов.

Установка и настройка
Установите библиотеку python-telegram-bot:

bash
pip install python-telegram-bot
Зарегистрируйте бота через BotFather в Telegram и получите токен.

Создайте файл .env для хранения токена:

text
BOT_TOKEN=your-telegram-bot-token
Пример кода
python
import os
from telegram import Update
from telegram.ext import Application, CommandHandler, MessageHandler, filters

# Загрузка токена из .env файла
BOT_TOKEN = os.getenv("BOT_TOKEN")

# Функция приветствия
async def start(update: Update, context):
    await update.message.reply_text("Добро пожаловать в квиз-бот! Используйте команду /quiz для начала викторины.")

# Функция начала квиза
async def quiz(update: Update, context):
    await update.message.reply_text("Вопрос 1: Какой язык программирования используется для создания этого бота?\n1) Python\n2) Java\n3) C++")

# Обработка ответов пользователя
async def handle_response(update: Update, context):
    user_response = update.message.text.strip()
    if user_response == "1":
        await update.message.reply_text("Верно! Вы ответили правильно.")
    else:
        await update.message.reply_text("Неверно! Попробуйте снова.")

# Основной код приложения
application = Application.builder().token(BOT_TOKEN).build()

application.add_handler(CommandHandler("start", start))
application.add_handler(CommandHandler("quiz", quiz))
application.add_handler(MessageHandler(filters.TEXT & ~filters.COMMAND, handle_response))

if __name__ == "__main__":
    application.run_polling()
Генерация документации
Для генерации документации можно использовать Sphinx. Пример настройки:

Установите Sphinx:

bash
pip install sphinx
Инициализируйте проект документации:

bash
sphinx-quickstart
Настройте конфигурацию conf.py для автоматического извлечения комментариев из исходного кода.

Сгенерируйте документацию:

bash
make html
Пример документации
text
### Telegram Quiz Bot Documentation

#### Overview
This bot allows users to participate in instant quizzes via Telegram.

#### Commands
- `/start`: Welcomes the user and provides initial instructions.
- `/quiz`: Starts the quiz with the first question.

#### Code Structure
- `start()`: Handles the `/start` command.
- `quiz()`: Initiates the quiz and sends the first question.
- `handle_response()`: Processes user responses and provides feedback.

#### Dependencies
- Python 3.x
- python-telegram-bot library (v20.x)
Архив документации
К проекту должен быть приложен архив с HTML-документацией, созданной с помощью Sphinx, для удобства использования и сопровождения разработчиками.
