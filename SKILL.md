---
name: flutter-design-skill
description: This skill provides the Comic style UI design guideline and code to make the Flutter app look better. ALWAYS use this skill when the user asks to create, update, design, modify, or build any page, screen, widget, or UI component in a Flutter application.
---

# Flutter Design Overview

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

  - **Border**:
    - Standard elements: `2.0` thickness
    - List-based widgets (ListTile, compact cards): `1.5` thickness for lighter visual weight
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

| Button Style | rounded  | padding  | textSize |
| ------------ | -------- | -------- | -------- |
| Large CTA    | `full`   | `large`  | `large`  |
| Standard     | `normal` | `medium` | `medium` |
| Compact      | `normal` | `small`  | `small`  |

## File Location

All ComicButton widgets are defined in:
`./lib/widgets/theme/comic_button.dart`

# List-Based Widgets Design

For list-based content such as `ListTile` and `Compact Cards`:

## Design Principles

- **Border**: Use `1.5` thickness (thinner than standard 2.0) for lighter visual weight in compact lists
- **Border Radius**: `12` for rounded corners
- **Elevation**: `0` (no shadow)
- **Margin**: `EdgeInsets.zero` (parent controls spacing)
- **Colors**: Use Theme colors (surface, outline, onSurface)

### Key Features

```dart
Card(
  elevation: 0, // Comic Design: no shadow
  margin: EdgeInsets.zero, // No margin (parent controls spacing)
  color: Theme.of(context).colorScheme.surface,
  // Comic Design: thinner border with rounded corners for compact list
  shape: RoundedRectangleBorder(
    borderRadius: BorderRadius.circular(12),
    side: BorderSide(
      color: Theme.of(context).colorScheme.outline,
      width: 1.0, // Thinner border for list items
    ),
  ),
  child: InkWell(
    onTap: onTap,
    borderRadius: BorderRadius.circular(12), // Match card radius for ripple
    child: // ... content
  ),
)
```

# ComicModalBottomSheet

## Concept & Intent

The **ComicModalBottomSheet** is a reusable modal bottom sheet component that implements the Comic design language. It provides a consistent way to display modal content from the bottom of the screen with Comic-style rounded top corners, proper spacing, and an integrated drag handle.

## Design Principles

- **Border Radius**: `12.0` for top-left and top-right corners (creates Comic-style rounded top)
- **Border Width**: `2.0` thickness on top, left, and right sides (no border on bottom)
- **Elevation**: `0` (flat design, no shadows)
- **Colors**: Theme-based (surface background, outline border)
- **Spacing**: Consistent padding using multiples of 8
- **Drag Handle**: Custom drag handle integrated inside the container (32px × 4px)

## Usage

```dart
// Show Comic Modal Bottom Sheet with integrated drag handle
showModalBottomSheet(
  context: context,
  backgroundColor: Colors.transparent, // Comic Design: transparent for custom styling
  elevation: 0, // Comic Design: no shadow
  builder: (context) {
    return Container(
      decoration: BoxDecoration(
        color: Theme.of(context).colorScheme.surface,
        borderRadius: const BorderRadius.only(
          topLeft: Radius.circular(12.0), // Comic Design: rounded top corners
          topRight: Radius.circular(12.0),
        ),
        border: Border(
          top: BorderSide(
            color: Theme.of(context).colorScheme.outline,
            width: 2.0, // Comic Design: 2.0 border
          ),
          left: BorderSide(
            color: Theme.of(context).colorScheme.outline,
            width: 2.0,
          ),
          right: BorderSide(
            color: Theme.of(context).colorScheme.outline,
            width: 2.0,
          ),
          // No bottom border
        ),
      ),
      child: Column(
        mainAxisSize: MainAxisSize.min,
        children: [
          // Drag handle indicator
          // Comic Design: 8px spacing from top
          const SizedBox(height: 8),
          Container(
            width: 32,
            height: 4,
            decoration: BoxDecoration(
              color: Theme.of(context).colorScheme.onSurfaceVariant.withValues(alpha: 0.4),
              borderRadius: BorderRadius.circular(2),
            ),
          ),
          const SizedBox(height: 8),
          // Your content here (wrapped in Flexible if scrollable)
          Flexible(
            child: ListView(
              shrinkWrap: true,
              children: [
                // Your list items
              ],
            ),
          ),
        ],
      ),
    );
  },
);
```

## Key Features

- **Rounded Top Corners**: 12.0 radius on top-left and top-right for Comic style
- **Selective Borders**: Border on top, left, and right only (no bottom border)
- **Theme Integration**: Uses Theme colors for surface and outline
- **No Shadow**: Elevation set to 0 for flat design
- **Transparent Background**: Parent backgroundColor set to transparent for custom styling
- **Integrated Drag Handle**: Custom drag handle (32×4px) with proper spacing inside the container
- **Flexible Layout**: Uses Column with MainAxisSize.min and Flexible for proper sizing

## Drag Handle Specifications

- **Size**: 32px wide × 4px tall
- **Color**: `onSurfaceVariant` with 40% opacity
- **Border Radius**: 2px for rounded corners
- **Spacing**: 8px top and bottom (multiples of 8)
- **Position**: Inside the container, above the content

## Best Practices

- Always use `backgroundColor: Colors.transparent` in `showModalBottomSheet`
- Apply `elevation: 0` to maintain flat design
- Use Theme colors for consistency
- Wrap the Container's child in a Column with `mainAxisSize: MainAxisSize.min`
- Add the drag handle as the first element in the Column
- Use `Flexible` wrapper for scrollable content (ListView, GridView, etc.)
- Use `shrinkWrap: true` for ListView to allow proper sizing
- Add appropriate spacing (multiples of 8) around content


# Scripts

- This skill does not provide scripts.
