# Advanced Projects

These projects are for experienced micro:bit programmers and involve complex programming concepts, external components, and sophisticated algorithms.

## Project 1: Bluetooth Heart Rate Monitor

**What you'll learn:** Bluetooth communication, external sensors

### Description
Create a heart rate monitor that sends data to your phone via Bluetooth.

### Python Code
```python
from microbit import *
import radio

# Simulated heart rate sensor (replace with actual sensor reading)
def read_heart_rate():
    # In a real project, read from analog pin connected to sensor
    # Example: sensor_value = pin0.read_analog()
    # Process and convert to BPM
    import random
    return random.randint(60, 100)

radio.on()
radio.config(channel=7)

while True:
    if button_a.was_pressed():
        # Take reading
        display.show(Image.HEART)
        sleep(500)
        
        bpm = read_heart_rate()
        
        # Display and transmit
        display.scroll(str(bpm) + " BPM")
        radio.send(str(bpm))
    
    sleep(100)
```

### Required Components
- Pulse sensor or heart rate sensor module
- Connecting wires
- Optional: Phone with BLE app

## Project 2: Line Following Robot

**What you'll learn:** External sensors, PID control, motor control

### Description
Build a robot that follows a black line on a white surface.

### Python Code
```python
from microbit import *

# Threshold for line detection (adjust based on your sensors)
THRESHOLD = 500

def read_left_sensor():
    return pin0.read_analog()

def read_right_sensor():
    return pin1.read_analog()

def set_motors(left_speed, right_speed):
    # PWM control for motors
    # Left motor on pin8 and pin12
    # Right motor on pin13 and pin14
    if left_speed > 0:
        pin8.write_analog(min(1023, left_speed))
        pin12.write_digital(0)
    else:
        pin8.write_digital(0)
        pin12.write_analog(min(1023, -left_speed))
    
    if right_speed > 0:
        pin13.write_analog(min(1023, right_speed))
        pin14.write_digital(0)
    else:
        pin13.write_digital(0)
        pin14.write_analog(min(1023, -right_speed))

# Main loop
while True:
    left = read_left_sensor()
    right = read_right_sensor()
    
    left_on_line = left < THRESHOLD
    right_on_line = right < THRESHOLD
    
    if left_on_line and right_on_line:
        # Both on line - go straight
        set_motors(512, 512)
        display.show(Image.ARROW_N)
    elif left_on_line:
        # Turn left
        set_motors(256, 768)
        display.show(Image.ARROW_W)
    elif right_on_line:
        # Turn right
        set_motors(768, 256)
        display.show(Image.ARROW_E)
    else:
        # Lost line - search
        set_motors(0, 0)
        display.show(Image.CONFUSED)
    
    sleep(20)
```

### Required Components
- 2 x IR line sensors
- Motor driver (L298N or similar)
- 2 x DC motors
- Robot chassis
- Battery pack

## Project 3: Weather Station

**What you'll learn:** Multiple sensors, data aggregation, long-term logging

### Description
Comprehensive weather station with temperature, humidity, and pressure sensors.

### Python Code
```python
from microbit import *
import radio

# Initialize radio for data transmission
radio.on()
radio.config(channel=7, power=7)

# Simulate external sensors (replace with actual I2C sensors)
def read_humidity():
    # Read from DHT22 or similar
    return 65  # Placeholder

def read_pressure():
    # Read from BMP280 or similar
    return 1013  # Placeholder in hPa

# Data collection interval (milliseconds)
INTERVAL = 60000  # 1 minute
last_reading = 0

while True:
    current_time = running_time()
    
    # Take readings at interval
    if current_time - last_reading >= INTERVAL:
        temp = temperature()
        humidity = read_humidity()
        pressure = read_pressure()
        
        # Format data
        data = "T:{},H:{},P:{}".format(temp, humidity, pressure)
        
        # Transmit
        radio.send(data)
        
        # Display briefly
        display.scroll("T:" + str(temp))
        
        last_reading = current_time
    
    # Manual reading on button press
    if button_a.was_pressed():
        display.scroll("Temp: " + str(temperature()) + "C")
        display.scroll("Humidity: " + str(read_humidity()) + "%")
        display.scroll("Pressure: " + str(read_pressure()) + "hPa")
    
    sleep(100)
```

### Required Components
- BME280 or BMP280 sensor (temperature, humidity, pressure)
- Connecting wires
- Optional: Second micro:bit for data logging

## Project 4: Smart Home Controller

**What you'll learn:** Home automation, relay control, scheduling

### Description
Control lights, fans, and appliances with your micro:bit.

