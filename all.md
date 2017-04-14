## Grial 2.0 Overview

![Grial](http://52.10.147.219/system/uploads/images/grial_2_hero.png)

Grial offers a set of beautiful XAML UI views made for Xamarin Forms. These cover the most typical Mobile UI patterns and crafted with developers in mind. 

We use the MVVM pattern, but Grial is agnostic, meaning it is not bound to any specific MVVM framework.

We provide easy way to focus on logic and to “almost forget” about the UI work by providing:

- ready made views
- templates
- bindings
- models and viewmodels
- and styling through a customizable theme

Grial is based on Artina, our library of custom renderers and UI controls.

### Need help? ###
Please [visit Grial support website](https://github.com/UXDivers/Grial-UI-Kit-Support-And-Issues).

We also provide design and Grial customization services.

[![UXDivers Design Services](http://52.10.147.219/system/uploads/images/custom_grial.png)](mailto:hello@uxdivers.com)
### Grial 2.0 New Features

- Easier project setup
    - Grial online admin allows to download your customized Grial Sample using your own namespaces and assembly names, saving lot of time with setup
    - Grial Starter 
        - Bare minimum Grial project with your namespaces and assemblies 
- Responsive features
    - Added Responsive helpers
        - Take full control of how things layout on pages, different devices, orientations and platforms
        - Tablet optimized experience
    - Responsive Android and iOS Splash pages
- New themes
    - 3 new themes
    - Added support for merged dictionaries
    - Added build task to ease colors compilation
- Icons 
    - New icons
        - New default base font (grialshapes)
        - [Fontawesome 4.7](http://fontawesome.io/icons/) and [Ionicicons 2.0.0](http://ionicons.com/cheatsheet.html) fonts
        - [Font helpers](#font-helpers) for easier icons referencing in your code
    - Easier icons setup through font helpers
- Improved documentation
- New UI Controls 
    - RoundedLabel
    - artina Repeater
    - artina TabControl (available on Grial Pro)
- [Lottie animations support](https://github.com/martijn00/LottieXamarin)
- Better and more efficient images support through [FFImageLoading](https://github.com/luberda-molinet/FFImageLoading)
- More screens


### Supported Platforms

Currently Grial UI Kit adds support for:

- Android 4.1+ (API Level 16) through AppCompatV7.
- iOS 8.0+




## Release Notes 

[Check Grial Release Notes](.release-notes.html)


##<a name="grial-download"></a> Downloading Grial

When you purchase Grial you received and email with the link to [Grial admin](https://uxdivers.com/secure/grial/front), our online site where you:

- Register your user
- Configure and download your Grial projects (Customized sample and/or Grial Starter)
- Administrate your Grial licenses

Once you download the product you will get a .zip file containing 2 folders:

    |_ <YourAppName.zip>
        |_ full
        |_ starter

- ***full***
    - This is a copy of Grial 2.0 sample app customized with your app name, assembly name, etc.
    - It contains every file used in our demo.

- ***starter***
    - This is just the minimum setup of your customized Grial for you to start working with.

##  <a name="grial-first-run"></a> Grial First Run

After you download your customized version of Grial, you will need to configure our private nugget packages source in order to get the needed packages to run Grial.

### Setting up UXDivers nugget source

![Nuget configure sources](http://52.10.147.219/system/uploads/images/nugget_configure_sources.png)

![Nuget add sources](http://52.10.147.219/system/uploads/images/nuget_add_package_source.png)

![Nuget source added](http://52.10.147.219/system/uploads/images/grial_nuget_source_added.png)


After adding Grial nuget source you will need to restore packages.


### <a name="nuget-access-setup"></a> Nuget Access Setup on Grial Admin

Grial 2.0 requires to setup a private Nuget source to get its packages.

Most of the cases you will use your Grial Admin credentials to authenticate.

Additionally, you can configure a dedicated nuget user to authenticate against the nuget server. You can share its credentials with your team and/or use them in your CI build servers.

To change this go to Grial Admin and then:

```
User Account > Profile > Nuget Access
```

** NOTE:** This can only be used to authenticate against the nuget server.

![](http://52.10.147.219/system/uploads/images/grial_admin_nuget_config.png)



### <a name="grial-license-setup"></a> Grial License Setup

Starting with Grial 2.0 you will need to register your user and your app to make use of Grial.

After you purchase the product and register your user on [Grial Admin website](https://uxdivers.com/secure/grial/front) you will be able to configure and download your Grial UI Kit custom solutions.

When you download the .zip fill containing both solutions (full and starter) the license file will be already included.
This file (called ***"GrialLicense"***) must have a BuildAction as EmbeddedResource, and must also be present in both platform projects (iOS and Android).

#### How it works?
The license verifies that the app name and package are the same on the license file (this is what was configured through Grial Admin and when the solution was downloaded).

In both platforms initializations (AppDelegate.cs and MainActivity.cs) the license will be invoked using the namespace configured on Grial Admin webiste as a parameter.

    Android -> UXDivers.Artina.Shared.GrialKit.Init(this, "UXDivers.Artina.Grial.GrialLicense");
    iOS -> UXDivers.Artina.Shared.GrialKit.Init(new ThemeColors(), "UXDivers.Artina.Grial.GrialLicense");

For example:

If your app is called ***"MySampleApp"***, after you register and download your custom Grial you will have the following on your projects:

    Android -> UXDivers.Artina.Shared.GrialKit.Init(this, "MySampleApp.GrialLicense");
    iOS -> UXDivers.Artina.Shared.GrialKit.Init(new ThemeColors(), "MySampleApp.GrialLicense");

***IMPORTANT***: In case you change your namespace through Grial admin you will need to download a ***NEW*** license and update your local "GrialLicense" file one in both projects (iOS and Android).


#### License modes

Basically there are two modes:

- Development
    - This is used while things are being developed and could change.
    - Expires in 30 days. In such case, it displays an error with a link to renew and download a new one.
    - Allows to renew the license as many times as could be needed.

- Production
    - ***Once in this mode there is no way to change it back***.
    - You use it once you are sure your project namespaces, etc., won't change. 


### Conventions
For your convenience we have structured the PCL project with the following folders:

       Grial
		|_ References
		|_ Packages
		|_ Helpers
		|_ Models
		|_ Properties
		|_ Themes
		|_ ViewModel
		|_ Views


## Theme And Branding Of Your App

Grial offers a simple way to customize the look and feel by providing an easy and extensible theme architecture. 
It provides several colors and styles that will ease your UI tweaks through platforms and achieving a consistent look and feel for your app.

To start customizing your app's look and feel, please refer to **App.xaml** file located on the Grial (PCL) folder project:

       Grial
		|_ App.xaml

Inside the file you will find basically two main things:

- Theme colors (through merged dictionaries)
	- These are the resources you will be mostly working with
- Theme styles, measures, images, etc. and other resources

	<Application.Resources> 

		<ResourceDictionary MergedWith="local:GrialLightTheme">
			<!--<ResourceDictionary MergedWith="local:GrialDarkTheme">-->
			<!--<ResourceDictionary MergedWith="local:GrialEnterpriseTheme">-->
			
			<!--	
				Use the following file as your theme colors.
				Simply replace colors to march your brand.
				(It is based on GrialLightTheme but you can use the colors
				of any other theme)
			-->
			<!--<ResourceDictionary MergedWith="local:MyAppTheme">-->
			...
		</ResourceDictionary>

	</Application.Resources>

A single resource dictionary (```local:GrialLightTheme```, is the Grial default theme for Grial 2.0) is actually being loaded and merged with the theme "base" resources.

There are 3 available themes you can use for your app:

#### **Light** (GrialLightTheme.xaml)
- ![](http://52.10.147.219/system/uploads/images/light0.png)
- ![](http://52.10.147.219/system/uploads/images/light1.png)
- ![](http://52.10.147.219/system/uploads/images/light2.png)



#### **Dark** (GrialDarkTheme.xaml)
- ![](http://52.10.147.219/system/uploads/images/dark0.png)
- ![](http://52.10.147.219/system/uploads/images/dark1.png)
- ![](http://52.10.147.219/system/uploads/images/dark2.png)


#### **Enterprise** (GrialEnterpriseTheme.xaml)
- ![](http://52.10.147.219/system/uploads/images/enterprise0.png)
- ![](http://52.10.147.219/system/uploads/images/enterprise1.png)
- ![](http://52.10.147.219/system/uploads/images/enterprise2.png)

These can be used as the starting point for your own theme.
An additional theme which is actually a copy of ```Grial Default theme``` (Light) is also provided so you can start working on that theme without changing the default ones:

- ***MyAppTheme*** (MyAppTheme.xaml)

If you want to change the current theme of your app, simply point the ```MergedWith``` attribute and point to any of the available themes (or simply uncomment the ones on ```App.xaml```).

### Themes files location

You can find the provided themes on the following location on your Grial PCL project: 

       Grial
		|_ Themes
			|_ GrialLightTheme.xaml
			|_ GrialDarkTheme.xaml
			|_ GrialEnterpriseTheme.xaml
			|
			|_ MyAppTheme.xaml

### Working with colors

The most important color is the **AccentColor** followed by the ***BaseTextColor***, which are used across the whole theme/app.
Basically changing these values will affect the overall look and feel of your App.

The theme is made with a "Top Down" approach, so the deeper you go into the theme styles the more specific tweaks are made.

### Compiling Themes

**Important**: Due to some limitations on Xamarin Forms it is not possible to style everything right from ```App.xaml```. 
That is the reason why when running our sample you can see most of the colors change but not the Navigaton Bar.

In Grial 2.0 we have added a new, easier and more reliable mechanism to compile theme colors on iOS and Android projects.

This is made through a ```Build Task``` so the process is transparent.

All you need to do is to set the theme on ```App.xaml``` through the ```MergedWith``` property, then the build task will:

- find the theme and propagate the theme's colors to
 - ```Colors.xml``` on the Android project
 - ```ThemeColors.cs``` on the iOS project

That way you will have everything in sync and only need to focus on the theme colors.

### Troubleshooting Themes Compilation
If your ```App.xaml``` file is not found, neither any xaml file whose root node is ```<Application>``` you will see the following warning on your build output:

***“Can’t find App.xaml file in ```<your_project>```. Aborting.”***

In order to instruct the build task the right path to your ```App.xaml``` or equivalent file, you will need to:

- Add a ***"Themes.json"*** file on your PCL project folder
- This file must exist in the file system but not necesarily on the project
- Add the following:

```
	{
		“AppXAMLPath” : “<absolute path of App.xaml in your project>” 
	}
```
Another possible output error from the build task can be:

*** "Unable to infer associated platform specific projects." ***

This means that the iOS and/or Android projects could not be automatically found, then, you must specify where are they located through these settings also on "Themes.json" file:

```
	{
		“AndroidProjectPath” : “<absolute path of your Android project>”,
 		“iOSProjectPath” : “<absolute path of your iOS project>”
	}
```

## Brand Image

We also provide an easy way to replace your app's logo by modifying an specific resource on ThemeDictionary, called **"BrandImage"**. Simply locate the resource and point it to your image file.

Additionally we provided an specific XAML view to help your branding needs, the **"BrandBlock.xaml"**, which can be found on the following location:


       Grial
		|_ Views
			|_ Common
				|_ BrandBlock.xaml
## <a name="using-font-icons"></a>Using Font Icons
Grial uses a common practice in design which is using icons through a font.

As icons are contained on a font it is really easy to use all the styling properties available to render a text control (`<Label>`):
    
* TextColor
* BackgroundColor
* FontSize

Since they are made from vectors they will render properly across different devices with different pixel densities. 
In other words, they will look sharp wherever you display them.

Grial 2.0 uses its own font: `GrialShapes.ttf` provided with Grial Sample.
All its icons are used on our sample and were made with Material Design Look and Feel.
The font acts as the source for basic shapes used on Grial's templates (circles, squares, etc.).
This way adding your font with your own icons should not create conflicts with Grial. 

### Adding your own icon font to you app

We have made easy to setup the fonts whitin the theme (App.xaml):

```
    <x:String x:Key="GrialShapesFontFamily">grialshapes</x:String>
    <!-- PUT YOUR OWN ICONS FONT FAMILY BELOW -->
    <x:String x:Key="IconsFontFamily">grialshapes</x:String>
    <!--<x:String x:Key="IconsFontFamily">FontAwesome</x:String>-->
    <!--<x:String x:Key="IconsFontFamily">Ionicons</x:String>-->
    ...

    <Style x:Key="FontIcon" TargetType="Label">				
        <Setter Property="FontFamily" Value="{ StaticResource IconsFontFamily }" />
    </Style>

    <Style x:Key="FontIconBase" TargetType="Label">
        <Setter Property="FontFamily" Value="{ StaticResource GrialShapesFontFamily }" />
    </Style>
```  

In the above code you can see that both styles are pointing actually to `grialshapes`.

Replace the `IconsFontFamily` resource with your font file name (for instance `FontAwesome`, `Ionicons`) then you will get all the basic shapes applied (for instance on badges, dashboard templates, etc.), but you will be able to change the icons displayed on the App. 

**NOTE:** Grial 2.0 comes with latest 
[fontawesome 4.7](http://fontawesome.io/icons/) and [ionicons 2.0.0](http://ionicons.com/cheatsheet.html) fonts added to the projects (iOS and Android) and also its helper classes to easily get the icons' characters:
~~~
 Grial
    |_ Helpers
       |_ FontawesomeFont.cs
       |_ GrialShapesFont.cs
       |_ IoniciconsFont.cs
~~~

Referencing icons will be easier this way.
For more info check [referencing icons on code behind and XAML](#using-icons-cs-and-xaml).


If you want to include this font on your compilation then please check [adding font icons to your project procedure](#adding-font-icons-to-your-project)

If you don't have the chance to produce the helper file with all the characters mappings for your icons you can directly use this procedure:

1. Go to [Weather icons](https://erikflowers.github.io/weather-icons/)
2. Find the icon you need on the page.
3. Copy the unicode value of that icon (something like **f00d**)
4. If you are using the icon on a .XAML file, you should use it as **"&#x"** + **UNICODE** + **";"**
5. If you are using the icon on a .CS file, you should use it as **"\u"** + **UNICODE**

Alternatively you can create your own font including your icons and add it to your project following previous steps.

**Important: Icons can ONLY be used on `<Label>` controls.**
## Artina Custom Renderers

​Xamarin Forms allows to customize only some properties of its UI controls. 
Usually a professional UI requires further customization. 
This can be achieved through Custom Renderers.

Artina provides a set of Custom Renderers and attached properties to improve the styling capabilities of Xamarin Forms' UI controls. 

For example, the Artina attached properties for an `<Entry>` control:

	<Entry
		...
		artina:EntryProperties.BorderStyle="BottomLine"
		artina:EntryProperties.BorderWidth="1"
		... />

* Artina attached properties:
	* `BorderStyle` 
		* Allows to customize how the border should look like.
		* Possible values are:
			* `None` 
				* Forces no border to be shown at all.
			* `BottomLine`
				* Renders a single line at the bottom of the entry.
			* `Rect`
				* Rect draws a rectangle around the Entry. 
			* `RoundRect`
				* Renders a rectangle with rounded corners.
			* `Default`
				* Default value.
	* `BorderWidth`
		* The width in pixels fo the border
	* `BorderCornerRadius`
		* The corner radiu in pixels
	* `BorderColor`
		* The color to be used for rendering the border

Besides of specifing the attached properties, we must instruct Xamarin Forms to use the appropiate Custom Renderer (in this case ArtinaEntryRenderer) which is the one that knows how these properties should be renderer.

Custom Renderers in Grial are declared in the `AssemblyInfo` file of the ***Grial.iOS*** and ***Grial.Droid*** projects.


If you want to use the attached properties in a different project you need to know that:

- Attached properties
	- Defined on the assembly **UXDivers.Artina.Shared.**, therefore you must reference it from your Xamarin Forms project (PCL).
- Custom Renderers 
	- Defined in **UXDivers.Artina.Shared.Droid** for Android 
		- On Android you need to reference both **UXDivers.Artina.Shared.** and **UXDivers.Artina.Shared.Droid**.
	- Defined on  **UXDivers.Artina.Shared.iOS** for iOS. 
		- On your iOS project you will need to reference both **UXDivers.Artina.Shared.** and **UXDivers.Artina.Shared.iOS**. 

For more info check 
[Setting Up Artina Dlls in your project ](#setting-artina-dlls)
and
[Setting Up Artina Custom Renderers in your project ](#artina-custom-renderers-setup)
## Splash Screen
Grial provides the needed infrastructure for your app to display your app's splash image.


**On Android:**

Starting from Grial 2.0 the Android splashes are responsive, which means they adapt to the size and orientation of your device.

This is made through the theme, a drawable called **"splash_drawable.xml"** and its background image called `splash.png`.

Since the splash is styled through the theme it is easy to setup the background color. 
By default it uses the **"ComplementColor"** but you can change it to any color by editing "**splash_drawable.xml"**.

Most of the cases you will only replace all the **"splash.png"** images files with yours.

    Grial
		|_ Grial.Droid
			|_ resources
				|_ drawable
					|_ splash.png
					|_ splash_drawable.xml
				|_ drawable-hdpi
					|_ splash.png
				|_ drawable-xhdpi
					|_ splash.png
				|_ drawable-xxhdpi
					|_ splash.png

**On iOS:**

Starting from Grial 2.0 the iOS splashes are responsive, which means they adapt to the size and orientation of your device.

We also use the new Unified Storyboards available from iOS 9+.
This eases the process since less images are required than before. 

Basically there is a single storyboard used across all different devices (phones and tablets).
It contains a centered image (```splash.png```) which is horixontally and vertically centered.

Most of the cases you will only replace all the **"splash.png"** images files with yours.

It is also possible to change the background color of the view which contains the image.

     Grial
		|_ Grial.iOS
			|_ Splash.storyboard
			|_ Resources
				|_ splash.png
				|_ splash@2x.png
				|_ splash3x.png
<!--- ## Grial Themes

Starting from Grial 2.0 we provide 3 themes:

* Default (Light Dark)
* Light
* Dark

-----------

  ````
  Grial (PCL)
    |_ Themes
      |_ Grial.Default.Theme.xaml
      |_ Grial.Dark.Theme.xaml
      |_ Grial.Light.Theme.xaml
  ````

  ### Grial Default Theme ###
  
  This is the default theme inside Grial sample `App.xaml`, you won't need to do anything to see it applied on your App.

  ![Grial Default Theme Preview](http://52.10.147.219/system/uploads/images/default_theme_preview_1.png)
  ![Grial Default Theme Preview](http://52.10.147.219/system/uploads/images/default_theme_preview_2.png)
  ![Grial Default Theme Preview](http://52.10.147.219/system/uploads/images/default_theme_preview_3.png)


  ### Grial Dark Theme ###
  
  This is the Dark theme. You will need to 
  follow the [Update Grial Theme On Your App Procedure](#update-grial-theme-on-your-app-procedure)

  ![Grial Default Theme Preview](http://52.10.147.219/system/uploads/images/dark_theme_preview_1.png)
  ![Grial Default Theme Preview](http://52.10.147.219/system/uploads/images/dark_theme_preview_2.png)
  ![Grial Default Theme Preview](http://52.10.147.219/system/uploads/images/dark_theme_preview_3.png)

  ### Grial Light Theme ###
  
  This is the Light theme. You will need to 
  follow the [Update Grial Theme On Your App Procedure](#update-grial-theme-on-your-app-procedure)

  ![Grial Default Theme Preview](http://52.10.147.219/system/uploads/images/light_theme_preview_1.png)
  ![Grial Default Theme Preview](http://52.10.147.219/system/uploads/images/light_theme_preview_2.png)
  ![Grial Default Theme Preview](http://52.10.147.219/system/uploads/images/light_theme_preview_3.png)


### <a name="update-grial-theme-on-your-app-procedure"></a>Update Grial Theme On Your App ###

In order to update your App's theme with any of the Grial themes you will need to manually update several files:

1. Open your theme file (Light, Dark or Default theme) on the Themes folder:

    ````
    Grial (PCL)
    |_ Themes
        |_ Grial.Default.Theme.xaml
        |_ Grial.Dark.Theme.xaml
        |_ Grial.Light.Theme.xaml
    ````
2. Copy its content and replace your ```App.xaml``` file content.
    
    ***Note***: If you added more styles to your App's theme remember to add those after copying and pasting, otherwise you will lose those.

3. Update the ***Android*** ```Colors.xml``` file.
    
    We have added the relative colors already set and commented, so you will only need to uncomment the values for your selected theme.

4. Update the ***iOS*** ```ExportedColors.cs``` file.
    
    We also left the values commented on this file so you will need to uncomment the values for your selected theme.

5. You will need to compile your app to see the theme applied.  --->

## Helpers

### GrialShapes Font

Starting from Grial 2.0 we provide a helper with all the keys of each icon, making it easier to work with font icons:

![GrialShapes.cs](http://52.10.147.219/system/uploads/images/grial-shapes-cs.png)

In order to ease the process, Grial provides a page to preview all the icons bundled with the grial font:
You can preview this page on the following location on Grial sample:

```Grial Theme > Grial Font Icons```

![GrialShapes.cs](http://52.10.147.219/system/uploads/images/grial-font-icons.png)

#### <a name="using-icons-cs-and-xaml"></a>Referencing icons on Code Behind and XAML

If you are on code behind you will need to call the right font helper and the selected icon like this:

~~~
    GrialShapesFont.Star;
~~~

On XAML you will need to use it this way:

~~~
    <Label
        Style="{ StaticResource FontIcon }"
        Text="{ x:Static local:GrialShapesFont.Star }" />
~~~

***Note***: Rememeber to add the right namespace and assembly names for the ```xmlns:local```:
You will also need to make sure the namespaces are the right ones. 
For more info check [Adding pages and templates to your project](#adding-pages-and-templates-to-your-project).

~~~
	xmlns:local="clr-namespace:YOUR_NAMESPACE_HERE;assembly=YOUR_ASSEMBLY_HERE">
~~~


### Navigation Service
This is a service made with the only purpose of handling Grial sample.


### Responsive Helpers

***Grial 2.0*** adds support for responsive design.
This is a powerful addition made over Xamarin Forms. 
Now it is possible to have full control on how things layout on pages and how they react to orientation changes.

The available properties listed by specificity are:

- `Default`
    - This applies to ALL cases by default.
- `Portrait`
    - Applies only when the device (cellphone, tablet or desktop) is in portrait orientation.
- `Landscape`
    - Applies only when the device (cellphone, tablet or desktop) is in landscape orientation.

- `PortraitPhone`
    - Applies only when the device is a phone and is in portrait orientation.
- `PortraitTablet`
    - Applies only when the device is a tablet and is in portrait orientation.
- `PortraitDesktop`
    - Applies only when the device is a desktop and is in portrait orientation.

- `LandscapePhone`
    - Applies only when the device is a phone and is in landscape orientation.
- `LandscapeTablet`
    - Applies only when the device is a tablet and is in landscape orientation.
- `LandscapeDesktop`
    - Applies only when the device is a desktop and is in landscape orientation.

All can be used in conjunction with the following types:

`Int|Color|String|Bool|LayoutOptions`

Usage:
~~~
<VisualElement Property="{ artina:OnOrientation|type responsiveCase=value }" />
~~~

It is possible to control how things display on a tablet landscape and how the should flow on a phone.  

Things can go deeper in customization adding more specificity to your declarations:


~~~
<Label
    Text="{ 
        artina:OnOrientationString 
            Portrait=IsPortrait, 
            Landscape=IsLandscape
        }" 
    TextColor="{ 
        artina:OnOrientationColor
            Default=Red,
            PortraitDesktop=Green 
        }"
    Rotation="{ 
        artina:OnOrientationInt 
            Default=0, 
            Landscape=90 
        }"
    IsVisible="{ 
        artina:OnOrientationBool 
            Default=true, 
            PortraitDesktop=false 
        }"
    HorizontalOptions="{ 
        artina:OnOrientationLayoutOptions
            PortraitPhone=Fill,
            LandscapePhone=Center,
            PortraitTablet=Fill,
            LandscapeTablet=Center 
        }"
/> 
~~~

It can be even used on styles:
~~~
    ...
    <Setter 
        Property="WidthRequest" 
        Value="{ 
            artina:OnOrientationInt 
                Portrait=-1,
                Landscape=700
        }" 
    />
    ...
~~~

In the above example, the value ```-1``` is used to reset the value to the default value (WidthRequest on Xamarin Forms with value ```-1``` acts as there is no width set at all).

For more examples please check:

~~~
   Grial
    |_ Views
        |_ ResponsiveHelpersPage.xaml
~~~

![Grial Responsive Helpers](http://52.10.147.219/system/uploads/images/responsive_helpers_page.png)



## Setting Up Grial On A Xamarin Forms Project

### Using Grial Sample

The fastest way for you to jump on Grial and start building your app or prototype is directly working on the sample provided with your purchase.

***NOTE:*** Starting from Grial 2.0 we allow to download your own customized Grial project and also a minimum project (Grial Starter) also customized with your namespace, assembly names, etc., so you don't have to waste time manually setting everything up.
For more info check [Downloading Grial](#grial-download).

It cover all the templates showing how to use them with its pages, templates, bindings, styles, navigation, etc.
So it is really easy just to use it as the base for your project.

***No project setup needed!*** 

The main reason why it will be easier is because you won't have to worry about setting up the project manually copying files to the right place, changing build options, etc.

### Grial Sample Project Structure

Typically Grial makes use of:

* `UXDivers.Artina.Shared.dll`
 * Contains Controls and Custom Renderers
* Pages, views and templates (XAML files)
* Grial theme 
  * `App.xaml`
   * Contais colors, main styles and resources shared across all the platforms
  * Platform specific styles and resources
* Navigation service
 * This is used across Grial sample to manage the Navigation
 * You can replace it with your own navigation mechanism.
* Image resources
 * These are the images used across all the project using Grial
 * Each platform needs its own images with their standard name and location


### <a name="setting-artina-dlls"></a>Setting Up Artina Dlls in your project

As mentioned before, Artina dlls contains most of our controls and Custom Renderers, so it is crucial you add them correctly into your project by following these steps:

1. In your ***PCL*** add references to:
 * ```UXDivers.Artina.Shared.dll```
 
  ![Artina.Shared on PCL](http://52.10.147.219/system/uploads/images/artina_shared_on_pcl.png)

2. In your Android project add references to: 
 * ```UXDivers.Artina.Shared.dll```
 * ```UXDivers.Artina.Shared.Droid.dll```

  ![Artina.Shared on Android](http://52.10.147.219/system/uploads/images/artina_shared_on_android.png)

3. In your iOS project add references to:
 * ```UXDivers.Artina.Shared.dll```
 * ```UXDivers.Artina.Shared.iOS.dll```

  ![Artina.Shared on iOS](http://52.10.147.219/system/uploads/images/artina_shared_on_ios.png)

  
### <a name="grial-license-setup"></a> Grial License Setup

Starting with Grial 2.0 you will need to register your user and your app to make use of Grial.

After you purchase the product and register your user on [Grial Admin website](https://uxdivers.com/secure/grial/front) you will be able to configure and download your Grial UI Kit custom solutions.

When you download the .zip fill containing both solutions (full and starter) the license file will be already included.
This file (called ***"GrialLicense"***) must have a BuildAction as EmbeddedResource, and must also be present in both platform projects (iOS and Android).

#### How it works?
The license verifies that the app name and package are the same on the license file (this is what was configured through Grial Admin and when the solution was downloaded).

In both platforms initializations (AppDelegate.cs and MainActivity.cs) the license will be invoked using the namespace configured on Grial Admin webiste as a parameter.

    Android -> UXDivers.Artina.Shared.GrialKit.Init(this, "UXDivers.Artina.Grial.GrialLicense");
    iOS -> UXDivers.Artina.Shared.GrialKit.Init(new ThemeColors(), "UXDivers.Artina.Grial.GrialLicense");

For example:

If your app is called ***"MySampleApp"***, after you register and download your custom Grial you will have the following on your projects:

    Android -> UXDivers.Artina.Shared.GrialKit.Init(this, "MySampleApp.GrialLicense");
    iOS -> UXDivers.Artina.Shared.GrialKit.Init(new ThemeColors(), "MySampleApp.GrialLicense");

***IMPORTANT***: In case you change your namespace through Grial admin you will need to download a ***NEW*** license and update your local "GrialLicense" file one in both projects (iOS and Android).


#### License modes

Basically there are two modes:

- Development
    - This is used while things are being developed and could change.
    - Expires in 30 days. In such case, it displays an error with a link to renew and download a new one.
    - Allows to renew the license as many times as could be needed.

- Production
    - ***Once in this mode there is no way to change it back***.
    - You use it once you are sure your project namespaces, etc., won't change. 
### <a name="adding-font-icons-to-your-project"></a> Adding Font Icons To Your Project


##### For iOS:

1. Add the font file: `grialshapes.ttf` 
to the 
`Resources` 
folder on your iOS project, then set it to:
***BundleResource***, just like in the sample app.

![iOS bundle resource](http://52.10.147.219/system/uploads/images/ios_bundle_resource.png)

2. Then add the following to your **info.plist** file:
```
<key>UIAppFonts</key>
<array>
    <string>grialshapes.ttf</string>
</array>
```
**NOTE:** The display name for the **UIAppFonts** in the ```info.plist``` editor is ```'Fonts provided by application'```.

![iOS info.plist](http://52.10.147.219/system/uploads/images/info_plist_ios.png)


##### For Android:

* Copy the file: 
`CustomFontLabelRenderer.cs` from Grial's sample project (located on ```Grial.Droid/Renderers```) to your Android project.

    ![CustomFontLabelRenderer.cs](http://52.10.147.219/system/uploads/images/custom-font-label-renderer.png)

* Then add the file:
`grialshapes.ttf`
to the 
`/Assets` folder on your Android project.

    ![Grial Shapes font.cs](http://52.10.147.219/system/uploads/images/android-font-asset.png)


* Select the file, and make sure the ***Build Action*** is set to:
`"AndroidAsset"`
in the Properties tab. (This is normally its default setting).

    ![AndroidAsset](http://52.10.147.219/system/uploads/images/android-build-action-asset.png)

* [Register the icons custom renderer](#artina-custom-renderers-setup) (`CustomFontLabelRenderer`)
on the `AssemblyInfo.cs` file with the following code (remember to use your custom namespace:

    ```[assembly: ExportRenderer(typeof(Label), typeof(YOUR_CUSTOM_NAMESPACE_HERE.Renderers.CustomFontLabelRenderer))]```

    ![iOS AssemblyInfo](http://52.10.147.219/system/uploads/images/assembly-info.png)

* Copy the ```CustomFontLabelRenderer.cs``` file from Grial sample to your Android project:
~~~
 Grial.Droid
    |_ Renderers
       |_ CustomFontLabelRenderer.cs
~~~
Remember to use the right namespaces according to your project.

* Open the recently copied ```CustomFontLabelRenderer.cs``` on your Android project, then add a reference to your font if it not there (```grialshapes``` is present by default).



### Grial Theme Setup
Grial's theme is made on top of:

* Android theme and resources
* iOS appeareance
* Custom Renderers on Artina.Shared dll
* Styles on `App.xaml` file

### Android Theme Setup

***Overview***: You will need to copy specific files from the ***Grial.Droid*** project Resources folder to your Android project and set the theme on the ```MainActivity.cs``` file.

![Android themes and layouts](http://52.10.147.219/system/uploads/images/grial-droid-themes-and-layouts.png)

***Important:*** Make sure you are using ***AppCompatV7*** on you project!


1. Start by copying the ***"Colors.xml"*** file and the theme files, both are named **"Style.xml"** and can be found on the folders:

  ````
  Grial.Droid
    |_ values
    |  |_ Colors.xml
    |  |_ Style.xml
    |
    |_ values-v21
      |_ Style.xml 
  ````
  You will need to paste them on the same location of your Android project.  
  These files are responsible for setting the colors and styles on Android apps.

2. Also, you will need to copy the files ***"Tabs.axml"*** and ***"Toolbar.axml"*** on the **layout** folder:

  ````
  Grial.Droid
    |_ layouts
      |_ Tabs.axml
      |_ Toolbar.axml
  ````

3. Finally, you will need to set the splash and on the `OnCreate` event switch to the theme on your `MainActivity.cs`.
  Just take a look at the `MainActivity.cs` provided with Grial sample on ***Grial.Droid*** project for better reference:

  ~~~
      ...
      namespace UXDivers.Artina.Grial

        {
          //https://developer.android.com/guide/topics/manifest/activity-element.html
          [Activity (
            Label = "Grial UIKit",
            Icon="@drawable/icon",
            Theme = "@style/Theme.Splash",
            MainLauncher = true,
            LaunchMode = LaunchMode.SingleTask,
            ConfigurationChanges = ConfigChanges.Orientation | ConfigChanges.ScreenSize
            )
          ]

          public class MainActivity : FormsAppCompatActivity
          {
            protected override void OnCreate (Bundle bundle)
            {
              // Changing to App's theme since we are OnCreate and we are ready to 
              // "hide" the splash
              base.Window.RequestFeature(WindowFeatures.ActionBar);
              base.SetTheme(Resource.Style.AppTheme);

              base.OnCreate (bundle);

              global::Xamarin.Forms.Forms.Init (this, bundle);

              ...
            }
          }

        }

  ~~~



### iOS Theme Setup

***Overview***: You will need to copy ```ThemeColors.cs``` file from the ```Grial.iOS``` project to your iOS project and you will need to invoke it from `AppDelegate.cs` file in order to get the styles applied.

  ![Grial iOS ThemeColors.cs](http://52.10.147.219/system/uploads/images/grial-ios-appearance.png) 

1. Copy **"ThemeColors.cs"** file from Grial sample to your iOS folder on your project.
  This file is the responsible for the styling iOS apps.

2. Finally, you will need to add this call on your `AppDelegate.cs` file:

```
UXDivers.Artina.Shared.GrialKit.Init( new ThemeColors(), "UXDivers.Artina.Grial.GrialLicense" );
```

***NOTE:*** Replace the above with your Grial license as explained on:
[Grial License Setup](#-grial-first-run-grial-license-setup).


#### Avoiding your App crashing on iOS
If you take over all the content of the `App.xaml` from the sample project, you app will crash on startup with an exception about not finding
`UXDivers.Artina.Shared.iOS.dll`.

Even though you have added a reference to the file in your **iOS project**, the linker cannot see it as you are not using directly from code, but only via the **XAML** files.

Therefore you need to add the `AssemblyInfo.cs` file from the sample project, which will make the linker include the
`UXDivers.Artina.Shared.iOS.dll` in your iOS build.





### <a name="artina-custom-renderers-setup"></a>Setting Up Artina Custom Renderers in your project

Grial makes use of several custom renderers declared on each platform through its own ```AssemblyInfo.cs``` file.
In order to get them available for your project you will need to add them to your ```AssemblyInfo.cs``` files on each project (PCL, Android, iOS).

For more info check: [Setting Up Artina Dlls in your project ](#setting-artina-dlls). 

**NOTE:** Depending on your needs, you could need to customize the Grial theme for your app. Also you could not need some of the custom renderers so in such case you can simply not declare them on your project.

#### Android Setup

1. Open the file ```AssemblyInfo.cs``` on your Android project:

  Grial.Droid
    |_ Properties
      |_ AssemblyInfo.cs

2. Paste the custom renderers definitions from Grial sample's ```AssemblyInfo.cs``` (also on the same folder form previous step):
    ~~~
    // Custom renderer definition.

    [assembly: ExportRenderer(typeof(Entry), typeof(UXDivers.Artina.Shared.ArtinaEntryRenderer))]
    [assembly: ExportRenderer(typeof(Editor), typeof(UXDivers.Artina.Shared.ArtinaEditorRenderer))]
    [assembly: ExportRenderer(typeof(Label), typeof(UXDivers.Artina.Grial.CustomFontLabelRenderer))]
    [assembly: ExportRenderer(typeof(Switch), typeof(UXDivers.Artina.Shared.ArtinaSwitchRenderer))]
    [assembly: ExportRenderer(typeof(ActivityIndicator), typeof(UXDivers.Artina.Shared.ArtinaActivityIndicatorRenderer))]
    [assembly: ExportRenderer(typeof(ProgressBar), typeof(UXDivers.Artina.Shared.ArtinaProgressBarRenderer))]
    [assembly: ExportRenderer(typeof(Slider), typeof(UXDivers.Artina.Shared.ArtinaSliderRenderer))]
    [assembly: ExportRenderer(typeof(SwitchCell), typeof(UXDivers.Artina.Shared.ArtinaSwitchCellRenderer))]
    [assembly: ExportRenderer(typeof(TextCell), typeof(UXDivers.Artina.Shared.ArtinaTextCellRenderer))]
    [assembly: ExportRenderer(typeof(ImageCell), typeof(UXDivers.Artina.Shared.ArtinaImageCellRenderer))]
    [assembly: ExportRenderer(typeof(ViewCell), typeof(UXDivers.Artina.Shared.ArtinaViewCellRenderer))]
    [assembly: ExportRenderer(typeof(EntryCell), typeof(UXDivers.Artina.Shared.ArtinaEntryCellRenderer))]
    [assembly: ExportRenderer(typeof(SearchBar), typeof(UXDivers.Artina.Shared.ArtinaSearchBarRenderer))]
    [assembly: ExportRenderer(typeof(UXDivers.Artina.Shared.Button), typeof(UXDivers.Artina.Shared.ArtinaButtonRenderer))]
    ~~~

#### iOS Setup

1. Open the file ```AssemblyInfo.cs``` on your iOS project:
  ````
  Grial.iOS
    |_ Properties
      |_ AssemblyInfo.cs
  ````
2. Paste the custom renderers definitions from Grial sample's ```AssemblyInfo.cs``` (also on the same folder form previous step):
    ~~~
    // Custom renderer definition

    [assembly: ExportRenderer(typeof(UXDivers.Artina.Shared.CircleImage), typeof(UXDivers.Artina.Shared.ImageCircleRenderer))]
    [assembly: ExportRenderer(typeof(EntryCell), typeof(UXDivers.Artina.Shared.ArtinaEntryCellRenderer))]
    [assembly: ExportRenderer(typeof(ImageCell), typeof(UXDivers.Artina.Shared.ArtinaImageCellRenderer))]
    [assembly: ExportRenderer(typeof(SwitchCell), typeof(UXDivers.Artina.Shared.ArtinaSwitchCellRenderer))]
    [assembly: ExportRenderer(typeof(TableView), typeof(UXDivers.Artina.Shared.ArtinaTableRenderer))]
    [assembly: ExportRenderer(typeof(TextCell), typeof(UXDivers.Artina.Shared.ArtinaTextCellRenderer))]
    [assembly: ExportRenderer(typeof(ViewCell), typeof(UXDivers.Artina.Shared.ArtinaViewCellRenderer))]

    [assembly: ExportRenderer(typeof(Entry), typeof(UXDivers.Artina.Shared.ArtinaEntryRenderer))]
    [assembly: ExportRenderer(typeof(Picker), typeof(UXDivers.Artina.Shared.ArtinaPickerRenderer))]
    [assembly: ExportRenderer(typeof(DatePicker), typeof(UXDivers.Artina.Shared.ArtinaDatePickerRenderer))]
    [assembly: ExportRenderer(typeof(TimePicker), typeof(UXDivers.Artina.Shared.ArtinaTimePickerRenderer))]

    #pragma warning disable 219
    internal static class WorkaroundLoadingCustomRenderersFromExternalAssemblies {
        static WorkaroundLoadingCustomRenderersFromExternalAssemblies()
        {
            var a = new UXDivers.Artina.Shared.ArtinaEntryRenderer();
        }
    }
    #pragma warning restore 219
    ~~~

**NOTE:** Remember to add the required namespaces at the top of both ```AssemblyInfo.cs``` files:
~~~
using Xamarin.Forms;
using UXDivers.Artina;
~~~

**TROUBLESHOOT**

In case you get the following exception:
![Grial License Exception](http://52.10.147.219/system/uploads/images/grial_license_exception.png)
please check [Grial License Setup](#grial-license-setup).

### Styles on App.xaml file

```App.xaml``` file centralizes all the theme resources used (colors, values, images, styles, etc.) on Grial sample.

We recommend is just to copy them to your App.xaml file on your new project.

Probably you will not use all of them but you can do that optimization part -remove not used resources, move resources to specific pages that uses them- later. 

The easiest way to make everything work at first will be just to copy everything.




### <a name="adding-pages-and-templates-to-your-project"></a> Adding pages and templates to your project

Now that you have the needed infrastructure for Grial theme it is time for you to use the pages and templates.

Basically you will need to copy and paste pages (`ContentPages`) and its templates (`ContentViews`) from Grial Sample to your project.

Pages reference templates using xml namespaces defined on the header of the document. 
This is typically something like the following:

```
xmlns:views="clr-namespace:UXDivers.Artina.Grial;assembly=UXDivers.Artina.Grial"
```

Since your pages will be on another assembly, you will need to change at least the assembly name by the one from the PCL assembly where these pages will be:

```
xmlns:local="clr-namespace:YOUR_NAMESPACE_HERE;assembly=YOUR_ASSEMBLY_HERE"
```

If you need to change the namespace on the pages and templates (`ContentViews`) you will need to change also the ```"clr-namespace"```. 
Here is an example for the ```MY_PROJECT``` project:

```
  <?xml version="1.0" encoding="UTF-8"?>
  <ContentView 
    ...
    xmlns:views="clr-namespace:MY_PROJECT;assembly=MY_PROJECT"
    x:Class="MY_PROJECT.Badge"
    ...
  >
```

It will be also neccessary to change ```x:Class``` as the code behind.

On your project's code behind typically you will need to replace the sample data view models with your app's ones.



### Gorilla Player

Finally, if you are using [Gorilla Player](http://gorillaplayer.com) remember to copy the `SampleData.json` file from the Grial sample to your project to allow previewing it. 

You will probably need to update your ```SampleData.json``` file to correctly feed your views with data according to your pages/templates names and data structures.

For more info please check:
https://github.com/UXDivers/Gorilla-Player-Support/wiki/Working-with-sample-data




## UI Templates

Grial provides templates which cover common UI patterns in mobile apps.

Each one of them is fully functional page sample, with its code behind and data bindings to help bootstrapping your app or prototype.

Basically the templates fit two categories, the **Common** ones:
    
	   Grial
		|_ Views
			|_ Common

...and the specific ones:

       Grial
		|_ Views
			|_ Articles
			|_ Dashboards
			|_ Ecommerce
			|_ Logins
			|_ Messages
			|_ Navigation
			|_ Settings
			|_ Social
			|_ Theme
			|_ Walkthrough

Inside each category folder you will find sample pages and in most cases item templates (used as items in repeaters controls such as ListViews). Take a look at the **Dashboards** folder as an example:

	   Grial
		|_ Views
			|_ Dashboards
				|_ Templates
				|	|_ DashboardItemTemplate.xaml
				|
				|_ DashboardWithImages.xaml
				|_ Dashboard.xaml
				|_ DashboardFlat.xaml


The **"DashWidgetView.xaml"** contains the common template that will be used in all of the dashboards pages.

### The common views

Common views are ContentViews that are used often more than once in an app. 

	   Grial
		|_ Views
			|_ Common				
				|_ Badge.xaml
				|_ BrandBlock.xaml
				|_ CircleIcon.xaml
				|_ CustomNavBar.xaml
				|_ CustomActivityIndicator.xaml
				|_ Rating.xaml
				|_ RoundedLabel.xaml

To visualize them simply run the sample app and go to:

	Grial Theme > Grial Common Views

---
###Badge.xaml

This is a ContenView which mimics a Badge Control.

***NOTE:*** You need to copy the ```Badge.xaml``` and its ```Badge.xaml.cs``` to your project in order to get this control available for your app.

To include it in your page first add the right namespace and assembly names for the ```xmlns:local```:
You will also need to make sure the namespaces are the right ones. 
For more info check [Adding pages and templates to your project](#adding-pages-and-templates-to-your-project).

~~~
	<?xml version="1.0" encoding="UTF-8"?>
		<ContentPage
			...
			xmlns:local="clr-namespace:YOUR_NAMESPACE_HERE;assembly=YOUR_ASSEMBLY_HERE">
~~~

Then place it on your page: 

~~~
	<local:Badge 
		BadgeText="My Badge" 
		BadgeTextColor="#FFFFFF" 
		BadgeBackgroundColor="#FF0000"
	>
~~~

The bindable properties are:

- **BadgeText** String
- **BadgeBackgroundColor** Color
- **BadgeTextColor** Color

---
###BrandBlock.xaml###

This is a ContenView which holds the app logo and branding info.

To include it in your page first add the right namespace and assembly names for the ```xmlns:local```:
You will also need to make sure the namespaces are the right ones. 
For more info check [Adding pages and templates to your project](#adding-pages-and-templates-to-your-project).

~~~
	<?xml version="1.0" encoding="UTF-8"?>
		<ContentPage
			...
			xmlns:local="clr-namespace:YOUR_NAMESPACE_HERE;assembly=YOUR_ASSEMBLY_HERE">
~~~

Then simply add it on our page:

	<local:BrandBlock />

***NOTE:*** This is not a bindable view.
Make also sure you have added all the resources used by this view, like the image on the theme, its colors, styles and images available on the different projects (Android and iOS).

---
###CircleIcon.xaml###

This is a ContenView that renders an icon inside a circle.

To include it in your page first add the right namespace and assembly names for the ```xmlns:local```:
You will also need to make sure the namespaces are the right ones. 
For more info check [Adding pages and templates to your project](#adding-pages-and-templates-to-your-project).


~~~
	<?xml version="1.0" encoding="UTF-8"?>
		<ContentPage
			...
			xmlns:local="clr-namespace:YOUR_NAMESPACE_HERE;assembly=YOUR_ASSEMBLY_HERE">
~~~

Then simply add it on our page:

	<commonViews:CircleIcon />

***NOTE:*** This is not a bindable view.
Make sure you are using ```grialshapes.ttf``` and got all its setup made in order to get the right visualization.
For more info, check [Adding Font Icons To Your Project](#adding-font-icons-to-your-project)

---
###CustomNavBar.xaml###

This is a ContenView which aims to replace standard ActionBar/NavBar. If you use it on a Master/Detail page it will trigger the menu states (presented or not). 

The main benefits are that:

- You can fully customize the look and feel and use font icons
- It will be displayed over the NavBar/ActionBar 

To make it look as native on your app, first you need to hide the real NavBar/ActionBar. To achieve it, simply go to the code behind file of your page and add the following:

    InitializeComponent ();
	NavigationPage.SetHasNavigationBar(this, false);

To include it in your page first add the right namespace and assembly names for the ```xmlns:local```:
You will also need to make sure the namespaces are the right ones. 
For more info check [Adding pages and templates to your project](#adding-pages-and-templates-to-your-project).


~~~
	<?xml version="1.0" encoding="UTF-8"?>
		<ContentPage
			...
			xmlns:local="clr-namespace:YOUR_NAMESPACE_HERE;assembly=YOUR_ASSEMBLY_HERE">
~~~

Then simply add it on our page:

~~~
	<local:CustomNavBar />
~~~

***Note:*** This is not a bindable view.

---
###CustomActivityIndicator.xaml###

This is a ContenView which contains an animated logo of your brand which you can use for instance to show a loading message while your app is fetching information.

***NOTE:*** You need to copy the ```CustomActivityIndicator.xaml``` and its ```CustomActivityIndicator.xaml.cs``` to your project in order to get this control available for your app.
You will also need to make sure the namespaces are the right ones. 
For more info check [Adding pages and templates to your project](#adding-pages-and-templates-to-your-project).

To include it in your page first add the namespace:

~~~
	<?xml version="1.0" encoding="UTF-8"?>
		<ContentPage
			...
			xmlns:local="clr-namespace:YOUR_NAMESPACE_HERE;assembly=YOUR_ASSEMBLY_HERE">
~~~

Then simply add it on our page:

	<local:CustomActivityIndicator />

***NOTE:*** This is not a bindable view.

---
###Rating.xaml###

Rating is an easy way for users to voice their opinion about a certain object.

***NOTE:*** You need to copy the ```Rating.xaml``` and its ```Rating.xaml.cs``` to your project in order to get this control available on your project.

To include it in your page first add the right namespace and assembly names for the ```xmlns:local```:
You will also need to make sure the namespaces are the right ones. 
For more info check [Adding pages and templates to your project](#adding-pages-and-templates-to-your-project).


~~~
	<?xml version="1.0" encoding="UTF-8"?>
		<ContentPage
			...
			xmlns:local="clr-namespace:YOUR_NAMESPACE_HERE;assembly=YOUR_ASSEMBLY_HERE">
~~~

Then simply add it on our page:

~~~
	<local:Rating 
        Max="10" 
        Value="5" />
~~~

The bindable properties are:

- **Value** Double
- **Max** Double

###RoundedLabel.xaml###

The RoundedLabel as its name suggests, is just a ```<Label/>``` with rounded corners.

***NOTE:*** You need to copy the ```RoundedLabel.xaml``` and its ```RoundedLabel.xaml.cs``` to your project in order to get this control available for your app.
You will also need to make sure the namespaces are the right ones. 
For more info check [Adding pages and templates to your project](#adding-pages-and-templates-to-your-project).

To include it in your page add the namespace:

~~~
	<?xml version="1.0" encoding="UTF-8"?>
		<ContentPage
			...
			xmlns:local="clr-namespace:YOUR_NAMESPACE_HERE;assembly=YOUR_ASSEMBLY_HERE">
~~~

Then simply add it on our page:

~~~
	<local:RoundedLabel
		RoundedLabelText="Hello Rounded World!"
		RoundedLabelTextColor="White"
		RoundedLabelBackgroundColor="#00FF00" 
		RoundedLabelCornerRadius="4"
		RoundedLabelPadding="6,0"
		RoundedLabelFontSize="10"
	/>
~~~

The bindable properties are:

- **RoundedLabelText** String
- **RoundedLabelTextColor** Color
- **RoundedLabelBackgroundColor** Color
- **RoundedLabelCornerRadius** Double
- **RoundedLabelPadding** Thickness
- **RoundedLabelFontSize** Double





## The Specific views

The Specific views are examples of pages that belongs to certain categories which implement common UI patterns to help users achieve specific goals.

Typically they use templates for rendering items inside ListViews or in looped items.

Artina Grial follows the following convention:

	Grial
	|_ Views
		|_ <CATEGORY NAME>
			|_ <PAGE NAME>Page.xaml
			|_ Templates
				|_ <PAGE NAME>ItemTemplate.xaml

---

### Articles

The articles views and their item templates are used to display blog posts, articles, feeds, etc.

	Grial
	|_ Views
		|_ Articles


---


### Dashboards

The Dashboards views and their item templates are used to display nice looking categories.

	   Grial
		|_ Views
			|_ Dashboards

There are 3 available dashboards visualizations available in Artina Grial:

1. Default (Dashboard.xaml)
	- A dashboard displaying circled icons
2. Flat (DashboardFlat.xaml)
	- A variation from previous one displaying rectangular tiles for each item
3. Images (DashboardWithImages.xaml)
	- Another variation using icons and images as background


---

### Ecommerce ###

The Ecommerce views and their item templates are used to display products lists and products previews.

	Grial
	|_ Views
		|_ Ecommerce

---

### Logins ###

The Logins views are used to sign-in, sign-up, login and password recovery pages.

	Grial
	|_ Views
		|_ Logins

The Logins views shows how to use validations and display error and warning messages.

---

###Messages###

The Messages views and their item templates are used to display email like UIs and chats/instant messaging UIs.

	Grial
	|_ Views
		|_ Messages


---

###Navigation###

The Navigation views are -as their name suggests- used for navigation purposes.

Basically there are 3 types:

1. Master/Detail (RootPage.xaml)
	- A Page that manages two panes of information: A master page that presents data at a high level, and a detail page that displays low-level details about information in the master.
2. Lists
	- Acts as proxies through categories navigations. They are similar to Dashboards but they are used to display much more information through ListViews.
3. Custom Navigation Bar Page Sample 
	- This is a sample showing the use of the common view `<commonViews:CustomNavBar />`

	|_ Grial
		|_ Views
			|_ Navigation


---

###Settings###

The Settings views are used -as its name suggest- for displaying settings.
Particularly, this sample illustrates the usage of Xamarin Forms TableViews with intent "Settings".

	Grial
	|_ Views
		|_ Settings


---

###Social###

The Social views and their item templates are used to display users social profiles, friends lists and image galleries.

	Grial
	|_ Views
		|_ Social

One of the remarkable features of this category is the use of subtle animations to improve the UX and also an image gallery specially implemented for Xamarin Forms.

---


###Theme###

The Theme views are mainly created to showcase the style features on Artina Grial.

	Grial
	|_ Views
		|_ Theme

One of the remarkable features of this category is the use of `<WebView>`

---

###Walkthroughs### 

The Walkthroughs views and their item templates are used to explain users the main features of your app. Think of it as a "tutorial mode" where the UI demonstrate features to the user.

	Grial
	|_ Views
		|_ Walkthroughs


We have created 2 types of walkthough to serve different purposes:

1. Default ```(WalkthroughPage.xaml)```
	- This type is intended to be used when you count with a design team who can provide you with images. These are ideal for final apps.  
2. Variant ```(WalkthroughVariantPage.xaml)```
	- This type was specially created for devs who lacks of a design team. These are also very useful while building prototypes.
3. Variant ```(WalkthroughFlatPage.xaml)```
	- This type is a beautiful walkthough variation design ideal for final apps.