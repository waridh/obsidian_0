# TK Widgets

A basic component of TK based applications. Here widgets and windows are used interchangeably. It gives a graphical component to creating graphical applications.

Widgets range from buttons to menus and data displays. Widgets are very configurable and are easy to use.

Widgets follow a hierarchy system where widgets are able to be placed inside another widget. The main widget will be known as the root widget, and can be created by making a new instance of the TkRoot class.

## Creating a Widget

Here is the syntax:

```tcl
type variableName arguments option
```

- **`type`** refers to the widget type, like `button`, `label`, etc. Arguments can be optional and required bases on the type, and the option ranges from size to formatting of each component.

## Widget Naming convention

Widget uses a structure similar to naming packages. In TK, the root window is named with a period (.) and an element in window, for example button is named .myButton1. The variable name should start with a lowercase letter, digit, or punctuation mark (except period). After the first character, other character maybe uppercase or lowercase letters, numbers, or punctuation marks (except periods). Lowercase letters are the recommended starting character.

## Color Naming Convention

You can either use English names for them, or you can hexadecimals with #. Your hexadecimal values have to be a multiple of 3 from 3 to 12.

## Dimension Convention

The default unit is pixels and it is used when we specify no dimension. The other dimension are i for inch, m for milimeters, c for centrimeters, and p for points.

## Common Options

| Syntax | Description |
| ------ | ----------- |
|        |             |