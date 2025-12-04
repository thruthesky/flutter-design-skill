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

# ComicTextFormField

## Concept & Intent

The **ComicTextFormField** is a reusable text input component that implements the Comic design language. It provides a consistent way to create text input fields across the entire Flutter application with Comic-style borders, proper spacing, and theme integration.

**Key Benefits:**

- **Consistency**: All text fields share the same Comic design DNA (2px border, no shadow, rounded corners)
- **Flexibility**: Extensive customization options while maintaining Comic design principles
- **Maintainability**: Change the text field style in one place, update everywhere
- **Theme Integration**: Automatically uses Theme colors and text styles

## Design Principles

All ComicTextFormField instances follow these Comic design rules:

- **Border**: 1.0px thickness with outline color (customizable) - lighter weight for compact input fields
- **Elevation**: Always 0 (flat design, no shadows)
- **Corners**: Rounded with borderRadius 12 (customizable)
- **Colors**: Theme-based (surface background, outline border, primary focus, error)
- **Typography**: Theme text styles (bodyLarge for content, bodyMedium for label/hint)
- **Spacing**: Content padding in multiples of 8

## Key Features

- **Full TextFormField API**: Supports all standard TextFormField parameters
- **Customizable Borders**: Configure border color, focus color, error color, width, and radius
- **Theme Integration**: Uses Theme colors for all visual elements
- **Validation Support**: Built-in validator and error text display
- **Input Control**: Supports read-only, enabled/disabled, obscure text, keyboard type
- **Icons**: Prefix and suffix icon support
- **Multi-line**: Configurable min/max lines for single or multi-line input
- **Length Control**: Maximum length with counter

## Usage Examples

### Basic Text Field

```dart
ComicTextFormField(
  controller: _nameController,
  labelText: T.fullName,
  hintText: T.fullNameHint,
)
```

### Password Field

```dart
ComicTextFormField(
  controller: _passwordController,
  labelText: T.password,
  hintText: T.enterPassword,
  obscureText: true,
  prefixIcon: Icon(Icons.lock),
)
```

### With Validation

```dart
ComicTextFormField(
  controller: _emailController,
  labelText: T.email,
  hintText: T.enterEmail,
  keyboardType: TextInputType.emailAddress,
  validator: (value) {
    if (value == null || value.isEmpty) {
      return T.emailRequired;
    }
    return null;
  },
)
```

### Multi-line Text Area

```dart
ComicTextFormField(
  controller: _bioController,
  labelText: T.bio,
  hintText: T.enterBio,
  maxLines: 5,
  minLines: 3,
  maxLength: 500,
)
```

### Disabled Field

```dart
ComicTextFormField(
  controller: _nicknameController,
  labelText: T.nickname,
  hintText: T.nicknameHint,
  enabled: false, // or readOnly: true
)
```

## Customization Options

### Border Styling

```dart
ComicTextFormField(
  controller: _controller,
  labelText: T.label,
  // Custom border styling
  borderWidth: 1.0,        // Default: 1.0
  borderRadius: 12,        // Default: 12
  borderColor: Colors.grey,
  focusedBorderColor: Colors.blue,
  errorBorderColor: Colors.red,
)
```

### Content Padding

```dart
ComicTextFormField(
  controller: _controller,
  labelText: T.label,
  // Custom padding (default: symmetric horizontal: 16, vertical: 16)
  contentPadding: EdgeInsets.all(20),
)
```

## Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| controller | TextEditingController? | null | Text field controller |
| labelText | String? | null | Label text displayed above input |
| hintText | String? | null | Hint text shown when empty |
| errorText | String? | null | Error message to display |
| prefixIcon | Widget? | null | Icon at the start of the field |
| suffixIcon | Widget? | null | Icon at the end of the field |
| keyboardType | TextInputType? | null | Keyboard type for input |
| obscureText | bool | false | Hide text for passwords |
| onChanged | ValueChanged<String>? | null | Callback when text changes |
| onFieldSubmitted | ValueChanged<String>? | null | Callback on submit |
| validator | String? Function(String?)? | null | Validation function |
| readOnly | bool | false | Prevent editing |
| enabled | bool | true | Enable/disable field |
| maxLines | int? | 1 | Maximum lines |
| minLines | int? | null | Minimum lines |
| maxLength | int? | null | Maximum characters |
| autofocus | bool | false | Auto focus on load |
| borderColor | Color? | null | Border color (default: outline) |
| focusedBorderColor | Color? | null | Focus border (default: primary) |
| errorBorderColor | Color? | null | Error border (default: error) |
| borderWidth | double | 1.0 | Border thickness |
| borderRadius | double | 12 | Corner radius |
| contentPadding | EdgeInsetsGeometry? | null | Internal padding |

## Border States

ComicTextFormField automatically handles five border states:

1. **Enabled Border**: Default state (outline color, 1.0px)
2. **Focused Border**: When field has focus (primary color, 1.0px)
3. **Error Border**: When validation fails (error color, 1.0px)
4. **Focused Error Border**: Error state with focus (error color, 1.0px)
5. **Disabled Border**: When field is disabled (outline with 50% opacity, 1.0px)

## File Location

