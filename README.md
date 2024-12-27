# heamac-baby-swing-motion-detection

Here’s a step-by-step guide to create a complete project for your motion detection system on a Raspberry Pi. The project will include organized folders, Python scripts, and configurations for deployment. Follow these steps to set it up and execute:

---
### Components
All components [Listed Here](./components.md)
### **Step 1: Setup Project Folder Structure**

Create a folder structure on your Raspberry Pi to organize your project files:
```bash
mkdir baby_motion_motor
cd baby_motion_motor
mkdir src config logs
touch src/motion_detector.py src/motor_control.py config/settings.py run.py
```

The folder structure will look like this:
```
baby_motion_motor/
├── src/
│   ├── motion_detector.py  # Motion detection logic
│   ├── motor_control.py    # Motor control logic
├── config/
│   ├── settings.py         # Configuration file
├── logs/                   # Logs for debugging
├── run.py                  # Main script to run the project
```

---

### **Step 2: Install Dependencies**

Install the required software and libraries on your Raspberry Pi:
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install python3 python3-pip python3-opencv -y
pip3 install RPi.GPIO
```

---

### **Step 3: Configure Settings**

Edit the `config/settings.py` file to store project configurations:
```python
# config/settings.py

# GPIO Pins
MOTOR_PIN = 17  # GPIO pin connected to the motor driver
CAMERA_INDEX = 0  # Camera index for OpenCV (0 for the default camera)

# Motion Detection Parameters
MOTION_SENSITIVITY = 5000  # Minimum contour area to detect motion

# Motor Control Parameters
MOTOR_RUN_TIME = 2  # Time (in seconds) for which the motor will run
```

---

### **Step 4: Write the Motor Control Script**

Edit the `src/motor_control.py` file for motor control logic:
```python
# src/motor_control.py

import RPi.GPIO as GPIO
import time
from config.settings import MOTOR_PIN, MOTOR_RUN_TIME

def setup_motor():
    GPIO.setmode(GPIO.BCM)
    GPIO.setup(MOTOR_PIN, GPIO.OUT)

def activate_motor():
    print("Motor activated")
    GPIO.output(MOTOR_PIN, GPIO.HIGH)
    time.sleep(MOTOR_RUN_TIME)
    GPIO.output(MOTOR_PIN, GPIO.LOW)

def cleanup_motor():
    GPIO.cleanup()
```

---

### **Step 5: Write the Motion Detection Script**

Edit the `src/motion_detector.py` file for motion detection logic:
```python
# src/motion_detector.py

import cv2
from src.motor_control import activate_motor
from config.settings import CAMERA_INDEX, MOTION_SENSITIVITY

def detect_motion():
    cap = cv2.VideoCapture(CAMERA_INDEX)
    ret, frame1 = cap.read()
    ret, frame2 = cap.read()

    try:
        while True:
            diff = cv2.absdiff(frame1, frame2)
            gray = cv2.cvtColor(diff, cv2.COLOR_BGR2GRAY)
            blur = cv2.GaussianBlur(gray, (5, 5), 0)
            _, thresh = cv2.threshold(blur, 20, 255, cv2.THRESH_BINARY)
            dilated = cv2.dilate(thresh, None, iterations=3)
            contours, _ = cv2.findContours(dilated, cv2.RETR_TREE, cv2.CHAIN_APPROX_SIMPLE)

            for contour in contours:
                if cv2.contourArea(contour) > MOTION_SENSITIVITY:
                    print("Motion Detected!")
                    activate_motor()

            frame1 = frame2
            ret, frame2 = cap.read()
            if not ret:
                break

    finally:
        cap.release()
        cv2.destroyAllWindows()
```

---

### **Step 6: Write the Main Script**

Edit the `run.py` file to tie everything together:
```python
# run.py

from src.motor_control import setup_motor, cleanup_motor
from src.motion_detector import detect_motion

if __name__ == "__main__":
    try:
        setup_motor()
        print("Starting Motion Detection...")
        detect_motion()
    except KeyboardInterrupt:
        print("Exiting Program")
    finally:
        cleanup_motor()
```

---

### **Step 7: Test the Project**

1. Navigate to the project folder:
   ```bash
   cd ~/baby_motion_motor
   ```

2. Run the project:
   ```bash
   sudo python3 run.py
   ```

3. Ensure the camera starts and detects motion. When motion is detected, the motor should activate.

---

### **Step 8: Automate Execution on Boot (Optional)**

If you want the system to run automatically when the Raspberry Pi boots:

1. Edit the crontab file:
   ```bash
   crontab -e
   ```

2. Add the following line at the end of the file:
   ```bash
   @reboot sudo python3 /path/to/baby_motion_motor/run.py > /path/to/baby_motion_motor/logs/output.log 2>&1
   ```

3. Save and exit. The script will run every time the Raspberry Pi starts.

---

### **Step 9: Debugging**

If something doesn’t work as expected:
1. Check the camera connection using this test script:
   ```python
   import cv2
   cap = cv2.VideoCapture(0)
   ret, frame = cap.read()
   if ret:
       print("Camera working")
   else:
       print("Camera not detected")
   cap.release()
   ```

2. Check motor connectivity using a simple motor test script:
   ```python
   import RPi.GPIO as GPIO
   import time

   MOTOR_PIN = 17
   GPIO.setmode(GPIO.BCM)
   GPIO.setup(MOTOR_PIN, GPIO.OUT)
   GPIO.output(MOTOR_PIN, GPIO.HIGH)
   time.sleep(2)
   GPIO.output(MOTOR_PIN, GPIO.LOW)
   GPIO.cleanup()
   ```

---

Let me know if you need any additional help or clarifications!
