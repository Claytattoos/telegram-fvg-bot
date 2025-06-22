# telegram-fvg-bot
Telegram bot for Tradingview FVG alerts 
import telegram
from flask import Flask, request

app = Flask(__name__)

BOT_TOKEN = "7328314506:AAGVxYGj9B4rTcxiHN8gHAK40HS8qunfifU"
CHAT_ID = "6340451644"

bot = telegram.Bot(token=BOT_TOKEN)

@app.route('/alert', methods=['POST'])
def alert():
    data = request.json
    message = data.get('message', 'No message received')

    try:
        bot.send_message(chat_id=CHAT_ID, text=f"📢 TradingView Alert: {message}")
        return 'Alert sent', 200
    except Exception as e:
        return f'Error: {str(e)}', 500

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
    Flask==2.3.3
python-telegram-bot==13.15
