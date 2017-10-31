#<a name="grial-troubleshooting" href="#grial-troubleshooting" class="iconTitle">Troubleshooting </a>

## Setting up UXDivers Nuget Source

We have received several comments from customers not being able to correctly setup the private nuget server for Grial packages.

Most of the time, the issue is just a typo on the URL.

To make sure you use the right URL, please copy and paste the one below:

`http://nuget.uxdivers.com/grial`

## License Issues

We have compiled the most typical technical issues in regards licenses here:

[Troubleshooting License Issues](/#grial-uikit-overview-grial-first-run-troubleshooting-license-issues)

## Grial Themes

We have compiled the most typical technical issues about themes compilation here:

[Troubleshooting Themes Compilation](/#grial-uikit-overview-theme-and-branding-of-your-app-troubleshooting-themes-compilation)

## i18n

If your app uses cultures that need special calendars you need to be sure to instantiate the specicic ones from code so they 
don't get stripped out by the linker. 

Please check the bug report here: https://bugzilla.xamarin.com/show_bug.cgi?id=59077

This may happen in both iOS and Android when compiling in `Release` config. If you face this problem you will probably see
an exception like this:

```
    System.ArgumentOutOfRangeException: Not a valid calendar for the given culture.
```

Grial comes with a method at the end of Android's `MainActivity` and iOS's `AppDelegate` that explains this problem and lists
the existing .net Calendars that you may need to reference according to your app, just uncomment the proper lines.

```
    private void ReferenceCalendars()
    {
        // When compiling in release, you may need to instantiate the specific
        // calendar so it doesn't get stripped out by the linker. Just uncomment
        // the lines you need according to the localization needs of the app.
        // For instance, in 'ar' cultures UmAlQuraCalendar is required.
        // https://bugzilla.xamarin.com/show_bug.cgi?id=59077

        // new System.Globalization.UmAlQuraCalendar();
        // new System.Globalization.ChineseLunisolarCalendar();
        // new System.Globalization.ChineseLunisolarCalendar();
        ...
```