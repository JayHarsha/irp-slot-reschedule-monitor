# Prerequisites
Before running the script, make sure you have:
-Python 3.8+
-Google Chrome
-ChromeDriver compatible with your Chrome version
-Telegram account (for bot setup)
-Pip packages: 
      pip install selenium python-telegram-bot

# Setup Guide 
Enable Chrome Debugging Mode:
You need to launch Chrome in remote debugging mode so Selenium can attach to your already logged-in session.
-Close all existing Chrome windows.
-Run this command in Command Prompt / Terminal:
      "C:\Program Files\Google\Chrome\Application\chrome.exe" --remote-debugging-port=9222 --user-data-dir="C:\selenium\ChromeProfile
-This will open a new Chrome window.
-Use this window only for IRP monitoring.
-Log into the IRP Website in this window with your creds
-Open the Reschedule Appointment page.
-Keep this tab open. Don’t close it.

# Create a Telegram Bot
-Open Telegram and search for @BotFather.
-Start a chat and send /newbot.
-Follow the instructions to name your bot and get a bot token (something like 123456789:ABCxyz...).
-Search for your bot like @YOUR_BOT_NAME on Telegram.
-Send a Hi or /Start to interact and wait for the bot to respond back
-Now hit the URL -> https://api.telegram.org/bot{Enter_Your_Bot_Token_Here(Remove_curly_braces)}/getUpdates
-Now you will see some JSON response which contains your chat_id like below, if not try making the telegram bot respond first
        "chat": {
          "id": ---------,
          "first_name": "---------",
          "type": "private"
        },
-Note down your Telegram chat ID and hit below URL
      https://api.telegram.org/bot{Enter_Your_Bot_Token_Here}/sendMessage?chat_id={Enter_Your_Chat_Id_Here}&text=Hello_from_IRP_Bot
-Now you should see something like below 
      {"ok":true,"result":{...}}
- This ensures your bot is working

# Code changes:
- Replace the below fields with the respective values you have recevied
      TELEGRAM_TOKEN = ""  # Your Telegram bot_token
      CHAT_ID = "" # Your chat_id

Now Run the script by inserting the intervals you need the reload for at the end in the below snippet
      schedule_window(dtime(16, 0), dtime(23, 55), interval=30) -> Reloads every 30 mins between 4:00PM and 11:55PM
The script will Clicks continue and checks 4 continous calendars and sends a notification in the Telegram via the BOT if there are any available slots.
      
