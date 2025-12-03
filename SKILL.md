---
name: flutter-design-skill
description: This skill provides the Comic style UI design guideline and code to make the Flutter app look better. ALWAYS use this skill when the user asks to create, update, design, modify, or build any page, screen, widget, or UI component in a Flutter application.
---

# Flutter Deisgn Overview

- This skill provides the Comic style UI design guideline and code.
- It ensures that the Flutter application will have Comic UI style.

# When to Use
- Use this skill when the user requests to design or improve the UI of a Flutter application.
- Use this skill when the user mention Comic style UI design.


# Design Guidelines

- Refer to the [comic-theme.md](./comic-theme.md) for detailed design guidelines and code examples.



# Comic Design Rules

- Follow these critical design rules when implementing the Comic style UI in Flutter.

- **Reusable Flutter Widgets**: Always re-use or create a re-usable widgets to not repeat code.

- **Comic Design**: Always follow these Comic design principles:
    - Thin borders
    - NO shadows
    - No elevation
    - Outline with outline color
    - Rounded corners
    - Use the Theme Background Color of the surface color.

- **Spacing**: Use multiples of 8 (8, 16, 24, 32, etc.)



## Theme Design Guidelines

**CRITICAL FLUTTER RULES:**

- **Use Theme ONLY**: Always use `Theme.of(context)` for colors, fonts, and styles. NEVER hardcode them.

❌ NEVER DO:
```dart
Text('Login')  // Hardcoded text
color: Colors.blue  // Hardcoded color
fontSize: 16  // Hardcoded size
border: Border.all()  // Borders not allowed
elevation: 4  // Must be 0
ElevatedButton(child: Text('Click', style: TextStyle(...)))  // Inline style overrides Theme
```

✅ ALWAYS DO:
```dart
Text(T.login)  // i18n translation
color: Theme.of(context).colorScheme.primary  // Theme color
style: Theme.of(context).textTheme.bodyLarge  // Theme text style
elevation: 0  // Flat design
ElevatedButton(child: Text(T.click))  // Let Theme handle styling
```



## Button Styles
  - Thin border, no elevation, no shadow, rounded corners.



# Scripts

- This skill does not provide scripts.