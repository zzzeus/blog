---
title: CSharp Tip1
date: 2018-03-03 13:56:09
tags: 
- Tip
- C#
---

### Today I try to reimplement a function which I have finished.But It seem not easy for me now because I barely remember how to realize it.I wasted a lot of time to look for data which I had found.So I think it is necessay to note it down in case I meet the same situation.

#### some good tools：
1. NHotkey  --When it is necessary to listen to key event Globely.
2. PInvoke  --When we need to use Win32 api,use this nuget package to simplify our work.

*************
#### something need to know.
* **WPF cannot listen globe event.**
When it lose focus,It will not respone to any key event.
* **Util now I didn't find a perfect way to simulate the function like Alt+tab(show all windows on the desktop).**
I tried win32 api(EnumDesktopWindows,EnumWindows,GetWindow etc).However the result is not good.Some extra windows show up even though I didn't open such app(window store,Moive and TV when I opened UWP app such as Iqiyi).And I tried use Process which has "MainWindowTitle" to get its windows.But it also has some problem.One Process may have several windows.And it only have one MainWindowHandle availble.
{% codeblock %}
  List<Process> taskBarProcesses = Process.GetProcesses().
                                        Where(p => !string.IsNullOrEmpty(p.MainWindowTitle))
                                        .ToList();
{% endcodeblock %}
* **wpf commandBing usage(sometimes visual studio can help us finish it.We need to take advantage of the IDE)**
{% codeblock %}
<Window.Resources>
        <RoutedUICommand x:Key="maketopmost" Text="MakeTopmost"/>
    </Window.Resources>
    <Window.CommandBindings>
        <CommandBinding Command="{StaticResource maketopmost}" CanExecute="CommandBinding_CanExecute" Executed="CommandBinding_Executed"/>
    </Window.CommandBindings>
    <Window.InputBindings>
        <KeyBinding Gesture="Ctrl+Q" Command="{DynamicResource maketopmost}" HotkeyManager.RegisterGlobalHotkey="True"/>
    </Window.InputBindings>
{% endcodeblock %}
* **The structure is important.I need to let the project easier to understand.**


