# Wikipediabot

import asyncio
import wikipedia
from aiogram import Bot, Dispatcher, types
from aiogram.filters import CommandStart

# TOKENingizni shu yerga qo'ying
TOKEN = "7410896864:AAG8gkew8R_VkuoFPkH-ONmvG_PjdGS8100"
wikipedia.set_lang('uz')
# Botni yaratish
bot = Bot(token=TOKEN)



# Dispatcher'ni yaratish (botni argument sifatida bermaymiz)
dp = Dispatcher()

# /start komandasi uchun handler
@dp.message(CommandStart())
async def start_handler(message: types.Message):
    await message.answer(f"Salom, {message.from_user.first_name}! Artur akamni botiga hush kelibsiz.")

# Oddiy echo handler - bot kelgan xabarni qaytaradi
@dp.message()
async def sendWiki(message: types.Message):
    try:
        respond = wikipedia.summary(message.text)
        await message.answer(respond)
    except:
        await message.answer("Bunday maqola yo'q aqlvoy")


# Asosiy botni ishga tushirish funksiyasi
async def main():
    print("✅ Bot ishga tushdi!")
    # Dispatcher'ni bot bilan ulash
    await dp.start_polling(bot)

# Botni ishga tushirish
if __name__ == "__main__":
    asyncio.run(main())
