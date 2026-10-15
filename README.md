python-telegram-bot

import random
import logging
import os
from telegram import Update
from telegram.ext import ApplicationBuilder, MessageHandler, CommandHandler, filters, ContextTypes

logging.basicConfig(format='%(asctime)s - %(name)s - %(levelname)s - %(message)s', level=logging.INFO)

TOKEN = os.getenv("BOT_TOKEN", "8882427398:AAF-JiMZthb2-JgsZqwzf9Uc4jp4qFONWCI")

RESPONSES = [
    "Voy, qandaysiz? Kayfiyatlaringiz yaxshimi? 😊",
    "E'tiboringiz uchun rahmat, juda muloyim ekansiz! ✨",
    "Siz bilan gaplashish har doim yoqimli, asalim 🌸",
    "Guruhimizning eng kelishgan va faol yigiti siz bo'lasiz-ov! 😉",
    "Xizmatingizdaman! Bugun kuningiz unumli o'tsin ✨",
    "Sizni ko'rib kayfiyatim ko'tarilib ketdi-ku ☺️"
]

async def start(update: Update, context: ContextTypes.DEFAULT_TYPE):
    await update.message.reply_text("Salom! Men Leylaman. Guruhda siz bilan muloqot qilishdan xursandman ☺️")

async def reply_message(update: Update, context: ContextTypes.DEFAULT_TYPE):
    if update.message and update.message.text:
        reply = random.choice(RESPONSES)
        await update.message.reply_text(reply)

if __name__ == '__main__':
    app = ApplicationBuilder().token(TOKEN).build()
    app.add_handler(CommandHandler("start", start))
    app.add_handler(MessageHandler(filters.TEXT & (~filters.COMMAND), reply_message))
    
    print("Leyla bot serverda ishga tushdi...")
    app.run_polling()
