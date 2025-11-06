# Beginner Projects

These projects are perfect for getting started with micro:bit programming. Each project introduces new concepts while building on what you've learned.

## Project 1: LED Heart Animation

**What you'll learn:** Basic LED display, animation

### Description
Create a beating heart animation on the LED display.

### MakeCode Blocks
1. Create a new project
2. In the `forever` block, add:
   - `show icon` (heart)
   - `pause` (500ms)
   - `show icon` (small heart)
   - `pause` (500ms)

### Python Code
```python
from microbit import *

while True:
    display.show(Image.HEART)
    sleep(500)
    display.show(Image.HEART_SMALL)
    sleep(500)
```

## Project 2: Button Counter

**What you'll learn:** Button inputs, variables, displaying numbers

### Description
Count how many times button A is pressed and display the count.

### MakeCode Blocks
1. Create a variable called `count`
2. Set `count` to 0 on start
3. On button A pressed:
   - Change `count` by 1
   - Show number `count`

### Python Code
```python
from microbit import *

count = 0

while True:
    if button_a.was_pressed():
        count += 1
        display.scroll(str(count))
    sleep(100)
```

## Project 3: Digital Dice

**What you'll learn:** Random numbers, shake detection

### Description
Shake the micro:bit to roll a dice and display a random number from 1 to 6.

### MakeCode Blocks
1. On shake:
   - Set variable `roll` to `pick random 1 to 6`
   - Show number `roll`

### Python Code
```python
from microbit import *
import random

while True:
    if accelerometer.was_gesture('shake'):
        number = random.randint(1, 6)
        display.show(str(number))
    sleep(100)
```

## Project 4: Name Badge

**What you'll learn:** Text scrolling, continuous loops

### Description
Display your name scrolling across the LED screen.

### MakeCode Blocks
1. In `forever`:
   - `show string` "Your Name"
   - `pause` (100ms)

### Python Code
```python
from microbit import *

while True:
    display.scroll("Your Name")
```

## Project 5: Temperature Display

**What you'll learn:** Sensors, conditional display

### Description
Press button A to display the current temperature in Celsius.

### MakeCode Blocks
1. On button A pressed:
   - Set variable `temp` to `temperature`
   - Show number `temp`
   - Show string "°C"

### Python Code
```python
from microbit import *

while True:
    if button_a.was_pressed():
        temp = temperature()
        display.scroll(str(temp) + "C")
    sleep(100)
```

## Project 6: Nightlight

**What you'll learn:** Light sensor, conditional logic

### Description
Turn on all LEDs when it's dark, turn them off when it's bright.

### MakeCode Blocks
1. In `forever`:
   - If `light level < 50`:
     - Show all LEDs
   - Else:
     - Clear screen

### Python Code
```python
from microbit import *

while True:
    light = display.read_light_level()
    if light < 50:
        display.show(Image.SQUARE)
    else:
        display.clear()
    sleep(100)
```

## Project 7: Compass

**What you'll learn:** Compass sensor, directions

### Description
Show an arrow pointing North when button A is pressed.

### MakeCode Blocks
1. On button A pressed:
   - Set variable `heading` to `compass heading`
   - Show arrow pointing in direction `heading`

### Python Code
```python
from microbit import *

compass.calibrate()

while True:
    if button_a.was_pressed():
        heading = compass.heading()
        if heading < 45 or heading > 315:
            display.show(Image.ARROW_N)
        elif heading < 135:
            display.show(Image.ARROW_E)
        elif heading < 225:
            display.show(Image.ARROW_S)
        else:
            display.show(Image.ARROW_W)
    sleep(100)
```

## Project 8: Step Counter

**What you'll learn:** Accelerometer, counting steps

### Description
Count your steps as you walk (shake detection).

### MakeCode Blocks
1. Create variable `steps` = 0
2. On shake:
   - Change `steps` by 1
3. On button A pressed:
   - Show number `steps`

### Python Code
```python
from microbit import *

steps = 0

while True:
    if accelerometer.was_gesture('shake'):
        steps += 1
    if button_a.was_pressed():
        display.scroll(str(steps))
    sleep(100)
```

## Project 9: Rock Paper Scissors

**What you'll learn:** Random selection, images

### Description
Shake to randomly select rock, paper, or scissors.

### MakeCode Blocks
1. On shake:
   - Set `choice` to random 0 to 2
   - If choice = 0: show icon rock
   - If choice = 1: show icon scissors
   - If choice = 2: show icon paper

### Python Code
```python
from microbit import *
import random

ROCK = Image("00000:09990:09990:09990:00000")
PAPER = Image("99999:90009:90009:90009:99999")
SCISSORS = Image("90009:09090:00900:09090:90009")

choices = [ROCK, PAPER, SCISSORS]

while True:
    if accelerometer.was_gesture('shake'):
        choice = random.choice(choices)
        display.show(choice)
    sleep(100)
```

## Project 10: Musical Buttons

**What you'll learn:** Sound/music output

### Description
Play different tones when buttons are pressed.

### MakeCode Blocks
1. On button A pressed:
   - Play tone `Middle C` for `1 beat`
2. On button B pressed:
   - Play tone `Middle E` for `1 beat`

### Python Code
```python
from microbit import *
import music

while True:
    if button_a.was_pressed():
        music.pitch(262, 500)  # Middle C
    if button_b.was_pressed():
        music.pitch(330, 500)  # Middle E
    sleep(100)
```

## Challenge Extensions

Once you've completed these projects, try these challenges:

1. **Combine projects** - Make a device that does different things based on button presses
2. **Add features** - Enhance existing projects with new functionality
3. **Create patterns** - Design custom LED patterns and animations
4. **Make it interactive** - Use multiple inputs for more complex behavior

## Tips for Building Projects

- Start with simple versions and add features gradually
- Test each new feature before adding the next one
- Save different versions as you go
- Comment your code to remember what each part does
- Share your creations with friends and family!
