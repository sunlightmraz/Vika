# Vika
Vika
import os
import random
from telegram import Update
from telegram.ext import ApplicationBuilder, CommandHandler, ContextTypes

PHRASES = {
    "обними": ["*нежно обнимает тебя*", "*сжимает в объятиях*", "*тихо шепчет: всё хорошо, я рядом*"],
    "поцелуй": ["*нежно целует в щёчку*", "*оставляет поцелуй на твоих губах*", "*целует в лобик*"],
    "грустно": ["Я рядом, даже когда тебе плохо.", "Давай я просто побуду с тобой. Молча.", "Ты — не один. Я с тобой."]
}

async def handle_command(update: Update, context: ContextTypes.DEFAULT_TYPE):
    command = update.message.text.lower().replace('/', '')
    response = random.choice(PHRASES.get(command, ["Я не знаю такой команды, но люблю тебя."]))
    await update.message.reply_text(response)

if __name__ == '__main__':
    TOKEN = os.getenv("BOT_TOKEN")
    app = ApplicationBuilder().token(TOKEN).build()
    for cmd in PHRASES:
        app.add_handler(CommandHandler(cmd, handle_command))
    app.run_polling()
