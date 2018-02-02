# Custom Renderers Attached Properties List

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

| Property                   | Notes           |
| -------------------------- | --------------------- |
| `PlaceholderColor`         | Watermark text color  |
| `BorderWidth`              |                       |
| `BorderColor`              |                       |
| `BorderCornerRadius`       | float                 |
| `BorderStyle`              | Default, None, BottomLine, Rect, RoundRect |
| `HorizontalTextAlignment`  | Start, Center, End |

## Entry

Attached properties for `Entry` are declared in class `UXDivers.Artina.Shared.EntryProperties`.

| Property                   | Notes           |
| -------------------------- | --------------------- |
| `PlaceholderColor`         | Watermark text color  |
| `BorderWidth`              |                       |
| `BorderColor`              |                       |
| `BorderCornerRadius`       | float                 |
| `BorderStyle`              | Default, None, BottomLine, Rect, RoundRect |

## Editor

Attached properties for `Editor` are declared in class `UXDivers.Artina.Shared.EditorProperties`.

| Property                   | Notes           |
| -------------------------- | --------------------- |
| `BorderWidth`              |                       |
| `BorderColor`              |                       |
| `BorderCornerRadius`       | float                 |

## Slider

Attached properties for `Slider` are declared in class `UXDivers.Artina.Shared.SliderProperties`.

| Property                   | Notes                 |
| -------------------------- | --------------------- |
| `TintColor`              | Slider left side color, android only |

## ProgressBar

Attached properties for `ProgressBar` are declared in class `UXDivers.Artina.Shared.ProgressBarProperties`.

| Property                   | Notes                 |
| -------------------------- | --------------------- |
| `TintColor`              | Progress color, android only |

## Switch

Attached properties for `Switch` are declared in class `UXDivers.Artina.Shared.SwitchProperties`.

| Property                   | Notes                 |
| -------------------------- | --------------------- |
| `TintColor`              | On color, android only |

## TableView

Attached properties for `TableView` are declared in class `UXDivers.Artina.Shared.TableViewProperties`.

| Property                   | Notes                 |
| -------------------------- | --------------------- |
| `HeaderFooterTextColor`    | Color on header and footer |
