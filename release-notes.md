# Release Notes - Grial 2.0.52.0

## Fixes

- The theme synchronization task has been reimplemented to fix issues (i.e. [#166](https://github.com/UXDivers/Grial-UI-Kit-Support/issues/166), [#164](https://github.com/UXDivers/Grial-UI-Kit-Support/issues/164), [#161](https://github.com/UXDivers/Grial-UI-Kit-Support/issues/161)) and add support for Shared projects too. The latter is still in beta. 
- Fixed issue with ```UXDivers.Artiona.*``` nuget package not being correctly updated, when the update was triggered from Visual Studio.
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
