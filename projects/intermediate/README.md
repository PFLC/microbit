# Intermediate Projects

These projects build on beginner concepts and introduce more advanced features like radio communication, complex sensors, and data handling.

## Project 1: Radio Messenger

**What you'll learn:** Radio communication between micro:bits

### Description
Send and receive messages between two micro:bits using radio.

### Setup
You'll need TWO micro:bits for this project.

### Python Code
```python
from microbit import *
import radio

radio.on()
radio.config(channel=7)  # Use same channel on both micro:bits

while True:
    # Send message when button A is pressed
    if button_a.was_pressed():
        radio.send("Hello!")
        display.show(Image.YES)
        sleep(500)
        display.clear()
    
    # Receive and display messages
    message = radio.receive()
    if message:
        display.scroll(message)
    
    sleep(100)
```

### MakeCode Blocks
1. On start:
   - `radio set group 1`
2. On button A pressed:
   - `radio send string "Hello"`
   - Show checkmark icon
3. On radio received:
   - `show string receivedString`

## Project 2: Tilt-Based Game

**What you'll learn:** Accelerometer for precise control

### Description
Control a dot on the screen by tilting the micro:bit. Collect randomly placed targets.

### Python Code
```python
from microbit import *
import random

# Player position
x, y = 2, 2
# Target position
tx, ty = random.randint(0, 4), random.randint(0, 4)
score = 0

while True:
    # Read tilt
    tilt_x = accelerometer.get_x()
    tilt_y = accelerometer.get_y()
    
    # Update position based on tilt
    if tilt_x < -200 and x > 0:
        x -= 1
    elif tilt_x > 200 and x < 4:
        x += 1
    
    if tilt_y < -200 and y > 0:
        y -= 1
    elif tilt_y > 200 and y < 4:
        y += 1
    
    # Check if target reached
    if x == tx and y == ty:
        score += 1
        tx, ty = random.randint(0, 4), random.randint(0, 4)
        display.show(Image.HAPPY)
        sleep(500)
    
    # Display
    display.clear()
    display.set_pixel(x, y, 9)
    display.set_pixel(tx, ty, 5)
    
    # Show score on button press
    if button_a.was_pressed():
        display.scroll(str(score))
    
    sleep(100)
```

## Project 3: Data Logger

**What you'll learn:** Collecting and storing sensor data

### Description
Log temperature readings over time and display statistics.

### Python Code
```python
from microbit import *

readings = []
max_readings = 50

while True:
    # Take reading when button A is pressed
    if button_a.was_pressed():
        temp = temperature()
        readings.append(temp)
        if len(readings) > max_readings:
            readings.pop(0)  # Remove oldest
        display.show(Image.YES)
        sleep(200)
        display.clear()
    
    # Show statistics when button B is pressed
    if button_b.was_pressed() and readings:
        avg = sum(readings) // len(readings)
        display.scroll("Avg: " + str(avg))
        display.scroll("Max: " + str(max(readings)))
        display.scroll("Min: " + str(min(readings)))
        display.scroll("Count: " + str(len(readings)))
    
    sleep(100)
```

## Project 4: Reaction Time Tester

**What you'll learn:** Timing, random delays, precision measurement

### Description
Test your reaction time by pressing button A when the LED lights up.

### Python Code
```python
from microbit import *
import random

while True:
    display.scroll("Press A when lit")
    sleep(1000)
    
    # Random delay
    delay = random.randint(1000, 5000)
    sleep(delay)
    
    # Show signal
    display.show(Image.SQUARE)
    start = running_time()
    
    # Wait for button press (timeout after 3 seconds)
    while running_time() - start < 3000:
        if button_a.was_pressed():
            reaction_time = running_time() - start
            display.clear()
            display.scroll(str(reaction_time) + "ms")
            break
        sleep(10)
    else:
        display.scroll("Too slow!")
    
    display.clear()
    sleep(2000)
```

## Project 5: Motion Alarm

**What you'll learn:** Complex sensor logic, state management

### Description
Create an alarm that detects motion and alerts you.

### Python Code
```python
from microbit import *
import music

armed = False
alarm_triggered = False

while True:
    # Arm/disarm with button A
    if button_a.was_pressed():
        armed = not armed
        alarm_triggered = False
        if armed:
            display.show(Image.SWORD)
            sleep(5000)  # 5 second delay to set up
            display.show(Image.SKULL)
        else:
            display.show(Image.HAPPY)
            music.stop()
    
    # Check for motion when armed
    if armed and not alarm_triggered:
        x = accelerometer.get_x()
        y = accelerometer.get_y()
        z = accelerometer.get_z()
        
        # Detect significant movement
        total = abs(x) + abs(y) + abs(z)
        if total > 2000:
            alarm_triggered = True
            
    # Sound alarm
    if alarm_triggered:
        display.show(Image.ANGRY)
        music.pitch(1000, 200)
        sleep(200)
    
    sleep(100)
```

## Project 6: Radio-Controlled Robot

**What you'll learn:** Remote control, radio communication patterns

### Description
Use one micro:bit as a remote control for another (connected to motors/servos).