### Python Code
```python
from microbit import *

# Device states
devices = {
    'light': False,
    'fan': False,
    'heater': False
}

# Pin assignments
LIGHT_PIN = pin0
FAN_PIN = pin1
HEATER_PIN = pin2

current_device = 0
device_names = ['light', 'fan', 'heater']
device_pins = [LIGHT_PIN, FAN_PIN, HEATER_PIN]

def update_display():
    device = device_names[current_device]
    state = "ON" if devices[device] else "OFF"
    display.scroll(device[0].upper() + ":" + state)

# Initialize all devices to off
for pin in device_pins:
    pin.write_digital(0)

while True:
    # Select device with button A
    if button_a.was_pressed():
        current_device = (current_device + 1) % len(device_names)
        update_display()
    
    # Toggle device with button B
    if button_b.was_pressed():
        device = device_names[current_device]
        devices[device] = not devices[device]
        device_pins[current_device].write_digital(1 if devices[device] else 0)
        update_display()
    
    # Emergency off - shake to turn everything off
    if accelerometer.was_gesture('shake'):
        for i, pin in enumerate(device_pins):
            pin.write_digital(0)
            devices[device_names[i]] = False
        display.show(Image.NO)
        sleep(500)
        display.clear()
    
    sleep(100)
```

### Required Components
- Relay module (3 or 4 channel)
- AC appliances (CAUTION: Work with adult supervision)
- Power supply for relays
- Connecting wires

### Safety Warning
⚠️ This project involves AC power. Only build this under adult supervision and follow all electrical safety guidelines.

## Project 5: Maze Solving Robot

**What you'll learn:** Pathfinding algorithms, autonomous navigation

### Description
Robot that can navigate and solve mazes using wall-following algorithm.

### Python Code
```python
from microbit import *

# Ultrasonic sensor reading
def get_distance(trigger_pin, echo_pin):
    # Send pulse
    trigger_pin.write_digital(1)
    sleep(0.01)
    trigger_pin.write_digital(0)
    
    # Measure echo
    # This is simplified - actual implementation needs precise timing
    duration = echo_pin.read_digital()
    distance = duration * 0.034 / 2  # Convert to cm
    return distance

# Motor control
def forward():
    pin0.write_digital(1)
    pin1.write_digital(0)
    pin2.write_digital(1)
    pin3.write_digital(0)

def turn_right():
    pin0.write_digital(1)
    pin1.write_digital(0)
    pin2.write_digital(0)
    pin3.write_digital(1)

def turn_left():
    pin0.write_digital(0)
    pin1.write_digital(1)
    pin2.write_digital(1)
    pin3.write_digital(0)

def stop():
    pin0.write_digital(0)
    pin1.write_digital(0)
    pin2.write_digital(0)
    pin3.write_digital(0)

# Right-hand wall following algorithm
while True:
    # Simplified - would need actual distance sensors
    front_clear = True  # Check with sensor
    right_clear = False  # Check with sensor
    
    if right_clear:
        # No wall on right, turn right
        turn_right()
        sleep(500)
        forward()
    elif front_clear:
        # Wall on right, no wall ahead, go forward
        forward()
    else:
        # Wall ahead, turn left
        turn_left()
        sleep(500)
    
    sleep(100)
```

### Required Components
- Ultrasonic sensors (3x recommended)
- Motor driver
- Robot chassis with motors
- Battery pack

## Project 6: RFID Access Control

**What you'll learn:** RFID reading, access control logic

### Description
Create a security system that unlocks with the right RFID card.

### Python Code
```python
from microbit import *

# Authorized card IDs
AUTHORIZED_CARDS = [
    "1234567890",
    "0987654321"
]

def read_rfid():
    # This would interface with an RFID reader module
    # Example using UART communication
    uart.init(baudrate=9600)
    if uart.any():
        card_id = str(uart.read(), 'utf-8').strip()
        return card_id
    return None

def unlock():
    pin0.write_digital(1)  # Servo or lock mechanism
    display.show(Image.YES)
    sleep(3000)
    pin0.write_digital(0)
    display.clear()

def deny():
    display.show(Image.NO)
    sleep(1000)
    display.clear()

display.scroll("Ready")

while True:
    card_id = read_rfid()
    
    if card_id:
        display.scroll("Card: " + card_id[:4])
        
        if card_id in AUTHORIZED_CARDS:
            unlock()
        else:
            deny()
    
    sleep(100)
```

### Required Components
- RFID RC522 module
- RFID cards/tags
- Servo motor or electronic lock
- Connecting wires

## Project 7: GPS Tracker

**What you'll learn:** GPS module integration, coordinate systems

### Description
Track location and display coordinates or distance traveled.

### Python Code
```python
from microbit import *
import math

def parse_gps():
    # Read from GPS module via UART
    uart.init(baudrate=9600)
    if uart.any():
        line = str(uart.read(), 'utf-8')
        # Parse NMEA sentences (simplified)
        # Real implementation would parse $GPGGA or $GPRMC
        return {"lat": 0.0, "lon": 0.0}
    return None

def calculate_distance(lat1, lon1, lat2, lon2):
    # Haversine formula
    R = 6371  # Earth's radius in km
    
    dlat = math.radians(lat2 - lat1)
    dlon = math.radians(lon2 - lon1)
    
    a = (math.sin(dlat/2) * math.sin(dlat/2) +
         math.cos(math.radians(lat1)) * math.cos(math.radians(lat2)) *
         math.sin(dlon/2) * math.sin(dlon/2))
    
    c = 2 * math.atan2(math.sqrt(a), math.sqrt(1-a))
    return R * c

# Starting position
start_pos = None
total_distance = 0

while True:
    pos = parse_gps()
    
    if pos and button_a.was_pressed():
        # Set starting position
        start_pos = pos
        display.show(Image.TARGET)
        sleep(500)
        display.clear()
    
    if pos and start_pos and button_b.was_pressed():
        # Calculate distance from start
        dist = calculate_distance(
            start_pos['lat'], start_pos['lon'],
            pos['lat'], pos['lon']
        )
        display.scroll(str(int(dist * 1000)) + "m")
    
    sleep(1000)
```

