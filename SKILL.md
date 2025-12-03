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
  - all of the `Comic` widgets must be saved in `./lib/widgets/theme/comic_<component_name>.dart`  
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

# ComicButton System

## Concept & Intent

The **ComicButton** system is a unified, reusable button component library that implements the Comic design language across the entire Flutter application. Instead of styling buttons individually with inline styles, all buttons use the `ComicButton` base widget or its variants.

**Key Benefits:**
- **Consistency**: All buttons share the same Comic design DNA (2px border, no shadow, rounded corners)
- **Flexibility**: Three design options (`rounded`, `padding`, `textSize`) allow creating any button style
- **Maintainability**: Change the button style in one place, update everywhere
- **Theme Integration**: Automatically uses Theme colors and text styles

## Core Design Principles

All ComicButton variants follow these Comic design rules:
- **Border**: 2.0px thickness with outline color
- **Elevation**: Always 0 (flat design, no shadows)
- **Corners**: Rounded with borderRadius 12 (normal) or fully rounded (full/pill)
- **Colors**: Theme-based (surface, primary, secondary)
- **Typography**: Theme text styles (bodyLarge, titleMedium, bodyMedium)
- **Spacing**: Padding in multiples of 8

## Design Options

Every `ComicXxxButton` variant supports three design option enums:

### ComicButtonRounded
Controls the corner shape of the button.
| Value | Description | Use Case |
|-------|-------------|----------|
| `full` | Pill/stadium shape (StadiumBorder) | CTA buttons, login buttons |
| `normal` | Rounded corners (borderRadius: 12) | Standard buttons |

### ComicButtonPadding
Controls the internal padding of the button.
| Value | Padding | Use Case |
|-------|---------|----------|
| `large` | 32×20 | Important action buttons (login, submit) |
| `medium` | 24×16 | Standard buttons (default) |
| `small` | 16×12 | Compact buttons, inline actions |

### ComicButtonTextSize
Controls the text size inside the button.
| Value | Text Style | Use Case |
|-------|------------|----------|
| `large` | titleMedium | Important action buttons |
| `medium` | bodyLarge | Standard buttons (default) |
| `small` | bodyMedium | Compact buttons |

## Button Variants

### ComicButton (Base)
The foundation widget with neutral colors (surface background, onSurface text).

```dart
// Standard button
ComicButton(
  onPressed: () => doSomething(),
  child: Text(Lo.of(context)!.action),
)

// Large login button (pill shape)
ComicButton(
  onPressed: () => login(),
  rounded: ComicButtonRounded.full,
  padding: ComicButtonPadding.large,
  textSize: ComicButtonTextSize.large,
  child: Text(Lo.of(context)!.login),
)
```

### ComicPrimaryButton
Primary action button using Theme primary color.

```dart
ComicPrimaryButton(
  onPressed: () => submit(),
  rounded: ComicButtonRounded.full,
  padding: ComicButtonPadding.large,
  textSize: ComicButtonTextSize.large,
  child: Text(Lo.of(context)!.submit),
)
```

### ComicSecondaryButton
Secondary action button using Theme secondary color.

```dart
ComicSecondaryButton(
  onPressed: () => cancel(),
  padding: ComicButtonPadding.small,
  textSize: ComicButtonTextSize.small,
  child: Text(Lo.of(context)!.cancel),
)
```

## Quick Reference

| Button Style | rounded | padding | textSize |
|--------------|---------|---------|----------|
| Large CTA | `full` | `large` | `large` |
| Standard | `normal` | `medium` | `medium` |
| Compact | `normal` | `small` | `small` |

## File Location

All ComicButton widgets are defined in:
`./lib/widgets/theme/comic_button.dart`
  

# Scripts

- This skill does not provide scripts.