### Controller Code
```python
from microbit import *
import radio

radio.on()
radio.config(channel=7)

while True:
    # Read tilt
    x = accelerometer.get_x()
    y = accelerometer.get_y()
    
    # Determine command
    if y < -300:
        command = "FORWARD"
    elif y > 300:
        command = "BACKWARD"
    elif x < -300:
        command = "LEFT"
    elif x > 300:
        command = "RIGHT"
    else:
        command = "STOP"
    
    # Send command
    radio.send(command)
    display.show(command[0])  # Show first letter
    sleep(100)
```

### Robot Code
```python
from microbit import *
import radio

radio.on()
radio.config(channel=7)

while True:
    message = radio.receive()
    if message:
        display.scroll(message)
        # Here you would control motors based on message
        # For example, using pins to control motor driver
        if message == "FORWARD":
            pin0.write_digital(1)
            pin1.write_digital(0)
        elif message == "BACKWARD":
            pin0.write_digital(0)
            pin1.write_digital(1)
        elif message == "STOP":
            pin0.write_digital(0)
            pin1.write_digital(0)
    
    sleep(100)
```

## Project 7: Stopwatch

**What you'll learn:** Time tracking, display formatting

### Description
A fully functional stopwatch with start, stop, and reset.

### Python Code
```python
from microbit import *

running = False
start_time = 0
elapsed = 0

while True:
    # Start/Stop with button A
    if button_a.was_pressed():
        if running:
            elapsed += running_time() - start_time
            running = False
        else:
            start_time = running_time()
            running = True
        display.show(Image.YES)
        sleep(200)
        display.clear()
    
    # Reset with button B
    if button_b.was_pressed():
        running = False
        elapsed = 0
        display.show(Image.NO)
        sleep(200)
        display.clear()
    
    # Display current time
    if running:
        current = elapsed + (running_time() - start_time)
    else:
        current = elapsed
    
    seconds = current // 1000
    display.scroll(str(seconds) + "s", wait=False, loop=True)
    
    sleep(100)
```

## Project 8: Pedometer

**What you'll learn:** Advanced accelerometer processing

### Description
Track steps with improved accuracy using step detection algorithm.

### Python Code
```python
from microbit import *

steps = 0
last_total = 0
threshold = 1200
cooldown = 0

while True:
    # Read acceleration
    x = accelerometer.get_x()
    y = accelerometer.get_y()
    z = accelerometer.get_z()
    total = abs(x) + abs(y) + abs(z)
    
    # Detect step (spike in movement)
    if cooldown == 0:
        if total > threshold and last_total < threshold:
            steps += 1
            cooldown = 5  # Prevent double-counting
            display.show(Image.HAPPY)
            sleep(100)
            display.clear()
    else:
        cooldown -= 1
    
    last_total = total
    
    # Show steps on button press
    if button_a.was_pressed():
        display.scroll("Steps: " + str(steps))
    
    # Reset on button B
    if button_b.was_pressed():
        steps = 0
        display.show(Image.YES)
        sleep(500)
        display.clear()
    
    sleep(100)
```

## Project 9: Spirit Level

**What you'll learn:** Precise tilt measurement, visual feedback

### Description
Create a digital spirit level showing which way to tilt.

### Python Code
```python
from microbit import *

while True:
    x = accelerometer.get_x()
    y = accelerometer.get_y()
    
    # Create display pattern
    image = Image("00000:00000:00000:00000:00000")
    
    # Calculate LED position (2,2 is center)
    led_x = 2
    led_y = 2
    
    if x > 200:
        led_x = 3
    elif x > 400:
        led_x = 4
    elif x < -200:
        led_x = 1
    elif x < -400:
        led_x = 0
    
    if y > 200:
        led_y = 3
    elif y > 400:
        led_y = 4
    elif y < -200:
        led_y = 1
    elif y < -400:
        led_y = 0
    
    # Clear and set pixel
    display.clear()
    display.set_pixel(led_x, led_y, 9)
    
    # Show level indicator when centered
    if led_x == 2 and led_y == 2:
        display.show(Image.DIAMOND)
    
    sleep(50)
```

## Project 10: Music Player

**What you'll learn:** Music sequences, melody creation

### Description
Create a music player with multiple songs selectable by buttons.

### Python Code
```python
from microbit import *
import music

songs = [
    ["C4:4", "D4:4", "E4:4", "F4:4", "G4:4"],  # Scale
    ["E4:2", "E4:2", "F4:2", "G4:2", "G4:2", "F4:2"],  # Ode to Joy
    ["C4:1", "D4:1", "E4:1", "C4:1", "C4:1", "D4:1", "E4:1", "C4:1"]  # Frere Jacques
]

current_song = 0

display.scroll("Music Player")

while True:
    # Select song
    if button_a.was_pressed():
        current_song = (current_song + 1) % len(songs)
        display.scroll(str(current_song + 1))
    
    # Play song
    if button_b.was_pressed():
        display.show(Image.MUSIC_QUAVER)
        music.play(songs[current_song])
        display.clear()
    
    sleep(100)
```

## Challenges

1. **Combine radio and sensors** - Create a weather station that transmits data
2. **Multi-player games** - Build games for 2+ micro:bits
3. **Complex state machines** - Create devices with multiple modes
4. **Data visualization** - Display sensor data graphically on the LEDs

## Next Steps

Ready for more? Check out the advanced projects folder for even more challenging builds!
