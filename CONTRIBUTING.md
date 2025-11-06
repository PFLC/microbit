# Contributing to micro:bit Workshop

Thank you for your interest in contributing! This repository is designed to help students learn programming with the BBC micro:bit.

## How to Contribute

### Types of Contributions

We welcome:
- 🐛 Bug fixes in code examples
- 📝 Improvements to documentation
- 💡 New project ideas
- 🎓 Educational exercises
- 🌍 Translations
- 📚 Additional resources and references

### Getting Started

1. **Fork the Repository**
   - Click the "Fork" button at the top right of this repository
   - Clone your fork to your local machine

2. **Create a Branch**
   ```bash
   git checkout -b feature/your-contribution-name
   ```

3. **Make Your Changes**
   - Follow the guidelines below
   - Test your code on an actual micro:bit if possible

4. **Submit a Pull Request**
   - Push your changes to your fork
   - Open a pull request against the main repository
   - Describe your changes clearly

## Contribution Guidelines

### Code Examples

All code examples should:
- ✅ Work on both micro:bit v1 and v2 (or clearly indicate version requirements)
- ✅ Include comments explaining key concepts
- ✅ Follow Python PEP 8 style guidelines where applicable
- ✅ Be tested on actual hardware
- ✅ Include both Python and MakeCode versions when possible
- ✅ Be appropriate for the target age/skill level

### Documentation

Documentation should:
- ✅ Be clear and concise
- ✅ Use proper grammar and spelling
- ✅ Include examples where helpful
- ✅ Be accessible to beginners
- ✅ Avoid jargon or explain technical terms
- ✅ Include visual aids (diagrams, screenshots) when helpful

### New Projects

When adding a new project, include:

1. **Clear Title and Description**
   - What the project does
   - What students will learn

2. **Difficulty Level**
   - Beginner, Intermediate, or Advanced
   - Estimated time to complete

3. **Requirements**
   - Hardware needed
   - Any additional components
   - Software/editor requirements

4. **Step-by-Step Instructions**
   - Clear, numbered steps
   - Code examples
   - Expected outcomes

5. **Extensions/Challenges**
   - Ways to expand the project
   - Additional learning opportunities

### Project Template

```markdown
# Project Title

Brief description of what the project does.

## What You'll Learn
- Concept 1
- Concept 2
- Concept 3

## Hardware Required
- List all required components

## Code

### Python Version
\`\`\`python
from microbit import *
# Your code here
\`\`\`

### MakeCode Version
Description of blocks needed

## Instructions
1. Step one
2. Step two
3. Step three

## Customization Ideas
Ways to modify the project

## Challenges
Extensions and advanced features

---
**Difficulty:** ⭐⭐☆☆☆  
**Time:** XX minutes  
**Age:** XX+
```

### Exercises

When creating exercises:
- State the learning objective clearly
- Provide hints, not complete solutions
- Include expected outcomes
- Offer extension challenges
- Indicate difficulty and time

## Code Style

### Python
- Use 4 spaces for indentation
- Follow PEP 8 naming conventions
- Add comments for complex logic
- Keep code simple and readable

Example:
```python
from microbit import *

# Initialize counter
count = 0

# Main loop
while True:
    # Check button press
    if button_a.was_pressed():
        count += 1
        display.scroll(str(count))
    
    sleep(100)
```

### MakeCode
- Provide clear block descriptions
- Include screenshots when possible
- Explain each block's purpose

## Testing

Before submitting:
- [ ] Test code on actual micro:bit hardware
- [ ] Verify on both v1 and v2 if applicable
- [ ] Check for typos and grammar errors
- [ ] Ensure links work
- [ ] Verify code formatting
- [ ] Test on both Python and MakeCode if applicable

## Review Process

1. **Submission**: You submit a pull request
2. **Review**: Maintainers review your contribution
3. **Feedback**: You may receive suggestions for improvements
4. **Approval**: Once approved, your contribution is merged
5. **Recognition**: You'll be added to the contributors list

## Reporting Issues

Found a bug or have a suggestion?

1. Check if the issue already exists
2. Create a new issue with:
   - Clear title
   - Detailed description
   - Steps to reproduce (for bugs)
   - Expected vs actual behavior
   - Your micro:bit version
   - Any error messages

## Community Guidelines

- Be respectful and constructive
- Focus on educational value
- Help beginners feel welcome
- Give credit where due
- Follow the Code of Conduct

## Questions?

If you have questions:
- Open an issue for discussion
- Check existing documentation
- Reach out to maintainers

## License

By contributing, you agree that your contributions will be licensed under the same license as this project (CC0 1.0 Universal).

## Recognition

Contributors will be acknowledged in:
- README.md contributors section
- Project documentation where applicable

Thank you for helping make learning with micro:bit better for everyone! 🎉
