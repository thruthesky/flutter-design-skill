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
  - For example, create a `./lib/widgets/theme/ComicButton` widget instead of styling each button individually.
  - It must create re-usable widgets for common UI elements like buttons, cards, text fields, etc.

- **Comic Design**: Always follow these Comic design principles:
    - **Border**: The border must be `2.0` thickness.
    - **No shadow**: Always no shadows
    - **No elevation**: Always zero elevation
    - **Outline**: Use outline color for borders
    - **Rounded corners**: The border radius must be `12` for large elements, `8` for other elements.
    - **Colors**: Use the Theme Primary Color for primary elements.
      - Use the Theme Secondary Color for secondary elements.
      - Use the Theme Surface Color for cards and containers.
      - Use the Theme Background Color for the surface color.
      - Use the Theme onSurface Color for text and icons on surface color.
    - **Fonts**: Use the Theme Text Styles for all text elements.
      - Use `bodyLarge` for regular text.
      - Use `titleMedium` for titles.
      - Use `labelLarge` for buttons.

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

## Components 
- For all of the `Comic` widgets must be saved in `./lib/widgets/theme/comic_<component_name>.dart` 

## Button Styles
  - Must use the reusable `ComicButton` at `./lib/widgets/theme/comic_button.dart` widget for all buttons.
    - If the widget does not exist, create it following the Comic design principles:
      - Border thickness: 2.0
      - No elevation
      - No shadow
      - Rounded corners: 12 for large elements, 8 for other elements
      - Use Theme colors for background, foreground, and border
      - Use Theme text styles for button text
  - The ComicButton has the following UI options:
    - `important`: bool - The text style is `labelLarge` if true, otherwise `bodyLarge`.


### TextFormField Styles
  - Must use the reusable `ComicTextFormField` for all TextFormField. 
    - If the widget does not exists, create it with the following Comic design principles 
      - Border thickness: 2.0
      - No elevation
      - No shadow
      - Rounded corners: 12


# Scripts

- This skill does not provide scripts.