# Workshop Exercises

These hands-on exercises are designed for classroom workshops and group learning sessions. Each exercise builds skills progressively.

## Exercise Set 1: First Steps (30 minutes)

### Exercise 1.1: Hello LED
**Time:** 5 minutes  
**Difficulty:** Beginner

**Task:** Make a single LED light up in the center of the display.

**Hints:**
- Use `display.set_pixel(x, y, brightness)`
- Center is at coordinates (2, 2)
- Brightness is 0-9 (0=off, 9=brightest)

**Expected Outcome:** Middle LED glows bright.

---

### Exercise 1.2: LED Pattern
**Time:** 10 minutes  
**Difficulty:** Beginner

**Task:** Create a cross pattern on the LED display.

**Hints:**
- You'll need to light up 5 LEDs
- Think about which coordinates form a cross
- The cross should go through the center

**Expected Outcome:** A cross shape appears on the display.

---

### Exercise 1.3: Blinking LED
**Time:** 10 minutes  
**Difficulty:** Beginner

**Task:** Make the center LED blink on and off every second.

**Hints:**
- Use `sleep()` to create delays
- Turn LED on, wait, turn LED off, wait, repeat
- Put this in a `while True:` loop

**Expected Outcome:** Center LED blinks continuously.

---

### Exercise 1.4: Animation
**Time:** 5 minutes  
**Difficulty:** Beginner

**Task:** Create an animation that shows a dot moving from left to right across the middle row.

**Hints:**
- Use a loop to change the x coordinate
- y coordinate stays at 2 (middle row)
- Clear the display between each frame

**Expected Outcome:** A dot moves smoothly across the screen.

---

## Exercise Set 2: Interaction (45 minutes)

### Exercise 2.1: Button Press Counter
**Time:** 10 minutes  
**Difficulty:** Beginner

**Task:** Count button A presses and show the count on the display.

**Hints:**
- Create a variable to store the count
- Check if button was pressed
- Increment the count
- Display the number

**Solution Template:**
```python
from microbit import *

count = 0

while True:
    if button_a.was_pressed():
        # Your code here
    sleep(100)
```

---

### Exercise 2.2: Two-Button Control
**Time:** 10 minutes  
**Difficulty:** Beginner

**Task:** Button A increases a number, Button B decreases it. Display the current number.

**Hints:**
- One variable for the number
- Two if statements for the buttons
- Display the number each time it changes

**Expected Outcome:** Number goes up with A, down with B.

---

### Exercise 2.3: Button Hold Detector
**Time:** 15 minutes  
**Difficulty:** Intermediate

**Task:** Detect if button A is held down for more than 2 seconds. Show different messages for short press vs long press.

**Hints:**
- Use `button_a.is_pressed()` to check if currently pressed
- Use `running_time()` to track how long it's pressed
- Record the time when button is first pressed

**Expected Outcome:** "Short" for quick press, "Long" for hold.

---

### Exercise 2.4: Both Buttons
**Time:** 10 minutes  
**Difficulty:** Beginner

**Task:** Display different images for: A pressed, B pressed, both A+B pressed, neither pressed.

**Hints:**
- Check both buttons in each iteration
- Use if/elif/else structure
- Test with `button_a.is_pressed() and button_b.is_pressed()`

**Expected Outcome:** Four different displays based on button state.

---

## Exercise Set 3: Sensors (60 minutes)

### Exercise 3.1: Temperature Reader
**Time:** 10 minutes  
**Difficulty:** Beginner

**Task:** Display the current temperature when button A is pressed.

**Hints:**
- Use `temperature()` function
- Convert to string for display
- Add "C" to show it's Celsius

**Expected Outcome:** Shows temperature in degrees.

---

### Exercise 3.2: Hot/Cold Indicator
**Time:** 15 minutes  
**Difficulty:** Beginner

**Task:** Continuously monitor temperature. Show a flame icon when hot (>25°C), snowflake when cold (<18°C), smiley face when comfortable.

**Hints:**
- Use if/elif/else with temperature comparisons
- Built-in icons: `Image.SQUARE`, `Image.HEART`, `Image.HAPPY`
- Update display continuously

**Expected Outcome:** Display changes with temperature.

---

### Exercise 3.3: Tilt Detector
**Time:** 15 minutes  
**Difficulty:** Intermediate

**Task:** Show an arrow pointing in the direction the micro:bit is tilted.

**Hints:**
- Read `accelerometer.get_x()` and `accelerometer.get_y()`
- Use thresholds (e.g., >300 or <-300) to detect tilt
- Use arrow images: `Image.ARROW_N`, `Image.ARROW_E`, etc.

**Expected Outcome:** Arrow follows tilt direction.

---

### Exercise 3.4: Light Meter
**Time:** 10 minutes  
**Difficulty:** Beginner

**Task:** Display a bar graph showing light level (0-255 as 0-5 bars).

**Hints:**
- Use `display.read_light_level()` (0-255)
- Divide by 51 to get 0-5 range
- Display that many bars/pixels in a row

**Expected Outcome:** Bar graph shows brightness.

---

### Exercise 3.5: Shake Counter
**Time:** 10 minutes  
**Difficulty:** Beginner

**Task:** Count how many times the micro:bit is shaken.

