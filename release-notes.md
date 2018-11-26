
# Release Notes - Grial 2.7.0.0

This release is mainly focused on adding support for `Xamarin Forms` 3+.

Additionally, we fixed issues related to RTL support mainly in Android and we added improvements on `TabControl` and `Repeater` controls.

## Updates on Grial:

- Updated `Xamarin Forms` packages to latest stable (3.1.0.583944).
- Updated `Newtonsoft.Json` (11.0.2) and `FFImageLoading` packages (2.4.3.840) to latest stable versions.
- Fixed default background color on `RoundedLabel` control to be `Color.Default`.
- Used new properties on `Xamarin Forms` 3.1 to style `ProgressBar` (through `ProgressColor`) and `Slider` (through `MinimumTrackColor` and `ThumbColor`) without using the old custom renderers.
- Used new `Xamarin Forms` 3.1 `OnColor` property to style iOS `Switch`. Kept custom renderer for Android as that property does not affect the thumb of the switch in Android.

## Updates on Grial RTL:

- Added label renderer to fix text alignment issues with RTL in Android, that behaves differently than in iOS. See details here:
    - https://github.com/xamarin/Xamarin.Forms/issues/3077
- Set Xamarin Forms' `FlowDirection` to LTR on content pages to make things predictable.

## Updates on Artina packages:

- RTL
    - Updated master detail renderer to work with `Xamarin Forms` 3 on RTL Android devices.

- Repeater
    - Added auto item size calculation.
    - Added `ScrollPadding` property to define a padding around the inner scrollable area.

- TabControl 
    - Fixed Xamarin.Forms `AutomationId` property on `TabItem` which was not working.
    - Fixed tab relayout on `Android` (got broken after moving from landscape to portait on `Android`).

- Android's switch renderer
    - Updated renderer to work with `Xamarin Forms` 3.1.

## Gorilla Player

This version requires Gorilla 1.2.2+ to be previewed. This is because it makes use of `MergedDictionaries` property which was not supported by previous versions of Gorilla.
# Release Notes - Grial 2.6.9.0

This release is mainly focused on promoting to RTM the support for **.NET Standard** 
that was originally released in `Grial version 2.6.0.0 RC`. 

XamlC works fine starting with `Xamarin.Forms version 2.5.0.280555` so there's no reason not to opt for **.NET Standard** over the old PCLs.

## New features

- **Added BorderStyle and Placeholder properties Editors**. 
	- Check here for more information: https://uxdivers.github.io/Grial-UI-Kit-Support/renderers.html
- **Added FieldBackgroundColor, SearchIconColor, BorderWidth and BorderColor for SearchBar**. 
	- Check here for more information: https://uxdivers.github.io/Grial-UI-Kit-Support/renderers.html

## Gorilla preview

This version is best previewed with Gorilla Player > 1.2.0.2. Using previous versions of Gorilla common views like Badge or the Rating control are not correctly previewed. 

## Bug fixes

### Android buttons

`Xamarin.Forms version 2.5.0.280555` introduced this issue with Android buttons:

https://github.com/xamarin/Xamarin.Forms/issues/1909

`UXDivers.Artina.Shared*` packages include a partial fix for it that make ArtinaButtons look better by default. This is done through a custom renderer declared in the Android's AssemblyInfo of Grial:

```[assembly: ExportRenderer(typeof(UXDivers.Artina.Shared.Button), typeof(UXDivers.Artina.Shared.ArtinaButtonRenderer))]```

When the bug is fixed we will remove the workaround. To stop using the workaround you can change our render for the default Xamarin's `ButtonRenderer` to render `UXDivers.Artina.Shared.Button` in the AssemblyInfo line above.

### TabItem property bindings

We enabled bindings for TabItem properties. Fixes this issue:

https://github.com/UXDivers/Grial-UI-Kit-Support/issues/358


### Android v21 Style.xml changed to correctly display Acr.UserDialogs

~~~
Grial.Droid
 |_ values-v21
   |_ Style.xml
~~~

We ported to source code the fix for this issue:
https://github.com/UXDivers/Grial-UI-Kit-Support/issues/297

# Release Notes - Grial 2.6.0.0 RC

This release is manily focused on adding support for **.NET Standard**. 
Now the `UXDivers.Artina.Shared*` packages are **.NET Standard** compatible. 
Starting in this version Grial UI Kit Sample project is a **.NET Standard 2.0 Project**, *not a PCL project anymore*. 
The packages target **.NET Standard 1.0** to maximize compatibility. 

