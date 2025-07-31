# Firstproject
import datetime
import time

# Step 1: Define your alarm time
alarm_time = "07:00"

# Step 2: Loop until the time matches
while True:
    now = datetime.datetime.now().strftime("%H:%M")
    print("Current time:", now)
    if now == alarm_time:
        print("⏰ Alarm triggered!")
        break
    time.sleep(30)
