# Getting Started with micro:bit

## What You'll Need

### Hardware
- BBC micro:bit board (v1 or v2)
- Micro USB cable
- Battery pack (optional, for portable projects)
- Computer (Windows, Mac, or Linux)

### Software
- Web browser (Chrome, Firefox, Edge, or Safari)
- Internet connection (for online editors)

## Setting Up Your micro:bit

### Step 1: Unpack Your micro:bit
Your micro:bit comes with:
- The micro:bit board
- USB cable
- Battery holder (sometimes included)

### Step 2: Connect to Computer
1. Connect the micro USB end of the cable to your micro:bit
2. Connect the other end to your computer's USB port
3. The micro:bit will power on and show a scrolling pattern

### Step 3: Choose Your Editor

#### Option 1: MakeCode (Recommended for Beginners)
- Visit: https://makecode.microbit.org/
- Block-based or JavaScript programming
- No installation required
- Works in your web browser

#### Option 2: Python Editor
- Visit: https://python.microbit.org/
- Text-based Python programming
- Great for learning Python
- Works in your web browser

#### Option 3: Mu Editor (Offline Python)
- Download from: https://codewith.mu/
- Install on your computer
- Works offline
- Includes REPL for interactive coding

## Your First Program: Hello World

### Using MakeCode

1. Go to https://makecode.microbit.org/
2. Click "New Project"
3. Name your project "Hello World"
4. You'll see two blocks already there:
   - `on start` - runs once when the micro:bit starts
   - `forever` - runs continuously

5. From the "Basic" menu, drag a "show string" block into the `on start` block
6. Change the text to "Hello World"
7. Click the "Download" button
8. Save the .hex file to your computer
9. Copy the .hex file to the MICROBIT drive
10. Watch your micro:bit display "Hello World"!

### Using Python

1. Go to https://python.microbit.org/
2. Replace the code with:

```python
from microbit import *

display.scroll("Hello World")
```

3. Click "Download"
4. Save the .hex file
5. Copy it to your MICROBIT drive
6. Your micro:bit will display "Hello World"!

## Understanding the micro:bit Hardware

### LED Display
- 5×5 grid of red LEDs
- Can show letters, numbers, and patterns
- Each LED can be controlled individually

### Buttons
- Button A (left)
- Button B (right)
- Both buttons can be pressed together

### Sensors
- **Accelerometer** - detects movement and tilt
- **Compass** - detects magnetic north
- **Light sensor** - uses LED display to detect light
- **Temperature sensor** - measures temperature

### Radio
- Can communicate with other micro:bits
- Range of about 70 meters

### GPIO Pins (Edge Connector)
- 25 pins for connecting external devices
- Can be used for inputs and outputs
- Allows expansion with accessories

## Common First Projects

### 1. Smiley Face
Display a happy face when button A is pressed, sad face when button B is pressed.

### 2. Name Badge
Scroll your name across the LED display continuously.

### 3. Dice
Shake the micro:bit to roll a dice and display a random number.

### 4. Temperature Display
Show the current temperature when button A is pressed.

## Tips for Success

1. **Save your work often** - Download your .hex files regularly
2. **Experiment** - Don't be afraid to try new things
3. **Read error messages** - They help you find problems
4. **Start simple** - Build complexity gradually
5. **Test frequently** - Upload to your micro:bit often to see results

## Next Steps

Once you're comfortable with the basics:
1. Try the beginner projects in the `projects/beginner` folder
2. Complete the exercises in the `exercises` folder
3. Explore sensors and more advanced features
4. Share your projects with others!

## Troubleshooting

If your micro:bit doesn't work:
1. Check the USB connection
2. Try a different USB cable
3. Make sure the .hex file copied completely
4. Press the reset button on the back
5. Check the troubleshooting guide in `docs/troubleshooting.md`

Happy coding! 🚀
