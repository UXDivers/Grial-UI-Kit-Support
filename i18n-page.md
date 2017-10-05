#<a name="grial-i18n" href="#grial-i18n" class="iconTitle">Grial Internationalization</a>

![Grial i18n](http://52.10.147.219/system/uploads/images/grial-internationalization.png)

## Overview

Grial based apps are localizable by default, which means your Application can support different languages effortlessly.

<div class="new">
All our templates and pages are made using the built-in mechanism for localizing .NET applications using RESX files and the classes in the `System.Resources` and `System.Globalization` namespaces.
</div>

For more info about how to work with **RESX** files and localization please check
[Xamarin Forms Localization docs](https://developer.xamarin.com/guides/xamarin-forms/advanced/localization/).

## First step: Grial Admin

[Grial Admin](https://uxdivers.com/secure/grial/front/) lets you configure which cultures your Application needs to support. Check the `App Settings` tab where you can also define custom Application names for each culture in case you need them.

<img class="image-with-border" src="http://52.10.147.219/system/uploads/images/localizing_on_grial_admin1.png" alt="Localizing app name on Grial Admin" />

![Localizing app name on Grial Admin](http://52.10.147.219/system/uploads/images/localizing_on_grial_admin2.png)

<div class="highlight">
We will configure the project you download adding specific RESX files for each culture, as well as customizing App names on Android and iOS projects.
</div>

When you add a language and region not present on Grial sample, you will still get the RESX files properly named, 
but they will be a copy of our default language (**English**), containing all the keys.
All the strings (still in **English**) will be preceeded with the language and region wrapped in `[]`, e.g.: `[ar-AE]`.

This is particularly useful to detect which strings have not being already translated in your App. 

Check the following picture which shows how the `he-IL` strings are displayed preceeded by `[he-IL]`:

<div class="iphone7"><img class="image" src="http://52.10.147.219/system/uploads/images/he_il_dashboard.png" alt="Dashboard displayed in Hebrew, Israel showing strings" /><img class="mask" src="http://52.10.147.219/system/uploads/images/iphone7_mask.png" /></div>

<div class="iphone7"><img class="image" src="http://52.10.147.219/system/uploads/images/he_il_menu.png" alt="Dashboard displayed in Hebrew, Israel showing strings" /><img class="mask" src="http://52.10.147.219/system/uploads/images/iphone7_mask.png" /></div>



### Special Considerations for iOS

<img class="image-with-border" src="http://52.10.147.219/system/uploads/images/i18n_os_considerations.png" alt="Special Considerations for iOS" />

When changing your iOS device language you should -in mostly of the cases- get your App strings and App name in that language, however, there are a few considerations:

1. Supose you are using `he-IL` (Hebrew language and Israel region) as one of your localized App names
2. The device you are using has the language set to `Hebrew`, but the region is set to `United States`.
3. It is expected that the App icon and App texts should be displayed both in `Hebrew`:

<div class="iphone7"><img class="image" src="http://52.10.147.219/system/uploads/images/hebrew_app_name.png" alt="Hebrew App name" /><img class="mask" src="http://52.10.147.219/system/uploads/images/iphone7_mask.png" /></div>

<div class="iphone7"><img class="image" src="http://52.10.147.219/system/uploads/images/hebrew_app_name_2.png" alt="Hebrew App name" /><img class="mask" src="http://52.10.147.219/system/uploads/images/iphone7_mask.png" /></div>

<div class="iphone7"><img class="image" src="http://52.10.147.219/system/uploads/images/hebrew_app_name_3.png" alt="Hebrew App name but texts in English" /><img class="mask" src="http://52.10.147.219/system/uploads/images/iphone7_mask.png" /></div>

...however this is not the case.
What happened is that iOS is considering the specificity of the region which in this case is United States, so even while the device has its language set to `Hebrew`
the region demands **English** as it is more specfic making the strings to be displayed in that language and not **Hebrew**.

<div class="highlight">
As a rule of thumb, we recommend to use just the language to make sure any user which has that language set on his device will see the 
texts properly beyond the region.
</div>



## Localizing XAML

Consuming RESX files from C# code is not a problem of course, but consuming them from XAML code is not something supported out of the box by Xamarin Forms.

To this end, Grial includes a [XAML Markup Extension](https://developer.xamarin.com/guides/xamarin-forms/xaml/xaml-basics/xaml_markup_extensions/) called `TranslateExtension` to display strings from RESX files in the UI. 

It's very easy to use. For instance, to localize the `Text` property of a `<Label>` you just need to write:

```
<Label Text="{ artina:Translate MyStringKey }" />
```

This is going to look for a string with the key `MyStringKey` in the RESX file of the runtime language.

For the above to work there're only 2 steps needed:

1. Declare the `artina` namespace on top like this: 

	```
	xmlns:artina="clr-namespace:UXDivers.Artina.Shared;assembly=UXDivers.Artina.Shared"
	```

2. Use the reserved string `DefaultStringResource` as key to declare the default RESX file in a reachable ResourceDictionary (for instance, the App.xaml). Assuming the RESX file is called `AppResources.resx`: 

	```
	<resx:AppResources x:Key="DefaultStringResources" />
	```

Don't forget to declare the `resx` namespace on top.

<div class="highlight">
The extension reacts if device -or Application- language changes, always displaying strings read from the correspondent RESX file. This is completely dynamic, no reload needed.
</div>

### Advanced scenarios

**Multiple RESX files**

In the example above we explained how to use a single RESX file type. If you have a large application and you need to split the strings into multiple RESX files you can still use the `Translate` extension by telling it on which file to look for a specific key.

There're 2 alternatives:

1. Declare the namespace of your alternative RESX file type on top, for instance: 

```
xmlns:resx="clr-namespace:UXDivers.Artina.Grial"
```

and then use it in your code like this: 

```
<Label Text="{ artina:Translate Key=resx:AlternativeResources.MyStringKey }" />
```

2. In any reachable ResourceDictionary declare the alternative RESX file, for instance: 

```
<resx:AlternativeResources x:Key="MyAlternativeResources" />
```

Don't forget to declare the `resx` nemspace on top. Then use it in your code like this: 

```
<Label Text="{ artina:Translate Key=MyStringKey, Source={ StaticResource MyAlternativeResources } }" />
```

**Converters and StringFormat**

The `Translate` extension supports both `Converter` and `StringFormat` properties as regular Bindings do.

### Grial sample project

If you explore the full Grial sample project you will notice we use the following convention on RESX files:

![RESX files on Grial PCL](http://52.10.147.219/system/uploads/images/resx_files_on_pcl.png)

- `AppResources.resx`
	- Contains all the localized UI strings used across the app.
- `DataResources.resx`
	- Contains all localized data loaded from ViewModels.

You will also find at the top of the `App.xaml` the default RESX file delcaration along with a brief explanation of the translate extension usage.

**NOTE:** The default Grial package comes with English strings (en). Arabic strings (ar) are **only** included on **[Grial RTL package](rtl-page.html)** (sold separately).

## Grial Culture Service

Grial provides a service that implements `ICultureService` interface that provides the API to interact with the device culture. To access it you can do:

```
var cultureService = DependencyService.Get<ICultureServiceLocator>().Service;
```

It provides:

1. A property to access the current culture 

	```
	CultureInfo CurrentCulture { get; }
	```

2. An event that notifies when the device culture changes 

	```
	event CultureChangedEventHandler CurrentCultureChanged
	```

3. A method to simulate a culture change 

	```
	void SimulateCultureChange(CultureInfo ci)
	```

The culture property always matches the one on the device unless at some point the simulate method is called. The simulate method is the way to go if you want to expose the Culture as an Application-level setting. 

Grial also provides a lightweight way to listen to culture changes to avoid subscribing to the service event that may provoke memory leaks if the code doesn't unsuscribe properly. This is achieved through the `CultureChangeNotifier` class like this:

```
this.notifier = new CultureChangeNotifier();

// No need to unsuscribe, the notifier will staty alive 
// if and only if the "this" object is alive
this.notifier.CultureChanged += CultureChanged;
```

## Gorilla Player and RESX support

[Gorilla Player](http://gorillaplayer.com/) can be configured to display XAML files that take strings from RESX files. 

In Gorilla config file (`Gorilla.json`) you need to declare which is the type of markup extension and which is the RESX file used to read the strings. For instance, to delcare the one that comes with Grial you can do this:

```
	"localization": {
		"markupExtension": {
			"name": "Translate",
			"namespace": "UXDivers.Artina.Shared",
			"keyPropertyName": "Key"
		},

		"resources": {
			"resourceId": "UXDivers.Artina.Grial.Resx.AppResources",
			"assembly": "UXDivers.Artina.Grial",
			"defaultCulture": "en"
		}
	},
```

<div class="highlight">
This is preconfigured in Grial.
</div>

### Language switch at runtime

To change the language from running Gorilla use long-press gesture to display Gorilla's menu:

<div class="iphone7"><img class="image" src="http://52.10.147.219/system/uploads/images/rtl-runtime-optimize.gif" alt="Gorilla Player config" /><img class="mask" src="http://52.10.147.219/system/uploads/images/iphone7_mask.png" /></div>

<img src="http://52.10.147.219/system/uploads/images/gorilla-rtl-optimize.gif" alt="Gorilla Player interaction switching to RTL" class="no-retina">


