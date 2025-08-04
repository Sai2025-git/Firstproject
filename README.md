# ----------- Basic imports and downloads-----------
''' we have to first download the chromedrive(34 bit) to activate the path between the code and the website
Then we have to install selerium to make our system adopt the code and present it as requested''' 
import time
from datetime import datetime
from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.chrome.options import Options

# ----------- USER SETTINGS -----------
alarm_time = "14:03"
chrome_driver_path = "C:/Users/hp/Downloads/my first project/python_combo/chromedriver.exe"
# -------------------------------------

# Configure Chrome options
options = Options()
options.add_argument("--mute-audio")  # Allows autoplay
options.add_argument("--start-maximized")
options.add_argument("--autoplay-policy=no-user-gesture-required")

print(f"Alarm is set for {alarm_time}... Waiting...")

# Wait for alarm time
while True:
    if datetime.now().strftime("%H:%M") == alarm_time:
        print("Alarm time reached! Launching YouTube Shorts...")
        break
    time.sleep(10)

# Launch browser
service = Service(chrome_driver_path)
driver = webdriver.Chrome(service=service, options=options)
driver.get("https://www.youtube.com/shorts")

# Wait for the page and video to load
time.sleep(8)

# Try autoplay via JavaScript
for i in range(5):
    try:
        driver.execute_script("""
            const video = document.querySelector('video');
            if (video) {
                video.muted = false;
                video.play();
                console.log("Video found and played.");
            } else {
                console.log("No video found.");
            }
        """)
        print(f"Attempt {i+1}: Tried to autoplay.")
        time.sleep(2)
    except Exception as e:
        print("Error during autoplay attempt:", e)

# Keep the browser open for 5 minutes
time.sleep(300)
driver.quit()
