# Troubleshooting Guide

Common issues and solutions when working with micro:bit.

## Hardware Issues

### micro:bit Not Recognized by Computer

**Symptoms:**
- MICROBIT drive doesn't appear
- No response when connected via USB
- Computer doesn't detect device

**Solutions:**
1. **Try a Different USB Cable**
   - Some cables are power-only and don't transfer data
   - Use a cable that supports data transfer
   - Try the cable that came with your micro:bit

2. **Check USB Port**
   - Try a different USB port on your computer
   - Front panel ports sometimes have issues; try rear ports
   - Avoid USB hubs; connect directly to computer

3. **Update Drivers (Windows)**
   - Visit [micro:bit Windows driver page](https://support.microbit.org/support/solutions/articles/19000105428)
   - Download and install the Windows driver
   - Restart computer after installation

4. **Check Connection**
   - Ensure USB cable is firmly connected
   - Look for LED indicator on micro:bit (should light up)
   - Try disconnecting and reconnecting

5. **Reset micro:bit**
   - Press the reset button on the back
   - Unplug and replug the USB cable

---

### Program Not Running After Upload

**Symptoms:**
- File copied successfully but nothing happens
- micro:bit shows error pattern
- Program worked before but not now

**Solutions:**
1. **Check Error Pattern**
   - If LEDs show a sad face or error code, check micro:bit error codes
   - Error codes: https://support.microbit.org/support/solutions/articles/19000016969

2. **Verify .hex File**
   - Make sure you downloaded the complete .hex file
   - File size should be reasonable (typically 500KB-700KB)
   - Don't rename the file after downloading

3. **Complete Transfer**
   - Wait for the LED on back to stop flashing
   - Don't unplug during file transfer
   - Let the micro:bit reset on its own

4. **Check Battery**
   - If using battery power, ensure batteries are fresh
   - Check battery connection
   - Try USB power to eliminate battery issues

5. **Re-download Program**
   - Sometimes files get corrupted
   - Delete old .hex file and download fresh copy
   - Try a simple test program first

---

### LED Display Issues

**Symptoms:**
- Some LEDs don't light up
- Display is dim
- Flickering display

**Solutions:**
1. **Check Power**
   - Insufficient power can cause dim LEDs
   - Try USB power instead of batteries
   - Replace batteries if using battery pack

2. **Brightness Settings**
   - LEDs have brightness levels 0-9
   - Check your code uses appropriate brightness
   - `display.set_pixel(x, y, 9)` for maximum brightness

3. **Physical Damage**
   - Check for visible damage to LED matrix
   - If LEDs are physically damaged, contact support
   - Handle micro:bit carefully to avoid damage

---

### Button Not Responding

**Symptoms:**
- Button presses not detected
- Inconsistent button behavior
- Stuck button

**Solutions:**
1. **Press Firmly**
   - Buttons need firm press to activate
   - Press directly on the button, not the label
   - Hold for a moment if using `is_pressed()`

2. **Use Correct Detection Method**
   ```python
   # For momentary detection
   if button_a.was_pressed():
   
   # For current state
   if button_a.is_pressed():
   
   # Get press count
   presses = button_a.get_presses()
   ```

3. **Debouncing**
   - Add small delays to avoid double-presses
   ```python
   if button_a.was_pressed():
       # Do something
       sleep(200)  # 200ms delay
   ```

4. **Physical Issue**
   - Check if button is stuck or damaged
   - Clean around button with dry cloth
   - Contact support if button is broken

---

## Software/Programming Issues

### Code Doesn't Work as Expected

**Symptoms:**
- Program runs but behaves incorrectly
- Unexpected output
- Logic errors

**Solutions:**
1. **Debug with Display**
   ```python
   # Show variable values
   display.scroll(str(my_variable))
   
   # Show checkpoint
   display.show(Image.HAPPY)  # Reached this point
   ```

2. **Check Indentation**
   - Python is sensitive to indentation
   - Use consistent spaces (usually 4)
   - Make sure loops and if statements are properly indented

3. **Verify Logic**
   - Walk through code step by step
   - Check if conditions are correct
   - Test one feature at a time

4. **Use REPL (with Mu Editor)**
   - Connect with Mu Editor
   - Click "REPL" button
   - Test commands interactively
   - See immediate results and error messages

5. **Start Simple**
   - Comment out complex parts
   - Test basic functionality first
   - Add features one at a time

---

### Import Errors

**Symptoms:**
- "ImportError" or "ModuleNotFoundError"
- `from microbit import *` fails

**Solutions:**
1. **Check Editor**
   - Make sure you're using micro:bit compatible editor
   - MakeCode Python or Mu Editor recommended
   - Online Python editor: https://python.microbit.org/

2. **Correct Import Statement**
   ```python
   # Correct
   from microbit import *
   
   # Also correct
   import microbit
   import music
   import radio
   ```

3. **Editor-Specific Modules**
   - Some modules only work in specific editors
   - `radio` works in Python but not MakeCode blocks
   - Check module compatibility

---

### Out of Memory

**Symptoms:**
- MemoryError
- Program stops unexpectedly
- Can't create more variables

**Solutions:**
1. **Reduce Variable Usage**
   - Delete variables when no longer needed
   - Use shorter variable names
   - Reuse variables where possible

2. **Optimize Lists**
   - Don't create huge lists
   - Limit list size
   ```python
   # Limit list length
   if len(my_list) > 100:
       my_list.pop(0)  # Remove oldest
   ```

3. **Avoid String Concatenation in Loops**
   ```python
   # Bad (creates many strings)
   text = ""
   for i in range(100):
       text += str(i)
   
   # Better
   for i in range(100):
       display.scroll(str(i))
   ```

4. **Use Generators**
   - For large sequences, use generators instead of lists
   - They use less memory

---

### Radio Communication Problems

**Symptoms:**
- Messages not received
- Intermittent communication
- Wrong messages received

**Solutions:**
1. **Same Channel/Group**
   ```python
   # Both micro:bits must use same settings
   radio.config(channel=7, group=1)
   ```

2. **Turn On Radio**
   ```python
   # Must call this on both sender and receiver
   radio.on()
   ```

3. **Check Range**
   - Maximum range ~70 meters in open space
   - Walls and obstacles reduce range
   - Keep micro:bits closer for testing

4. **Check Receiving Code**
   ```python
   # Continuous checking
   while True:
       message = radio.receive()
       if message:
           display.scroll(message)
       sleep(100)
   ```

5. **Increase Power**
   ```python
   # Power level 0-7, 7 is maximum
   radio.config(power=7)
   ```

---

### Sensor Reading Issues

**Symptoms:**
- Accelerometer gives wrong values
- Compass points wrong direction
- Temperature seems incorrect

**Solutions:**
1. **Calibrate Compass**
   ```python
   # Must calibrate compass before first use
   compass.calibrate()  # Follow on-screen instructions
   ```

2. **Understand Coordinate System**
   - X-axis: left (-) to right (+)
   - Y-axis: back (-) to front (+)
   - Z-axis: down (-) to up (+)
   - Values in milli-g (1g ≈ 1000)

3. **Temperature Offset**
   - micro:bit CPU generates heat
   - Reading may be 2-4°C higher than ambient
   - Account for this in calculations

4. **Averaging Readings**
   ```python
   # Take multiple readings for accuracy
   total = 0
   for i in range(10):
       total += temperature()
       sleep(100)
   average = total // 10
   ```

---

## Common Error Codes

### Error 020: Micro:bit ran out of memory
- See "Out of Memory" section above
- Reduce variable usage
- Optimize code

### Error 040: Invalid .hex file
- Re-download the program
- Don't modify .hex file
- Try different browser

### Error 050: Hardware configuration error
- Reset micro:bit
- Check for physical damage
- Try re-flashing firmware

---

## Getting More Help

If these solutions don't work:

1. **Official Support**
   - Visit: https://support.microbit.org/
   - Search knowledge base
   - Submit support ticket

2. **Community Forum**
   - https://community.microbit.org/
   - Ask questions
   - Search existing discussions

3. **Stack Overflow**
   - Tag: `micro-bit`
   - Search existing answers
   - Post new questions with code examples

4. **Documentation**
   - MicroPython: https://microbit-micropython.readthedocs.io/
   - MakeCode: https://makecode.microbit.org/reference

---

## Prevention Tips

1. **Save Work Regularly**
   - Download .hex files with descriptive names
   - Keep backup copies
   - Use version control for larger projects

2. **Test Incrementally**
   - Don't write all code at once
   - Test each feature as you add it
   - Easier to identify what broke

3. **Comment Your Code**
   - Explain complex sections
   - Note what works and what doesn't
   - Help future you understand

4. **Handle Errors Gracefully**
   ```python
   try:
       # Code that might fail
       result = something()
   except:
       display.show(Image.SAD)
   ```

5. **Keep Firmware Updated**
   - Check for firmware updates periodically
   - Follow official update procedures

Good luck, and happy debugging! 🔧