### Required Components
- GPS module (NEO-6M or similar)
- Antenna
- Battery for portable use

## Project 8: Air Quality Monitor

**What you'll learn:** Environmental sensing, data interpretation

### Python Code
```python
from microbit import *
import radio

# Initialize
radio.on()
radio.config(channel=7)

def read_air_quality():
    # Read from MQ-135 or similar sensor
    value = pin0.read_analog()
    # Convert to air quality index (simplified)
    aqi = value // 4  # 0-255 range
    return aqi

def get_quality_level(aqi):
    if aqi < 50:
        return "Good", Image.HAPPY
    elif aqi < 100:
        return "Moderate", Image.MEH
    elif aqi < 150:
        return "Unhealthy", Image.SAD
    else:
        return "Hazardous", Image.SKULL

while True:
    aqi = read_air_quality()
    level, icon = get_quality_level(aqi)
    
    # Display on button press
    if button_a.was_pressed():
        display.show(icon)
        sleep(1000)
        display.scroll("AQI: " + str(aqi))
        display.scroll(level)
    
    # Continuous monitoring mode
    if button_b.was_pressed():
        for i in range(10):
            aqi = read_air_quality()
            level, icon = get_quality_level(aqi)
            display.show(icon)
            
            # Alert if dangerous
            if aqi > 150:
                import music
                music.pitch(1000, 200)
            
            sleep(5000)
        display.clear()
    
    sleep(100)
```

### Required Components
- MQ-135 Air Quality Sensor
- Connecting wires

## Project 9: Gesture Recognition

**What you'll learn:** Machine learning basics, pattern recognition

### Python Code
```python
from microbit import *

# Simple gesture templates
GESTURES = {
    'shake': [1000, 1200, 1000, 1200],  # High variation pattern
    'tilt_left': [-800, -700, -800, -700],  # Consistent left tilt
    'tilt_right': [800, 700, 800, 700],  # Consistent right tilt
}

def record_gesture():
    """Record a gesture pattern"""
    pattern = []
    display.show(Image.ARROW_S)
    
    for i in range(20):
        x = accelerometer.get_x()
        pattern.append(x)
        sleep(50)
    
    return pattern

def match_gesture(pattern):
    """Simple pattern matching"""
    # Calculate average and variation
    avg = sum(pattern) // len(pattern)
    variation = sum(abs(x - avg) for x in pattern) // len(pattern)
    
    if variation > 500:
        return 'shake'
    elif avg < -500:
        return 'tilt_left'
    elif avg > 500:
        return 'tilt_right'
    else:
        return 'still'

# Main loop
while True:
    if button_a.was_pressed():
        pattern = record_gesture()
        gesture = match_gesture(pattern)
        display.scroll(gesture)
    
    sleep(100)
```

## Project 10: Encryption Messenger

**What you'll learn:** Cryptography basics, secure communication

### Python Code
```python
from microbit import *
import radio

# Simple Caesar cipher
KEY = 3

def encrypt(text):
    result = ""
    for char in text:
        if char.isalpha():
            shift = 65 if char.isupper() else 97
            result += chr((ord(char) - shift + KEY) % 26 + shift)
        else:
            result += char
    return result

def decrypt(text):
    result = ""
    for char in text:
        if char.isalpha():
            shift = 65 if char.isupper() else 97
            result += chr((ord(char) - shift - KEY) % 26 + shift)
        else:
            result += char
    return result

radio.on()
radio.config(channel=7)

# Predefined messages
messages = ["HELLO", "SECRET", "MEETUP"]
current_msg = 0

while True:
    # Select message
    if button_a.was_pressed():
        current_msg = (current_msg + 1) % len(messages)
        display.scroll(messages[current_msg])
    
    # Send encrypted
    if button_b.was_pressed():
        encrypted = encrypt(messages[current_msg])
        radio.send(encrypted)
        display.show(Image.YES)
        sleep(500)
        display.clear()
    
    # Receive and decrypt
    received = radio.receive()
    if received:
        decrypted = decrypt(received)
        display.scroll("Got: " + decrypted)
    
    sleep(100)
```

## Challenges

1. **Build a complete robot** - Combine multiple advanced features
2. **Create IoT device** - Connect to internet via external module
3. **Implement AI** - Add machine learning for advanced recognition
4. **Multi-sensor fusion** - Combine data from multiple sensors

## Competition Ideas

- Sumo robot competition
- Fastest maze solver
- Most accurate sensor readings
- Most creative use of radio communication

These advanced projects will push your skills to the limit. Good luck!
