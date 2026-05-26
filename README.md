# bot.py
Telegram passport service bot
import telebot
from telebot import types

# Token kee kan haaraa `@ICSPassportBot`
API_TOKEN = '8359606731:AAHHnXcDMJcE8qyQUN-P82zBKsF0BtP2f3Y'
bot = telebot.TeleBot(API_TOKEN)

# 1. Yeroo namni /start jedhu Kuflaa (Buttons) fiduuf
@bot.message_handler(commands=['start'])
def send_welcome(message):
    maqaa = message.from_user.first_name
    
    # Buttons qopheessuu
    markup = types.ReplyKeyboardMarkup(row_width=2, resize_keyboard=True)
    btn1 = types.KeyboardButton("⭐ Paaspoortii Haaraa")
    btn2 = types.KeyboardButton("🔄 Paaspoortii Haaromsuu")
    btn3 = types.KeyboardButton("💰 Kaffaltii fi Beellama")
    btn4 = types.KeyboardButton("📞 Quunnamtii / Gargaarsa")
    markup.add(btn1, btn2, btn3, btn4)
    
    ergaa = (
        f"Akkam jirtu {maqaa}!\n\n"
        "👋 Bagatuma gara Botii **Tajaajila Paaspoortii Biyyoolessaa Ethiopian** nagaan dhuftan.\n\n"
        "Maaloo odeeffannoo barbaaddan argachuuf kuflaa (buttons) gadii keessaa tokko tuqaa:"
    )
    bot.send_message(message.chat.id, ergaa, reply_markup=markup, parse_mode="Markdown")

# 2. Button cuqaasame dubbisuu fi deebii sirrii deebisuu
@bot.message_handler(func=lambda message: True)
def handle_passport_services(message):
    text = message.text
    
    # --- 1. Paaspoortii Haaraa ---
    if text == "⭐ Paaspoortii Haaraa":
        deebii = (
            "📋 **Ulaagaalee Paaspoortii Haaraa Baafachuuf Barbaachisan:**\n\n"
            "1️⃣ **Waraqaa Eenyummaa (ID):** Waraqaa eenyummaa gandaa kan haaromfame (Orijinaala fi Kooppii).\n"
            "2️⃣ **Waraqaa Dhalootaa:** Waraqaa ragaa dhalootaa seeraa ta'e (Birth Certificate).\n"
            "3️⃣ **Suuraa:** Suuraa guutuu yeroo dhiyoo ka'ame (Passport size).\n"
            "4️⃣ **Galmee:** Galmeen guutummaatti toora interneetii (Online) kanaan raawwatama."
        )
        bot.reply_to(message, deebii, parse_mode="Markdown")
        
    # --- 2. Paaspoortii Haaromsuu ---
    elif text == "🔄 Paaspoortii Haaromsuu":
        deebii = (
            "🔄 **Paaspoortii Haaromsuu ykn Jijjiiruuf:**\n\n"
            "🔹 **Paaspoortii Duraanii:** Paaspoortii kee isa moofaa (Orijinaala fi kooppii fuula suuraa jiru).\n"
            "🔹 **Waraqaa Eenyummaa:** ID gandaa kan haaromfame.\n"
            "🔹 **Yoo bade:** Ragaa poolisii irraa paaspoortiin sun akka bade ibsu (Loss Report) fiduu barbaachisa."
        )
        bot.reply_to(message, deebii, parse_mode="Markdown")
        
    # --- 3. Kaffaltii fi Beellama ---
    elif text == "💰 Kaffaltii fi Beellama":
        deebii = (
            "💰 **Kaffaltii fi Beellama (Appointment):**\n\n"
            "📌 **Akkaataa Galmee:** Galmeen toora interneetii (Online) kanaan kan dhiyaatu yoo ta'u, kaffaltiin bankiidhaan (Telebirr ykn CBE Birr) raawwatama.\n"
            "📌 **Beellama:** Kaffaltii erga xumurtanii booda guyyaa fi sa'aatii biiroo paaspoortii dhaqxanii suuraa fi guuttata qubaa itti kennitan isiniif kenna."
        )
        bot.reply_to(message, deebii, parse_mode="Markdown")
        
    # --- 4. Quunnamtii ---
    elif text == "📞 Quunnamtii / Gargaarsa":
        deebii = (
            "📞 **Gargaarsa Dabalataaf:**\n\n"
            "Odeeffannoo dabalataa ykn gaaffii yoo qabaattan, qopheessaa bot kanaa quunnamuu dandeessu.\n"
            "👤 **Admin:** @abdurezack_aliyi\n"
            "🤖 **Username:** @ICSPassportBot"
        )
        bot.reply_to(message, deebii, parse_mode="Markdown")
        
    # --- Ergaa dabalataa namni barreesseef ---
    else:
        bot.reply_to(message, "Maaloo kuflaa (buttons) skiriinii keessan gadii jiran fayyadamaa odeeffannoo argachuuf!")

print("Botii '@ICSPassportBot' guutummaatti hojii jalqabeera...")
bot.polling()
