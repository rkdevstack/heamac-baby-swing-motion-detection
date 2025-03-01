Here’s a list of components you'll need for your project, along with their configurations and estimated costs.

---

### **Components List**

#### **1. Raspberry Pi**
- **Model:** Raspberry Pi 4 Model B (4GB or 8GB RAM)
- **Purpose:** Acts as the processing unit for motion detection and motor control.
- **Included Accessories:**
  - Raspberry Pi power adapter (5V 3A)
  - MicroSD card (16GB or higher) with Raspberry Pi OS pre-installed.

#### **2. Camera**
- **Option 1:** Raspberry Pi Camera Module V2
  - **Resolution:** 8 MP
  - **Connection:** CSI (Camera Serial Interface)
  - **Purpose:** Captures video feed for motion detection.

- **Option 2:** USB Webcam (Logitech C270 or similar)
  - **Resolution:** 720p or 1080p
  - **Connection:** USB
 

#### **3. Motor**
- **Type:** DC Motor
  - **Voltage:** 6V–12V
  - **RPM:** 100–500 (depending on swing speed requirements).
  - **Torque:** Choose based on the weight of the baby and swing (e.g., 1-2 Nm for typical swings).


#### **4. Motor Driver**
- **Model:** L298N Motor Driver Module
  - **Purpose:** Controls the DC motor by providing the necessary voltage and direction signals from the Raspberry Pi.
  - **Features:** Dual H-bridge, can handle 5V–35V motors.


#### **5. Power Supply**
- **For Raspberry Pi:**
  - Official Raspberry Pi power adapter (5V 3A).

- **For Motor:**
  - DC Power Adapter (12V, 2A–5A).


#### **6. Jumper Wires**
- **Type:** Male-to-Male, Male-to-Female
- **Purpose:** To connect Raspberry Pi GPIO pins to the motor driver.
- **Quantity:** ~10–20 wires.


#### **7. Breadboard (Optional)**
- **Size:** Medium or large (for prototyping).
- **Purpose:** Temporary connections for motor driver and Raspberry Pi GPIO pins.


#### **8. Mounting Accessories**
- **Camera Mount:**
  - Purpose: Securely position the camera facing the baby.
 
- **Motor Mount and Swing Mechanism:**
  - Purpose: Attach the motor to the swing.


#### **9. Additional Tools**
- **MicroSD Card Reader:**
  - To flash the Raspberry Pi OS onto the microSD card.

- **Screwdriver Set:**
  - For assembling components.


---

### **Component List**
| **Component**         | 
|------------------------|
| Raspberry Pi 4 Model B | 
| Camera Module          | 
| DC Motor               | 
| L298N Motor Driver     | 
| Power Supplies         | 
| Jumper Wires           | 
| Breadboard             | 
| Mounting Accessories   | 


---

### **Where to Buy**
1. **Raspberry Pi and Accessories:**
   - Official Raspberry Pi distributors (e.g., [PiShop.us](https://www.pishop.us), [ThePiHut](https://thepihut.com)).
   - Amazon or eBay.

2. **Electronics and Motors:**
   - [Adafruit](https://www.adafruit.com)
   - [SparkFun](https://www.sparkfun.com)
   - [Pololu](https://www.pololu.com)
   - Amazon or local electronics stores.

3. **Mounting Accessories and Tools:**
   - Home improvement stores like Home Depot or Lowe’s.
   - Online platforms like Amazon.

---

### **Configurations and Selection Tips**
1. **Camera:**
   - Choose the Raspberry Pi Camera Module for direct compatibility.
   - USB webcam is a good fallback if CSI camera isn’t available.

2. **Motor:**
   - Ensure the motor has enough torque to swing the baby.
   - Use a geared DC motor if more torque is needed.

3. **Power Supplies:**
   - Ensure the motor power supply matches the motor's voltage and current requirements.
   - Use separate power supplies for the Raspberry Pi and motor to prevent voltage drops.

4. **Motor Driver:**
   - The L298N is suitable for small to medium-sized motors. For higher loads, consider other drivers like BTS7960.

5. **Testing Setup:**
   - Use a breadboard initially for prototyping. Solder connections for the final build for reliability.

