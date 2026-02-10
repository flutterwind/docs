---
title: UI Blocks
description: Built-in preset tokens for common interface patterns.
icon: lucide:blocks
---

Flutterwind includes preset tokens that expand into reusable utility combinations.

## Built-in preset tokens

From the current support matrix:

- `btn`
- `card`
- `card-header`
- `card-body`
- `group`
- `peer`
- `input-filled`

## Basic examples

```dart
ElevatedButton(
  onPressed: () {},
  child: const Text('Continue'),
).className('btn')
```

```dart
Container(
  child: Column(
    children: const [
      Text('Card Title'),
      Text('Card description'),
    ],
  ),
).className('card card-header card-body')
```

## Group and peer variants

Use `group` and `peer` to coordinate states across related widgets:

```dart
Container(
  child: [
    TextField().className('peer input-filled'),
    Text('Helper text').className('peer-focus:text-blue-600'),
  ],
).className('group')
```

## Extending presets

Add custom preset tokens through the Plugin SDK:

```dart
ComponentPresetRegistry.registerPreset(
  'btn-brand',
  'btn bg-primary text-primary-foreground rounded-lg px-6 py-3',
);
```