Additionally, this version includes some enhancements for the license verification and some improvements for the `Tab Control`.

## IMPORTANT NOTICE: Why RC?

`UXDivers.Artina.Shared*` nuget packages are released as fully flagged **RTM**, meanwhile, the Grial app will be released as **RC**.

We chose to label it as **Release Candidate** due a few bugs in `Xamarin Forms` latest stable version that breaks `XAMLC` in the context of **.NET Standard** projects. 

As a result `XAMLC` **must be disabled** which degrades performance, especially in Android. Once those bugs hit the Xamarin stable channel we will release Grial app as **RTM**.

What does this means to you?
`UXDivers.Artina.Shared*` are **RTM** packages, so it is perfectly safe to upgrade to those
You can base your app on **Grial 2.6.0.0 RC** sample app and it will work like a charm. You must only be aware that `XAMLC` has been disabled. If that is not an issue for you, just go with it.

## How to base your app on **Grial 2.6 RC**
In order to base your app on **Grial 2.6 RC**, you must configure that on Grial Admin through the following steps:

- Open your app details page on [Grial Admin](https://uxdivers.com/secure/grial/front/#/myapps)
- Choose **Grial Settings tab**
- Uncheck the **"Stick to latest stable version"** checkbox
- Select version **2.6.0.0** Release Candidate
- Press **"Save Changes"** button

![grial_admin_2_6_rc](https://user-images.githubusercontent.com/7670773/34412512-741ab69c-ebbc-11e7-8f1a-4c6abee3e2b7.png)

Then, simply download your Grial Full or Starter customized projects:

![grialadmin_download_dropdown](https://user-images.githubusercontent.com/15996999/34399039-8d286e5e-eb62-11e7-808e-49ef6a52036c.png)

For more detail about the `XAMLC` bugs see:

- https://github.com/xamarin/Xamarin.Forms/issues/1316
- https://bugzilla.xamarin.com/show_bug.cgi?id=60452#c2

**Above bugs require that XAMLC should be NOT enabled for .NET Standard 2.0 projects in order to compile and run succesfully.**

If you need to enable `XAMLC` for your app, then you should download a previous Grial 
version with support for **PCL** at least until Microsoft releases an unpdate that fixes this issue.

Keep in mind that if you choose to avoid `XAMLC` in your app you will experience a performance hit, 
which might be more noticeable on Android.

## New features

- **.NET Standard support**. 
	- `UXDivers.Artina.Shared*` nuget packages are now compatible with .NET Standard. 
	- Starting with Grial 2.6, Grial Sample application is based on .NET Standard too. 
	- **PCL based apps is only supported for Grial versions < 2.6.**
- **Production mode**. 
	- Added a safty check in Release mode that the license being used is in Production mode.
- **Tab Control**. 
	- Added support for Font Icons and Badge for the Tabs.
- **Tab Control Samples**. 
	- The Tab Control sample was splitted to make things easier.

## Bug Fixes/Enhancements

1. Fixed [issue #173 - iOS Keybord overlay on text field](https://github.com/UXDivers/Grial-UI-Kit-Support/issues/173). 
2. Improved Android renderers for `DatePicker`, `Picker` and `TimePicker` to honor the `PickerProperties`.
3. Added responsive helpers for `Thinkness`, called `OnOrientationThickness`.
4. Fixed [issue #309 - GridOptionsView does not update properly when there are no items](https://github.com/UXDivers/Grial-UI-Kit-Support/issues/309).

## Production Mode License

Grial License verification menchanism is performed entirly offline, based on the license file included in your project. 

Before publishing your app **it is crucial that you switch your license to Production Mode** and update the license file in your project. If for some reason you forget to do so, license verification might start failing and you will need to do an update in order to fix it.

To avoid this, starting in **Grial 2.6** all sample projects verifies that when running in **Release Mode** your application uses a license in production mode. If not, it will display a message with a warning:

![Grial License Release Mode Reminder](http://52.10.147.219/system/uploads/images/license_release_reminder_ios.png)

This check is included in the `MainActivity`:

~~~
if (!UXDivers.Artina.Shared.License.IsProductionLicense())
{
	AlertDialog.Builder alert = new AlertDialog.Builder(this);
	alert.SetTitle("Grial UI Kit Release Reminder");
	alert.SetMessage("Before publishing this App remember to change the license file to PRODUCTION MODE so it doesn't expire.");
	alert.SetPositiveButton("OK", (sender, e) => { });

	var dialog = alert.Create();
	dialog.Show();
}
~~~

and in the `AppDelegate` as follows:

~~~
if (!UXDivers.Artina.Shared.License.IsProductionLicense())
{
	BeginInvokeOnMainThread(() =>
	{
		var alert = UIAlertController.Create(
			"Grial UI Kit Release Reminder",
			"Before publishing this App remember to change the license file to PRODUCTION MODE so it doesn't expire.",
			UIAlertControllerStyle.Alert);

		alert.AddAction(UIAlertAction.Create("Ok", UIAlertActionStyle.Default, null));

		UIApplication.SharedApplication.KeyWindow.RootViewController.PresentedViewController.PresentViewController(alert, animated: true, completionHandler: null);
	});
}
~~~

**NOTE**: If you already have an app based in Grial, we strongly recommend you to update nugets packages to 2.6 and add this check after the `GrialKit.Init()`.  

## Gorilla Player Support

In order to preview your Grial projects with support for **.NET Standard** you will need to use latest version (**Gorilla Player 1.2.0.0**).

You can download it from <a href="http://gorillaplayer.com" target="_blank">Gorilla Player website</a>

## TabControl Update

In order to make things easier, we splitted the big previous sample of `TabControl` into four different samples:

~~~
Grial
	|_ Views
		|_ Theme
			|_ TabControlAndroidSamplePage.xaml
			|_ TabControlBottomPlacementSamplePage.xaml
			|_ TabControlCustomSamplePage.xaml
			|_ TabControliOSSamplePage.xaml
~~~

* `TabControlAndroidSamplePage.xaml`
	* This sample demonstrates using a `TabControl` with a Material Design look and feel.

* `TabControlAndroidSamplePage.xaml`
	* This sample demonstrates using a `TabControl` also with a Material Design look and feel but using the "TabStripPlacement" property set to "Bottom".

* `TabControlAndroidSamplePage.xaml`
	* This sample demonstrates using a `TabControl` with a custom look and feel.

* `TabControlAndroidSamplePage.xaml`
	* This sample demonstrates using a `TabControl` with an iOS look and feel.

Also, we moved the different resources needed for Android, iOS and custom look and feel for the `TabControl`.

You will find those in the following folder:

~~~
Grial
	|_ Views
		|_ Theme
			|_ Resources
				|_ TabControlAndroidResources.xaml
				|_ TabControlCustomResources.xaml
				|_ TabControliOSResources.xaml
~~~

## TabControl new features

We added support for:

1. Font icons
2. Badge control

### Font Icons on `TabItem`

From now and on you can add your font icons to your `TabItem` and you can even combine them with bitmap icons.

To add a font icon to your `TabItem` simply use the following properties:

* `IconText`
	* Used for the default state of the icon
* `IconTextSelected`
	* Used for the selected state of the icon

#### Usage:

~~~
<tab:TabItem
	IconText="YOUR_ICON_CHAR"
	IconTextSelected="YOUR_ICON_SELECTED_CHAR" >
~~~

With the above you can specify different icons for each icon state. This is particularly useful for instance on iOS tabs where you will need an outliend and filled versions of your icon.

Alternatively, you can simply use the default icon only:

~~~
<tab:TabItem
	IconText="{ x:Static
	local:GrialShapesFont.InsertPhoto }" >
~~~

 ...then later change its appeareance through styles (inclueded on the resources files mentioned above).


### Badges on `TabItem`

Starting from this version, you can add a `Badge` to each one of your `TabItem` items.

To add a font icon to your `TabItem` simply use the following properties:

* `BadgeText`
	* Used to display the value of the `Badge` within the `TabItem`.

#### Usage:

~~~
<tab:TabItem
	BadgeText="1" >
~~~

## Modified Artina packages in this version

- `UXDivers.Artina.Shared.Base` upgraded to version **2.6.4**
- `UXDivers.Artina.Shared` upgraded to version **2.6.4**
- `UXDivers.Artina.Controls.Tab` upgraded to version **2.6.4**
- `UXDivers.Artina.Controls.Repeater` upgraded to version **2.6.4**

## Upgraded packages in this version

### Xamarin Forms
- `Xamarin.Forms` upgraded to version **2.5.0.121934**

### FFImageLoading
- `Xamarin.FFImageLoading` upgraded to version **2.3.1**
- `Xamarin.FFImageLoading.Forms` upgraded to version **2.3.1**
- `Xamarin.FFImageLoading.Transformations` upgraded to version **2.3.1**

### Lottie
- `Com.Airbnb.Xamarin.Forms.Lottie` upgraded to version **2.4.0**
- `Com.Airbnb.Android.Lottie` upgraded to version **2.2.5**
- `Com.Airbnb.iOS.Lottie` upgraded to version **2.1.5**


# Release Notes - Grial 2.5.2.0

### New features

- Localization support through regular RESX files consumables from XAML through our extensions, see [i18n](i18n-page.html).
- Support for Right-to-left layouts in every page and template, see [Grial RTL](rtl-page.html).
- WrapPanel layout that allow elements to flow in an HTML-like fashion (used in `MovieSelectionPage.xaml`).
- Circle buttons (`CustomRenderersPage.xaml`)
	- ![Circle Buttons](http://52.10.147.219/system/uploads/images/circle_buttons.png)

### Bug Fixes

1. iOS 11 back button gone (issue [#254](https://github.com/UXDivers/Grial-UI-Kit-Support/issues/254))
2. TabControl does not render Bindable content (issue [#200](https://github.com/UXDivers/Grial-UI-Kit-Support/issues/200))
3. Button BorderColor works on iOS but not Android (issue [#214](https://github.com/UXDivers/Grial-UI-Kit-Support/issues/214))
4. Apply theme base color to iOS steppers
5. Layout issue when on GridOptionsView after changing the device orientation on Android
6. Missing `When` property in `FrontPageNewsPage.xaml`
7. Fixing issues in Parallax effect on `ArticleViewPage.xaml`
8. Ipad rotation breakes header layout on `ArticleViewPage.xaml`
9. Fixed issue with gesture recognizers stop working on `TableView`'s Cells when the `ArtinaTableViewRenderer` was used.

### Modified Artina packages in this version

- ```UXDivers.Artina.Shared.Base``` upgraded to version **2.5.2**
- ```UXDivers.Artina.Shared``` upgraded to version **2.5.2**
- ```UXDivers.Artina.Controls.Tab``` upgraded to version **2.5.2**
- ```UXDivers.Artina.Controls.Repeater``` upgraded to version **2.5.2**

### Upgraded packages in this version

#### Xamarin Forms
- ```Xamarin.Forms``` upgraded to version **2.4.0.282**

#### FFImageLoading
- ```Xamarin.FFImageLoading``` upgraded to version **2.2.19**
- ```Xamarin.FFImageLoading.Forms``` upgraded to version **2.2.19**
- ```Xamarin.FFImageLoading.Transformations``` upgraded to version **2.2.9**



# Release Notes - Grial 2.0.60.0

This update has three main goals:

1. Compatibility with ```Xamarin Froms 2.3.4```. 
2. Improved integration with ```Gorilla Player```. 
3. Bug fixes and other improvements.

```Grial 2.0.60.0``` is based on ```Xamarin Froms 2.3.4.247```. ```Xamarin Froms 2.3.4``` introduced a bug that may affect any app that uses the ```MergedWith``` property of ```ResourceDictionaries```, like Grial does. The bug has been reported [here](https://bugzilla.xamarin.com/show_bug.cgi?id=56030). It has been fixed but still it is not available in the stable channel. In the context of Grial, the bug only affects how colors are resolved, specially the "AccentColor" color. A workaround has been implemented to avoid the bug, which mainly consists of changing the order in which the accent color is defined in the themes XAML files.

Starting in this version you can download Grial preconfigured to preview it using [Gorilla Player](http://www.gorillaplayer.com). This will allow you to go faster than ever building your app. The Gorilla Ready solution cames with the [Gorilla SDK](https://github.com/UXDivers/Gorilla-Player-Support/wiki/Gorilla-SDK) integrated + the ```DesignTimeData.json``` with all the design time data required to preview Grial. The Gorilla Ready solution is available as a new option of the **Download dropdown** in [MyApps page](https://uxdivers.com/secure/grial/front/index.html#/myapps) of the [Grial Admin](https://uxdivers.com/secure/grial/front). Please notice that it requries [```Gorilla Player 1.0.0.11```](http://blog.uxdivers.com/release-notes-gorilla-player-1-0) to be installed in your computer and IDE. 

### Fixes/Changes Shared Nuget Packages

- Fixed Memory Leak Responsive Helpers
- The following Responsive Helpers has been marked as obsolete: ```OnScreenSizeDouble```, ```OnScreenSizeInt```, ```StylePerSize```, ```HiddenPerSize```, ```IsExtraSmallScreen```, ```IsLargeScreen```, ```IsMediumScreen```, ```IsNotExtraSmallScreen```, ```IsNotLargeScreen```, ```IsNotMediumScreen```, ```IsNotSmallScreen```, ```IsSizeScreenBase```, ```IsSmallScreen``` and ```VisiblePerSize```.
- Fixed bug in the ```GridOptionsView```. ```ItemClickCommand``` command was not correctly associated in some cases.
- Added ```ItemWidthAuto``` and ```ItemHeightAuto``` properties to the ```GridOptionsView``` that allows grid cells to dimension based on its content.
- Added support for ```ObservableCollection``` to the ```Repeater``` control.
- Fixed issue with ```Repeater.ItemSource``` property not being correctly refreshed in some cases.

- **Breaking change** Removed iOS Navigation Bar customization through using iOS Appearance API. Now this is done directly from XAML using Xamarin Forms. If you update the nuget packages but not the solution template you will need to create an implicit style for the ```NavigationBar``` and add it to the ```App.xaml```, as shown in the following snippet.

~~~~
<Style TargetType="NavigationPage">
   <Setter Property="BarBackgroundColor" Value="{ DynamicResource AccentColor }" />
   <Setter Property="BarTextColor" Value="{ DynamicResource InverseTextColor }" />
</Style>
~~~~

### Fixes in the Grial Solution

- Added ```windowActionModeOverlay``` property to android theme so context menus are property displayed.
- Fixed ```TabControl``` font size issue in the ```TabControlSamplePage.xaml``` sample page.
- Renamed ```SampleData.json``` to ```DesignTimeData.json```.
- Added missing design time data in several samples to improve Gorilla Player preview experience.
- Replaced ```DashboardTemplateSelector``` with the generic ```BoolMemberTemplateSelector``` in the ```DashboardMultipleTilesPage```.
- Replaced some unnecessary ```DynamicResource``` with ```StaticResource```. Now only colors uses ```DynamicResource```, the rest of the resources are resolved with ```StaticResource```.

### Gorilla Ready

The Gorilla Ready solution cames with an additional configuration (besides ```Debug```/```Release```) called ```Gorilla```. If you run your app using this configuration your app will start in preview mode. That means that you will see Gorilla Player starting instead of your app. Once you connect with the Gorilla Server you will be able to start previewing and you normally do with the standard Gorilla Player app.

### Modified Files In This Version

~~~
Droid/Grial.Droid.csproj
Droid/MainActivity.cs
Droid/Resources/Resource.designer.cs
Droid/Resources/values-v21/Style.xml
Droid/Resources/values/Colors.xml
Droid/Resources/values/Style.xml
Droid/packages.config
Grial.sln
Grial/App.xaml
Grial/DesignTimeData.json
Grial/Gorilla.json
Grial/GorillaSdkHelper.cs
Grial/Grial.csproj
Grial/Helpers/FontawesomeFont.cs
Grial/Helpers/NotificationColorConverter.cs
Grial/Models/Message.cs
Grial/Themes/GrialDarkTheme.xaml
Grial/Themes/GrialEnterpriseTheme.xaml
Grial/Themes/GrialLightTheme.xaml
Grial/Views/Articles/ArticleViewPage.xaml
Grial/Views/Articles/ArticlesClassicViewPage.xaml
Grial/Views/Articles/ArticlesListVariantPage.xaml
Grial/Views/Common/BrandBlock.xaml
Grial/Views/Common/CustomActivityIndicator.xaml
Grial/Views/Common/CustomNavBar.xaml
Grial/Views/Common/Rating.xaml
Grial/Views/Dashboards/DashboardMultipleTilesPage.xaml
Grial/Views/Dashboards/Templates/DashboardAppNotificationItemTemplate.xaml
Grial/Views/Dashboards/Templates/DashboardCardItemTemplate.xaml
Grial/Views/Dashboards/Templates/DashboardItemTemplate.xaml
Grial/Views/Dashboards/Templates/DashboardItemTemplateBase.cs
Grial/Views/Dashboards/Templates/DashboardMultipleScrollMainItemTemplate.xaml
Grial/Views/Ecommerce/ProductItemFullScreenPage.xaml
Grial/Views/Ecommerce/ProductItemViewPage.xaml
Grial/Views/Ecommerce/ProductOrder.xaml
Grial/Views/Ecommerce/Templates/ProductGridItemTemplate.xaml
Grial/Views/Ecommerce/Templates/ProductsCatalogItemTemplate.xaml
Grial/Views/Logins/LoginPage.xaml
Grial/Views/Logins/PasswordRecoveryPage.xaml
Grial/Views/Logins/SignUpPage.xaml
Grial/Views/Logins/SimpleLoginPage.xaml
Grial/Views/Logins/SimpleSignUpPage.xaml
Grial/Views/Messages/ChatMessagesListPage.xaml
Grial/Views/Messages/ChatTimelinePage.xaml
Grial/Views/Messages/Selectors/ChatTemplateSelector.cs
Grial/Views/Messages/Templates/ChatRightMessageItemTemplate.xaml
Grial/Views/Messages/Templates/RecentChatItemTemplate.xaml
Grial/Views/Navigation/CustomNavBarPage.xaml
Grial/Views/Navigation/EmptyStatePage.xaml
Grial/Views/Navigation/MainMenuPage.xaml
Grial/Views/Navigation/SamplesListFromCategoryPage.xaml
Grial/Views/Navigation/Templates/CardsListItemTemplate.xaml
Grial/Views/Navigation/Templates/CategoriesListWithIconsItemTemplate.xaml
Grial/Views/Navigation/Templates/MainMenuGroupHeaderTemplate.xaml
Grial/Views/Navigation/Templates/MainMenuItemTemplate.xaml
Grial/Views/Navigation/Templates/NotificationsListItemTemplate.xaml
Grial/Views/Navigation/Templates/SamplesListFromCategoryItemTemplate.xaml
Grial/Views/Navigation/WelcomePage.xaml
Grial/Views/Settings/CustomSettingsPage.xaml
Grial/Views/Settings/SettingsPage.xaml
Grial/Views/Social/DocumentTimelinePage.xaml
Grial/Views/Social/Selectors/DocumentTimelineSelector.cs
Grial/Views/Social/Templates/DocumentTimelineLeftItemTemplate.xaml
Grial/Views/Social/Templates/DocumentTimelineRightItemTemplate.xaml
Grial/Views/Social/Templates/TimelineItemTemplate.xaml
Grial/Views/Social/TimelinePage.xaml
Grial/Views/Theme/AnimationsPage.xaml
Grial/Views/Theme/CommonViewsPage.xaml
Grial/Views/Theme/CustomRenderersPage.xaml
Grial/Views/Theme/IconsPage.xaml
Grial/Views/Theme/TabControlSamplePage.xaml
Grial/Views/Theme/ThemePage.xaml
Grial/Views/Walkthroughs/Templates/WalkthroughFlatStepItemTemplate.xaml
Grial/Views/Walkthroughs/Templates/WalkthroughGradientItemTemplate.xaml
Grial/Views/Walkthroughs/Templates/WalkthroughStepItemTemplate.xaml
Grial/Views/Walkthroughs/Templates/WalkthroughVariantStepItemTemplate.xaml
Grial/Views/Walkthroughs/Templates/WalkthroughVariantStepItemTemplate.xaml.cs
Grial/Views/Walkthroughs/WalkthroughVariantPage.xaml
Grial/packages.config
iOS/AppDelegate.cs
iOS/Grial.iOS.csproj
iOS/ThemeColors.cs
iOS/packages.config
~~~

### Modified Packages In This Version

The following nuget packages where updated:

- ```UXDivers.Artina.Shared.Base``` to version 2.0.60.0
- ```UXDivers.Artina.Shared``` to version 2.0.60.0
- ```UXDivers.Artina.Controls.Tab``` to version 2.0.60.0
- ```UXDivers.Artina.Controls.Repeater``` to version 2.0.60.0


# Release Notes - Grial 2.0.52.0

### Fixes

- The theme synchronization task has been reimplemented to fix issues (i.e. [#166](https://github.com/UXDivers/Grial-UI-Kit-Support/issues/166), [#164](https://github.com/UXDivers/Grial-UI-Kit-Support/issues/164), [#161](https://github.com/UXDivers/Grial-UI-Kit-Support/issues/161)) and add support for Shared projects too. The latter is still in beta. 
- Fixed issue with ```UXDivers.Artina.*``` nuget package not being correctly updated, when the update was triggered from Visual Studio.
- Fixed issue with ```Themes.json``` (used to configure theme synchronization task) not correctly being loaded in Windows enviornments.
- Fixed issue [#167](https://github.com/UXDivers/Grial-UI-Kit-Support/issues/167).
- Fixed Tab Control layout refresh issue in Android when the device was rotated within a Navigation Page.
- Fixed Walkthrough layout issue
- Improved Walkthrough implementation
- Workaround for Entry trigger not setting back Border to the original color when focus is lost.
- Fixed ```CustomNavBar``` Issues
- Workaround for Xamarin Forms bug on Android:
    *"Transparent Grid causes Java.Lang.IllegalStateException: Unable to create layer for Platform_DefaultRenderer"*
    https://bugzilla.xamarin.com/show_bug.cgi?id=51238
- Fixed Grial namespaces to be different for .iOS and Droid projects
- Added ```GrialVersion``` attribute to the ```AssemblyInfo``` to track the version of Grial sample project.

Starting in this version **Themes Synchronization task** will report a warning, instead of an error if something goes wrong during the synchronization process.

The behavior can be changed if needed, see [Advanced Theme Synchronization](#advanced-theme-sync-configuration) for more information.

### Modified Files In This Version
~~~
  Droid/Grial.Droid.csproj
  Droid/MainActivity.cs
  Droid/packages.config
  Droid/Properties/AndroidManifest.xml
  Droid/Properties/AssemblyInfo.cs
  Droid/Renderers/CustomFontLabelRenderer.cs
  Grial/App.xaml
  Grial/App.xaml.cs
  Grial/Gorilla.json
  Grial/Grial.csproj
  Grial/packages.config
  Grial/Helpers/NavigationService.cs
  Grial/Properties/AssemblyInfo.cs
  Grial/ViewModels/Sample.cs
  Grial/ViewModels/WalkthroughViewModel.cs
  Grial/Views/Common/CustomActivityIndicator.xaml.cs
  Grial/Views/Ecommerce/ProductsCarouselPage.xaml.cs
  Grial/Views/Ecommerce/ProductsGridPage.xaml.cs
  Grial/Views/Messages/MessagesListPage.xaml.cs
  Grial/Views/Messages/Selectors/ChatTemplateSelector.cs
  Grial/Views/Navigation/CustomNavBarPage.xaml
  Grial/Views/Social/Selectors/DocumentTimelineSelector.cs
  Grial/Views/Theme/AnimationsPage.xaml
  Grial/Views/Theme/CustomActivityIndicatorPage.xaml
  Grial/Views/Theme/CustomActivityIndicatorPage.xaml.cs
  Grial/Views/Theme/CustomRenderersPage.xaml.cs
  Grial/Views/Theme/GenericAboutPage.xaml
  Grial/Views/Theme/TabControlSamplePage.xaml
  Grial/Views/Walkthroughs/WalkthroughFlatPage.xaml.cs
  Grial/Views/Walkthroughs/WalkthroughGradientPage.xaml.cs
  Grial/Views/Walkthroughs/WalkthroughPage.xaml.cs
  Grial/Views/Walkthroughs/WalkthroughVariantPage.xaml.cs
  Grial/Views/Walkthroughs/Templates/WalkthroughFlatStepItemTemplate.xaml
  Grial/Views/Walkthroughs/Templates/WalkthroughFlatStepItemTemplate.xaml.cs
  Grial/Views/Walkthroughs/Templates/WalkthroughGradientItemTemplate.xaml
  Grial/Views/Walkthroughs/Templates/WalkthroughGradientItemTemplate.xaml.cs
  Grial/Views/Walkthroughs/Templates/WalkthroughStepItemTemplate.xaml
  Grial/Views/Walkthroughs/Templates/WalkthroughStepItemTemplate.xaml.cs
  Grial/Views/Walkthroughs/Templates/WalkthroughVariantStepItemTemplate.xaml
  Grial/Views/Walkthroughs/Templates/WalkthroughVariantStepItemTemplate.xaml.cs
  iOS/AppDelegate.cs
  iOS/Grial.iOS.csproj
  iOS/GrialLicense
  iOS/Info.plist
  iOS/Main.cs
  iOS/packages.config
  iOS/ThemeColors.cs
  iOS/Properties/AssemblyInfo.cs
~~~

### Modified Packages In This Version

The following nuget packages where updated:

- ```UXDivers.Artina.Shared.Base``` to version 2.0.52.0
- ```UXDivers.Artina.Shared``` to version 2.0.52.0
- ```UXDivers.Artina.Controls.Tab``` to version 2.0.52.0
- ```UXDivers.Artina.Controls.Repeater``` to version 2.0.52.0

###  <a name="advanced-theme-sync-configuration"></a> Advanced Theme Synchronization Configuration

Theme syncrhonization task can be configured using ```Themes.json``` file. 

This file is just a JSON file that must be created in the same folder as the ```.csproj``` that contains the task resides. 
The task will read that file looking for settings. 

Starting in this version, the file **must be placed in the platform specific projects** (not the PCL as previous versions requires). 
If you want to configure both Android and iOS you will need to add two ```Themes.json``` independent files for each project.

```Themes.json``` may contain one or more of these properties (the values reflect the default value of the property if not specified at all):

~~~
  {
    "ThemeSyncEnabled": true,
    "AppXamlPath": null,
    "AppXamlProjectPath": null,
    "iOSColorsFileName": "ThemeColors.cs",
    "AndroidColorsFile": "Resources\\values\\Colors.xml",
    "iOSColorsNamespace": null,
    "ThemesFolder":"Themes"
  }
~~~

- **ThemeSyncEnabled** (```boolean```). 
  - Default value: ```true```.
  - If set to false, theme sync will not happen at all for the projects in the folder.

- **AppXamlPath** (```string```).
  - Default value: ```null```.
  - The full path to the ```App.xaml```, if specified the task will not try to infer it.

- **AppXamlProjectPath** (```string```).
  - Default value: ```null```.
  - This parameter is only considered if **AppXamlPath** was specified.  
  - The parameter specifies the full path to the project that contains the ```App.xaml```. 
  - If only **AppXamlPath** is specified, the task will try to infer **AppXamlProjectPath**. 
    - If you specify both it will just stick to them.

- **iOSColorsFileName** (```string```)
  - Default value: ```"ThemeColors.cs"```.
  - Name of the ```Colors``` file in ```iOS```, just in case someone need to change its name.

- **AndroidColorsFile** (```string```) 
  - Default value: ```"Resources\\values\\Colors.xml"```.
  - Path of the ```Android.Colors.xaml```, just in case the default one is changed.

- **iOSColorsNamespace** (```string```)
  - Default value: ```null```.
  - Namespace used for the ```ThemesColor class```. If not specified the ```default root namespace``` of the project will be used.

- **ThemesFolder** (```string```)
  - Default value: ```"Themes"```.
  - Specifies the name of the ```Folder``` where ```Themes``` are stored. 
  - This is just to optimize performance. 
    - We try to resolve the ```Theme XAML``` against the XAMLs within this folder first. 
    - If we don't find it we will look across the whole project.


One final comment:
- Now by default if the task fails for some reason it will report a **Warning**, not an **Error**.
- If you still want to report an **Error**, simply add a property to your ```.csproj``` called ```GrialFailOnError``` and set it to ```true```:

~~~
  <GrialFailOnError>true</GrialFailOnError>
~~~

For example:

~~~
<Project DefaultTargets="Build" ToolsVersion="4.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <PropertyGroup>
    <Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>
    <Platform Condition=" '$(Platform)' == '' ">iPhoneSimulator</Platform>
    <ProjectTypeGuids>{FEACFBD2-3405-455C-9665-78FE426C6842};{FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}</ProjectTypeGuids>
    <ProjectGuid>{45DA7B47-C579-4BC1-B1E5-97EEA0C669CD}</ProjectGuid>
    <OutputType>Exe</OutputType>
    <RootNamespace>UXDivers.Artina.Grial</RootNamespace>
    <IPhoneResourcePrefix>Resources</IPhoneResourcePrefix>
    <AssemblyName>UXDiversArtinaGrialiOS</AssemblyName>
    <ReleaseVersion>1.5</ReleaseVersion>

    <GrialFailOnError>true</GrialFailOnError>

  </PropertyGroup>
</Project>
~~~
