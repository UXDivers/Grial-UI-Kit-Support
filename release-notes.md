# Release Notes - Grial 2.0.60.0

This update has three main goals: 
1. Compatibility with ```Xamarin Froms 2.3.4```. 
2. Improved integration with ```Gorilla Player```. 
3. Bug fixes and other improvements.

```Grial 2.0.60.0``` is based on ```Xamarin Froms 2.3.4.247```. ```Xamarin Froms 2.3.4``` introduced a bug that may affect any app that uses the ```MergedWith``` property of ```ResourceDictionaries```, like Grial does. The bug has been reported [here](https://bugzilla.xamarin.com/show_bug.cgi?id=56030). It has been fixed but still it is not available in the stable channel. In the context of Grial, the bug only affects how colors are resolved, specially the "AccentColor" color. A workaround has been implemented to avoid the bug, which mainly consists of changing the order in which the accent color is defined in the themes XAML files.

Starting in this version you can download Grial preconfigured to preview it using [Gorilla Player](http://www.gorillaplayer.com). This will allow you to go faster than ever building your app. The Gorilla Ready solution cames with the [Gorilla SDK](https://github.com/UXDivers/Gorilla-Player-Support/wiki/Gorilla-SDK) integrated + the ```DesignTimeData.json``` with all the design time data required to preview Grial. The Gorilla Ready solution is available as a new option of the **Download dropdown** in [MyApps page](https://uxdivers.com/secure/grial/front/index.html#/myapps) of the [Grial Admin](https://uxdivers.com/secure/grial/front). Please notice that it requries [```Gorilla Player 1.0.0.11```](http://blog.uxdivers.com/release-notes-gorilla-player-1-0) to be installed in your computer and IDE. 

## Fixes/Changes Shared Nuget Packages

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

## Fixes in the Grial Solution

- Added ```windowActionModeOverlay``` property to android theme so context menus are property displayed.
- Fixed ```TabControl``` font size issue in the ```TabControlSamplePage.xaml``` sample page.
- Renamed ```SampleData.json``` to ```DesignTimeData.json```.
- Added missing design time data in several samples to improve Gorilla Player preview experience.
- Replaced ```DashboardTemplateSelector``` with the generic ```BoolMemberTemplateSelector``` in the ```DashboardMultipleTilesPage```.
- Replaced some unnecessary ```DynamicResource``` with ```StaticResource```. Now only colors uses ```DynamicResource```, the rest of the resources are resolved with ```StaticResource```.

## Gorilla Ready

The Gorilla Ready solution cames with an additional configuration (besides ```Debug```/```Release```) called ```Gorilla```. If you run your app using this configuration your app will start in preview mode. That means that you will see Gorilla Player starting instead of your app. Once you connect with the Gorilla Server you will be able to start previewing and you normally do with the standard Gorilla Player app.

## Modified Files In This Version

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

## Modified Packages In This Version

The following nuget packages where updated:

- ```UXDivers.Artina.Shared.Base``` to version 2.0.60.0
- ```UXDivers.Artina.Shared``` to version 2.0.60.0
- ```UXDivers.Artina.Controls.Tab``` to version 2.0.60.0
- ```UXDivers.Artina.Controls.Repeater``` to version 2.0.60.0


---

# Release Notes - Grial 2.0.52.0

## Fixes

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

## Modified Files In This Version
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

## Modified Packages In This Version

The following nuget packages where updated:

- ```UXDivers.Artina.Shared.Base``` to version 2.0.52.0
- ```UXDivers.Artina.Shared``` to version 2.0.52.0
- ```UXDivers.Artina.Controls.Tab``` to version 2.0.52.0
- ```UXDivers.Artina.Controls.Repeater``` to version 2.0.52.0

##  <a name="advanced-theme-sync-configuration"></a> Advanced Theme Synchronization Configuration

Theme syncrhonization task can be configured using ```Themes.json``` file. 

This file is just a JSON file that must be created in the same folder as the ```.csproj``` that contains the task resides. 
The task will read that file looking for settings. 

Starting in this version, the file **must be placed in the platform specific projects** (not the PCL as previous versions requires). 
If you want to configure both Android and iOS you will need to add two ```Themes.json``` independent files for each project.

```Themes.json``` may contain one or more of these properties (the values reflect the default value of the property if not specified at all):

~~~
  {
    "ThemeSyncEnabled": true,
    "AppXamlFullPath": null,
    "AppXamlProjectFullPath": null,
    "iOSColorsFileName": "ThemeColors.cs",
    "AndroidColorsFile": "Resources\\values\\Colors.xml",
    "iOSColorsNamespace": null,
    "ThemesFolder":"Themes"
  }
~~~

- **ThemeSyncEnabled** (```boolean```). 
  - Default value: ```true```.
  - If set to false, theme sync will not happen at all for the projects in the folder.

- **AppXamlFullPath** (```string```).
  - Default value: ```null```.
  - The full path to the ```App.xaml```, if specified the task will not try to infer it.

- **AppXamlProjectFullPath** (```string```).
  - Default value: ```null```.
  - This parameter is only considered if **AppXamlFullPath** was specified.  
  - The parameter specifies the full path to the project that contains the ```App.xaml```. 
  - If only **AppXamlFullPath** is specified, the task will try to infer **AppXamlProjectFullPath**. 
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
