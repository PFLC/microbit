# Name Badge

Create a scrolling name badge that displays your name on the LED screen.

## What You'll Learn
- Text scrolling
- Infinite loops
- Basic display functions
- Customizing text speed

## Hardware Required
- 1× BBC micro:bit
- 1× USB cable
- Optional: Battery pack for wearing as a badge

## How It Works

This program continuously scrolls your name (or any message) across the LED display, perfect for wearing as a digital name badge at events!

## Python Code

```python
from microbit import *

# Change this to your name!
my_name = "Your Name"

while True:
    display.scroll(my_name)
```

## MakeCode Blocks

1. Go to https://makecode.microbit.org/
2. Create a new project named "Name Badge"
3. Inside the `forever` block, add:
   - `show string` "Your Name"

## Step-by-Step Instructions

### Using Python:
1. Open https://python.microbit.org/
2. Replace the code with the Python code above
3. Change `"Your Name"` to your actual name
4. Click "Download"
5. Copy the .hex file to your MICROBIT drive
6. Watch your name scroll!

## Customization Ideas

### Add Delay Between Scrolls
```python
from microbit import *

my_name = "Alice"

while True:
    display.scroll(my_name)
    sleep(1000)  # 1 second pause before repeating
```

### Scroll Slower
```python
from microbit import *

while True:
    display.scroll("Slow Mo", delay=200)  # Default is 150
```

### Multiple Lines
```python
from microbit import *

name = "Alice"
role = "Maker"

while True:
    display.scroll(name)
    display.scroll(role)
    sleep(500)
```

### Add Icons
```python
from microbit import *

while True:
    display.show(Image.HAPPY)
    sleep(500)
    display.scroll("Alice")
    sleep(500)
```

### Interactive Badge
```python
from microbit import *

name = "Alice"
fact = "I love coding!"

while True:
    display.scroll(name)
    if button_a.was_pressed():
        display.scroll(fact)
    sleep(100)
```

### Different Messages for Each Button
```python
from microbit import *

name = "Alice"
hobby = "Robotics"
age = "12"

while True:
    display.scroll(name)
    
    if button_a.was_pressed():
        display.scroll("Age: " + age)
    
    if button_b.was_pressed():
        display.scroll("Hobby: " + hobby)
    
    sleep(100)
```

## Challenges

1. **Temperature Badge**: Display your name, then show temperature when button pressed
2. **Countdown Badge**: Show name and a countdown timer
3. **Multi-Language**: Show name in different languages
4. **Secret Message**: Press both buttons for a secret message

## Physical Badge Ideas

### Make It Wearable
- Use battery pack for power
- Attach to lanyard or clip
- Put in clear plastic case
- Wear at coding club or science fair

### Badge Holder
Materials needed:
- Cardboard or foam board
- Clear plastic sheet
- String or lanyard
- Tape or glue

Steps:
1. Cut cardboard to size (larger than micro:bit)
2. Cut window for LED display
3. Secure micro:bit behind window
4. Attach string/lanyard
5. Add decorations!

## Extensions

### Workshop Ice Breaker
Perfect for:
- First day of class
- Coding club meetings
- Science fairs
- School events

Everyone makes their own personalized badge!

### Badge Contest
Categories:
- Most creative message
- Best use of icons
- Coolest animation
- Funniest badge

## Troubleshooting

**Problem:** Name scrolls too fast
- **Solution:** Add `delay` parameter: `display.scroll("Name", delay=200)`

**Problem:** Want name to stay visible longer
- **Solution:** Add `sleep()` after scrolling: `sleep(1000)`

**Problem:** Text is cut off
- **Solution:** Check spelling, make sure string is complete

## Learning Objectives

After completing this project:
- ✅ Understand text scrolling
- ✅ Know how to use variables for text
- ✅ Can customize scrolling speed
- ✅ Understand infinite loops
- ✅ Can add user interaction

## Next Steps

Try these related projects:
- [Heart Beat](heart-beat.md) - Add animation
- [Button Counter](../beginner/README.md#project-2-button-counter) - Add interaction
- [Temperature Display](../beginner/README.md#project-5-temperature-display) - Add sensors

---

**Difficulty:** ⭐☆☆☆☆ (Beginner)  
**Time:** 5 minutes  
**Age:** 7+
