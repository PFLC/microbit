# Resources and References

A curated collection of useful resources for learning and teaching with micro:bit.

## Official Resources

### Documentation
- [micro:bit Website](https://microbit.org/) - Official homepage
- [micro:bit Technical Documentation](https://tech.microbit.org/) - Hardware specifications
- [MicroPython Documentation](https://microbit-micropython.readthedocs.io/) - Python API reference
- [MakeCode Documentation](https://makecode.microbit.org/reference) - Block and JavaScript reference

### Editors and Tools
- [MakeCode Editor](https://makecode.microbit.org/) - Block and JavaScript programming (online)
- [Python Editor](https://python.microbit.org/) - Browser-based Python editor
- [Mu Editor](https://codewith.mu/) - Desktop Python editor (offline)
- [micro:bit Educational Foundation](https://microbit.org/teach/) - Teaching resources

### Support
- [Support Portal](https://support.microbit.org/) - Official help and troubleshooting
- [Community Forum](https://community.microbit.org/) - Discussion forum
- [YouTube Channel](https://www.youtube.com/microbit) - Video tutorials

---

## Learning Platforms

### Interactive Tutorials
- [micro:bit Classroom](https://classroom.microbit.org/) - Curriculum-aligned lessons
- [Code Club micro:bit Projects](https://projects.raspberrypi.org/en/codeclub/microbit) - Structured projects
- [CS First micro:bit](https://csfirst.withgoogle.com/) - Google's computer science curriculum

### Online Courses
- [FutureLearn micro:bit Courses](https://www.futurelearn.com/courses/microbit) - Free online courses
- [micro:bit on Khan Academy](https://www.khanacademy.org/) - Programming fundamentals
- [Code.org micro:bit Activities](https://code.org/) - Hour of Code activities

### Video Tutorials
- [The Coding Train - micro:bit](https://thecodingtrain.com/) - Creative coding tutorials
- [Adafruit micro:bit Tutorials](https://learn.adafruit.com/category/micro-bit) - Hardware integration
- [SparkFun micro:bit Guides](https://learn.sparkfun.com/tutorials/tags/microbit) - Project tutorials

---

## Books and Publications

### Beginner Books
- "Getting Started with micro:bit" by Wolfram Donat
- "Learn to Program with micro:bit" by The Micro:bit Foundation
- "micro:bit in Wonderland" by The Micro:bit Foundation

### Advanced Books
- "Programming the BBC micro:bit" by Simon Monk
- "micro:bit IoT in C" by Parmeet Singh
- "Artificial Intelligence with micro:bit" by Radhika Ghosal

### Free E-books
- [micro:bit MicroPython Guide](https://microbit-micropython.readthedocs.io/) - Official guide
- [micro:bit User Guide](https://microbit.org/get-started/user-guide/) - Getting started

---

## Project Ideas

### Project Galleries
- [micro:bit Projects](https://microbit.org/projects/) - Official project gallery
- [Hackster.io micro:bit](https://www.hackster.io/microbit) - Community projects
- [Instructables micro:bit](https://www.instructables.com/circuits/microbit/) - DIY projects with instructions

### Inspiration
- [micro:bit Awards](https://microbit.org/do-your-bit/) - Award-winning projects
- [micro:bit Blog](https://microbit.org/news/) - Latest projects and news
- [Twitter #microbit](https://twitter.com/hashtag/microbit) - Community sharing

---

## Hardware and Accessories

### Official Accessories
- [micro:bit Go Bundle](https://microbit.org/buy/) - Starter kit
- [micro:bit Club Pack](https://microbit.org/buy/) - Classroom set
- Battery holders and USB cables

### Third-Party Add-ons
- **Kitronik** - Wide range of accessories and kits
- **SparkFun** - Electronics and breakout boards
- **Adafruit** - Sensors and components
- **Elecfreaks** - Robot kits and expansion boards
- **MonkMakes** - Educational electronics kits

### Recommended Accessories
- **Sensors:**
  - Ultrasonic distance sensor
  - PIR motion sensor
  - Soil moisture sensor
  - Sound sensor
  - Gas/air quality sensor

- **Outputs:**
  - Servo motors
  - DC motors with driver
  - RGB LED strips (NeoPixels)
  - OLED displays
  - Buzzers and speakers

- **Power:**
  - Battery packs (2xAAA or 3.7V LiPo)
  - USB power banks
  - Solar panels

- **Robotics:**
  - Robot chassis
  - Wheels and motors
  - Motor drivers (L298N)
  - Ultrasonic sensors

---

## Programming References

### Python (MicroPython)

#### Essential Modules
```python
from microbit import *  # Core functionality
import radio           # Radio communication
import music          # Sound and music
import speech         # Text-to-speech
import random         # Random numbers
import math           # Mathematical functions
```

#### Quick Reference
```python
# Display
display.show("A")
display.scroll("Hello")
display.set_pixel(x, y, brightness)
display.clear()

# Buttons
button_a.was_pressed()
button_a.is_pressed()
button_a.get_presses()

# Sensors
temperature()
accelerometer.get_x()
accelerometer.get_y()
accelerometer.get_z()
compass.heading()

# Pins
pin0.read_analog()     # 0-1023
pin0.write_analog(512)
pin0.read_digital()    # 0 or 1
pin0.write_digital(1)

# Radio
radio.on()
radio.send("message")
radio.receive()

# Music
music.play(music.NYAN)
music.pitch(440, 1000)
```

### JavaScript (MakeCode)

#### Common Blocks
- **Basic:** show string, show number, show icon
- **Input:** on button pressed, on shake
- **Loops:** forever, repeat, while
- **Logic:** if/then/else, and/or
- **Variables:** set, change
- **Math:** arithmetic, random
- **Radio:** send, receive

---

## Classroom Resources

### Lesson Plans
- [micro:bit Curriculum](https://microbit.org/teach/) - Complete curriculum
- [CS Unplugged](https://csunplugged.org/) - Computer science without computers
- [Barefoot Computing](https://www.barefootcomputing.org/) - Primary computing

### Assessment Tools
- [Computing at School Resources](https://www.computingatschool.org.uk/)
- [Digital Schoolhouse Worksheets](https://www.digitalschoolhouse.org.uk/)
- micro:bit Skills Builder Framework

### Workshop Materials
- [micro:bit Workshop Cards](https://microbit.org/teach/classroom-resources/)
- Printable reference sheets
- Student workbooks

---

## Community and Events

### Competitions
- [micro:bit Awards](https://microbit.org/do-your-bit/) - Annual competition
- [First Lego League](https://www.firstlegoleague.org/) - Robotics competition
- Local hackathons and coding clubs

### User Groups
- [micro:bit Educational Foundation](https://microbit.org/get-involved/)
- Local Code Clubs and CoderDojos
- School coding clubs

### Social Media
- Twitter: [@microbit_edu](https://twitter.com/microbit_edu)
- Facebook: micro:bit Educational Foundation
- Instagram: @microbit_edu
- YouTube: micro:bit

---

## Development Tools

### Advanced Programming
- [C/C++ with CODAL](https://tech.microbit.org/software/runtime/) - Low-level programming
- [Rust for micro:bit](https://github.com/nrf-rs/microbit) - Systems programming
- [Ada for micro:bit](https://github.com/AdaCore/Ada_Drivers_Library) - Safety-critical applications

### Simulators
- [MakeCode Simulator](https://makecode.microbit.org/) - Built-in simulator
- [Python Simulator](https://python.microbit.org/) - Test code in browser

### Version Control
- GitHub repositories for sharing code
- Git for tracking project changes

---

## Accessibility

### Inclusive Resources
- [micro:bit Accessibility](https://microbit.org/teach/send/) - SEND resources
- Text-to-speech functionality
- Large print resources
- Audio descriptions for projects

### Assistive Technologies
- Screen reader compatible editors
- Voice control options
- Alternative input methods

---

## Research and Academic Papers

### Educational Research
- "The Effect of micro:bit on Student Learning" - Various studies
- "Physical Computing in Primary Education" - Research papers
- "Gender Differences in STEM with micro:bit" - Academic research

### Conference Papers
- SIGCSE - Computer Science Education
- EDUCON - Engineering Education
- ICER - International Computing Education Research

---

## Additional Languages and Localizations

### Translations
- MakeCode available in 40+ languages
- Python editor supports multiple languages
- Community translations of resources

### Regional Resources
- UK: Computing At School
- USA: Code.org, CS Teachers Association
- Europe: SciFest, CodeWeek
- Asia: Tech Kids, Coding Lab
- Australia: CSER Digital Technologies

---

## Safety and Ethics

### Online Safety
- [Internet Safety Guidelines](https://www.saferinternet.org.uk/)
- Digital citizenship resources
- Privacy considerations with IoT

### Responsible Computing
- Environmental impact of electronics
- E-waste and recycling
- Ethical AI and data collection

---

## Troubleshooting Resources

### Common Issues
- See `troubleshooting.md` in this repository
- [Official Support Articles](https://support.microbit.org/)
- Community-contributed solutions

### Firmware Updates
- [Updating micro:bit Firmware](https://microbit.org/get-started/user-guide/firmware/)
- [Latest Firmware Versions](https://tech.microbit.org/software/daplink-interface/)

---

## Contributing to micro:bit

### Open Source
- [MicroPython GitHub](https://github.com/bbcmicrobit/micropython)
- [MakeCode GitHub](https://github.com/microsoft/pxt-microbit)
- [DAL Runtime GitHub](https://github.com/lancaster-university/microbit-dal)

### Getting Involved
- Report bugs and issues
- Contribute code improvements
- Create and share projects
- Help in community forums
- Translate resources

---

## Stay Updated

### Newsletters
- micro:bit Educational Foundation newsletter
- MakeCode newsletter
- Community updates

### Blogs
- [micro:bit News](https://microbit.org/news/)
- [Microsoft MakeCode Blog](https://makecode.com/blog)
- Community member blogs

---

## Quick Links Summary

| Resource | URL |
|----------|-----|
| Main Website | https://microbit.org/ |
| MakeCode Editor | https://makecode.microbit.org/ |
| Python Editor | https://python.microbit.org/ |
| Support | https://support.microbit.org/ |
| Community | https://community.microbit.org/ |
| Teaching Resources | https://microbit.org/teach/ |
| Projects | https://microbit.org/projects/ |

---

**Last Updated:** November 2025

For the most current resources, always check the official micro:bit website and community forums.