ComicTextFormField is defined in:
`./lib/widgets/theme/comic_text_form_field.dart`

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

# Comic AppBar Design

## Concept & Intent

The **Comic AppBar** implements the Comic design language for app bars and header sections. It provides consistent styling with a characteristic 2.0px bottom border using the outline color, creating a clear visual separation between the header and content areas.

## Design Principles

- **Border**: 2.0px bottom border with outline color
- **Typography**: Use Theme titleLarge text style for titles
- **Height**: Standard AppBar height (56px) or custom heights for special cases
- **Colors**: Theme-based (surface background, outline border, onSurface text)
- **No Elevation**: Always 0 (flat design, no shadows)

## Usage Patterns

### Pattern 1: Standard Scaffold AppBar

Use this pattern when you have a `Scaffold` widget with an `appBar` property.

```dart
Scaffold(
  appBar: AppBar(
    title: Text(T.editProfile, style: theme.textTheme.titleLarge),
    bottom: PreferredSize(
      preferredSize: const Size.fromHeight(1),
      child: Container(height: 2, color: scheme.outline),
    ),
  ),
  body: // Your content here
)
```

**Key Features:**
- Uses standard `AppBar` widget
- Title uses `titleLarge` text style from Theme
- Bottom border achieved using `PreferredSize` with 2.0px height Container
- Border color uses Theme `outline` color

### Pattern 2: Custom Header (Without Scaffold)

Use this pattern when you need an app bar-like header without a Scaffold (e.g., in special layouts, custom scrolling views, or nested navigation).

```dart
SafeArea(
  child: Container(
    height: 56, // Standard AppBar height
    padding: const EdgeInsets.only(right: 4, left: 12),
    decoration: BoxDecoration(
      border: Border(
        bottom: BorderSide(
          // Comic Design: 2.0px border with outline color
          color: Theme.of(context).colorScheme.outline,
          width: 2.0,
        ),
      ),
    ),
    child: Row(
      children: [
        // Title
        Expanded(
          child: Text(
            T.pageTitle,
            style: Theme.of(context)
                .textTheme
                .titleLarge
                ?.copyWith(fontWeight: FontWeight.w600),
            overflow: TextOverflow.ellipsis,
          ),
        ),
        // Action buttons (optional)
        IconButton(
          icon: const FaIcon(FontAwesomeIcons.someIcon),
          onPressed: () {
            // Action handler
          },
        ),
      ],
    ),
  ),
)
```

**Key Features:**
- Uses `Container` with bottom border decoration
- Wrapped in `SafeArea` for proper top spacing
- Height set to 56px (standard AppBar height)
- Padding adjusts for left/right spacing
- Border applied only to bottom (2.0px with outline color)
- Title uses `titleLarge` text style
- Supports action buttons via `IconButton` or other widgets

## Design Specifications

| Property | Value | Description |
|----------|-------|-------------|
| **Height** | 56px | Standard AppBar height |
| **Border Position** | Bottom only | Visual separation from content |
| **Border Width** | 2.0px | Comic standard thickness |
| **Border Color** | `colorScheme.outline` | Theme outline color |
| **Title Style** | `titleLarge` | Theme text style |
| **Elevation** | 0 | Flat design (no shadow) |
| **Padding** | Left: 12px, Right: 4px | Balanced spacing for text and icons |

## When to Use Each Pattern

### Use Pattern 1 (Scaffold AppBar) when:
- Building a standard screen with Scaffold
- Need standard AppBar features (back button, actions, etc.)
- Want Flutter's built-in AppBar behavior

### Use Pattern 2 (Custom Header) when:
- Working without a Scaffold widget
- Building custom scrolling layouts
- Creating nested navigation structures
- Need more control over header layout and behavior
- Implementing complex header interactions (e.g., dropdown menus, category pickers)

## Example: Header with Action Buttons

```dart
SafeArea(
  child: Container(
    height: 56,
    padding: const EdgeInsets.only(right: 4, left: 12),
    decoration: BoxDecoration(
      border: Border(
        bottom: BorderSide(
          color: Theme.of(context).colorScheme.outline,
          width: 2.0,
        ),
      ),
    ),
    child: Row(
      children: [
        Expanded(
          child: Text(
            T.categories,
            style: Theme.of(context)
                .textTheme
                .titleLarge
                ?.copyWith(fontWeight: FontWeight.w600),
            overflow: TextOverflow.ellipsis,
          ),
        ),
        IconButton(
          icon: const FaIcon(FontAwesomeIcons.penToSquare),
          onPressed: () {
            // Create new item
          },
        ),
        IconButton(
          icon: const FaIcon(FontAwesomeIcons.chevronDown),
          onPressed: () {
            // Show dropdown menu
          },
        ),
      ],
    ),
  ),
)
```

## Best Practices

- **Always** use Theme colors (outline for border, titleLarge for text)
- **Always** set border width to 2.0px for consistency
- **Always** apply border only to the bottom (not top/left/right)
- **Always** use SafeArea when implementing custom headers
- **Never** add elevation or shadows
- Use `overflow: TextOverflow.ellipsis` for long titles
- Use multiples of 8 for padding and spacing
- Maintain 56px height for consistency with standard AppBar


# Scripts

- This skill does not provide scripts.
