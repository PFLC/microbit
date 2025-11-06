# Hardware Setup Guide

Complete guide to setting up and understanding your micro:bit hardware.

## micro:bit Overview

The BBC micro:bit is a pocket-sized computer designed to teach programming and electronics. It includes:

### Front Features
```
     [Button A]              [Button B]
           ┌───────────────┐
           │ ■ ■ ■ ■ ■     │
           │ ■ ■ ■ ■ ■     │  5×5 LED Display
           │ ■ ■ ■ ■ ■     │
           │ ■ ■ ■ ■ ■     │
           │ ■ ■ ■ ■ ■     │
           │               │
           │    [Logo]     │  Touch-sensitive (v2 only)
           │               │
           └───────────────┘
```

### Back Features
- **USB Port:** For programming and power
- **Battery Connector:** JST connector for external battery
- **Reset Button:** Restart the micro:bit
- **Edge Connector:** 25 pins for external connections

## micro:bit v1 vs v2

### micro:bit v2 (Latest - Recommended)
Released in 2020, includes:
- Touch-sensitive logo (acts as a third button)
- Built-in speaker and microphone
- More memory (512KB flash, 128KB RAM)
- Faster processor (64MHz Nordic nRF52833)
- Power LED indicator
- Notched edge connector

### micro:bit v1 (Original)
Released in 2016, includes:
- 2 buttons only
- No built-in speaker/microphone
- Less memory (256KB flash, 16KB RAM)
- Slower processor (16MHz Nordic nRF51822)

**Note:** All projects in this repository work on both versions unless specifically noted.

## Initial Setup

### What You Need
1. **micro:bit board** (v1 or v2)
2. **USB cable** (Micro-B to USB-A or USB-C depending on your computer)
3. **Computer** with internet access
4. **Battery pack** (optional, for portable projects)

### First Time Setup

#### Step 1: Unpack
- Remove micro:bit from packaging
- Keep the USB cable handy
- Note any included batteries or accessories

#### Step 2: Connect to Computer
1. Plug the micro USB end into the micro:bit
2. Plug the other end into your computer's USB port
3. The micro:bit should light up with a pattern

#### Step 3: Verify Connection
- Look for a drive named "MICROBIT" in your file explorer
- You should see a few files:
  - `DETAILS.TXT` - Information about your micro:bit
  - `MICROBIT.HTM` - Link to getting started guide

#### Step 4: Check Version
1. Open `DETAILS.TXT` on the MICROBIT drive
2. Look for the version information:
   ```
   # Interface Version: 0257
   # DAPLink: 0257
   # Git Commit: ...
   # Board ID: 9904...
   ```
3. Interface version 0254+ indicates v2, earlier versions are v1

## Pin Connections

### Edge Connector Pinout

The edge connector has 25 pins arranged in two rows:

```
Large Pins (easy to access):
┌─────────────────────────────┐
│ 0   1   2   3V  GND         │
│                              │
│     [micro:bit body]         │
│                              │
│         3V  GND              │
└─────────────────────────────┘

Small Pins (require edge connector):
Additional GPIO, I2C, SPI, etc.
```

### Pin Functions

| Pin | Primary Use | Alternative Functions |
|-----|-------------|----------------------|
| 0   | GPIO/ADC    | Touch input, I2C SDA |
| 1   | GPIO/ADC    | Touch input, I2C SCL |
| 2   | GPIO/ADC    | Touch input |
| 3V  | Power Out   | 3.0V supply (~90mA max) |
| GND | Ground      | 0V reference |
| 8   | GPIO        | - |
| 12  | GPIO        | - |
| 13  | GPIO/SPI    | SPI SCK |
| 14  | GPIO/SPI    | SPI MISO |
| 15  | GPIO/SPI    | SPI MOSI |
| 16  | GPIO        | - |
| 19  | GPIO/I2C    | I2C SCL |
| 20  | GPIO/I2C    | I2C SDA |

### Using Pins

#### Digital Output (LED)
```python
from microbit import *

# Turn on LED connected to pin0
pin0.write_digital(1)

# Turn off LED
pin0.write_digital(0)

# Blink LED
while True:
    pin0.write_digital(1)
    sleep(500)
    pin0.write_digital(0)
    sleep(500)
```

#### Analog Input (Sensor)
```python
from microbit import *

# Read analog value (0-1023)
value = pin0.read_analog()
display.scroll(str(value))

# Read as percentage
percentage = value * 100 // 1023
```

#### Touch Sensor (pins 0, 1, 2)
```python
from microbit import *

while True:
    if pin0.is_touched():
        display.show(Image.HAPPY)
    else:
        display.clear()
```

## Power Options

### USB Power
- **Voltage:** 5V from USB
- **Current:** Unlimited (from computer)
- **Best for:** Programming, testing, continuous use
- **Limitations:** Requires cable connection

### Battery Power
- **Battery Pack:** 2×AAA (3V) or 3V coin cell
- **Connector:** JST connector on back
- **Best for:** Portable projects, untethered use
- **Limitations:** Limited runtime, needs replacement

### External Power (Advanced)
- Can power through 3V or GND pins
- **Warning:** Do not exceed 3.3V on 3V pin
- Be careful with polarity

## Connecting External Components

### Using Crocodile Clips
Easiest method for beginners:

