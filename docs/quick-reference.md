# micro:bit Quick Reference

A handy cheatsheet for common micro:bit commands and patterns.

## Display

### Show Text
```python
# Scroll text
display.scroll("Hello")

# Show single character
display.show("A")

# Show number
display.show(42)
```

### Images
```python
# Built-in images
display.show(Image.HEART)
display.show(Image.HAPPY)
display.show(Image.SAD)
display.show(Image.ANGRY)
display.show(Image.SMILE)
display.show(Image.CONFUSED)
display.show(Image.ASLEEP)
display.show(Image.SURPRISED)
display.show(Image.SILLY)
display.show(Image.YES)
display.show(Image.NO)

# Arrows
display.show(Image.ARROW_N)  # North
display.show(Image.ARROW_NE)
display.show(Image.ARROW_E)
display.show(Image.ARROW_SE)
display.show(Image.ARROW_S)
display.show(Image.ARROW_SW)
display.show(Image.ARROW_W)
display.show(Image.ARROW_NW)
```

### Individual LEDs
```python
# Set pixel (x, y, brightness)
display.set_pixel(2, 2, 9)  # Center LED, full brightness

# Clear pixel
display.set_pixel(2, 2, 0)

# Clear entire display
display.clear()
```

### Custom Images
```python
# Create custom 5x5 image (0-9 brightness)
boat = Image("05050:"
             "05050:"
             "05050:"
             "99999:"
             "09990")
display.show(boat)
```

## Buttons

```python
# Check if button was pressed
if button_a.was_pressed():
    # Do something

# Check if button is currently pressed
if button_a.is_pressed():
    # Do something

# Count presses
presses = button_a.get_presses()

# Both buttons
if button_a.is_pressed() and button_b.is_pressed():
    # Do something
```

## Sensors

### Accelerometer
```python
# Get acceleration (milli-g)
x = accelerometer.get_x()  # -1024 to 1024
y = accelerometer.get_y()
z = accelerometer.get_z()

# Check gestures
if accelerometer.was_gesture('shake'):
    # Shaken!

# Other gestures: 'up', 'down', 'left', 'right', 'face up', 'face down', 'freefall'
```

### Compass
```python
# Must calibrate first!
compass.calibrate()

# Get heading (0-359 degrees, 0 = North)
heading = compass.heading()
```

### Temperature
```python
# Get temperature in Celsius
temp = temperature()
```

### Light Level
```python
# Get light level (0-255)
light = display.read_light_level()
```

## Pins

### Digital
```python
# Read digital (0 or 1)
value = pin0.read_digital()

# Write digital
pin0.write_digital(1)  # On
pin0.write_digital(0)  # Off
```

### Analog
```python
# Read analog (0-1023)
value = pin0.read_analog()

# Write analog (PWM)
pin0.write_analog(512)  # 50% brightness/speed
```

### Touch
```python
# Check if pin touched (pins 0, 1, 2)
if pin0.is_touched():
    # Touched!
```

## Timing

```python
# Pause/sleep (milliseconds)
sleep(1000)  # Wait 1 second

# Get running time
time = running_time()  # Milliseconds since start
```

## Radio

```python
import radio

# Turn on radio
radio.on()

# Set channel (0-83)
radio.config(channel=7)

# Set group (0-255)
radio.config(group=1)

# Send message
radio.send("Hello")

# Receive message
message = radio.receive()
if message:
    display.scroll(message)
```

## Music

```python
import music

# Play built-in melody
music.play(music.NYAN)

# Other melodies: DADADADUM, ENTERTAINER, PRELUDE, ODE, BIRTHDAY, FUNERAL, PUNCHLINE, PYTHON, BADDY, CHASE, BA_DING, WAWAWAWAA, JUMP_UP, JUMP_DOWN, POWER_UP, POWER_DOWN

# Play note (frequency, duration)
music.pitch(440, 1000)  # A note for 1 second

# Play tone sequence
music.play(['C4:4', 'D4:4', 'E4:4'])

# Stop music
music.stop()
```

## Random

```python
import random

# Random integer
num = random.randint(1, 6)  # Dice roll

# Random choice from list
choice = random.choice(['A', 'B', 'C'])
```

## Common Patterns

### Infinite Loop
```python
from microbit import *

while True:
    # Your code here
    sleep(100)
```

### Button Toggle
```python
from microbit import *

state = False

while True:
    if button_a.was_pressed():
        state = not state  # Toggle
        if state:
            display.show(Image.YES)
        else:
            display.show(Image.NO)
    sleep(100)
```

### Counter
```python
from microbit import *

count = 0

while True:
    if button_a.was_pressed():
        count += 1
        display.scroll(str(count))
    if button_b.was_pressed():
        count = 0
        display.show(Image.YES)
    sleep(100)
```

### Animation
```python
from microbit import *

frames = [Image.HEART, Image.HEART_SMALL]
frame = 0

while True:
    display.show(frames[frame])
    frame = (frame + 1) % len(frames)
    sleep(500)
```

### Tilt Control
```python
from microbit import *

while True:
    x = accelerometer.get_x()
    
    if x > 300:
        display.show(Image.ARROW_E)
    elif x < -300:
        display.show(Image.ARROW_W)
    else:
        display.show(Image.DIAMOND)
    
    sleep(100)
```

### Radio Communication
```python
from microbit import *
import radio

radio.on()
radio.config(channel=7)

while True:
    # Send
    if button_a.was_pressed():
        radio.send("Hi!")
    
    # Receive
    msg = radio.receive()
    if msg:
        display.scroll(msg)
    
    sleep(100)
```

## Tips

- Remember to `import` modules you need
- Use `sleep()` to control timing
- Store values in variables: `x = pin0.read_analog()`
- Convert numbers to strings for display: `str(42)`
- Comment your code: `# This is a comment`
- Test often - upload after small changes

## Common Errors

### ImportError
```python
# Wrong
from micro:bit import *

# Right
from microbit import *
```

### Indentation
```python
# Wrong - no indentation
while True:
display.show(Image.HEART)

# Right
while True:
    display.show(Image.HEART)
```

### Missing Import
```python
# If using radio, must import
import radio
radio.on()

# If using music, must import
import music
music.play(music.NYAN)
```

## Quick Links

- **MakeCode Editor:** https://makecode.microbit.org/
- **Python Editor:** https://python.microbit.org/
- **Documentation:** https://microbit-micropython.readthedocs.io/
- **Support:** https://support.microbit.org/

---

**Keep this handy while coding!** 📝
