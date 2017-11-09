# <a name="setup-grial-existing-project"></a> Setting Up Grial On An Existing Project

###Overview

Adding Grial assets and dependencies to your projects implies adding Nuget packages, copying files, 
adding styles and configuring some properties in your solution. 
All the steps will be described in this guide.

<div class="highlight">Minimize boilerplate by taking advantage of Grial Starter and Grial Full samples!</div>

Before starting, we recommend you to generate both a Grial `Starter project` and a `Full project` on 
[Grial Admin website](https://uxdivers.com/secure/grial/front) which mimics the following data from your existing project:


- Namespaces, 
- Assembly names,
- Application name (both Android and iOS)
- Package name (Android)
- Boundle indentifier (iOS)
- Solution name
- Project names

You will use this starter solution to get the required bare minimum setup to have Grial infrastructure in your current project (including the license).
Then, you will be able to progressively add any of the remaining screens from Grial full project to your existing project.

The easiest way will be to simultaneously open in Visual Studio the 3 projects:

- Your existing project
- Grial Starter project
- Grial Full project

That way it will be easier to copy and paste folders and files from one project to the other.

## <a name="pcl-setup-grial-existing-project"></a> PCL Project Setup

### Adding Nuget Packages

As part of your project's setup, you will need to add Nuget Packages and restore them.
Similarly as how you proceed when you download the `Grial Starter` and `Grial Full` projects, 
you will need to previously configured [UXDivers private Nuget source](/#grial-uikit-overview-grial-first-run-setting-up-uxdivers-nuget-source) to get acces to Grial packages.

Add the following packages:
~~~
UXDivers.Artina.Shared.Base
UXDivers.Artina.Shared
UXDivers.Effects

Xamarin.FFImageLoading
Xamarin.FFImageLoading.Forms
Xamarin.FFImageLoading.Transformations
~~~

**(Only in Grial Pro projects)**
~~~
UXDivers.Artina.Controls.Tab
UXDivers.Artina.Controls.Repeater
~~~

If your app will use Lottie animations then also add the following package:

~~~
Com.Airbnb.Xamarin.Forms.Lottie
~~~

### Copying Required Files

The easiest way is to copy everything from your downloaded `Grial Starter` project, 
since it will have fewer files (just the minimum). 

- `Themes Folder`

    You will need to copy the whole `Themes` folder (with its contents ) to your PCL on your existing project.
    ~~~
    <YourGrialStarterProject>
        |_ Themes
    ~~~

- `App.xaml`
  - If this file is already present in your project you will need to make sure to add all styles 
  from Grial's `App.xaml` file and also make sure to:
    - Add all the assemblies references used by Grial's App.xaml (replace `<YOUR_EXISTING_PROJECT>` with your project name):

    ~~~
    xmlns:local="clr-namespace:<YOUR_EXISTING_PROJECT>;assembly=<YOUR_EXISTING_PROJECT>"
    xmlns:resx="clr-namespace:<YOUR_EXISTING_PROJECT>.Resx;assembly=<YOUR_EXISTING_PROJECT>"

    xmlns:artina="clr-namespace:UXDivers.Artina.Shared;assembly=UXDivers.Artina.Shared"
    xmlns:converter="clr-namespace:UXDivers.Artina.Shared;assembly=UXDivers.Artina.Shared.Base"
    xmlns:effects="clr-namespace:UXDivers.Effects;assembly=UXDivers.Effects"
    xmlns:ffimageloading="clr-namespace:FFImageLoading.Forms;assembly=FFImageLoading.Forms"
    ~~~
    
    - Include the `MergedWith` attribute pointing to the right theme. 
    By default it is `GrialLightTheme`:
    
    ~~~
    <ResourceDictionary MergedWith="local:GrialLightTheme">
    ~~~

- `Common Views Folder`
    - To make things easier, you will probably want to copy the whole folder and its content to your existing project.
    Later you can remove unused stuff.
    ~~~
    <YourGrialStarterProject>
        |_ Views
            |_ Common
    ~~~

- `Helpers Folder`
    - Again, to make things easier, you will probably want to copy the whole folder and its content to your existing project and later you can remove unused stuff.
    
        ~~~
        <YourGrialStarterProject>
            |_ Helpers
        ~~~

- `Resx Folder`
    ~~~
    <YourGrialStarterProject>
        |_ AppResources.resx
    ~~~

## <a name="android-setup-grial-existing-project"></a> Android Project Setup

### Adding Android Nuget Packages

As part of your project's setup, you will need to add Nuget Packages and restore them.
Similarly as how you proceed when you download the `Grial Starter` and `Grial Full` projects, 
you will need to previously configured [UXDivers private Nuget source](/docs.html#grial-uikit-overview-grial-first-run-setting-up-uxdivers-nuget-source) to get acces to Grial packages.

Add the following packages:

~~~
UXDivers.Artina.Shared.Base
UXDivers.Artina.Shared
UXDivers.Effects

Xamarin.FFImageLoading
Xamarin.FFImageLoading.Forms
Xamarin.FFImageLoading.Transformations
~~~

**(Only in Grial Pro projects)**
~~~
UXDivers.Artina.Controls.Tab
UXDivers.Artina.Controls.Repeater
~~~

If your app will use Lottie animations then also add the following packages:
~~~
Com.Airbnb.iOS.Lottie
Com.Airbnb.Xamarin.Forms.Lottie
~~~

Eventually, you would like to add Gorilla SDK package:
~~~
UXDivers.GorillaPlayer.SDK
~~~

### Copying Required Files

The easiest way is to copy everything from your downloaded `Grial Starter` Android project, 
since it will have fewer files (just the minimum). 

- `Resources`
    - Fonts: Copy the fonts files from your `Assets` folder on your Android `GrialStarterProject` project: 
        ~~~
        <YourGrialStarterProject.Droid>
            |_ Assets
                |_ fontawesome-webfont.ttf
                |_ grialshapes.ttf
                |_ ionicons.ttf
        ~~~

        Paste them on the same place in your existing project Android assets folder:
        ~~~
        <YourExistingProject.Droid>
            |_ Assets
        ~~~

        <div class="highlight">Remember to check the proper `Build Action` is set after you copy the files.</div>

    - `Images`
        - Android manages different images densities by providing special folders targeting each density.
        ~~~
        <YourGrialStarterProject.Droid>
            |_ Resources
                |_ drawables
                |_ drawables-hdpi
                |_ drawables-xhdpi
                |_ drawables-xxhdpi
        ~~~

        That makes a little bit harder to manually copying each file to your android project.
        In order to ease the process you can only copy the following images:
        ~~~
        <YourGrialStarterProject.Droid>
            |_ Resources
                |_ drawables
                    |_ hamburguer_icon.png
                    |_ logo.png
                    |_ splash.png
                    |_ splash_drawable.xml
        ~~~
        Later you can add your images to your `Android Existing Project`.

    - `Layouts`
        -  Next thing you will need to copy from your `Android Starter Project` are the `Tabs.axml` and `Toolbar.axml`:
        ~~~
        <YourGrialStarterProject.Droid>
            |_ Resources
                |_ layouts
                    |_ Tabs.axml
                    |_ Toolbar.axml
        ~~~

    - `Colors and Styles`
        - Finally, you will need to copy the files in charge to make possible to achieve the Grial Theme styling on Android.
        
        If you don't have any custom styles on your Android project and just simply want to use Grial, then the easiest will be to 
        copy the fil following to your existing Android project:
        ~~~
        <YourGrialStarterProject.Droid>
            |_ Resources
                |_ values
                    |_ Colors.xml
                    |_ Style.xml
                |_ values-v21
                    |_ Style.xml
        ~~~

        If you have your own styles and want to preserve them, then you will need to just copy the `Colors.xml` file to your Android existing project.
        Next, you will need to manually merge the styles provided with Grial with your own ones.


### Adding Export For Custom Renderers

To ease the process just copy `Properties` folder and its `AssemblyInfo.cs` file from your downloaded `Grial Starter` project to your Android existing project:

~~~
<YourGrialStarterProject.Droid>
    |_ Properties
        |_ AssemblyInfo.cs
~~~
Open pasted `AssemblyInfo.cs` and add the following:

~~~
    // Custom renderers definition.

    [assembly: ExportRenderer(typeof(Entry), typeof(UXDivers.Artina.Shared.ArtinaEntryRenderer))]
    [assembly: ExportRenderer(typeof(Editor), typeof(UXDivers.Artina.Shared.ArtinaEditorRenderer))]
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
    [assembly: ExportRenderer(typeof(Picker), typeof(UXDivers.Artina.Shared.ArtinaPickerRenderer))]
    [assembly: ExportRenderer(typeof(DatePicker), typeof(UXDivers.Artina.Shared.ArtinaDatePickerRenderer))]
    [assembly: ExportRenderer(typeof(TimePicker), typeof(UXDivers.Artina.Shared.ArtinaTimePickerRenderer))]
    [assembly: ExportRenderer(typeof(UXDivers.Artina.Shared.Button), typeof(UXDivers.Artina.Shared.ArtinaButtonRenderer))]
~~~

### Initialize Grial Properly

<div class="highlight">Make sure your page inherits from `FormsAppCompatActivity`!!!</div>

You will need to make sure your `MainActivity.cs` contains the following:

~~~
...
using UXDivers.Artina.Shared;
...

namespace <YOUR_EXISTING_PROJECT_NAMESPACE>.Droid
{
    [Activity(
        Label = "<YOUR_EXISTING_PROJECT>", 
        Icon = "@drawable/icon", 
        Theme = "@style/MyTheme", 
        MainLauncher = true,
        LaunchMode = LaunchMode.SingleTask,
        ConfigurationChanges = ConfigChanges.Orientation | ConfigChanges.ScreenSize | ConfigChanges.Locale | ConfigChanges.LayoutDirection
        )
    ]

    public class MainActivity : FormsAppCompatActivity
	{
        private Locale _locale;

		protected override void OnCreate(Bundle bundle)
		{
            // Changing to App's theme since we are OnCreate and we are ready to 
			// "hide" the splash
			base.Window.RequestFeature(WindowFeatures.ActionBar);
			base.SetTheme(Resource.Style.AppTheme);

            FormsAppCompatActivity.ToolbarResource = Resource.Layout.Toolbar;
            FormsAppCompatActivity.TabLayoutResource = Resource.Layout.Tabs;

			base.OnCreate(bundle);

            ...

			// Initializing FFImageLoading
			CachedImageRenderer.Init();

			global::Xamarin.Forms.Forms.Init(this, bundle);
			GrialKit.Init(this, "<YOUR_EXISTING_PROJECT_NAMESPACE>.Droid.GrialLicense");
			
            FormsHelper.ForceLoadingAssemblyContainingType(typeof(UXDivers.Effects.Effects));

			_locale = Resources.Configuration.Locale;

			LoadApplication(new App());

            ...
        }

        public override void OnConfigurationChanged(Android.Content.Res.Configuration newConfig)
        {
			base.OnConfigurationChanged(newConfig);

			GrialKit.NotifyConfigurationChanged(newConfig);

			if ((int)Build.VERSION.SdkInt <= 19 &&
			    !_locale.Equals(newConfig.Locale))
			{
				// Need to recreate the activity when locale has changed for APIs 18 and 19 
				// as changes in ConfigChanges.Locale break images used in the app
				Recreate();
			}
        }
	}
}
~~~


### Download Grial License and Invoke Init

- Copy your downloaded license from your `Grial Starter` project to the root folder of your existing Droid project folder:

    ~~~
    <YourGrialStarterProject.Droid>
        |_ GrialLicense
    ~~~

- Make sure the file compile action is set as emmbedded resource.
- Check Grial License is initialized properly on your `MainActivity.cs`:

    ~~~
    namespace <YOUR_EXISTING_PROJECT_NAMESPACE>.Droid
    {
    	...
    	public class MainActivity : FormsAppCompatActivity
    	{
    		protected override void OnCreate(Bundle bundle)
    		{
                ...
                GrialKit.Init(this, "<YOUR_EXISTING_PROJECT_NAMESPACE>.GrialLicense"); 
                ...
    ~~~
For more details please check [Grial License Setup](/docs.html#grial-uikit-overview-grial-first-run-grial-license-setup).

## <a name="ios-setup-grial-existing-project"></a> iOS Project Setup

### Adding iOS Nuget Packages

As part of your project's setup, you will need to add Nuget Packages and restore them.
Similarly as how you proceed when you download the `Grial Starter` and `Grial Full` projects, 
you will need to previously configured [UXDivers private Nuget source](/docs.html#grial-uikit-overview-grial-first-run-setting-up-uxdivers-nuget-source) to get acces to Grial packages.

Add the following packages:

~~~
UXDivers.Artina.Shared.Base
UXDivers.Artina.Shared
UXDivers.Effects

Xamarin.FFImageLoading
Xamarin.FFImageLoading.Forms
Xamarin.FFImageLoading.Transformations
~~~

**(Only in Grial Pro projects)**
~~~
UXDivers.Artina.Controls.Tab
UXDivers.Artina.Controls.Repeater
~~~

If your app will use Lottie animations then also add the following packages:
~~~
Com.Airbnb.iOS.Lottie
Com.Airbnb.Xamarin.Forms.Lottie
~~~

Eventually, you could like to add Gorilla SDK package:
~~~
UXDivers.GorillaPlayer.SDK
~~~

### Copying Required Files

The easiest way is to copy everything from your downloaded `Grial Starter` Android project, 
since it will have fewer files (just the minimum). 

- There are some files you will need to copy from your `Grial Starter` project to the root folder of your existing iOS project folder:
    ~~~
    <YourGrialStarterProject.iOS>
        |_ GrialLicense
        |_ ThemeColors.cs
        |_ Splash.storyboard
    ~~~

    <div class="highlight">Remember to add the Splash.storyboard to the Info.plist file in your iOS project!</div>
    In order to use Grial's `Splash.storyboard` in your existing iOS project, you must add it on `Info.plist` by adding the following block:
    ~~~
    <key>UILaunchStoryboardName</key>
	<string>Splash</string>
    ~~~

- `Info.plist`
    - You will need to make sure to add Grial font to this file in your existing project in order to see font icons properly.
    - For more info, please check [Adding Font Icons To Your Project](/docs.html#grial-uikit-overview-working-with-projects-adding-font-icons-to-your-project) docs.

- `Resources`
    - Fonts
        ~~~
        <YourGrialStarterProject.iOS>
            |_ Resources
                |_ fontawesome-webfont.ttf
                |_ grialshapes.ttf
                |_ ionicons.ttf
        ~~~

        <div class="highlight">Remember to check the proper `Build Action` is set after you copy the files.</div>

        For more info, please check [Adding Font Icons To Your Project](/docs.html#grial-uikit-overview-working-with-projects-adding-font-icons-to-your-project) docs.

    - Images
        - Copy the images from your `Resources` folder on your iOS `Grial Starter` project. 
        You can copy all of them but if you just want the minimum copy the following:
        ~~~
        <YourGrialStarterProject.iOS>
            |_ Resources
                |_ hamburguer_icon.png
                |_ logo.png
                |_ splash@2x.png
        ~~~
        
        Of course, also at this point you could add any additional image we provide if you want.

    - Animations (Lottie)
        - In case you could be adding Lottie animations through any of our pages (i.e.: `WelcomePage.xaml`) you will need to also copy our sample animation (later you can replace it):
        ~~~
        <YourGrialStarterProject.iOS>
            |_ Resources
                |_ grial_animation.json
        ~~~


### Adding Export For iOS Custom Renderers

To ease the process just copy `Properties` folder and its `AssemblyInfo.cs` file from your downloaded `Grial Starter` project to your iOS existing project:

~~~
<YourGrialStarterProject.iOS>
    |_ Properties
        |_ AssemblyInfo.cs
~~~

Open pasted `AssemblyInfo.cs` and add the following:

~~~
    // Custom renderers definition

    [assembly: ExportRenderer(typeof(UXDivers.Artina.Shared.CircleImage), typeof(UXDivers.Artina.Shared.ImageCircleRenderer))]
    [assembly: ExportRenderer(typeof(EntryCell), typeof(UXDivers.Artina.Shared.ArtinaEntryCellRenderer))]
    [assembly: ExportRenderer(typeof(ImageCell), typeof(UXDivers.Artina.Shared.ArtinaImageCellRenderer))]
    [assembly: ExportRenderer(typeof(SwitchCell), typeof(UXDivers.Artina.Shared.ArtinaSwitchCellRenderer))]
    [assembly: ExportRenderer(typeof(TableView), typeof(UXDivers.Artina.Shared.ArtinaTableRenderer))]
    [assembly: ExportRenderer(typeof(TextCell), typeof(UXDivers.Artina.Shared.ArtinaTextCellRenderer))]
    [assembly: ExportRenderer(typeof(ViewCell), typeof(UXDivers.Artina.Shared.ArtinaViewCellRenderer))]

    [assembly: ExportRenderer(typeof(Entry), typeof(UXDivers.Artina.Shared.ArtinaEntryRenderer))]
    [assembly: ExportRenderer(typeof(Editor), typeof(UXDivers.Artina.Shared.ArtinaEditorRenderer))]
    [assembly: ExportRenderer(typeof(Picker), typeof(UXDivers.Artina.Shared.ArtinaPickerRenderer))]
    [assembly: ExportRenderer(typeof(DatePicker), typeof(UXDivers.Artina.Shared.ArtinaDatePickerRenderer))]
    [assembly: ExportRenderer(typeof(TimePicker), typeof(UXDivers.Artina.Shared.ArtinaTimePickerRenderer))]

    [assembly: ExportRenderer(typeof(CarouselPage), typeof(MyExistingProject.iOS.CarouselPageVerticalScrollFixRenderer))]


    #pragma warning disable 219
    internal static class WorkaroundLoadingCustomRenderersFromExternalAssemblies {
        static WorkaroundLoadingCustomRenderersFromExternalAssemblies()
        {
            var a = new UXDivers.Artina.Shared.ArtinaEntryRenderer();
        }
    }
    #pragma warning restore 219
~~~

### Registering Icon Font on iOS

Register the icon font on `Info.plist` file:

~~~
...
<key>UIAppFonts</key>
	<array>
		<string>grialshapes.ttf</string>
	</array>
...
~~~

### Download Grial License and Invoke Init

- Copy your downloaded license from your `Grial Starter` project to the root folder of your existing Droid project folder:

    ~~~
    <YourGrialStarterProject.iOS>
        |_ GrialLicense
    ~~~
    
- Make sure the file compile action is set as emmbedded resource.
- Check Grial License is initialized properly on your `AppDelegate.cs`:

    ~~~
    namespace <YOUR_EXISTING_PROJECT_NAMESPACE>.iOS
    {
    	public class AppDelegate : FormsApplicationDelegate
    	{
    		public override bool FinishedLaunching (UIApplication app, NSDictionary options)
    		{
    			...
    			GrialKit.Init(new ThemeColors(), "<YOUR_EXISTING_PROJECT_NAMESPACE>.GrialLicense");
    			...
    ~~~
For more details please check [Grial License Setup](/docs.html#-grial-first-run-grial-license-setup).

### Initialize Grial Properly

Make your `AppDelegate.cs` includes the following:

~~~
	public class AppDelegate : global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate
	{
		public override bool FinishedLaunching (UIApplication app, NSDictionary options)
		{
			global::Xamarin.Forms.Forms.Init ();

			CachedImageRenderer.Init(); // Initializing FFImageLoading
			AnimationViewRenderer.Init(); // Initializing Lottie

			UXDivers.Artina.Shared.GrialKit.Init(new ThemeColors(), "UXDivers.Artina.Grial.iOS.GrialLicense");

			FormsHelper.ForceLoadingAssemblyContainingType(typeof(UXDivers.Effects.Effects));
			FormsHelper.ForceLoadingAssemblyContainingType<UXDivers.Effects.iOS.CircleEffect>();

			LoadApplication (new App ());

			return base.FinishedLaunching (app, options);
		}
	}
~~~