**Hints:**
- Use `accelerometer.was_gesture('shake')`
- Increment counter each shake
- Display count on button press

**Expected Outcome:** Shake count displayed on demand.

---

## Exercise Set 4: Games (90 minutes)

### Exercise 4.1: Simple Dice
**Time:** 15 minutes  
**Difficulty:** Beginner

**Task:** Create a dice that shows a random number (1-6) when shaken.

**Hints:**
- Import random module
- Use `random.randint(1, 6)`
- Detect shake gesture
- Display the number

**Expected Outcome:** Random number appears on shake.

---

### Exercise 4.2: Coin Flip
**Time:** 10 minutes  
**Difficulty:** Beginner

**Task:** Flip a coin (Heads/Tails) when button A is pressed.

**Hints:**
- Random choice between 0 and 1
- Display "H" for heads, "T" for tails
- Could also use images

**Expected Outcome:** Random H or T on button press.

---

### Exercise 4.3: Reaction Game
**Time:** 20 minutes  
**Difficulty:** Intermediate

**Task:** After a random delay, show an image. Time how fast the player presses button A.

**Hints:**
- Random delay before signal
- Record start time with `running_time()`
- Wait for button press
- Calculate difference
- Display reaction time

**Expected Outcome:** Shows reaction time in milliseconds.

---

### Exercise 4.4: Catch the Dot
**Time:** 25 minutes  
**Difficulty:** Intermediate

**Task:** A dot moves randomly. Player tilts to move their dot. Score when they overlap.

**Hints:**
- Two sets of coordinates (player and target)
- Read accelerometer to move player
- Check if coordinates match
- Keep score

**Expected Outcome:** Tilt-controlled dot-catching game.

---

### Exercise 4.5: Memory Game
**Time:** 20 minutes  
**Difficulty:** Advanced

**Task:** Show a sequence of LEDs. Player must repeat by pressing buttons in correct order.

**Hints:**
- Store sequence in a list
- Display sequence one LED at a time
- Wait for button inputs
- Check if input matches sequence
- Increase difficulty each round

**Expected Outcome:** Simon-says style memory game.

---

## Exercise Set 5: Communication (60 minutes)

### Exercise 5.1: Radio Hello
**Time:** 15 minutes  
**Difficulty:** Beginner  
**Required:** 2 micro:bits

**Task:** Send "Hello" from one micro:bit to another when button A is pressed.

**Hints:**
- Turn on radio with `radio.on()`
- Set same group/channel
- Use `radio.send()` and `radio.receive()`
- Display received messages

**Expected Outcome:** Message appears on receiving micro:bit.

---

### Exercise 5.2: Wireless Doorbell
**Time:** 15 minutes  
**Difficulty:** Beginner  
**Required:** 2 micro:bits

**Task:** One micro:bit is the button, one is the bell. Press A on button to ring bell.

**Hints:**
- Sender: button press triggers radio send
- Receiver: displays icon and plays sound on receive
- Use music.play() for sound

**Expected Outcome:** Remote doorbell system.

---

### Exercise 5.3: Chat System
**Time:** 20 minutes  
**Difficulty:** Intermediate  
**Required:** 2 micro:bits

**Task:** Create a simple chat with predefined messages selectable by buttons.

**Hints:**
- Array of messages
- Button A cycles through messages
- Button B sends current message
- Display received messages

**Expected Outcome:** Two-way message system.

---

### Exercise 5.4: Score Keeper
**Time:** 10 minutes  
**Difficulty:** Intermediate  
**Required:** 2 micro:bits

**Task:** Keep track of scores for two players. Each player's micro:bit shows their score.

**Hints:**
- Button A increments score
- Button B decrements score
- Broadcast score changes
- Display both scores

**Expected Outcome:** Synchronized scoreboard.

---

## Challenge Exercises

### Challenge 1: Ultimate Reaction Timer
Combine multiple concepts: random delays, button timing, best score tracking, and radio to compete with a friend.

### Challenge 2: Remote Control Car
Use one micro:bit as a controller (tilt-based) to send commands to another micro:bit connected to motors.

### Challenge 3: Weather Dashboard
Collect temperature from multiple micro:bits and display average, min, and max.

### Challenge 4: Treasure Hunt
Create a hot/cold indicator using radio signal strength to find a hidden micro:bit.

## Workshop Tips for Teachers

1. **Group Work**: Pair students for radio exercises
2. **Debugging**: Teach students to use `display.scroll()` to debug values
3. **Progression**: Ensure students complete basics before advanced exercises
4. **Time Management**: Adjust time allocations based on class pace
5. **Extensions**: Have bonus challenges for fast learners
6. **Sharing**: Have students demonstrate their solutions

## Assessment Rubric

### Beginner Level
- [ ] Can create basic display patterns
- [ ] Understands button inputs
- [ ] Can use loops and delays
- [ ] Creates simple animations

### Intermediate Level
- [ ] Uses variables effectively
- [ ] Reads and responds to sensors
- [ ] Implements conditional logic
- [ ] Debugs own code

### Advanced Level
- [ ] Combines multiple concepts
- [ ] Creates original projects
- [ ] Optimizes code
- [ ] Helps others learn

Good luck with your workshop! 🎓
