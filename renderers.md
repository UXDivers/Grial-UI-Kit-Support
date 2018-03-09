# Grial UI Kit Renderers

Grial companion nuget packages define a set of [attached properties](https://developer.xamarin.com/guides/xamarin-forms/xaml/attached-properties/) and custom renderers that extend the out-of-the-box customization options of Xamarin.Forms controls. 

For instance, there's a property to define the text alignment of a `Picker` which is something not available in the platform. 

Attached properties are defined in their own class (outside the target control type). In this case that class is `UXDivers.Artina.Shared.PickerProperties` and the name of the property is `HorizontalTextAlignment`. 

Here's an example of how to use it:

- Xaml

Include this namespace declaration in the top of the Page / ContentView.
```
xmlns:artina="clr-namespace:UXDivers.Artina.Shared;assembly=UXDivers.Artina.Shared" 
```

And to use the property simply do this:

```
<Picker artina:PickerProperties.HorizontalTextAlignment="Start" ... />
```

- C#

```
PickerProperties.SetHorizontalTextAlignment(picker, TextAlignment.Start);
```

Below there's a list of properties per control.

## Picker, DatePicker, TimePicker

Attached properties for `Picker`, `DatePicker`, `TimePicker` are declared in class `UXDivers.Artina.Shared.PickerProperties`.

| Property                   | Android | iOS | Notes           |
| -------------------------- | ------- | --- | --------------------- |
| `PlaceholderColor`         | ✔       | ✔   | Watermark text color  |
| `BorderWidth`              | ✔       | ✔   |                       |
| `BorderColor`              | ✔       | ✔   |                       |
| `BorderCornerRadius`       | ✔       | ✔   | float                 |
| `BorderStyle`              | ✔       | ✔   | Default, None, BottomLine, Rect, RoundRect |
| `HorizontalTextAlignment`  | ✔       | ✔   | Start, Center, End |

## Entry

Attached properties for `Entry` are declared in class `UXDivers.Artina.Shared.EntryProperties`.

| Property                   | Android | iOS | Notes                 |
| -------------------------- | ------- | --- | --------------------- |
| `PlaceholderColor`         | ✔       | ✔   | Watermark text color  |
| `BorderWidth`              | ✔       | ✔   |                       |
| `BorderColor`              | ✔       | ✔   |                       |
| `BorderCornerRadius`       | ✔       | ✔   | float                 |
| `BorderStyle`              | ✔       | ✔   | Default, None, BottomLine, Rect, RoundRect |

## Editor

Attached properties for `Editor` are declared in class `UXDivers.Artina.Shared.EditorProperties`.

| Property                   | Android | iOS | Notes                 |
| -------------------------- | ------- | --- | --------------------- |
| `Placeholder`              | ✔       | ✔   | Watermark text        |
| `PlaceholderColor`         | ✔       | ✔   | Watermark text color  |
| `BorderWidth`              | ✔       | ✔   |                       |
| `BorderColor`              | ✔       | ✔   |                       |
| `BorderCornerRadius`       | ✔       | ✔   | float                 |
| `BorderStyle`              | ✔       | ✔   | Default, None, BottomLine, Rect, RoundRect |

## Slider

Attached properties for `Slider` are declared in class `UXDivers.Artina.Shared.SliderProperties`.

| Property                   | Android | iOS | Notes                 |
| -------------------------- | ------- | --- | --------------------- |
| `TintColor`                | ✔       | ✘   | Slider left side color |

## ProgressBar

Attached properties for `ProgressBar` are declared in class `UXDivers.Artina.Shared.ProgressBarProperties`.

| Property                   | Android | iOS | Notes                 |
| -------------------------- | ------- | --- | --------------------- |
| `TintColor`                | ✔       | ✘   | Progress color        |

## Switch

Attached properties for `Switch` are declared in class `UXDivers.Artina.Shared.SwitchProperties`.

| Property                   | Android | iOS | Notes                 |
| -------------------------- | ------- | --- | --------------------- |
| `TintColor`                | ✔       | ✘   | On color              |

## TableView

Attached properties for `TableView` are declared in class `UXDivers.Artina.Shared.TableViewProperties`.

| Property                   | Android | iOS | Notes                 |
| -------------------------- | ------- | --- | --------------------- |
| `HeaderFooterTextColor`    | ✔       | ✔   | Color on header and footer |

## SearchBar

Attached properties for `SarchBar` are declared in class `UXDivers.Artina.Shared.SearchBarProperties`.

| Property                   | Android   | iOS | Notes                        |
| -------------------------- | --------- | --- | ---------------------------- |
| `FieldBackgroundColor`     | ✘         | ✔   | Inner background field color |
| `IconColor`          | API >= 21 | ✔   | Glass icon color             |
| `BorderColor`              | API >= 21 | ✔   |                              |
| `BorderWidth`              | ✘         | ✔   | float                        |
