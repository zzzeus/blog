---
title: 'UWP: Make the UWP app Topmost'
date: 2017-09-03 20:29:23
tags: 
- English
- UWP
- C#
---

I want to develop an app which can float over all other apps.

However I did not find the way.The UWP App had no such API method.

Recently I found that the BiliBili UWP App has a small window model which allow user to topmost the window.

So I searched the web and tried to find the api.The official document has no description.So I tried to use key words such as "topmost",to search the Internet.

Finally I found the API.It was rleased in February and has been used on the "Moive and TV" Microsoft Official UWP APP.

>Here is a blog post which is clear<br>[CompactOverlay mode – aka Picture-in-Picture](https://blogs.msdn.microsoft.com/universal-windows-app-model/2017/02/11/compactoverlay-mode-aka-picture-in-picture/)

The way making the window over all other app windows is called "CompactOverlay mode".

## Quick Summary of the CompactOverlay API

* the ability to check if CompactOverlay mode is availible to the app 
* the ability to transition an existing view in and out of the CompactOverlay mode.
* the ability to show a standalone view in CompactOverlay mode.

### Check if the model is availible
Since the intent of the CompactOverlay view mode is a very specific type of user experience,it is not necessarily supported across all windows devices and interaction modes
{% codeblock %}
// Check if the CompactOverlay mode is availible
if (ApplicationView.GetForCurrentView().IsViewModeSupported(ApplicationViewMode.CompactOverlay))
{
    compactOverlayButton.Visibility = Visibility.Visible;
}
{% endcodeblock %}

### transition the mode
>note that: the title bar may be wired<br>
if you move focus away from the CompactOverlay window the title bar will disappear
{% codeblock %}
bool modeSwitched = await ApplicationView.GetForCurrentView().TryEnterViewModeAsync(ApplicationViewMode.CompactOverlay);
{% endcodeblock %}

### set the size of the window
{% codeblock %}
ViewModePreferences compactOptions = ViewModePreferences.CreateDefault(ApplicationViewMode.CompactOverlay);
    compactOptions.CustomSize = new Windows.Foundation.Size(320, 200);
    bool modeSwitched = await ApplicationView.GetForCurrentView().TryEnterViewModeAsync(ApplicationViewMode.Default, compactOptions);
{% endcodeblock %}

### We also can use another window to show what need to be CompactOverlay and continue to browse other items meanwhile.
{% codeblock %}
await CoreApplication.CreateNewView().Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
    {
        var frame = new Frame();
        compactViewId = ApplicationView.GetForCurrentView().Id;
        frame.Navigate(typeof(SecondaryCompactViewPage));
        Window.Current.Content = frame;
        Window.Current.Activate();
        ApplicationView.GetForCurrentView().Title = "CompactOverlay Window";
    });
    bool viewShown = await ApplicationViewSwitcher.TryShowAsViewModeAsync(compactViewId, ApplicationViewMode.CompactOverlay);
{% endcodeblock %}