1. **LED Connection:**
   - Clip positive (longer leg) to pin 0
   - Clip negative (shorter leg) to GND
   - Add 100Ω resistor if available

2. **Button/Switch:**
   - One side to pin 0
   - Other side to 3V
   - Use pull-down in code: `pin0.read_digital()`

3. **Buzzer:**
   - Positive to pin 0
   - Negative to GND

### Using Edge Connector Breakout
For more permanent connections:

1. **Get an edge connector breakout board**
   - Provides easy access to all pins
   - Allows breadboard connections
   - Available from Kitronik, SparkFun, etc.

2. **Connect micro:bit to breakout**
   - Align carefully
   - Press firmly into connector

3. **Wire components on breadboard**
   - Use jumper wires
   - More stable than clips

### Common Sensors

#### Ultrasonic Distance Sensor (HC-SR04)
```python
from microbit import *

trigger = pin1
echo = pin2

def get_distance():
    # Send pulse
    trigger.write_digital(1)
    sleep(0.01)
    trigger.write_digital(0)
    
    # Measure echo time
    # Note: MicroPython on micro:bit doesn't have precise timing
    # This is simplified - use dedicated library for accuracy
    
get_distance()
```

#### Servo Motor
```python
from microbit import *

# Connect servo signal to pin0
# Connect servo power to 3V (if low power) or external supply
# Connect servo ground to GND

def set_angle(angle):
    # Angle 0-180 degrees
    # Pulse width 1000-2000 microseconds
    pulse = 1000 + (angle * 1000 // 180)
    pin0.set_analog_period(20)
    pin0.write_analog(pulse // 20)

# Move to 90 degrees
set_angle(90)
```

#### Temperature Sensor (DS18B20)
Requires OneWire library (not built-in).

#### PIR Motion Sensor
```python
from microbit import *

# Connect PIR output to pin0
# Connect VCC to 3V, GND to GND

while True:
    if pin0.read_digital() == 1:
        display.show(Image.SURPRISED)
    else:
        display.clear()
    sleep(100)
```

## I2C Devices

The micro:bit has an I2C bus on pins 19 (SCL) and 20 (SDA).

### Common I2C Devices
- OLED displays
- BME280 temperature/humidity/pressure sensor
- Accelerometers
- Real-time clocks

### Basic I2C Communication
```python
from microbit import *

# Scan for I2C devices
i2c.scan()  # Returns list of addresses

# Read from device
data = i2c.read(address, n)  # n bytes

# Write to device
i2c.write(address, data)
```

## Building a Robot

### Basic Components
1. **micro:bit** - The brain
2. **Motor driver** - L298N or similar
3. **2× DC motors** - For wheels
4. **Chassis** - Platform with wheels
5. **Battery pack** - For motors (separate from micro:bit)
6. **Wheels** - Matched to motors

### Wiring
```
micro:bit pin0 → Motor Driver IN1
micro:bit pin1 → Motor Driver IN2
micro:bit pin8 → Motor Driver IN3
micro:bit pin12 → Motor Driver IN4

Motor Driver OUT1 & OUT2 → Left Motor
Motor Driver OUT3 & OUT4 → Right Motor

Motor Driver 12V → Battery Pack (+)
Motor Driver GND → Battery Pack (-) AND micro:bit GND
```

### Basic Motor Control
```python
from microbit import *

def forward():
    pin0.write_digital(1)
    pin1.write_digital(0)
    pin8.write_digital(1)
    pin12.write_digital(0)

def backward():
    pin0.write_digital(0)
    pin1.write_digital(1)
    pin8.write_digital(0)
    pin12.write_digital(1)

def stop():
    pin0.write_digital(0)
    pin1.write_digital(0)
    pin8.write_digital(0)
    pin12.write_digital(0)

# Drive forward for 2 seconds
forward()
sleep(2000)
stop()
```

## Safety Guidelines

### Electrical Safety
⚠️ **Important Safety Rules:**

1. **Never exceed voltage limits**
   - micro:bit operates at 3.3V logic
   - USB provides 5V (safe)
   - Don't connect higher voltages directly to pins

2. **Current Limitations**
   - Each pin: max 5mA (safe), 15mA (absolute max)
   - Total for all pins: 90mA max
   - Use transistors/MOSFETs for high-current devices

3. **Polarity**
   - Check + and - before connecting
   - Reversed polarity can damage micro:bit
   - Use a multimeter to verify

4. **Heat**
   - Don't short-circuit pins
   - If micro:bit gets hot, disconnect immediately
   - Check for wiring mistakes

### Handling
- Hold by edges, avoid touching components
- Keep away from water and liquids
- Store in anti-static bag when not in use
- Don't flex or bend the board

### Adult Supervision
Projects involving:
- AC power (mains electricity)
- LiPo batteries
- High-power motors
- Sharp tools

Should only be done with adult supervision.

## Care and Maintenance

### Cleaning
- Use dry cloth only
- Compressed air for dust
- Don't use liquids or solvents

### Storage
- Keep in dry place
- Room temperature
- Anti-static bag recommended
- Store away from magnets

### Troubleshooting Hardware
See `troubleshooting.md` for common hardware issues.

## Next Steps

Now that your hardware is set up:
1. Try the [Getting Started Guide](../getting-started/README.md)
2. Build a [Beginner Project](../projects/beginner/README.md)
3. Complete some [Exercises](../exercises/README.md)

Happy making! 🔧
