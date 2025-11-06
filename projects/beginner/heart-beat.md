# Heart Beat Animation

A simple animated heart that beats on your micro:bit's LED display.

## What You'll Learn
- Creating animations
- Using the LED display
- Working with delays
- Infinite loops

## Hardware Required
- 1× BBC micro:bit
- 1× USB cable (for programming)
- Optional: Battery pack for portable use

## How It Works

This program creates a beating heart animation by alternating between two heart images:
1. A large heart (fully expanded)
2. A small heart (contracted)

The animation loops forever, creating a heartbeat effect.

## MakeCode Version

### Blocks
1. Go to https://makecode.microbit.org/
2. Create a new project named "Heart Beat"
3. Delete the default blocks
4. Add a `forever` block
5. Inside the forever block, add:
   - `show icon` (select large heart)
   - `pause` (500 ms)
   - `show icon` (select small heart)
   - `pause` (500 ms)

### JavaScript Code
```javascript
basic.forever(function () {
    basic.showIcon(IconNames.Heart)
    basic.pause(500)
    basic.showIcon(IconNames.SmallHeart)
    basic.pause(500)
})
```

## Python Version

```python
from microbit import *

while True:
    display.show(Image.HEART)
    sleep(500)
    display.show(Image.HEART_SMALL)
    sleep(500)
```

## Step-by-Step Instructions

### Using MakeCode:
1. Open https://makecode.microbit.org/ in your browser
2. Click "New Project"
3. Name it "Heart Beat"
4. Drag the blocks as described above
5. Click "Download" to save the .hex file
6. Connect your micro:bit via USB
7. Copy the .hex file to the MICROBIT drive
8. Watch your micro:bit's heart beat!

### Using Python:
1. Open https://python.microbit.org/ in your browser
2. Delete the existing code
3. Copy and paste the Python code above
4. Click "Download" to save the .hex file
5. Connect your micro:bit via USB
6. Copy the .hex file to the MICROBIT drive
7. Watch your micro:bit's heart beat!

## Customization Ideas

### Change the Speed
Modify the pause/sleep duration:
- Faster beat: Use 250 ms instead of 500 ms
- Slower beat: Use 1000 ms instead of 500 ms

```python
# Faster heartbeat
from microbit import *

while True:
    display.show(Image.HEART)
    sleep(250)
    display.show(Image.HEART_SMALL)
    sleep(250)
```

### Add More Frames
Create a smoother animation with custom images:

```python
from microbit import *

# Define custom heart frames
frame1 = Image("09090:99999:99999:09990:00900")
frame2 = Image("00000:09090:09990:00900:00000")

while True:
    display.show(Image.HEART)
    sleep(300)
    display.show(frame1)
    sleep(200)
    display.show(Image.HEART_SMALL)
    sleep(200)
    display.show(frame2)
    sleep(300)
```

### Make It Interactive
Add button control:

```python
from microbit import *

# Control with button A
while True:
    if button_a.is_pressed():
        display.show(Image.HEART)
        sleep(500)
        display.show(Image.HEART_SMALL)
        sleep(500)
    else:
        display.clear()
```

### Add Different Speeds
Use buttons to change speed:

```python
from microbit import *

speed = 500  # Default speed

while True:
    # Button A = faster
    if button_a.was_pressed():
        speed = max(100, speed - 100)
        display.scroll(str(speed))
    
    # Button B = slower
    if button_b.was_pressed():
        speed = min(1000, speed + 100)
        display.scroll(str(speed))
    
    # Animate heart
    display.show(Image.HEART)
    sleep(speed)
    display.show(Image.HEART_SMALL)
    sleep(speed)
```

## Challenges

1. **Triple Beat**: Make the heart beat three times, then pause
2. **Color Shift**: If using external RGB LEDs, change colors with each beat
3. **Sound**: Add a "thump" sound on each beat (micro:bit v2)
4. **Pulse Detection**: Connect a real pulse sensor and match the animation to your heartbeat

## Troubleshooting

**Problem:** Heart doesn't animate
- **Solution:** Check that both heart images are displaying
- Verify the pause/sleep times are present

**Problem:** Animation is too fast/slow
- **Solution:** Adjust the pause/sleep duration values

**Problem:** micro:bit shows error
- **Solution:** Check code for typos, re-download the .hex file

## Extension: Real Heartbeat Monitor

For advanced students, connect a pulse sensor:

```python
from microbit import *

def read_pulse():
    # Read from pulse sensor on pin0
    value = pin0.read_analog()
    # Detect heartbeat (simplified)
    return value > 512

last_beat = running_time()

while True:
    if read_pulse():
        # Beat detected
        current = running_time()
        if current - last_beat > 300:  # Debounce
            display.show(Image.HEART)
            sleep(100)
            display.show(Image.HEART_SMALL)
            last_beat = current
    sleep(10)
```

## Learning Objectives

After completing this project, you should understand:
- ✅ How to use the LED display
- ✅ How to create simple animations
- ✅ How to use delays/timing
- ✅ How to create infinite loops
- ✅ How to use built-in images

## Next Steps

Try these related projects:
- [Name Badge](../name-badge.md) - Scroll text
- [Dice](../dice.md) - Random numbers
- [Button Counter](../button-counter.md) - User input

## Share Your Creation!

Take a video of your beating heart and share it:
- Twitter: #microbit
- Instagram: @microbit_edu
- School coding club

## Credits

This is a classic beginner project adapted for the micro:bit workshop.

---

**Difficulty:** ⭐☆☆☆☆ (Beginner)  
**Time:** 5-10 minutes  
**Age:** 7+
