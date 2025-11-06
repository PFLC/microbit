# Smiley Button

Display a smiley face when button A is pressed, sad face when button B is pressed.

## What You'll Learn
- Button inputs
- Conditional statements (if/else)
- Displaying icons
- User interaction

## Hardware Required
- 1× BBC micro:bit
- 1× USB cable

## How It Works

This program listens for button presses and displays different faces based on which button you press. It's a simple way to learn about input and output!

## Python Code

```python
from microbit import *

while True:
    if button_a.is_pressed():
        display.show(Image.HAPPY)
    elif button_b.is_pressed():
        display.show(Image.SAD)
    else:
        display.clear()
    
    sleep(100)
```

## Alternative Version (Using was_pressed)

```python
from microbit import *

# Start with clear display
display.clear()

while True:
    if button_a.was_pressed():
        display.show(Image.HAPPY)
    
    if button_b.was_pressed():
        display.show(Image.SAD)
    
    sleep(100)
```

## MakeCode Blocks

1. Go to https://makecode.microbit.org/
2. Add block: `on button A pressed`
   - Inside: `show icon` (happy face)
3. Add block: `on button B pressed`
   - Inside: `show icon` (sad face)

## Understanding the Code

### is_pressed() vs was_pressed()

**is_pressed()** - True while button is held down
```python
if button_a.is_pressed():
    # Runs continuously while holding button
```

**was_pressed()** - True once per press
```python
if button_a.was_pressed():
    # Runs once when button is clicked
```

Choose based on your needs:
- Use `is_pressed()` for continuous actions
- Use `was_pressed()` for toggle/count actions

## Customization Ideas

### More Faces
```python
from microbit import *

while True:
    if button_a.is_pressed():
        display.show(Image.HAPPY)
    elif button_b.is_pressed():
        display.show(Image.SAD)
    elif button_a.is_pressed() and button_b.is_pressed():
        display.show(Image.SURPRISED)  # Both buttons!
    else:
        display.clear()
    
    sleep(100)
```

### Emoji Selector
```python
from microbit import *

faces = [
    Image.HAPPY,
    Image.SAD,
    Image.SURPRISED,
    Image.SILLY,
    Image.ANGRY,
    Image.ASLEEP,
    Image.CONFUSED
]

current = 0

while True:
    # Change face
    if button_a.was_pressed():
        current = (current + 1) % len(faces)
        display.show(faces[current])
    
    # Reset to happy
    if button_b.was_pressed():
        current = 0
        display.show(faces[current])
    
    sleep(100)
```

### Mood Tracker
```python
from microbit import *

happy_count = 0
sad_count = 0

while True:
    if button_a.was_pressed():
        happy_count += 1
        display.show(Image.HAPPY)
        sleep(1000)
        display.scroll(str(happy_count))
    
    if button_b.was_pressed():
        sad_count += 1
        display.show(Image.SAD)
        sleep(1000)
        display.scroll(str(sad_count))
    
    sleep(100)
```

### Animated Faces
```python
from microbit import *

def happy_animation():
    display.show(Image.SMILE)
    sleep(200)
    display.show(Image.HAPPY)
    sleep(200)

def sad_animation():
    display.show(Image.CONFUSED)
    sleep(200)
    display.show(Image.SAD)
    sleep(200)

while True:
    if button_a.is_pressed():
        happy_animation()
    elif button_b.is_pressed():
        sad_animation()
    else:
        display.clear()
    
    sleep(100)
```

### Random Emotion
```python
from microbit import *
import random

emotions = [
    Image.HAPPY,
    Image.SAD,
    Image.ANGRY,
    Image.SURPRISED,
    Image.SILLY,
    Image.CONFUSED
]

while True:
    if button_a.was_pressed():
        emotion = random.choice(emotions)
        display.show(emotion)
    
    if button_b.was_pressed():
        display.clear()
    
    sleep(100)
```

## Challenges

1. **Three Buttons**: Use button A, B, and logo touch (v2) for three different faces
2. **Face Timer**: Show happy face for 5 seconds, then automatically clear
3. **Opposite Day**: Button A shows sad, Button B shows happy
4. **Gradient**: Create custom faces with different brightness levels
5. **Shake to Clear**: Shake to clear the display

## Game Ideas

### Emotion Mirror
Two players:
- Player 1 presses a button
- Player 2 tries to match the emotion on their micro:bit
- Take turns and have fun!

### Quick Draw
- Program shows random face
- First person to press matching button wins
- Keep score!

## Educational Uses

### Mood Check-In
In classroom:
- Start of day mood check
- Students press button matching their mood
- Teacher can see general class mood

### Communication Tool
For non-verbal communication:
- Happy = Yes
- Sad = No
- Other faces for different needs

## Code Explanation

Let's break down the main code:

```python
from microbit import *  # Import micro:bit library

while True:  # Loop forever
    if button_a.is_pressed():  # Check if button A pressed
        display.show(Image.HAPPY)  # Show happy face
    elif button_b.is_pressed():  # Otherwise, check button B
        display.show(Image.SAD)  # Show sad face
    else:  # If no buttons pressed
        display.clear()  # Clear display
    
    sleep(100)  # Wait 0.1 seconds before checking again
```

## Troubleshooting

**Problem:** Faces appear even without pressing buttons
- **Solution:** Check wiring, buttons might be stuck or shorted

**Problem:** Need to press hard for button to work
- **Solution:** This is normal! Press firmly on the button

**Problem:** Display doesn't clear
- **Solution:** Make sure `else: display.clear()` is included

**Problem:** Both buttons show same face
- **Solution:** Check your if/elif logic and button names

## Learning Objectives

After completing this project:
- ✅ Understand button inputs
- ✅ Use conditional statements (if/elif/else)
- ✅ Display built-in images
- ✅ Create interactive programs
- ✅ Understand program flow

## Next Steps

Try these related projects:
- [Button Counter](../beginner/README.md#project-2-button-counter) - Count button presses
- [Rock Paper Scissors](../beginner/README.md#project-9-rock-paper-scissors) - Game with buttons
- [Name Badge](name-badge.md) - Add text to your buttons

## Fun Facts

😊 The human face can make over 7,000 different expressions!

🤖 Emojis were first created in Japan in 1999.

💡 The micro:bit can display simple emotions, just like our faces do!

---

**Difficulty:** ⭐☆☆☆☆ (Beginner)  
**Time:** 5-10 minutes  
**Age:** 7+
